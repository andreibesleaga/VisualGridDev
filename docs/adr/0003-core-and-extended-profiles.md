# ADR-0003: Split the specification into a Core profile and Extension packs

## Status

Proposed — requires a maintainer decision.

## Date

2026-09-12

## Context

The specification currently claims interoperability with a very large protocol
surface: A2A, MCP, ANP, ACP, HTTP, MQTT, gRPC, CoAP, AMQP, Kafka, WebSocket,
WebRTC, Bluetooth, Zigbee, LoRaWAN, Modbus, DNP3, OPC-UA, BACnet, HL7, FHIR,
SQL dialects, GraphQL, SSH, SNMP, LDAP, and others. It also covers web, AI/agent
orchestration, IoT, healthcare, industrial control, and distributed ledgers.

The consequence is that nobody can implement "AGCP-compliant" and be finished.
There is no smallest thing to build, so there is no way to demonstrate progress,
and no way to test interoperability between two implementations.

This is the single largest obstacle to the specification becoming useful. It is
not a criticism of ambition; it is a criticism of testability.

## Decision

Restructure the specification into:

- **Core profile.** A small, mandatory, frozen set: the envelope, the core
  transport, identity, errors, observability, and the safety boundary. This is
  what `CONFORMANCE.md` `CON-CORE-*` already describes.
- **Extension packs.** One document per protocol family, each independently
  versioned and independently conformant. Adding an extension MUST NOT change the
  core.

An implementation declares the core plus the extensions it supports. "Core
conformant" becomes a meaningful, testable phrase.

## Consequences

**Positive.** Conformance becomes demonstrable. Two teams can interoperate on a
small surface and grow. The specification stops promising everything in one
breath, which is currently its least credible aspect.

**Negative.** Significant editorial work: existing documents must be classified as
core or extension, and several currently blend the two. Some material that reads
as central today becomes optional. That reclassification will feel like a
downgrade and should be communicated as a scoping decision, not a retraction.

**Obligation.** The core profile must be frozen for a period once chosen, or the
split achieves nothing.

## Alternatives considered

- **Keep the monolithic scope and rely on "implement what you need".** Rejected:
  it is what is happening today, and it produces no shared definition of
  conformance.
- **Drop the low-priority domains (healthcare, industrial, distributed ledgers)
  entirely.** Considered, and consistent with the earlier audit advice to focus
  on web and AI first. Rejected as an ADR because deleting domains is a product
  decision, not an architectural one. If the maintainer prefers this, it can be
  recorded as a superseding decision.
- **Define priority tiers only.** Rejected as insufficient: a priority list still
  leaves conformance undefined.

## Open questions

- Which bridges are in the core? The likely candidates are the internal transport
  plus the two agent protocols the ecosystem actually uses. The maintainer must
  choose.
- Does a core implementation have to support any bridge at all, or is a
  bridge-free core conformant? Recommend the latter, so that the core is
  independently testable.
