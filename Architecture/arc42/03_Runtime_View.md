# 3. Runtime Architecture View

> **Status: draft specification - not implemented and not validated.**
> This document proposes a design. No component described here has been built,
> deployed, or tested, and any figure quoted is a target rather than a
> measurement. Claims of "production ready" or "complete" inherited from earlier
> drafts are unsupported and are being retired.
> See [PROJECT_STATUS.md](../../PROJECT_STATUS.md) for the maturity boundary and known gaps.

## Self-Healing Runtime Scenario

1. Agent Starts
2. MAPE-K Monitoring Activated
3. Failure Detected
4. Analyze Metrics
5. Plan Recovery
6. Execute Restart/Redeploy
7. Resume Execution

## Key Components

- Node-RED Engine
- AI agents Protocol Layer
- MAPE-K Controller
- Kafka + Fitness Evaluator
