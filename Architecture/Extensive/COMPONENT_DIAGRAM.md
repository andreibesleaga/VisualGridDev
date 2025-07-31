# VisualGridDev Studio Component Interaction Diagram

## System Overview Flow

```
┌─────────────────────────────────────────────────────────────────────────────────┐
│                            VisualGridDev Studio IDE (Web UI)                    │
│  ┌─────────────────┐ ┌─────────────────┐ ┌─────────────────┐ ┌─────────────────┐│
│  │ Visual Flow     │ │ Real-Time       │ │ Code Editor     │ │ Deployment      ││
│  │ Designer        │ │ Monitor         │ │ (Monaco?)       │ │ Manager         ││
│  │ - Canvas        │ │ - Live Metrics  │ │ - Python/JS     │ │ - K8s Deploy    ││
│  │ - Node Palette  │ │ - Topology View │ │ - SQL Queries   │ │ - Edge Deploy   ││
│  │ - Flow Config   │ │ - Log Viewer    │ │ - Inline Debug  │ │ - Health Check  ││
│  └─────────────────┘ └─────────────────┘ └─────────────────┘ └─────────────────┘│
└─────────────────────────────────────────────────────────────────────────────────┘
                                        │
                                   WebSocket/HTTP
                                        │
┌─────────────────────────────────────────────────────────────────────────────────┐
│                          VisualGridDev Core Runtime Engine                      │
│  ┌─────────────────┐ ┌─────────────────┐ ┌─────────────────┐ ┌─────────────────┐│
│  │ Flow Execution  │ │ Mesh Network    │ │ Node Registry   │ │ Event Bus       ││
│  │ Engine          │ │ Manager         │ │ & Lifecycle     │ │ (Pub/Sub)       ││
│  │ - Node-RED Fork │ │ - Peer Discovery│ │ - Node Types    │ │ - Message Route ││
│  │ - Scheduler     │ │ - Routing Table │ │ - Capabilities  │ │ - Event Stream  ││
│  │ - State Machine │ │ - Health Checks │ │ - Versions      │ │ - Dead Letter   ││
│  └─────────────────┘ └─────────────────┘ └─────────────────┘ └─────────────────┘│
└─────────────────────────────────────────────────────────────────────────────────┘
                                        │
                              Multi-Protocol Transport
                                        │
┌─────────────────────────────────────────────────────────────────────────────────┐
│                            Node Runtime Layer                                   │
│  ┌─────────────────┐ ┌─────────────────┐ ┌─────────────────┐ ┌─────────────────┐│
│  │ AI    Agent     │ │ MCP Client      │ │ Node-RED Compat │ │  SQLite-AI Edge ││
│  │ Nodes           │ │ Nodes           │ │ Nodes           │ │ Nodes           ││
│  │ - A2A Protocol  │ │ - External APIs │ │ - Legacy Support│ │ - Vector DB     ││
│  │ - Internal Comm │ │ - LLM Services  │ │ - Flow Import   │ │ - MCP Resources ││
│  │ - Agent Mesh    │ │ - Databases     │ │ - Node Catalog  │ │ - Local AI      ││
│  └─────────────────┘ └─────────────────┘ └─────────────────┘ └─────────────────┘│
└─────────────────────────────────────────────────────────────────────────────────┘
                                        │
                              MCP External Systems Layer
                                        │
┌─────────────────────────────────────────────────────────────────────────────────┐
│                          External Systems (via MCP)                             │
│  ┌─────────────────┐ ┌─────────────────┐ ┌─────────────────┐ ┌─────────────────┐│
│  │ Database        │ │ LLM Services    │ │ File Systems    │ │ Version Control ││
│  │ Systems         │ │                 │ │                 │ │                 ││
│  │ - PostgreSQL    │ │ - OpenAI        │ │ - Local Files   │ │ - Git Repos     ││
│  │ - MongoDB       │ │ - Claude        │ │ - Cloud Storage │ │ - GitHub        ││
│  │ - Redis         │ │ - Custom LLMs   │ │ - Network Drives│ │ - GitLab        ││
│  └─────────────────┘ └─────────────────┘ └─────────────────┘ └─────────────────┘│
└─────────────────────────────────────────────────────────────────────────────────┘
                                        │
                                 Data & State Layer
                                        │
┌─────────────────────────────────────────────────────────────────────────────────┐
│                        Distributed Data & State Management                      │
│  ┌─────────────────┐ ┌─────────────────┐ ┌─────────────────┐ ┌─────────────────┐│
│  │ SQLite-AI Grid  │ │ State Sync      │ │ Event Store     │ │ Config Store    ││
│  │ - Distributed   │ │ - Raft Consensus│ │ - Event Sourcing│ │ - Flow Configs  ││
│  │ - Replication   │ │ - CRDT Merge    │ │ - Audit Trail   │ │ - Node Settings ││
│  │ - Edge Cache    │ │ - Conflict Res. │ │ - Replay Logic  │ │ - Secrets Mgmt  ││
│  └─────────────────┘ └─────────────────┘ └─────────────────┘ └─────────────────┘│
└─────────────────────────────────────────────────────────────────────────────────┘
                                        │
                              Self-Healing & Evolution
                                        │
┌─────────────────────────────────────────────────────────────────────────────────┐
│                      Evolutionary Control & Self-Healing                        │
│  ┌─────────────────┐ ┌─────────────────┐ ┌─────────────────┐ ┌─────────────────┐│
│  │ Health Monitor  │ │ Fitness         │ │ Change          │ │ Anomaly         ││
│  │ (MAPE-K)        │ │ Evaluator       │ │ Orchestrator    │ │ Detection       ││
│  │ - Monitor       │ │ - Performance   │ │ - Canary Deploy │ │ - ML-based      ││
│  │ - Analyze       │ │ - Availability  │ │ - Rollback      │ │ - Predictive    ││
│  │ - Plan          │ │ - Resource Use  │ │ - Auto-scaling  │ │ - Alert System  ││
│  │ - Execute       │ │ - Latency       │ │ - Migration     │ │ - Root Cause    ││
│  └─────────────────┘ └─────────────────┘ └─────────────────┘ └─────────────────┘│
└─────────────────────────────────────────────────────────────────────────────────┘
```

