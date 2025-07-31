# AI A2A Integration Guide for VisualGridDev Studio

## Overview

VisualGridDev Studio can integrate the official A2A SDK (or the proven optimized Artinet SDK (@artinet/sdk)) as its core agent communication layer, extending it with Node-RED flow capabilities and distributed mesh networking. This document outlines the integration strategy based on the architecture patterns.

## Core Concepts Adopted

### 1. Agent2Agent (A2A) Protocol
- **JSON-RPC over HTTP**: Standard request/response pattern
- **Server-Sent Events (SSE)**: Real-time streaming updates
- **AgentCard**: Agent discovery and capability advertisement
- **TaskHandler**: Async generator pattern for agent logic

### 2. Key SDK Components

#### A2AServer (ExpressServer)
```typescript
import { A2AServer, AgentEngine, ExecutionContext, FileStore } from '@artinet/sdk';

// VisualGridDev extends A2AServer
class VisualGridDevServer extends A2AServer {
  private flowEngine: NodeRedFlowEngine;
  private meshNetwork: LibP2PMeshNetwork;
  
  constructor(config: VisualGridDevServerConfig) {
    super({
      handler: this.createFlowAwareAgentEngine(),
      taskStore: new FileStore(config.dataPath),
      card: this.generateAgentCard(config),
      port: config.port,
      basePath: '/a2a'
    });
    
    this.flowEngine = new NodeRedFlowEngine(config.flows);
    this.meshNetwork = new LibP2PMeshNetwork(config.mesh);
  }
  
  private createFlowAwareAgentEngine(): AgentEngine {
    return async function* (context: ExecutionContext) {
      const params = context.getRequestParams();
      const message = params.message;
      
      yield { state: "working" };
      
      // Execute through Node-RED flow
      const flowResult = await this.flowEngine.execute(message, context);
      
      yield {
        state: "completed",
        message: {
          role: "agent",
          parts: [{ kind: "text", text: flowResult }]
        }
      };
    }.bind(this);
  }
}
```

#### A2AClient for Inter-Agent Communication
```typescript
import { A2AClient, Message } from '@artinet/sdk';

class VisualGridDevMeshClient {
  private clients: Map<string, A2AClient> = new Map();
  
  async sendToAgent(agentUrl: string, message: Message): Promise<Task> {
    let client = this.clients.get(agentUrl);
    if (!client) {
      client = new A2AClient(agentUrl);
      this.clients.set(agentUrl, client);
    }
    
    return await client.sendMessage({ message });
  }
  
  async streamFromAgent(agentUrl: string, message: Message): AsyncIterable<UpdateEvent> {
    const client = this.clients.get(agentUrl) || new A2AClient(agentUrl);
    return client.sendStreamingMessage({ message });
  }
}
```

### 3. AgentCard Integration
```typescript
interface VisualGridDevAgentCard extends AgentCard {
  name: string;
  url: string;
  version: string;
  capabilities: {
    streaming: boolean;
    nodeRed: boolean;
    mesh: boolean;
    sqliteAI: boolean;
  };
  skills: Array<{
    id: string;
    name: string;
    type: 'flow' | 'ml' | 'data' | 'agent';
    nodeRedCompatible?: boolean;
  }>;
  // VisualGridDev extensions
  flowTypes?: string[];
  meshPeers?: string[];
  supportedProtocols?: ('A2A' | 'MCP' | 'HTTP' | 'MQTT')[];
}
```

### 4. TaskStore Integration with Distributed State
```typescript
import { TaskStore, Task } from '@artinet/sdk';

class DistributedTaskStore implements TaskStore {
  private localStore: FileStore;
  private raftConsensus: RaftConsensus;
  
  constructor(dataPath: string, raftConfig: RaftConfig) {
    this.localStore = new FileStore(dataPath);
    this.raftConsensus = new RaftConsensus(raftConfig);
  }
  
  async createTask(task: Task): Promise<void> {
    // Store locally first
    await this.localStore.createTask(task);
    
    // Replicate across mesh if critical
    if (task.metadata?.replicate) {
      await this.raftConsensus.replicate('task:create', task);
    }
  }
  
  async getTask(taskId: string): Promise<Task | null> {
    return await this.localStore.getTask(taskId);
  }
  
  async updateTask(taskId: string, updates: Partial<Task>): Promise<void> {
    await this.localStore.updateTask(taskId, updates);
    
    // Sync updates across mesh
    await this.raftConsensus.replicate('task:update', { taskId, updates });
  }
}
```

