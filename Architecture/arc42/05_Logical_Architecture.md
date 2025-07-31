# 5. Logical Architecture (C4 Level 2)

- VisualGridDev Studio (IDE)
- Flow Runtime (Node-RED)
- A2A/MCP Protocol Router
- MAPE-K Feedback Loops
- Event Bus (Kafka)
- AI Orchestrators (LangChain)
- Vector Indexing (SQLite-AI)

---

## 🛡️ Logical Flow: Self-Healing, Extensibility, and Monitoring

1. Visual programming flows are created/edited in the Visual IDE (with live collaboration).
2. Flows are versioned and deployed to target environments (cloud, edge, hybrid) via orchestrators.
3. Self-healing agents on each node receive, validate, and activate flows, monitoring health and auto-remediating failures.
4. Extensions (protocols, agents, UI, etc.) can be hot-loaded at runtime via manifest/schema-based plugins.
5. Real-time health, deployment, and flow status are streamed to the Visual IDE dashboard for live monitoring and troubleshooting.
6. All system components are versioned, compatible, and future-proofed for new/emerging tech.
