# AGCP Schemas (machine-readable, draft)

> **Status: draft, non-normative until frozen.** These files make the AGCP
> envelope and the bridge interface reviewable by tooling. They are derived from
> the prose specification and have not been validated against any implementation,
> because none exists.

## Licence

Everything in this directory is a **normative artefact** and is licensed under
the Apache License 2.0. See [LICENSE-SPEC.md](../../LICENSE-SPEC.md) and
[LICENSE-APACHE](../../LICENSE-APACHE).

## Files

| File | Purpose |
|---|---|
| [`agcp-envelope.schema.json`](agcp-envelope.schema.json) | JSON Schema (2020-12) for the AGCP message envelope |
| [`agcp-core.proto`](agcp-core.proto) | Protocol Buffers (proto3) for the envelope and the bridge service |
| [`bridges.json`](bridges.json) | Machine-readable bridge registry with profile classification |

## Why JSON Schema _and_ Protocol Buffers

They serve different purposes and neither replaces the other.

- **Protocol Buffers** is the proposed on-wire format for internal AGCP
  communication (`CONFORMANCE.md` `CON-CORE-006`). It is compact and gives a
  generated, typed API.
- **JSON Schema** validates the JSON form used at the external boundary
  (`CON-CORE-007`) and, more importantly here, lets a documentation repository
  validate its own examples. It is the artefact a reader can check without a
  toolchain.

## Alignment deltas against the prose

The prose schema in `Architecture/Extensive/AGCP_PROTOCOL_SCHEMAS.md` predates
this directory. These are the deltas, recorded rather than silently applied.
They must be folded back into the prose during the next editorial pass.

| # | Delta | Reason |
|---|---|---|
| 1 | `correlationId` is a first-class field, not an overload of `trace` | `CON-CORE-005` requires correlation to survive bridge translation; overloading an optional tracing field cannot guarantee that. |
| 2 | `encoding` is a closed enum of `json` and `protobuf` | `binary` is ambiguous and cannot be validated. `CON-CORE-006` names Protocol Buffers explicitly. |
| 3 | `data` is bounded in size by `maxPayloadBytes` | `CON-CORE-013` requires an enforced maximum; an unbounded `any` field cannot enforce one. |
| 4 | `auth` is removed from the envelope | `CON-CORE-011` prohibits credentials in the payload or envelope; authentication belongs to the transport. A message-level signature is retained. |
| 5 | `version` is a semantic version string, not the literal `"2.0"` | A literal cannot express a future compatible revision. |
| 6 | The bridge registry classifies every bridge as `core` or `extension` | See `docs/adr/0003-core-and-extended-profiles.md`. |

## Validation

```bash
# JSON Schema is valid and self-consistent
python3 -c "import json; json.load(open('Architecture/Schemas/agcp-envelope.schema.json'))"

# Protocol Buffers compiles (requires protoc)
protoc --proto_path=Architecture/Schemas --descriptor_set_out=/dev/null Architecture/Schemas/agcp-core.proto

# The bridge registry is valid JSON and every entry has a profile
python3 -c "import json; d=json.load(open('Architecture/Schemas/bridges.json')); \
assert all('profile' in b for b in d['bridges']); print(len(d['bridges']), 'bridges')"
```

## Status of each file

Nothing here is frozen. A bridge entry is a _claim that a bridge is planned_, not
evidence that it works. `CONFORMANCE.md` `CON-MUSTNOT-003` forbids claiming
support for a bridge that has not passed stored fixtures.
