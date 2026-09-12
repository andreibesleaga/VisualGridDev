# Changelog

All notable changes to this specification are recorded here.

The format follows [Keep a Changelog](https://keepachangelog.com/en/1.1.0/).
Because this repository is a specification rather than software, version numbers
describe the document set, not a deployed system. See
[PROJECT_STATUS.md](PROJECT_STATUS.md) for the maturity boundary.

## [Unreleased]

### Added

- [PROJECT_STATUS.md](PROJECT_STATUS.md): evidenced maturity, a claim policy, a
  known-gaps list, release gates, and open questions.
- [CONFORMANCE.md](CONFORMANCE.md): normative requirements using RFC 2119
  keywords, split into a Core profile and a bridge profile, with explicit
  prohibitions and a conformance-report format.
- [GLOSSARY.md](GLOSSARY.md): every acronym expanded once. AGCP is defined for
  the first time in the repository's history.
- [READING-ORDER.md](READING-ORDER.md): four curated reading routes.
- [docs/adr/](docs/adr/): five architecture decision records, plus the record
  format and index.
- [LICENSE-SPEC.md](LICENSE-SPEC.md): dual licensing — Apache-2.0 for normative
  artefacts, CC BY-NC-ND 4.0 for prose.
- [Architecture/Requirements/STANDARDS-VERSIONS.md](Architecture/Requirements/STANDARDS-VERSIONS.md):
  every external standard pinned to a revision with a retrieval date.
- `Architecture/Schemas/`: machine-readable AGCP envelope and bridge definitions.
- [SECURITY.md](SECURITY.md), [CONTRIBUTING.md](CONTRIBUTING.md),
  [CODE_OF_CONDUCT.md](CODE_OF_CONDUCT.md).
- Documentation continuous integration and a pull-request template.

### Changed

- Retired unsupported "production ready", "complete", and "100%" claims across
  the document set. Requirements met by documents are not requirements met by a
  system.
- [Architecture/Requirements/Requirements.md](Architecture/Requirements/Requirements.md):
  the traceability matrix no longer reports every requirement as satisfied.
- [README.md](README.md): rewritten around the status boundary, the core/extended
  profile split, and the reading routes.

### Removed

- The reference to a non-existent `Archive/` directory.
- An empty deployment document that listed manifest headings with no manifests
  beneath them. It is now an honest description of the proposed topology and of
  what does not exist.

### Fixed after adversarial review

An adversarial review found that the corrective layer had been applied around the
legacy corpus rather than through it. This pass corrected that.

- Removed the "Key Achievements" block in
  [FINAL_UNIFIED_ARCHITECTURE_v5.0.md](Architecture/Extensive/FINAL_UNIFIED_ARCHITECTURE_v5.0.md),
  including "all inconsistencies resolved", "complete interfaces for all
  protocols", and "production deployment".
- Replaced the "Complete Protocol Schema Summary" in
  [AGCP_PROTOCOL_SCHEMAS.md](Architecture/Extensive/AGCP_PROTOCOL_SCHEMAS.md),
  which claimed 40+ protocols supported, comprehensive testing, and penetration
  testing.
- Replaced the green-tick implementation checklist in
  [IMPLEMENTATION_ROADMAP_v5.0.md](Architecture/Extensive/IMPLEMENTATION_ROADMAP_v5.0.md),
  which claimed 90%+ coverage and completed security testing.
- Replaced the "no gaps, no contradictions" section of
  [Requirements.md](Architecture/Requirements/Requirements.md).
- Framed [AI_COMPLIANCE_MATRIX_DETAILED.md](Architecture/Extensive/AI_COMPLIANCE_MATRIX_DETAILED.md)
  as a gap analysis and converted its present-tense assertions to requirements.
- Added binding sandbox constraints to the self-evolution sections of
  [FINAL_UNIFIED_ARCHITECTURE_v5.0.md](Architecture/Extensive/FINAL_UNIFIED_ARCHITECTURE_v5.0.md)
  and [TECH_STACK.md](Architecture/Extensive/TECH_STACK.md).
- Added the Apache-2.0 licence text and a scope notice, resolving the licensing
  ambiguity.
- Corrected the AGCP expansion conflict, and reclassified HTTP and WebSocket out
  of the proposed core profile.

### Known remaining work

Contradictory agent-role counts (70+, 20, and five primitives) still coexist in
legacy documents; the resolution is proposed but undecided in
[docs/adr/0005](docs/adr/0005-agent-role-primitives.md). Four AGCP version labels
also remain. Both are recorded as open questions in
[PROJECT_STATUS.md](PROJECT_STATUS.md).

## [5.0-draft] - 2025-08-05

The state of the specification as previously published: a unified architecture
draft with protocol schemas, compliance mapping, implementation roadmap, UI
mockups, and PlantUML/C4 diagrams. It asserted production readiness that was not
supported by evidence; see [PROJECT_STATUS.md](PROJECT_STATUS.md).

[Unreleased]: https://github.com/andreibesleaga/VisualGridDev/compare/main...HEAD
