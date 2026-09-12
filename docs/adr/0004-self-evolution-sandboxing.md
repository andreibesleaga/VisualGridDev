# ADR-0004: Sandbox all self-evolution and dynamic protocol inference

## Status

Accepted — as a constraint on any future implementation.

## Date

2026-09-12

## Context

The specification proposes two closely related capabilities:

1. **ML-based protocol inference** — automatically deriving a translator for an
   unknown binary protocol.
2. **LLM-based code generation** — generating adapter code at runtime.

Both are attractive, and both are, as stated, unsafe.

Parsing untrusted binary input is one of the oldest and most productive sources
of memory-safety and logic vulnerabilities in software history. Dynamically
generating code that parses attacker-influenced input removes the last barrier:
instead of a fixed parser with fixed bugs, the attacker influences the parser. In
addition, the honest version of "infer an unknown protocol automatically" is an
open research problem. A system that claims it will silently produce a wrong
translator, and a wrong translator in an agent orchestration fabric is a
privilege-escalation primitive.

The specification elsewhere claims the platform is "self-healing" and
"self-evolving". Those words describe intent; they do not describe a mechanism,
and they must not be read as evidence that the mechanism is safe.

## Decision

1. **No dynamic inference in a trusted path.** A translator for an unknown
   protocol MUST NOT be created and executed inside a process that holds
   credentials, network reach, or filesystem access.
2. **All generated or inferred translation runs in an isolated sandbox** —
   WebAssembly with no ambient authority, bounded memory, a CPU budget, and no
   network or filesystem access by default.
3. **Human promotion is mandatory.** A generated translator MUST NOT be used in
   any non-experimental path until it has been reviewed and promoted by a human,
   with the promotion recorded.
4. **Self-healing is bounded by an enumerated failure model.** Automated
   remediation MUST NOT act on a failure mode that is not explicitly documented
   for that component, and MUST NOT be able to escalate privilege.
5. **MAPE-K must be instantiated, not named.** The shared Knowledge model — its
   schema, lifetime, and conflict resolution — MUST be specified before any
   claim of "self-healing" is made public.

## Consequences

**Positive.** The most dangerous mechanism in the specification is contained, and
the claims attached to it become proportionate.

**Negative.** "Self-evolution" becomes a research track with a sandbox boundary,
not a headline feature. Some existing documents present it as a shipped
capability and will need correction.

**Obligation.** `CONFORMANCE.md` `CON-MUSTNOT-001` carries this constraint into
the normative requirement set.

## Alternatives considered

- **Allow inference with a strong review process only.** Rejected: a review
  process does not bound the blast radius of a parser bug.
- **Drop the capability entirely.** Reasonable and arguably wisest; not adopted
  as an ADR because sandboxing preserves the research option at low cost. A
  superseding ADR may remove it.
- **Rely on language-level memory safety alone (Rust, Go, or Wasm for the
  parser).** Insufficient on its own: logic flaws and resource exhaustion survive
  memory safety, and the parser still runs with ambient authority.