## Message Flow Examples

### 1. Flow Execution Message Flow
```
User (IDE) → Flow Config → Core Runtime → Node Registry → Specific Node → Execute
                                      ↓
                              Event Bus → Other Nodes → Response → User (Monitor)
```

### 2. Self-Healing Trigger Flow
```
Node Failure → Health Monitor → Analyze → Plan Recovery → Execute Failover
                            ↓
                    Fitness Evaluator → Update Metrics → Trigger Evolution
```

### 3. AI/ML Inference Flow (via MCP)
```
Data Input → Flow Engine → MCP Client Node → External LLM Service → Model Inference
                                   ↓
                           SQLite-AI Cache → Response → Flow Output
```

### 4. External System Integration Flow
```
Flow Trigger → MCP Client → External System (DB/File/Git/API) → MCP Response → Flow Continue
```

### 5. Universal External Communication Pattern
```
VisualGridDev Flow → MCP Client Manager → MCP Server (Any System) → System Response → Flow Result
```

## Inter-Component Communication Protocols

### Protocol Matrix
| Source Component | Target Component | Protocol | Purpose |
|------------------|------------------|----------|---------|
| IDE | Core Runtime | WebSocket | Real-time updates |
| Core Runtime | Internal Agents | A2A (JSON-RPC+SSE) | Agent communication |
| Core Runtime | External Systems | MCP (stdio/SSE) | Universal external access |
| Mesh Nodes | Mesh Nodes | libp2p | P2P mesh communication |
| MCP Clients | Databases | MCP Tools | Database operations |
| MCP Clients | LLM Services | MCP Tools | AI/ML inference |
| MCP Clients | File Systems | MCP Resources | File operations |
| MCP Clients | Git Repos | MCP Tools | Version control |
| State Sync | SQLite-AI | Raft | Consensus |
| Health Monitor | All Components | A2A + MCP | Health checks |
| Event Bus | All Subscribers | Pub/Sub | Event distribution |

## Data Flow Patterns

### 1. Event-Driven Pattern
```
Sensor Data → Event Bus → Multiple Subscribers → Parallel Processing → Aggregation
```

### 2. Request-Response Pattern
```
User Request → API Gateway → Service → Database → Response → User
```

### 3. Stream Processing Pattern
```
Data Stream → Buffer → Transform → Filter → Enrich → Output Stream
```

### 4. Mesh Replication Pattern
```
Local Update → Raft Leader → Consensus → Replicate → All Nodes → Acknowledge
```