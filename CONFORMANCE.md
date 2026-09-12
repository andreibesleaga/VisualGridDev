# Conformance Requirements

> **Status: draft requirements — no implementation exists and no conformance has
> been demonstrated.** This document states what an implementation would have to
> satisfy to call itself conformant. Nothing in this repository has been verified
> against it.

## 1. How to read this document

The key words **MUST**, **MUST NOT**, **REQUIRED**, **SHALL**, **SHALL NOT**,
**SHOULD**, **SHOULD NOT**, **RECOMMENDED**, **MAY**, and **OPTIONAL** are to be
interpreted as described in [RFC 2119](https://www.rfc-editor.org/rfc/rfc2119) and
[RFC 8174](https://www.rfc-editor.org/rfc/rfc8174), and are normative only when
they appear in **bold capitals**.

Terms in capitals are defined in [GLOSSARY.md](GLOSSARY.md).

## 2. Conformance levels

An implementation declares exactly one level.

| Level | Name | Meaning |
|---|---|---|
| 1 | **Core conformant** | Satisfies every `CON-CORE` requirement. May interoperate with other core-conformant implementations over the core transport. |
| 2 | **Core + Bridge conformant** | Level 1, plus at least one `CON-BRIDGE` requirement. The declaration MUST name which bridges are supported. |
| 3 | **Experimental** | Claims no conformance. MUST NOT be described as conformant anywhere. |

A conformance claim MUST state: the level, the specification revision, the
supported bridges, the core transport, and the date. A claim without a stored
conformance report (section 7) is not a conformance claim.

## 3. Core profile requirements (`CON-CORE`)

### 3.1 Message model

- **CON-CORE-001:** An implementation MUST carry every inter-component message in
  a single envelope type, `AGCPMessage`, with the field set defined in
  `Architecture/Schemas/agcp-envelope.schema.json`.
- **CON-CORE-002:** `AGCPMessage.id` MUST be a version-4 UUID, unique per logical
  message, and stable across retransmissions and retries.
- **CON-CORE-003:** `AGCPMessage.version` MUST be present and MUST name the
  protocol revision the sender implements.
- **CON-CORE-004:** The envelope MUST separate routing metadata from payload; a
  router MUST NOT need to parse the payload to route a message.
- **CON-CORE-005:** Every message MUST carry a correlation identifier that
  survives every translation across a bridge.

### 3.2 Transport

- **CON-CORE-006:** Internal AGCP communication MUST use gRPC over HTTP/2 with
  Protocol Buffers as the default serialisation.
- **CON-CORE-007:** JSON MAY be used at the external boundary only, and a
  conformant implementation MUST document where the JSON boundary lies.
- **CON-CORE-008:** An implementation MUST reject an envelope whose declared
  version it does not implement, with a typed error, rather than attempting a
  best-effort parse.

### 3.3 Identity and authorisation

- **CON-CORE-009:** Peer communication MUST be mutually authenticated with mTLS;
  an implementation MUST NOT accept an unauthenticated peer on the internal
  transport.
- **CON-CORE-010:** Every agent action MUST be authorised against an explicit
  policy; authorisation MUST NOT be inferred from network position.
- **CON-CORE-011:** Secrets MUST NOT appear in an `AGCPMessage` payload, in logs,
  or in traces.

### 3.4 Errors, limits, and degradation

- **CON-CORE-012:** Every rejection MUST return a typed error with a stable code;
  an implementation MUST NOT fail silently.
- **CON-CORE-013:** An implementation MUST enforce per-peer rate limits and a
  maximum message size, and MUST publish both as configuration.
- **CON-CORE-014:** On loss of a dependency, an implementation MUST degrade in a
  defined way and MUST surface the degraded state to operators.

### 3.5 Observability and audit

- **CON-CORE-015:** Every component MUST emit structured logs, metrics, and
  traces, correlated by the envelope's correlation identifier.
- **CON-CORE-016:** Every state-changing operation MUST produce an append-only
  audit record identifying actor, action, target, and outcome.

### 3.6 Safety boundary

- **CON-CORE-017:** An implementation MUST place any action with external,
  physical, or irreversible effect behind an explicit, authenticated human
  authorisation step.
- **CON-CORE-018:** An implementation MUST provide an operator-accessible
  mechanism to stop automated activity, and that mechanism MUST NOT depend on the
  components it stops.

## 4. Bridge requirements (`CON-BRIDGE`)

- **CON-BRIDGE-001:** A bridge MUST implement the `ProtocolBridge` interface
  defined in `Architecture/Schemas/agcp-core.proto`.
- **CON-BRIDGE-002:** A bridge MUST preserve the full original message alongside
  the translation, so that a recipient can recover what the sender actually sent.
- **CON-BRIDGE-003:** A bridge MUST NOT silently drop a field it cannot map; it
  MUST fail the translation or record the loss in the envelope metadata.
- **CON-BRIDGE-004:** A bridge MUST declare the foreign protocol revision it
  targets, and MUST reject messages from a revision it does not implement.
- **CON-BRIDGE-005:** A bridge MUST pass a stored round-trip fixture set: for
  every fixture, translate in, translate out, and compare against the recorded
  expectation.

## 5. Prohibitions

- **CON-MUSTNOT-001:** An implementation MUST NOT dynamically infer and execute a
  translator for an unknown binary protocol in a trusted path. Any such
  translation MUST run in an isolated sandbox with no ambient authority.
- **CON-MUSTNOT-002:** An implementation MUST NOT describe itself as
  "production ready", "certified", "compliant", or "secure" on the basis of this
  specification alone.
- **CON-MUSTNOT-003:** An implementation MUST NOT claim support for a bridge it
  has not tested against stored fixtures.
- **CON-MUSTNOT-004:** An implementation MUST NOT apply self-healing actions to a
  component whose failure mode is not enumerated in its own documentation.

## 6. What conformance does not mean

Conformance is a statement about protocol behaviour. It is **not** a statement
about safety, security, fitness for purpose, regulatory compliance, or
production readiness. Those require separate, deployment-specific assessment.

## 7. Conformance report

A conformance claim MUST be backed by a report recording:

1. the specification revision and the implementation revision;
2. the declared conformance level and supported bridges;
3. the result of every `CON-CORE` and claimed `CON-BRIDGE` requirement;
4. the fixture set used, and its stored location;
5. every known deviation, with justification;
6. the reviewer, the date, and the environment.

A conformance report MUST be reproducible by a third party from the stored
artefacts.

## 8. Open questions

- Which bridges are in the CORE profile? See ADR-0003.
- What is the minimum executable fixture set? No suite exists yet.
- Does a bridge-preserving round trip require byte equality, or semantic
  equality? Byte equality is stricter and is the safer default until decided.
