# Implementation-Readiness Checklist

> **Status: draft specification - not implemented and not validated.**
> This is a checklist of what an implementer would have to produce. Every item is
> unmet: there is no implementation in this repository. An unticked box here
> means "not done", not "to be confirmed".

## How to use this document

This is not a release checklist for a system. It is a list of the evidence an
implementation would owe before anyone could reasonably rely on it. Several items
are requirements rather than tasks; where that is so, the corresponding
requirement identifier is given.

## 1. Documentation

- [ ] Architecture documents internally consistent, with contradictions resolved
- [ ] Requirements traceable, with each requirement stating an acceptance
      criterion and an owner
- [ ] Compliance analysis reviewed by counsel and pinned to specific revisions
      (`Architecture/Requirements/STANDARDS-VERSIONS.md`)
- [ ] Every diagram referenced from prose, and source committed alongside render

## 2. Architecture and code

- [ ] A core profile chosen and frozen (see `docs/adr/0003`)
- [ ] AGCP envelope implemented and validated against
      `Architecture/Schemas/agcp-envelope.schema.json`
- [ ] At least one bridge implemented and passing stored round-trip fixtures
      (`CON-BRIDGE-005`)
- [ ] Agent role catalogue reduced to primitives, with a published mapping table
      (see `docs/adr/0005`)
- [ ] Plugin and extension surface versioned, with a manifest schema

## 3. Security

- [ ] Threat model produced, including the bridge and sandbox surfaces
- [ ] Mutual authentication on all internal transport (`CON-CORE-009`)
- [ ] Explicit authorisation for every agent action (`CON-CORE-010`)
- [ ] Generated or inferred translators running only in an isolated sandbox
      (`CON-MUSTNOT-001`; see `docs/adr/0004`)
- [ ] Secret-scanning, dependency scanning, and SBOM generation in the build
- [ ] Independent security review of the protocol and the sandbox boundary

## 4. Safety and human oversight

- [ ] Every action with external, physical, or irreversible effect behind an
      authenticated human authorisation step (`CON-CORE-017`)
- [ ] A stop mechanism that does not depend on the components it stops
      (`CON-CORE-018`)
- [ ] Self-healing failure modes enumerated per component, with the actions
      permitted for each (`CON-MUSTNOT-004`)
- [ ] Sandbox escape and resource-exhaustion behaviour tested and documented

## 5. Deployment

- [ ] Core transport implemented with documented backpressure and degradation
      behaviour (`CON-CORE-014`)
- [ ] Rate limits and maximum message size enforced and configurable
      (`CON-CORE-013`)
- [ ] Deployment manifests, image builds, and pipeline definitions that actually
      build and deploy
- [ ] Rollback and recovery procedures exercised

## 6. Observability

- [ ] Structured logs, metrics, and traces correlated across components
      (`CON-CORE-015`)
- [ ] Append-only audit record for every state-changing operation
      (`CON-CORE-016`)
- [ ] Dashboards and alerting that an operator has actually used in an exercise

## 7. Testing and validation

- [ ] Conformance test suite covering every `CON-CORE` requirement
- [ ] Protocol fuzzing and malformed-input handling
- [ ] Round-trip fixtures stored for every claimed bridge (`CON-BRIDGE-005`)
- [ ] Benchmarks with a stated operational design domain, and published results
- [ ] A stored conformance report in the format given by `CONFORMANCE.md` section 7

## 8. Packaging and publication

- [ ] Licensing reconciled: prose and normative artefacts clearly separated
      (`LICENSE-SPEC.md`)
- [ ] Version numbering that reflects reality - a draft is not "1.0"
- [ ] A published core specification with a change process

---

**This checklist is unmet in every respect.** The repository is a specification.
See [PROJECT_STATUS.md](../../PROJECT_STATUS.md) for the current maturity and the
list of known gaps.
