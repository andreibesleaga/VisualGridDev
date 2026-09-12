# Architecture Decision Records

This directory records the decisions that shape the specification, in the form
of numbered, dated, immutable records. Each record states the context, the
decision, the consequences, and the alternatives that were considered.

The purpose is to preserve the **why**. A specification that states only _what_
cannot be implemented confidently, because an implementer cannot tell which
constraints are load-bearing and which are incidental.

## Format

Each record follows the structure popularised by Michael Nygard:

```text
# ADR-NNNN: Short title
## Status
## Date
## Context
## Decision
## Consequences
## Alternatives considered
```

Status is one of: **Proposed**, **Accepted**, **Deprecated**, **Superseded by
ADR-NNNN**.

Records are never edited after acceptance. A change of mind produces a new record
that supersedes the old one, and the old record's status is updated to point at
its successor. That single change to the status line is the only permitted
mutation.

## Index

| Record | Title | Status |
|---|---|---|
| [ADR-0001](0001-single-unified-protocol.md) | One unified protocol (AGCP) rather than three profiles | Accepted |
| [ADR-0002](0002-arc42-and-c4.md) | arc42 for narrative, C4 for structural views | Accepted |
| [ADR-0003](0003-core-and-extended-profiles.md) | Split the specification into a Core profile and Extension packs | Proposed |
| [ADR-0004](0004-self-evolution-sandboxing.md) | Sandbox all self-evolution and dynamic protocol inference | Accepted |
| [ADR-0005](0005-agent-role-primitives.md) | Reduce the agent role catalogue to five primitives and personas | Proposed |
