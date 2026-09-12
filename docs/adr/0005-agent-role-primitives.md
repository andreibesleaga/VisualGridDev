# ADR-0005: Reduce the agent role catalogue to five primitives and personas

## Status

Proposed — requires a maintainer decision.

## Date

2026-09-12

## Context

The specification defines "70+ agent roles across 11 categories", and separately
a "reduced" set of 20 essential roles, and separately retains all 70+ roles. These
three statements coexist in the repository and contradict one another:

- `Architecture/Extensive/FINAL_UNIFIED_ARCHITECTURE_v5.0.md`: "70+ agent roles
  organized in 11 categories"
- `Architecture/Extensive/AGCP_PROTOCOL_SCHEMAS.md`: "Reduced agent roles (20
  essential)"
- `Architecture/Extensive/AGCP_SIMPLIFIED_PROTOCOL_proposed.md`: "Maintained all
  70+ roles with 8 new AI compliance supervisors"

A catalogue of 70 roles is a taxonomy, not an architecture. It is Big Design Up
Front: it front-loads vocabulary that no implementation can validate, and it
buries the small number of genuinely distinct behaviours. It also makes the
specification look less considered than it is, because most of the 70 roles
differ only in configuration.

## Decision

Define a **small set of behavioural primitives** and express the role catalogue as
personas layered on them.

Proposed primitives:

| Primitive | Responsibility |
|---|---|
| **Ingestor** | Accepts input from a source, validates it, and emits it. |
| **Processor** | Transforms input into output without external effect. |
| **Router** | Directs a message to a destination based on routing metadata. |
| **Actor** | Applies an effect outside the system, always behind human authorisation. |
| **Store** | Persists and retrieves state. |

Every one of the 70+ named roles MUST be expressible as a configuration of these
five. If a role cannot be, that is evidence the primitive set is wrong — or that
the role is not a distinct behaviour.

## Consequences

**Positive.** An implementer builds five things and configures the rest. The role
catalogue becomes documentation rather than architecture. The three contradictory
role counts collapse into one statement.

**Negative.** Named roles are more legible to a reader than "a Processor with this
configuration", so some clarity is traded for coherence. The mapping work is
non-trivial: someone must classify all 70+ roles, and some will not map cleanly.

**Obligation.** Publish the mapping table. A role that does not map is an open
question, not a silent omission.

## Alternatives considered

- **Keep 70+ first-class roles.** Rejected: unvalidatable, and it does not
  describe behaviour that differs.
- **Keep the 20-role reduction.** Better, but still a taxonomy: several of the 20
  differ only in name. Five primitives is the smaller honest answer.
- **Model roles as a behaviour tree or state machine instead of primitives.**
  Not rejected on merit, but it is a larger change and a different ADR. Worth
  revisiting once the primitives are validated by an implementation.
