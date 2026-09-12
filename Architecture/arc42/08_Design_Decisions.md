# 8. Design Decisions

> **Status: draft specification - not implemented and not validated.**
> This document proposes a design. No component described here has been built,
> deployed, or tested, and any figure quoted is a target rather than a
> measurement. Claims of "production ready" or "complete" inherited from earlier
> drafts are unsupported and are being retired.
> See [PROJECT_STATUS.md](../../PROJECT_STATUS.md) for the maturity boundary and known gaps.

The load-bearing decisions have dated records in [docs/adr/](../../docs/adr/).
Each states the context, the decision, the consequences, and the alternatives
that were considered.

| Decision | Record | Status |
|---|---|---|
| One unified protocol (AGCP) rather than profiling three | [ADR-0001](../../docs/adr/0001-single-unified-protocol.md) | Accepted |
| arc42 for narrative, C4 for structural views | [ADR-0002](../../docs/adr/0002-arc42-and-c4.md) | Accepted |
| Core profile plus extension packs | [ADR-0003](../../docs/adr/0003-core-and-extended-profiles.md) | Proposed |
| Sandbox self-evolution and dynamic inference | [ADR-0004](../../docs/adr/0004-self-evolution-sandboxing.md) | Accepted |
| Five agent primitives instead of 70+ roles | [ADR-0005](../../docs/adr/0005-agent-role-primitives.md) | Proposed |

The technology selections listed below are **preferences recorded in the
documents**, not committed dependencies. Each requires a decision record with a
measurable benefit before it can be called a decision.

- Node-RED as the visual-flow runtime, on the strength of its extensibility.
- A2A, ACP, and MCP as the agent-interoperability targets.
- Kafka as the streaming substrate.
- MAPE-K as the self-healing control loop.
- SQLite-AI for edge inference and vector indexing.
