# Project Status and Verification

## Current maturity

This repository is a **draft architecture specification**. It contains proposals,
narrative, and diagrams. It contains no implementation, no executable component,
no test suite, and no deployment. Nothing described here has been built, run,
measured, or independently reviewed.

Earlier drafts of this repository asserted that the architecture was "production
ready", "complete", and "100%" compliant. Those assertions were not supported by
evidence and are being retired. Where they remain in older documents, they are
historical prose, not claims.

| Capability | Current evidence | Public claim permitted |
|---|---|---|
| Architecture description (arc42, C4, PlantUML) | Documents and diagrams only | A proposed architecture exists |
| AGCP protocol | Interface sketches and schemas | A protocol is proposed, not specified to implementation quality |
| Protocol bridges | Interface definitions for a subset | A bridge design is sketched, not built or tested |
| Agent role system | Enumerated role names | Role vocabulary is proposed, not implemented |
| Visual IDE | Mockups and screenshots | A user-interface concept is illustrated |
| Mesh deployment | Narrative and diagrams | Deployment is described, not performed |
| Self-healing / self-evolution | Concept descriptions | Mechanisms are proposed; safety behaviour is undefined |
| Compliance mapping | Mapping tables to named regulations | Mappings are analysis, not certification or legal advice |
| Conformance | This repository's `CONFORMANCE.md` | Requirements are stated; no implementation has been verified against them |

## Claim policy

Use **proposed**, **draft**, **illustrated**, **target**, or **requires
validation** for every design statement.

Do not use **production ready**, **complete**, **finished**, **fully
implemented**, **validated**, **certified**, **compliant**, **secure**,
**battle-tested**, or any quantified performance figure, unless the claim links
to reproducible evidence with conditions, version, date, and limitations. If no
such record exists, the claim must be removed or restated as a target.

## Known gaps

These are the material gaps between what the specification asserts and what is
demonstrated. They are stated here deliberately.

1. **No implementation and no reference firmware.** AGCP exists only as schema
   and prose.
2. **No conformance test suite.** `CONFORMANCE.md` states requirements; nothing
   verifies them.
3. **No benchmark evidence.** Latency, throughput, and availability figures are
   targets, not measurements.
4. **Scope exceeds a single coherent product.** The specification covers web,
   AI/agent orchestration, IoT, healthcare, industrial control, and distributed
   ledgers simultaneously. See ADR-0003 for the proposed core/extended split.
5. **Agent role catalogue is inflated.** "70+ roles" is a taxonomy, not a design.
   See ADR-0005 for the proposed reduction to a small set of primitives.
6. **Self-evolution is an unsolved problem.** Dynamic inference of unknown binary
   protocols has no demonstrated safe implementation and is a security hazard.
   See ADR-0004.
7. **Licence previously blocked implementation.** CC BY-NC-ND 4.0 prohibits
   derivative and commercial use, which is incompatible with the stated goal of
   driving conforming implementations. See `LICENSE-SPEC.md`.
8. **No external standard versions pinned.** See
   `Architecture/Requirements/STANDARDS-VERSIONS.md`.
9. **`Archive/` was referenced but does not exist.** The reference has been
   removed.
10. **The acronym AGCP was never expanded anywhere in this repository.** It is
    now defined in `GLOSSARY.md` as _Agentic Grid Communication Protocol_. One
    legacy document still uses a different expansion and a different version
    label, and that document has not yet had its consistency pass.

## Release gates

No specification release may be labelled "1.0" or "complete" until every gate
below is closed with reviewable evidence.

| Gate | Minimum evidence | Accountable role |
|---|---|---|
| Scope | A published core profile with an explicit deferred list | Editor |
| Protocol | A frozen, versioned AGCP core specification with a change process | Protocol editor |
| Conformance | A normative requirement set with an executable test suite and at least two independent implementations | Conformance lead |
| Security | Threat model, sandboxing design for generated code, and a security review | Security lead |
| Safety | Analysis of self-healing and self-evolution behaviour, including failure modes and manual override | Safety lead |
| Performance | Reproducible benchmarks under a stated operational design domain | Performance lead |
| Compliance | Version-pinned regulatory assessment reviewed by counsel | Compliance lead |
| Licence | Clear licensing for prose and for normative artefacts | Maintainer |

## Verification record format

Every future claim must record: repository revision; artefact version;
environment; procedure; pass or fail criterion; actual result; limitation;
reviewer; date; and a link to retained evidence. The absence of that record means
**not verified**.

## Open questions for the maintainer

1. **AGCP name collision.** "AGCP" is not currently registered with IANA or a
   standards body as far as this audit could determine; confirm no collision
   before publishing the name as normative.
2. **Core profile contents.** Which of the ~40 bridges belong in the core
   mandatory set, and which move to an extension pack?
3. **Primary reader.** External implementers, internal architects, or a
   regulator? This determines what `CONFORMANCE.md` must guarantee.
4. **Version 5.0 meaning.** The specification calls itself v5.0 while no v1.0 was
   ever implemented. Consider resetting to 0.x until the first conformance
   result exists.
5. **Third-party protocol status.** A2A, MCP, ANP, and ACP are moving targets.
   Confirm which revision this specification targets.
6. **Protocol version label.** Four different AGCP version labels appear across
   the documents (v1.0, 2.0, 5.0, and 0.1.0-draft). One must be chosen.
7. **arc42 debt.** Several `Architecture/arc42/` documents are near-empty stubs.
   Either complete them or fold them into the narrative they restate.
