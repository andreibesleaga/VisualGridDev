# Final Architecture Summary

> **Status: draft specification - not implemented and not validated.**
> This is a summary of a _proposal_. Every item below describes a design
> intention. Nothing has been built or measured, and no status here is "done".
> See [PROJECT_STATUS.md](../../PROJECT_STATUS.md) for the maturity boundary and
> the list of known gaps.

## What this document is

A one-page index to the unified architecture specification. It summarises what is
proposed and how mature each part is. The authoritative description is
[FINAL_UNIFIED_ARCHITECTURE_v5.0.md](FINAL_UNIFIED_ARCHITECTURE_v5.0.md); this
summary must not contradict it, and does not replace it.

This document previously reported the architecture as "complete" and "production
ready", with a table of green ticks. That was unsupported and has been removed.
The maturity column below is the honest version.

## The proposal in one paragraph

VisualGridDev proposes a visual, event-driven programming environment in which
agents, services, and protocol adapters are composed graphically and deployed
across cloud, edge, and peer-to-peer environments. Interoperability is intended to
be achieved through a single message envelope, the **Agentic Grid Communication
Protocol (AGCP)**, with foreign protocols handled by translation bridges. A
MAPE-K-style control loop is proposed for self-healing, and runtime protocol
inference for self-evolution.

## Components and maturity

| Component | What is proposed | Maturity |
|---|---|---|
| AGCP envelope | One message shape for all internal communication | Schema and prose sketches. See `Architecture/Schemas/`. |
| Core transport | gRPC over HTTP/2 with Protocol Buffers; JSON only at the boundary | Proposed in `CONFORMANCE.md` `CON-CORE-006`. Not implemented. |
| Protocol bridges | Adapters translating foreign protocols to AGCP and back | Interface definitions for a subset. See `Architecture/Schemas/bridges.json`. None built. |
| Visual IDE | Web-based, event-driven, node-graph programming | UI mockups only. See `UI-mockups/`. |
| Agent roles | A role vocabulary for the orchestration fabric | Taxonomy. Reduction to five primitives proposed in [ADR-0005](../../docs/adr/0005-agent-role-primitives.md). |
| Deployment | Kubernetes, Docker, and GitOps across cloud, edge, and peer to peer | Narrative and diagrams. See [DEPLOYMENT_ARCHITECTURE.md](DEPLOYMENT_ARCHITECTURE.md). |
| Self-healing | MAPE-K control loop with automated remediation | Concept. The shared Knowledge model is undefined; see [ADR-0004](../../docs/adr/0004-self-evolution-sandboxing.md). |
| Self-evolution | Runtime inference of unknown protocols and generated translators | Concept, and the highest-risk element in the specification. Sandboxing is a hard constraint; see [ADR-0004](../../docs/adr/0004-self-evolution-sandboxing.md). |
| Compliance mapping | Analysis against the EU AI Act, NIST AI RMF, GDPR, HIPAA, SOC 2, and ISO/IEC 27001 | Analysis, not certification, and not legal advice. Revisions pinned in [STANDARDS-VERSIONS.md](../Requirements/STANDARDS-VERSIONS.md). |
| Observability | Structured logs, metrics, traces, and audit records | Required by `CONFORMANCE.md` `CON-CORE-015` and `CON-CORE-016`. Not implemented. |

## The decisions that matter

| Record | Decision | Status |
|---|---|---|
| [ADR-0001](../../docs/adr/0001-single-unified-protocol.md) | One unified protocol rather than profiling three | Accepted |
| [ADR-0002](../../docs/adr/0002-arc42-and-c4.md) | arc42 for narrative, C4 for structural views | Accepted |
| [ADR-0003](../../docs/adr/0003-core-and-extended-profiles.md) | Split into a core profile and extension packs | **Proposed - needs your decision** |
| [ADR-0004](../../docs/adr/0004-self-evolution-sandboxing.md) | Sandbox all self-evolution and dynamic inference | Accepted as a constraint |
| [ADR-0005](../../docs/adr/0005-agent-role-primitives.md) | Reduce 70+ roles to five primitives and personas | **Proposed - needs your decision** |

## The honest position

The specification's strength is the breadth of its design thinking and the
coherence of the AGCP premise. Its weakness is that it has never been reduced to
something buildable: the protocol surface is too wide, the role catalogue is a
taxonomy rather than a design, and the self-evolution mechanism is stated as a
capability when it is an unsolved problem with serious security implications.

The single most valuable next step is not to write more specification. It is to
choose the core profile ([ADR-0003](../../docs/adr/0003-core-and-extended-profiles.md)),
then build one end-to-end path through it.

## Related documents

- [Project status and verification](../../PROJECT_STATUS.md)
- [Conformance requirements](../../CONFORMANCE.md)
- [Reading order](../../READING-ORDER.md)
- [Glossary](../../GLOSSARY.md)
- [Pinned standard versions](../Requirements/STANDARDS-VERSIONS.md)
