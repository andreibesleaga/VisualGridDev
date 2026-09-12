# 9. Architecture Analysis

> **Status: draft specification - not implemented and not validated.**
> This document proposes a design. No component described here has been built,
> deployed, or tested, and any figure quoted is a target rather than a
> measurement. Claims of "production ready" or "complete" inherited from earlier
> drafts are unsupported and are being retired.
> See [PROJECT_STATUS.md](../../PROJECT_STATUS.md) for the maturity boundary and known gaps.

## Gaps identified

_Addressed in documents_ means a document discusses the gap. It does **not**
mean the gap is closed in a system, because no system exists.

| Gap | How the documents address it | Status |
|---|---|---|
| Protocol fragmentation | A single envelope is proposed; see [ADR-0001](../../docs/adr/0001-single-unified-protocol.md) | Proposed |
| MAPE-K named but never instantiated | The shared Knowledge model remains undefined | **Open** |
| Security under-specified | Control requirements stated in [06_Security_Architecture.md](06_Security_Architecture.md) and `CONFORMANCE.md` | Requirements stated, unverified |
| No runtime view | A runtime view exists at [03_Runtime_View.md](03_Runtime_View.md) | Documented |
| Non-functional requirements missing | Targets stated in [07_NFR_SLA_Table.md](07_NFR_SLA_Table.md) | Targets, not measurements |
| Scope too wide to implement | Core profile split proposed; see [ADR-0003](../../docs/adr/0003-core-and-extended-profiles.md) | **Open** |
| Role catalogue inflated | Reduction to primitives proposed; see [ADR-0005](../../docs/adr/0005-agent-role-primitives.md) | **Open** |
| No implementation and no conformance suite | See [PROJECT_STATUS.md](../../PROJECT_STATUS.md) | **Open** |
