# 6. Security Architecture

> **Status: draft specification - not implemented and not validated.**
> This document proposes a design. No component described here has been built,
> deployed, or tested, and any figure quoted is a target rather than a
> measurement. Claims of "production ready" or "complete" inherited from earlier
> drafts are unsupported and are being retired.
> See [PROJECT_STATUS.md](../../PROJECT_STATUS.md) for the maturity boundary and known gaps.

## Trust Boundaries

- Agent-to-Agent: mTLS
- Device-to-Agent: Encrypted + Signed
- IDE Access: OAuth2 + JWT

## Identity Management

- X.509 per agent
- RBAC policies for admin/developer roles
- Signed workflows and encrypted messages

## Threat Mitigations

- Certificate rotation
- Secure bootstrap
- Attack surface minimization at edges

---

## 🛡️ Security for Extensibility, Self-Healing, and Compliance

These are **requirements, not achieved properties**. Nothing is implemented.

- Extensions and plugins **must** be signed, validated, and sandboxed at runtime
  (`CONFORMANCE.md`; [ADR-0004](../../docs/adr/0004-self-evolution-sandboxing.md)).
- Self-healing **must not** act on an undocumented failure mode and **must not**
  be able to escalate privilege (`CON-MUSTNOT-004`). No agent enforces anything
  today, because no agent exists.
- Compliance hooks are **requirements to be designed**, not integrations that
  exist. The mapping documents are analysis, not certification; see
  [SECURITY.md](../../SECURITY.md) and [PROJECT_STATUS.md](../../PROJECT_STATUS.md).
- Real-time security status and alerts are streamed to the Visual IDE dashboard.
- All system upgrades and schema imports are versioned, auditable, and can be rolled back.