## Node-RED Integration Pattern

### 1. AI-Aware Node-RED Nodes
```typescript
// Custom Node-RED node that wraps A2A communication
module.exports = function(RED) {
  function AiAgentNode(config) {
    RED.nodes.createNode(this, config);
    
    this.agentUrl = config.agentUrl;
    this.client = new A2AClient(this.agentUrl);
    
    this.on('input', async (msg) => {
      try {
        const a2aMessage: Message = {
          kind: "message",
          role: "user",
          parts: [{ kind: "text", text: msg.payload }]
        };
        
        if (config.streaming) {
          const stream = this.client.sendStreamingMessage({ message: a2aMessage });
          for await (const update of stream) {
            this.send({ payload: update, topic: 'stream' });
          }
        } else {
          const task = await this.client.sendMessage({ message: a2aMessage });
          this.send({ payload: task.message, topic: 'response' });
        }
      } catch (error) {
        this.error(error.message);
      }
    });
  }
  
  RED.nodes.registerType("ai-agent", AiAgentNode);
};
```

### 2. Flow-to-Agent Bridge
```typescript
class FlowToAgentBridge {
  private server: VisualGridDevServer;
  private flowEngine: NodeRedFlowEngine;
  
  constructor(server: VisualGridDevServer, flowEngine: NodeRedFlowEngine) {
    this.server = server;
    this.flowEngine = flowEngine;
  }
  
  // Convert Node-RED flow execution to A2A agent response
  async executeFlowAsAgent(context: ExecutionContext): Promise<AsyncGenerator<UpdateEvent, Task | void, unknown>> {
    const params = context.getRequestParams();
    const inputMessage = params.message;
    
    return async function* () {
      yield { state: "working" };
      
      // Execute Node-RED flow
      const flowContext = {
        payload: inputMessage.parts[0]?.text || "",
        topic: "a2a-input",
        executionId: context.taskId,
        a2aContext: context
      };
      
      const flowResult = await this.flowEngine.executeFlow(flowContext);
      
      yield {
        state: "completed",
        message: {
          role: "agent",
          parts: [{ kind: "text", text: flowResult.payload }]
        }
      };
    }.bind(this);
  }
}
```

## Mesh Network Integration

### 1. Agent Discovery via libp2p + AgentCard
```typescript
import { createLibp2p } from 'libp2p';
import { A2AClient } from '@artinet/sdk';

class VisualGridDevMeshDiscovery {
  private libp2p: Libp2p;
  private knownAgents: Map<string, AgentCard> = new Map();
  
  async discoverAgents(): Promise<AgentCard[]> {
    const peers = await this.libp2p.peerStore.all();
    const agents: AgentCard[] = [];
    
    for (const peer of peers) {
      try {
        // Try to fetch AgentCard from peer
        const agentUrl = `http://${peer.addresses[0]}/a2a`;
        const client = new A2AClient(agentUrl);
        const card = await client.agentCard();
        
        agents.push(card);
        this.knownAgents.set(peer.id.toString(), card);
      } catch (error) {
        // Peer is not an A2A agent
        continue;
      }
    }
    
    return agents;
  }
}
```

### 2. Distributed Flow Execution
```typescript
class DistributedFlowExecutor {
  private meshClient: VisualGridDevMeshClient;
  private localAgents: Map<string, VisualGridDevServer> = new Map();
  
  async executeDistributedFlow(flow: NodeRedFlow, context: ExecutionContext): Promise<any> {
    const executionPlan = this.analyzeFlowDistribution(flow);
    
    for (const step of executionPlan) {
      if (step.location === 'local') {
        // Execute locally
        await this.executeLocalStep(step, context);
      } else {
        // Execute on remote agent
        const message: Message = {
          kind: "message",
          role: "user",
          parts: [{ kind: "text", text: JSON.stringify(step.data) }]
        };
        
        await this.meshClient.sendToAgent(step.agentUrl, message);
      }
    }
  }
}
```

## MCP Integration (Model Context Protocol) - Universal External Communication

### 1. MCP Server Integration (Exposing VisualGridDev to External Systems)
```typescript
import { Server } from '@modelcontextprotocol/sdk/server/index.js';
import { StdioServerTransport } from '@modelcontextprotocol/sdk/server/stdio.js';

