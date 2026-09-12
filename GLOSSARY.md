# Glossary

Every acronym used in this specification is expanded here once. Where a term
refers to a third-party protocol or standard, the entry states that the
specification cites it but does not own, vendor, or version it.

## This project

| Term | Expansion | Note |
|---|---|---|
| **AGCP** | **Agentic Grid Communication Protocol** | The unified protocol this specification proposes. It is a _proposal_; it is not registered with any standards body and has no independent implementations. See `PROJECT_STATUS.md`. |
| **AGCP Core** | — | The proposed minimal mandatory subset of AGCP. Scope is unresolved; see ADR-0003. |
| **VisualGridDev** | — | Working name of the proposed visual orchestration platform. |
| **Core profile** | — | The bridge and feature subset an implementation must support to claim baseline conformance. |
| **Extended profile** | — | Optional bridges and features beyond the core profile. |
| **Bridge** | Protocol bridge | A component that translates between a foreign protocol and AGCP. |

## Agent and interoperability protocols cited

| Term | Expansion | Note |
|---|---|---|
| **A2A** | Agent-to-Agent | A third-party open protocol for interoperability between independent agents. Cite, verify current revision; not owned by this project. |
| **MCP** | Model Context Protocol | A third-party open protocol for connecting AI applications to tools and data sources. Cite, verify current revision; not owned by this project. |
| **ANP** | Agent Network Protocol | A third-party agent-interoperability effort. Confirm current scope and governance before relying on it. |
| **ACP** | Agent Communication Protocol | A third-party agent-interoperability effort. Confirm current scope and governance before relying on it. |
| **RAG** | Retrieval-Augmented Generation | Retrieving external context and supplying it to a model at generation time. |

## Architecture and operations

| Term | Expansion | Note |
|---|---|---|
| **ADR** | Architecture Decision Record | A dated record of a decision, its context, and its consequences. See `docs/adr/`. |
| **C4** | Context, Containers, Components, Code | A hierarchical software-architecture diagramming model. |
| **arc42** | — | A template for architecture documentation. |
| **MAPE-K** | Monitor, Analyse, Plan, Execute over shared Knowledge | The autonomic-computing control loop. Naming it does not define it; see ADR-0004. |
| **CRDT** | Conflict-free Replicated Data Type | A data type that merges deterministically without coordination. |
| **ODD** | Operational Design Domain | The conditions under which a system is designed to operate. |
| **SLO** | Service Level Objective | A target for a measurable service property. |
| **TTL** | Time To Live | A retention or expiry bound. |

## Security and supply chain

| Term | Expansion | Note |
|---|---|---|
| **mTLS** | Mutual Transport Layer Security | Both peers authenticate with certificates. |
| **RBAC** | Role-Based Access Control | Authorisation by assigned role. |
| **Wasm** | WebAssembly | A portable binary format used for sandboxing. |
| **SBOM** | Software Bill of Materials | An inventory of components in an artefact. |
| **CycloneDX** | — | An SBOM standard. |
| **SLSA** | Supply-chain Levels for Software Artefacts | A framework for build-integrity levels. |
| **SARIF** | Static Analysis Results Interchange Format | A standard format for analysis findings. |
| **CVE** | Common Vulnerabilities and Exposures | A public identifier for a disclosed vulnerability. |
| **OSV** | Open Source Vulnerabilities | A vulnerability database and scanner. |
| **OpenSSF** | Open Source Security Foundation | The foundation publishing the Scorecard checks. |

## Regulations and frameworks cited

| Term | Expansion | Note |
|---|---|---|
| **EU AI Act** | Regulation (EU) 2024/1689 | Cited for mapping analysis only; classification is deployment-specific. |
| **GDPR** | Regulation (EU) 2016/679 | General Data Protection Regulation. |
| **NIST AI RMF** | NIST AI Risk Management Framework | Cited; verify the targeted revision. |
| **SOC 2** | System and Organization Controls 2 | An assurance reporting framework. |
| **ISO/IEC 27001** | — | An information-security management standard. |
| **HIPAA** | Health Insurance Portability and Accountability Act | A United States health-data statute. |
| **IEEE CertifAIEd** | IEEE Certification Program for Ethical AI | Cited; verify the targeted programme revision. |

## Specification language

| Term | Expansion | Note |
|---|---|---|
| **RFC 2119** | IETF RFC 2119 | Defines MUST, MUST NOT, SHOULD, SHOULD NOT, and MAY. Used normatively in `CONFORMANCE.md`. |
| **RFC 8174** | IETF RFC 8174 | Clarifies that RFC 2119 keywords are normative only when capitalised. |
