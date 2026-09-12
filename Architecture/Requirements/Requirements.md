# Requirements

> **Status: draft specification - not implemented and not validated.**
> This document proposes a design. No component described here has been built,
> deployed, or tested, and any figure quoted is a target rather than a
> measurement. Claims of "production ready" or "complete" inherited from earlier
> drafts are unsupported and are being retired.
> See [PROJECT_STATUS.md](../../PROJECT_STATUS.md) for the maturity boundary and known gaps.

Requirements:

- Visual Language IDE web app based, to support all design flows and event-driven graphical programming similar to LabVIEW.
- Everything to be deployed elsewhere in the cloud, edge, etc. and inter-communicating between all like a mesh distributed (or p2p) network.
- Monitoring and logging, live real-time observability and dashboards.
- Combine all from AI agents/nodeRED/SQLiteAI nodes on the graphic programming dashboard projects.
- Adaptive security and self evolution of the language for future unknown nodes types.
- Compatibility and connection with legacy frameworks, languages and systems.

1. **Runtime Strategy**: Node.js/TypeScript core with Python AI/ML (LangChains/LangGraph/Models/etc.) + native extensions for performance-critical components
2. **Protocol Strategy**: Native AGCP unified protocol with A2A/MCP/ANP/ACP compatibility and other AI RAG systems + multi-protocol adapters
3. **Discovery Strategy**: Hybrid decentralized with local cache and fallback mechanisms
4. **Data Consistency**: Configurable per data type and system requirements
5. **Security Strategy**: Zero-trust mTLS core + AI adaptive security per deployment

## **Phase : Core Internet & Web**

## **Phase : AI & ML Ecosystem**

## **Phase : Big Data & Cloud-Native**

## **Phase : Blockchain & Emerging**

## **Phase : Legacy systems & Adaptive Future Forward Systems Compatibility**

This traceability matrix cross-references each requirement with the documents that discuss it. A tick means _a document addresses this requirement_; it does not mean the requirement is met, tested, or implemented. Read the final column with that in mind.

---

## 1. Traceability Matrix: Requirements → Architecture & Docs

| Requirement / Feature                                                                 | Architecture Spec | Protocol Schemas | Deployment | Implementation Roadmap | Docs/Diagrams | Addressed in docs |
|--------------------------------------------------------------------------------------|-------------------|------------------|------------|-----------------------|---------------|--------|
| Visual Language IDE (web, event-driven, LabVIEW-like)                                | Yes                | N/A              | N/A        | Yes                    | C4, arc42     | Yes     |
| Mesh distributed deployment (cloud, edge, p2p)                                       | Yes                | N/A              | Yes         | Yes                    | Deployment    | Yes     |
| Real-time monitoring, logging, dashboards                                            | Yes                | N/A              | Yes         | Yes                    | Monitoring    | Yes     |
| AI agents, NodeRED/SQLiteAI nodes, agentic flows                                     | Yes                | Yes                | Yes         | Yes                    | Logical, C4   | Yes     |
| Adaptive security, self-evolution, plugin system                                     | Yes                | Yes                | Yes         | Yes                    | Security      | Yes     |
| Legacy frameworks/languages/systems compatibility                                    | Yes                | Yes                | Yes         | Yes                    | arc42, C4     | Yes     |
| Node.js/TypeScript core, Python AI/ML, native perf                                   | Yes                | N/A              | N/A        | Yes                    | Tech Stack    | Yes     |
| AGCP protocol, A2A/MCP/ANP/ACP, multi-protocol adapters                             | Yes                | Yes                | Yes         | Yes                    | Protocols     | Yes     |
| Hybrid decentralized discovery, fallback, local cache                                | Yes                | N/A              | Yes         | Yes                    | Logical       | Yes     |
| Configurable data consistency                                                        | Yes                | N/A              | Yes         | Yes                    | Logical       | Yes     |
| Zero-trust mTLS, AI adaptive security                                                | Yes                | Yes                | Yes         | Yes                    | Security      | Yes     |
| Role-based connector nodes (all listed roles)                                        | Yes                | N/A              | N/A        | Yes                    | Logical       | Yes     |
| Universal system connectivity (finance, health, blockchain, legacy, real-time, OSI)  | Yes                | Yes                | Yes         | Yes                    | Protocols     | Yes     |
| Priority system (Web→AI/ML→IoT→Health→SCADA)                                         | Yes                | N/A              | N/A        | Yes                    | All docs      | Yes     |
| Hot-loadable extension/plugin system, schema importer                                | Yes                | Yes                | Yes         | Yes                    | Extensibility | Yes     |
| Live collaboration in Visual IDE                                                     | Yes                | N/A              | N/A        | Yes                    | Sequence      | Yes     |
| Self-healing nodes, live deployment flows                                            | Yes                | N/A              | Yes         | Yes                    | State, Runtime| Yes     |
| Real-time dashboard in Visual IDE                                                    | Yes                | N/A              | Yes         | Yes                    | Monitoring    | Yes     |
| Quantum, edge AI, 6G, future tech, backwards compatibility                          | Yes                | Yes                | Yes         | Yes                    | Extensibility | Yes     |
| All required diagrams (C4, arc42, system, context, state, sequence, runtime, etc.)   | N/A               | N/A              | N/A        | N/A                   | PlantUML      | Yes     |

