# Referenced Standards — Pinned Versions

> **Status: draft specification - not implemented and not validated.**
> This document proposes a design. No component described here has been built,
> deployed, or tested, and any figure quoted is a target rather than a
> measurement. Claims of "production ready" or "complete" inherited from earlier
> drafts are unsupported and are being retired.
> See [PROJECT_STATUS.md](../../PROJECT_STATUS.md) for the maturity boundary and known gaps.
>
> This register pins the revision of every external standard the specification
> targets. A conforming implementation cannot be assessed against a moving
> target, so each citation must resolve to a specific revision.

**Register snapshot date:** 2026-09-12

Retrieval URLs are given for the primary source. Where a source is a "living"
document with no fixed revision, that is stated explicitly and the retrieval date
is the pin.

## Regulation

| Standard | Pinned revision | Primary source | Notes |
|---|---|---|---|
| EU AI Act | Regulation (EU) 2024/1689 | <https://eur-lex.europa.eu/eli/reg/2024/1689/oj> | In force 1 Aug 2024; general application from 2 Aug 2026, with staged provisions. Article 6 obligations apply later. Classification is deployment-specific; verify current guidance before relying on it. |
| GDPR | Regulation (EU) 2016/679 | <https://eur-lex.europa.eu/eli/reg/2016/679/oj> | As adopted. EDPB guidance is living and must be checked separately. |
| HIPAA Privacy and Security Rules | 45 CFR Parts 160 and 164 | <https://www.ecfr.gov/current/title-45/subtitle-A/subchapter-C/part-164> | Living eCFR; the Security Rule NPRM of January 2025 is not yet final. Verify status. |

## Frameworks and programmes

| Standard | Pinned revision | Primary source | Notes |
|---|---|---|---|
| NIST AI Risk Management Framework | AI RMF 1.0 (NIST AI 100-1, January 2023) | <https://doi.org/10.6028/NIST.AI.100-1> | The Generative AI Profile (NIST AI 600-1, July 2024) is cited separately where applicable. A revision may be in progress; verify. |
| NIST Generative AI Profile | NIST AI 600-1, July 2024 | <https://doi.org/10.6028/NIST.AI.600-1> | — |
| IEEE CertifAIEd | Programme based on the IEEE 7000 series | <https://standards.ieee.org/products-programs/icap/ieee-certifaied/> | Confirm the targeted programme revision; the mapping in this repository does not claim certification. |
| SOC 2 | AICPA Trust Services Criteria (2017), with the 2022 revised points of focus | <https://www.aicpa-cima.com/topic/audit-assurance/audit-and-assurance-greater-than-soc-2> | SOC 2 is an attestation outcome, not a specification one can comply with unilaterally. |
| ISO/IEC 27001:2022 | ISO/IEC 27001:2022 | <https://www.iso.org/standard/27001> | Supersedes the 2013 edition. |

## Engineering standards and methods

| Standard | Pinned revision | Primary source | Notes |
|---|---|---|---|
| RFC 2119 | RFC 2119 (March 1997) | <https://www.rfc-editor.org/rfc/rfc2119> | Requirement keywords. |
| RFC 8174 | RFC 8174 (May 2017) | <https://www.rfc-editor.org/rfc/rfc8174> | Keywords are normative only in capitals. |
| C4 model | As published by Simon Brown | <https://c4model.com/> | Living; no numbered revision. |
| arc42 | Template version 8 | <https://arc42.org/> | Verify the current template version when regenerating the arc42 section. |
| PlantUML | Living language | <https://plantuml.com/> | Diagrams are validated by rendering, not by version pin. |
| OpenTelemetry | Living specification | <https://opentelemetry.io/docs/specs/> | Pin the SDK version at implementation time. |
| OWASP ASVS | 5.0 (May 2025) | <https://owasp.org/www-project-application-security-verification-standard/> | Applies only once an implementation exists. |
| SLSA | v1.1 | <https://slsa.dev/spec/v1.1/> | Build-integrity levels. |
| CycloneDX | 1.6 | <https://cyclonedx.org/specification/overview/> | SBOM format. |
| SPDX licence list | Living | <https://spdx.org/licenses/> | Used for licence identifiers. |
| AI Act Annex III | Annex III to Regulation (EU) 2024/1689 | <https://eur-lex.europa.eu/eli/reg/2024/1689/oj> | High-risk use categories referenced by the compliance mapping. |

## Third-party protocols cited by the specification

These are **not owned by this project**. AGCP translations must declare the exact
foreign revision they target.

| Protocol | Revision targeted here | Primary source | Notes |
|---|---|---|---|
| A2A | Not pinned | Verify the current published revision and governance | Cited as an interoperability target. |
| MCP | Not pinned | Verify the current published revision and governance | Cited as an interoperability target. |
| ANP | Not pinned | Verify scope and governance | Cited; status uncertain. |
| ACP | Not pinned | Verify scope and governance | Cited; status uncertain. |
| gRPC | Not pinned | <https://grpc.io/> | Proposed internal transport baseline. |
| Protocol Buffers | Proto3 | <https://protobuf.dev/programming-guides/proto3/> | Proposed internal serialisation. |
| MQTT | MQTT 5.0 (OASIS) | <https://docs.oasis-open.org/mqtt/mqtt/v5.0/> | Cited bridge target. |
| CAP | CAP 1.2 (OASIS) | <https://docs.oasis-open.org/emergency/cap/v1.2/> | Referenced where alerting is discussed; alert publication is out of scope for this platform. |

## Rules for maintainers

1. Adding a citation to a standard requires an entry in this table.
2. Do not cite a standard without a revision. "GDPR-compliant" and "SOC 2
   compliant" are not revisions.
3. A living standard is pinned by retrieval date, and the pin must be refreshed
   as part of each specification release.
4. A mapping table (for example `AI_COMPLIANCE_MATRIX_DETAILED.md`) must state
   which revision it maps against.