class VisualGridDevMCPServer {
  private server: Server;
  private VisualGridDevServer: VisualGridDevServer;
  
  constructor(VisualGridDevServer: VisualGridDevServer) {
    this.VisualGridDevServer = VisualGridDevServer;
    this.server = new Server({
      name: "VisualGridDev-mcp-server",
      version: "1.0.0"
    }, {
      capabilities: {
        tools: {},
        resources: {},
        prompts: {},
        logging: {}
      }
    });
    
    this.setupMCPHandlers();
  }
  
  private setupMCPHandlers() {
    // Expose VisualGridDev flows as MCP tools
    this.server.setRequestHandler('tools/list', async () => {
      const flows = await this.VisualGridDevServer.getAvailableFlows();
      return {
        tools: flows.map(flow => ({
          name: flow.id,
          description: flow.description,
          inputSchema: flow.inputSchema
        }))
      };
    });
    
    this.server.setRequestHandler('tools/call', async (request) => {
      const { name, arguments: args } = request.params;
      
      // Execute flow via A2A protocol
      const message: Message = {
        kind: "message",
        role: "user",
        parts: [{ kind: "text", text: JSON.stringify(args) }]
      };
      
      const result = await this.VisualGridDevServer.executeFlow(name, message);
      return { content: [{ type: "text", text: result }] };
    });
    
    // Expose flow data as MCP resources
    this.server.setRequestHandler('resources/list', async () => {
      const flows = await this.VisualGridDevServer.getAvailableFlows();
      return {
        resources: flows.map(flow => ({
          uri: `VisualGridDev://flows/${flow.id}`,
          name: flow.name,
          description: flow.description,
          mimeType: "application/json"
        }))
      };
    });
    
    // Expose flow templates as MCP prompts
    this.server.setRequestHandler('prompts/list', async () => {
      const templates = await this.VisualGridDevServer.getFlowTemplates();
      return {
        prompts: templates.map(template => ({
          name: template.id,
          description: template.description,
          arguments: template.parameters
        }))
      };
    });
  }
}
```

### 2. MCP Client Integration (Connecting to External Systems)
```typescript
import { Client } from '@modelcontextprotocol/sdk/client/index.js';
import { StdioClientTransport, SSEClientTransport } from '@modelcontextprotocol/sdk/client/stdio.js';

class VisualGridDevMCPClientManager {
  private clients: Map<string, Client> = new Map();
  private connections: Map<string, MCPConnection> = new Map();
  
  // Connect to external MCP servers
  async connectToMCPServer(config: MCPServerConfig): Promise<void> {
    const transport = config.transport === 'stdio' 
      ? new StdioClientTransport({ command: config.command, args: config.args })
      : new SSEClientTransport(config.url);
    
    const client = new Client({
      name: "VisualGridDev-client",
      version: "1.0.0"
    }, {
      capabilities: {
        experimental: {},
        sampling: {}
      }
    });
    
    await client.connect(transport);
    this.clients.set(config.id, client);
    this.connections.set(config.id, { config, client, transport });
  }
  
  // Universal tool calling interface
  async callExternalTool(serverId: string, toolName: string, args: any): Promise<any> {
    const client = this.clients.get(serverId);
    if (!client) throw new Error(`MCP server ${serverId} not connected`);
    
    return await client.request({
      method: "tools/call",
      params: { name: toolName, arguments: args }
    });
  }
  
  // Universal resource access interface
  async getExternalResource(serverId: string, uri: string): Promise<any> {
    const client = this.clients.get(serverId);
    if (!client) throw new Error(`MCP server ${serverId} not connected`);
    
    return await client.request({
      method: "resources/read",
      params: { uri }
    });
  }
  