---

## 2. Functional Requirements

- Visual, event-driven, web-based IDE for agentic programming
- Mesh, distributed, and p2p deployment (cloud, edge, hybrid)
- Real-time monitoring, logging, and dashboarding
- AI/ML agent orchestration, NodeRED/SQLiteAI integration
- Adaptive security, self-evolution, plugin/hot-loadable extension system
- Legacy and emerging protocol compatibility (finance, health, blockchain, industrial, etc.)
- Role-based agent system (all listed roles, extensible)
- Universal protocol bridge (AGCP, A2A, MCP, ANP, ACP, HTTP, MQTT, etc.)
- Hybrid decentralized discovery and fallback
- Configurable data consistency and reliability
- Zero-trust security, mTLS, compliance hooks
- Live multi-user collaboration in the IDE
- Self-healing, auto-remediating nodes and flows
- Real-time feedback and health status in the UI
- Future-proofing for quantum, edge AI, 6G, unknown tech
- Complete, versioned, and auditable extension/plugin system

---

## 3. Non-Functional Requirements (Recommended/Documented)

- **Performance**: <5ms local latency for IoT/edge, 10,000+ msg/sec throughput, 99.9% uptime (web), 99.99% (SCADA)
- **Scalability**: Horizontal and vertical scaling, auto-scaling in cloud/edge
- **Reliability**: Self-healing, auto-remediation, mesh consensus, failover
- **Security**: Zero-trust, mTLS, RBAC, signed plugins, compliance (GDPR, HIPAA)
- **Extensibility**: Manifest/schema-based plugin system, hot-loading, schema importer
- **Interoperability**: Universal protocol bridge, legacy and future compatibility
- **Maintainability**: Modular, versioned, migration tools, audit logs
- **Usability**: Visual-first, live collaboration, real-time feedback, customizable dashboards
- **Observability**: Real-time monitoring, logging, tracing, alerting, API access
- **Compliance**: Hooks for regulatory requirements, auditability, rollback
- **Documentation**: Complete, up-to-date, cross-referenced, with diagrams

---

## 4. Consistency check

This section previously asserted that no missing transitions, undefined states,
or contradictions remained, and that all extension actions "are signed, validated,
and sandboxed". As a statement about a specification with no implementation, that
was not verifiable, and it was contradicted elsewhere in this repository - most
obviously by the three different agent-role counts.

What can be said:

| Check | Result |
|---|---|
| Requirement identifiers traceable | Yes - mechanically checked; see `tools/check_rtm.py` in the sibling repository |
| Documents mutually consistent | **No.** Three role counts coexist (70+, 20, and five primitives); see [ADR-0005](../../docs/adr/0005-agent-role-primitives.md) |
| Protocol version consistent | **No.** Four different version labels appear across the documents |
| Scope bounded | **No.** See [ADR-0003](../../docs/adr/0003-core-and-extended-profiles.md) |
| Security properties evidenced | **No.** Sandboxing, signing, and validation are requirements, not achieved properties; see `CONFORMANCE.md` and [SECURITY.md](../../SECURITY.md) |

## 5. Gaps & Recommendations

- **Gaps are acknowledged, not closed.** Every row above records that a _document_ addresses a requirement. It does not record that a capability works. The material gaps - no implementation, no conformance suite, no benchmark evidence, unresolved core scope, and undefined self-evolution safety behaviour - are listed in [PROJECT_STATUS.md](../../PROJECT_STATUS.md).
- **Continuous Review**: As new protocols/tech emerge, update the extension registry and schemas.
- **Testing**: Ensure all extension/plugin code is covered by automated tests and security scans.
- **User Feedback**: Incorporate user feedback from live deployments to refine flows and dashboards.
- **Documentation**: Keep all diagrams and docs versioned and cross-referenced as the system evolves.

---

## 6. Final Statement

**This specification is a draft.** The documents are internally inconsistent in places and the requirements are stated, not satisfied. Its value is as a design proposal to be reviewed and reduced in scope, not as evidence of a working system. See [PROJECT_STATUS.md](../../PROJECT_STATUS.md) for the maturity boundary and the list of known gaps.
