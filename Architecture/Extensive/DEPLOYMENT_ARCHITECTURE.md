# VisualGridDev Deployment Architecture

> **Status: draft specification - not implemented and not validated.**
> This document proposes a design. No component described here has been built,
> deployed, or tested, and any figure quoted is a target rather than a
> measurement. Claims of "production ready" or "complete" inherited from earlier
> drafts are unsupported and are being retired.
> See [PROJECT_STATUS.md](../../PROJECT_STATUS.md) for the maturity boundary and known gaps.

**Version**: 5.0-draft
**Date**: 2025-08-05

## What this document contains, and what it does not

This document describes a **proposed** deployment topology. It contains no
manifests, no Helm values, no Dockerfiles, no Terraform, and no pipeline
definitions. Earlier revisions of this document listed headings such as
"Kubernetes Deployment Manifests" with no manifest beneath them; those empty
placeholders have been removed rather than left to imply content that does not
exist.

## Proposed deployment targets

| Target | Intended shape | Status |
|---|---|---|
| Cloud | Kubernetes with Helm release management, GitOps reconciliation | Proposed |
| Edge | Lightweight agent on constrained nodes, offline-capable | Proposed |
| Peer to peer | Node-to-node AGCP peering without a central broker | Proposed |
| Local development | Container composition for a single-machine environment | Proposed |

## Cloud topology

The proposal is a Kubernetes deployment reconciled by a GitOps controller, with
Git as the single source of truth for desired state.

- Each AGCP component (core router, bridge, agent runtime) is proposed as its own
  workload, so it can be scaled and upgraded independently.
- Configuration is proposed to be declarative and environment-scoped, with
  secrets supplied from an external secret store and never committed.
- Network policy is proposed to default to deny, with explicit allowances per
  component pair.

None of this exists. The design intent is recorded here so that an implementer
inherits the constraints rather than inventing them.

## Edge topology

Edge nodes are the hardest deployment target and the least specified.

- An edge node is assumed to be resource-constrained, intermittently connected,
  and physically accessible to third parties.
- The proposed agent must therefore operate offline, bound its own resource use,
  and treat local state as untrusted on restart.
- Update and rollback must be signed and reversible; an edge node that cannot be
  recovered in the field is a liability.

## Development environment

A single-machine composition is proposed so a contributor can run the core and
its dependencies without cloud credentials. This is a prerequisite for the
conformance test suite and does not exist yet.

## Infrastructure as code

Infrastructure is proposed to be declarative and reviewable, with no manual
console changes. This is a stated intent, not an implemented practice.

## Build and release pipeline

The proposed pipeline stages are: lint, schema validation, build, conformance
tests, security scanning, SBOM generation, signing, and staged rollout. The
repository ships a documentation-only pipeline today (see
[`.github/workflows/docs.yml`](../../.github/workflows/docs.yml)); the build and
release stages cannot exist until there is something to build.

## Self-healing deployment

The specification proposes self-healing agents that monitor health, restart or
migrate workloads, and accept hot-patched plugins.

**This is the least defined and most dangerous part of the design.** Automated
remediation that can restart, migrate, or reconfigure workloads is a privileged
capability, and it must not act on failure modes that are not enumerated for the
component in question. The constraints are recorded in
[ADR-0004](../../docs/adr/0004-self-evolution-sandboxing.md) and carried as
`CONFORMANCE.md` `CON-MUSTNOT-004`. Until those constraints are satisfied, the
self-healing claims in the wider document set must be read as intent.

## What does not exist

- No container images, Helm charts, or manifests.
- No Terraform or equivalent infrastructure definitions.
- No CI/CD pipeline beyond documentation checks.
- No edge agent.
- No environment in which any of this has run.
