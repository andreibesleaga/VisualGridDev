# AI Compliance Mapping Matrix

> **Status: draft specification - not implemented and not validated.**
> This document proposes a design. No component described here has been built,
> deployed, or tested, and any figure quoted is a target rather than a
> measurement. Claims of "production ready" or "complete" inherited from earlier
> drafts are unsupported and are being retired.
> See [PROJECT_STATUS.md](../../PROJECT_STATUS.md) for the maturity boundary and known gaps.

This matrix maps VisualGridDev’s controls and features to major AI regulations and security standards.

| Control/Feature                | EU AI Act | NIST AI RMF | IEEE CertifAIEd | GDPR | SOC2 | ISO 27001 | HIPAA |
|--------------------------------|:---------:|:-----------:|:--------------:|:----:|:----:|:---------:|:-----:|
| Risk Management                |     X     |      X      |        X       |      |   X  |     X     |   X   |
| Data Governance                |     X     |      X      |        X       |  X   |   X  |     X     |   X   |
| Transparency/Explainability    |     X     |      X      |        X       |      |      |           |       |
| Human Oversight                |     X     |      X      |        X       |      |      |           |       |
| Robustness/Safety              |     X     |      X      |        X       |      |   X  |     X     |   X   |
| Cybersecurity                  |     X     |      X      |        X       |      |   X  |     X     |   X   |
| Accuracy/Validation            |     X     |      X      |        X       |      |   X  |     X     |   X   |
| Registration/Traceability      |     X     |      X      |        X       |  X   |   X  |     X     |   X   |
| Data Residency                 |     X     |      X      |        X       |  X   |   X  |     X     |   X   |
| Privacy/Confidentiality        |     X     |      X      |        X       |  X   |   X  |     X     |   X   |
| Algorithmic Bias/Fairness      |     X     |      X      |        X       |      |      |           |       |
| Auditability/Monitoring        |     X     |      X      |        X       |  X   |   X  |     X     |   X   |
| Ongoing Monitoring/Recert.     |     X     |      X      |        X       |      |   X  |     X     |   X   |
| Human-Centric/Ethical Design   |     X     |      X      |        X       |      |      |           |       |

Legend: X = a document in this repository discusses this area. It does **not** mean a control exists: no control, feature, or component has been implemented. See [PROJECT_STATUS.md](../../PROJECT_STATUS.md).
