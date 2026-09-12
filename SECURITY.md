# Security Policy

## Scope

This repository contains **architecture documentation only**. There is no
executable code, no build system, no runtime, and no deployed service. The
security scope is therefore the repository's contents and its supply chain, not
an operating system.

## Reporting a vulnerability

Do not open a public issue for a security problem.

- Use GitHub's private vulnerability reporting for this repository where
  available.
- If it is not available, open a minimal public issue asking the maintainer for a
  private channel. Include no exploit detail.

Please include: the affected file and revision; a concise impact statement;
reproduction steps or a safe proof of concept; and any proposed remediation.

Reports are handled on a best-effort basis. This document promises no response
time or support window.

## What counts as a security issue here

- A normative requirement in [CONFORMANCE.md](CONFORMANCE.md) that, if followed,
  would create a vulnerability.
- A schema in `Architecture/Schemas/` that permits injection, unsafe
  deserialisation, or unauthenticated behaviour.
- A design in the specification that places untrusted input in a trusted path —
  for example, executing a generated protocol translator outside a sandbox.
- A committed secret, credential, or token.
- A materially misleading security or compliance claim.

## Design constraints that are security-relevant

These are recorded as requirements, not as achieved properties.

- Generated or inferred protocol translators MUST run in an isolated sandbox with
  no ambient authority. See [docs/adr/0004](docs/adr/0004-self-evolution-sandboxing.md)
  and `CONFORMANCE.md` `CON-MUSTNOT-001`.
- Internal transport MUST be mutually authenticated. See `CON-CORE-009`.
- Agent actions MUST be authorised explicitly and MUST NOT be inferred from
  network position. See `CON-CORE-010`.
- Actions with external, physical, or irreversible effect MUST require explicit
  human authorisation. See `CON-CORE-017`.
- Self-healing MUST NOT act on an undocumented failure mode. See `CON-MUSTNOT-004`.

## Compliance claims

Mappings to the EU AI Act, NIST AI RMF, GDPR, HIPAA, SOC 2, and ISO/IEC 27001 in
this repository are **analysis**, not certification, and not legal advice. See
`PROJECT_STATUS.md` and `Architecture/Requirements/STANDARDS-VERSIONS.md`.
