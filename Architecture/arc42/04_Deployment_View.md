# 4. Deployment View

> **Status: draft specification - not implemented and not validated.**
> This document proposes a design. No component described here has been built,
> deployed, or tested, and any figure quoted is a target rather than a
> measurement. Claims of "production ready" or "complete" inherited from earlier
> drafts are unsupported and are being retired.
> See [PROJECT_STATUS.md](../../PROJECT_STATUS.md) for the maturity boundary and known gaps.

## Layers and Platforms

- **Frontend IDE**: React, Monaco Editor
- **Edge Runtime**: Node-RED fork, SQLite-AI
- **Streaming Layer**: Kafka, LangChain Workers
- **Cloud Orchestration**: Kubernetes, Prometheus

## Platforms

- Edge: Linux, Android
- Backend: Cloud (K8s)
- Monitoring: Prometheus + Grafana
