# ADR-0001: One unified protocol (AGCP) rather than three profiles

## Status

Accepted

## Date

2026-09-12 (recorded retroactively; the decision predates this record)

## Context

The platform is intended to orchestrate agents and bridges across web, IoT,
industrial control, and legacy systems. The obvious alternative to inventing a
protocol is to pick a small number of existing ones — for example A2A for agent
interoperability, MCP for tool and context access, and gRPC for internal
transport — and profile each.

The specification instead defines a single envelope, the **Agentic Grid
Communication Protocol (AGCP)**, and translates every foreign protocol into it.

The tension is real. A universal envelope has to express HTTP request semantics,
streaming media semantics, and industrial polling semantics in one shape. Each
of those carries features the others do not, and a single envelope will either
grow to accommodate all of them or silently lose information.

## Decision

Adopt a single unified envelope (AGCP) as the internal representation, and treat
all foreign protocols as edge adapters.

Two constraints make this decision safe rather than merely convenient:

1. **The envelope carries a lossless sidecar.** A bridge preserves the original
   message alongside the translation so that a recipient can always recover what
   the sender actually sent. See `CONFORMANCE.md` `CON-BRIDGE-002`.
2. **The core is deliberately small.** AGCP does not attempt to model HTTP,
   DNP3, or WebRTC semantics in the envelope. It models a message with routing,
   identity, and a payload, and pushes protocol semantics into the adapter.

## Consequences

**Positive.** Components need to implement one dispatch path, one identity model,
one observability model, and one error model. Bridges become independently
testable and independently replaceable. A new protocol is an addition, not a
change to the core.

**Negative.** Every bridge is a source of fidelity loss; the sidecar mitigates
but does not eliminate this. Translation costs latency, which makes the
specification's most aggressive latency targets harder to reach, not easier. The
specification therefore must not promise low latency for a path that crosses two
bridges until that path is measured.

**Obligation.** The specification must document, per bridge, which source
features have no AGCP representation. That list is currently incomplete.

## Alternatives considered

- **Profile three protocols and translate only at the boundary.** Rejected
  because it pushes the translation problem into every component rather than into
  one place, and loses the single observability and identity model.
- **Adopt A2A as the core envelope.** Rejected at the time because A2A targets
  agent interoperability specifically and does not describe industrial or
  streaming transports. Revisit if A2A's scope broadens.
- **No unified envelope; each subsystem speaks its native protocol.** Rejected as
  it removes the interoperability premise of the product.
