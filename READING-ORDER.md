# Reading Order

> **Status: draft specification — not implemented.** This repository contains
> proposals and diagrams only. See [PROJECT_STATUS.md](PROJECT_STATUS.md).

There are roughly 11,200 lines of Markdown here. Reading it front to back is not
the fastest path to understanding it. This document gives four routes.

## Route 1 — Orientation (about 20 minutes)

For anyone evaluating whether this project is relevant to them.

1. [PROJECT_STATUS.md](PROJECT_STATUS.md) — what exists, what does not, and the
   known gaps.
2. [README.md](README.md) — the proposal in brief.
3. [GLOSSARY.md](GLOSSARY.md) — expand the acronyms before they pile up.
4. [CONFORMANCE.md](CONFORMANCE.md) — what an implementation would have to do,
   and what conformance does not mean.

## Route 2 — Architecture review (about 2 hours)

For an architect assessing the design.

1. [Architecture/arc42/01_Introduction_and_Vision.md](Architecture/arc42/01_Introduction_and_Vision.md)
2. [Architecture/arc42/02_Architecture_Overview.md](Architecture/arc42/02_Architecture_Overview.md)
3. [Architecture/Extensive/FINAL_UNIFIED_ARCHITECTURE_v5.0.md](Architecture/Extensive/FINAL_UNIFIED_ARCHITECTURE_v5.0.md)
   — the master specification. Read it critically; it is the document that
   inherited the most unsupported claims.
4. [Architecture/Extensive/C4_DIAGRAMS.md](Architecture/Extensive/C4_DIAGRAMS.md)
5. [Architecture/Requirements/Requirements.md](Architecture/Requirements/Requirements.md)
   — note that its status column is being reworked; treat every tick as a claim
   under review, not as evidence.
6. [docs/adr/](docs/adr/) — why the load-bearing decisions were made, and which
   are still open.

## Route 3 — Protocol review (about 2 hours)

For anyone implementing or evaluating AGCP.

1. [Architecture/Extensive/AGCP_SIMPLIFIED_PROTOCOL_proposed.md](Architecture/Extensive/AGCP_SIMPLIFIED_PROTOCOL_proposed.md)
   — start here. It is the most current protocol statement.
2. [Architecture/Extensive/AGCP_PROTOCOL_SCHEMAS.md](Architecture/Extensive/AGCP_PROTOCOL_SCHEMAS.md)
   — the fuller schema set, including per-bridge interfaces.
3. [Architecture/Schemas/](Architecture/Schemas/) — machine-readable envelope
   and bridge definitions.
4. [CONFORMANCE.md](CONFORMANCE.md) — the normative requirements that follow from
   the above.

## Route 4 — Compliance and risk review (about 1 hour)

For a risk, security, or compliance reviewer.

1. [PROJECT_STATUS.md](PROJECT_STATUS.md) — the gap list, first.
2. [Architecture/arc42/06_Security_Architecture.md](Architecture/arc42/06_Security_Architecture.md)
3. [Architecture/Extensive/AI_COMPLIANCE_MATRIX_DETAILED.md](Architecture/Extensive/AI_COMPLIANCE_MATRIX_DETAILED.md)
   and [Architecture/Extensive/AI_COMPLIANCE_REGULATIONS.md](Architecture/Extensive/AI_COMPLIANCE_REGULATIONS.md)
   — read as analysis, not as certification.
4. [Architecture/Requirements/STANDARDS-VERSIONS.md](Architecture/Requirements/STANDARDS-VERSIONS.md)
   — which revision of each standard the mapping targets.
5. [docs/adr/0004-self-evolution-sandboxing.md](docs/adr/0004-self-evolution-sandboxing.md)
   — the highest-risk mechanism in the specification.

## What to read first if you only have five minutes

Read [PROJECT_STATUS.md](PROJECT_STATUS.md). If the maturity boundary and the
known-gaps list are acceptable to you, continue. If not, the remaining 9,600
lines will not change that.