  // Universal prompt interface
  async getExternalPrompt(serverId: string, promptName: string, args: any): Promise<any> {
    const client = this.clients.get(serverId);
    if (!client) throw new Error(`MCP server ${serverId} not connected`);
    
    return await client.request({
      method: "prompts/get",
      params: { name: promptName, arguments: args }
    });
  }
}
```

### 3. MCP Node-RED Integration
```typescript
// Universal MCP Node for Node-RED
module.exports = function(RED) {
  function MCPExternalNode(config) {
    RED.nodes.createNode(this, config);
    
    this.serverId = config.serverId;
    this.operation = config.operation; // 'tool', 'resource', 'prompt'
    this.name = config.name;
    this.mcpManager = RED.settings.get('mcpManager');
    
    this.on('input', async (msg) => {
      try {
        let result;
        
        switch (this.operation) {
          case 'tool':
            result = await this.mcpManager.callExternalTool(
              this.serverId, 
              this.name, 
              msg.payload
            );
            break;
          case 'resource':
            result = await this.mcpManager.getExternalResource(
              this.serverId, 
              this.name
            );
            break;
          case 'prompt':
            result = await this.mcpManager.getExternalPrompt(
              this.serverId, 
              this.name, 
              msg.payload
            );
            break;
        }
        
        this.send({ payload: result, topic: 'mcp-response' });
      } catch (error) {
        this.error(error.message);
      }
    });
  }
  
  RED.nodes.registerType("mcp-external", MCPExternalNode);
};
```

### 4. External System Integration Examples

#### Database Systems via MCP
```typescript
// PostgreSQL MCP Server Integration
const postgresConfig: MCPServerConfig = {
  id: 'postgres-main',
  transport: 'stdio',
  command: 'npx',
  args: ['@modelcontextprotocol/server-postgres', 'postgresql://user:pass@localhost/db']
};

// Usage in flow
const dbResult = await mcpManager.callExternalTool('postgres-main', 'query', {
  sql: 'SELECT * FROM users WHERE active = true'
});
```

#### File System via MCP
```typescript
// File System MCP Server Integration
const filesystemConfig: MCPServerConfig = {
  id: 'filesystem',
  transport: 'stdio',
  command: 'npx',
  args: ['@modelcontextprotocol/server-filesystem', '/allowed/path']
};

// Usage in flow
const fileContent = await mcpManager.getExternalResource('filesystem', 'file:///allowed/path/data.json');
```

#### LLM Services via MCP
```typescript
// Claude/OpenAI MCP Integration
const claudeConfig: MCPServerConfig = {
  id: 'claude-ai',
  transport: 'stdio',
  command: 'npx',
  args: ['@modelcontextprotocol/server-claude']
};

// Usage in flow
const aiResponse = await mcpManager.callExternalTool('claude-ai', 'complete', {
  prompt: 'Analyze this data and provide insights',
  data: flowData
});
```

#### Git Repository via MCP
```typescript
// Git MCP Server Integration
const gitConfig: MCPServerConfig = {
  id: 'git-repo',
  transport: 'stdio',
  command: 'npx',
  args: ['@modelcontextprotocol/server-git', '/path/to/repo']
};

// Usage in flow
const commitInfo = await mcpManager.callExternalTool('git-repo', 'log', {
  limit: 10,
  branch: 'main'
});
```

## Implementation Strategy

### Phase 1: Core A2A + MCP Integration
1. **Wrap A2A/Artinet SDK**: Create VisualGridDevServer extending A2AServer/A2AClient
2. **MCP Client Manager**: Universal external system connectivity
3. **Agent Registry**: Implement distributed AgentCard discovery
4. **Basic Flow-to-Agent**: Convert Node-RED flows to AgentEngine handlers
5. **TaskStore**: Implement distributed task storage with Raft

### Phase 2: Advanced Integration
1. **Mesh Communication**: libp2p + A2A protocol for internal agents
2. **MCP Server**: Expose VisualGridDev flows as MCP tools/resources/prompts
3. **Universal MCP Nodes**: Node-RED nodes for all external systems
4. **Streaming Flows**: Real-time flow execution via SSE
5. **Visual Designer**: React frontend with A2A + MCP integration

### Phase 3: Production Features
1. **Self-Healing**: MAPE-K loops with A2A + MCP health checks
2. **Load Balancing**: Distribute flows across mesh agents
3. **Security**: mTLS + RBAC for A2A + MCP communications
4. **Monitoring**: Real-time agent and external system observability
5. **MCP Registry**: Dynamic discovery and connection to MCP servers

This integration strategy uses the proven A2A protocol for internal agent communication and MCP for universal external system integration, while extending it with Node-RED's visual programming and distributed mesh capabilities, creating a unified platform for agentic flow programming that can connect to any external system via standardized protocols.
