# Contributing

## What this repository is

A draft architecture specification. Not an implementation. Contributions that
improve clarity, correctness, scope discipline, or verifiability are welcome.
Contributions that add implementation code are out of scope until the core
profile is settled.

## Before you start

Read, in order:

1. [PROJECT_STATUS.md](PROJECT_STATUS.md) — the maturity boundary and known gaps.
2. [GLOSSARY.md](GLOSSARY.md) — expand the acronyms first.
3. [CONFORMANCE.md](CONFORMANCE.md) — how requirements are stated.
4. [docs/adr/](docs/adr/) — the decisions already made, and the open ones.

## The contribution standard

1. **Open an issue before drafting a material change.** Scope, protocol, and
   safety-boundary changes need agreement before text exists.
2. **State the claim level.** Every statement is a fact, a proposal, an
   assumption, a target, or a verified result. Label it. Unlabelled capability
   statements are the repository's most common defect.
3. **Cite versions.** When you reference an external standard, pin the revision
   in [Architecture/Requirements/STANDARDS-VERSIONS.md](Architecture/Requirements/STANDARDS-VERSIONS.md).
4. **Prefer removal.** A deleted unsupported claim is worth more than a new
   paragraph hedging it.
5. **Keep the core small.** See [docs/adr/0003](docs/adr/0003-core-and-extended-profiles.md).
   New protocol coverage belongs in an extension pack, not in the core.
6. **Define before you use.** Every acronym goes in `GLOSSARY.md` on first use.
7. **Update the ADRs.** A decision change creates a new record that supersedes the
   old one. Do not edit an accepted record except to set its status.
8. **Do not add secrets, personal data, or third-party material you cannot
   licence.** See [LICENSE-SPEC.md](LICENSE-SPEC.md).
9. **Do not claim conformance, certification, or compliance.** Those follow from
   evidence, not from prose.

## Review focus

Changes touching the protocol envelope, identity, the safety boundary, or
self-evolution require review against `CONFORMANCE.md` and ADR-0004. Changes that
widen scope require an ADR.

## Licensing of contributions

Contributing prose means you agree it is licensed under CC BY-NC-ND 4.0.
Contributing a normative artefact (schema, conformance requirement, requirement
statement, diagram source) means you agree it is licensed under Apache-2.0. See
[LICENSE-SPEC.md](LICENSE-SPEC.md).

## Documentation conventions

- Descriptive, unique headings; sentence case.
- Relative links for anything inside the repository.
- RFC 2119 keywords in bold capitals only where they are normative.
- Diagrams as PlantUML source with rendered SVG committed alongside.
- Tables for enumerations; prose for reasoning.
