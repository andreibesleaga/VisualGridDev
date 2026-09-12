# 7. SLA and Non-Functional Requirements

> **Status: draft specification - not implemented and not validated.**
> This document proposes a design. No component described here has been built,
> deployed, or tested, and any figure quoted is a target rather than a
> measurement. Claims of "production ready" or "complete" inherited from earlier
> drafts are unsupported and are being retired.
> See [PROJECT_STATUS.md](../../PROJECT_STATUS.md) for the maturity boundary and known gaps.

| Metric                | Target                     |
|-----------------------|----------------------------|
| Availability          | 99,90% core services       |
| Latency (intra-mesh)  | <50ms                      |
| Latency (cloud-edge)  | <200ms                     |
| Throughput            | 1M msgs/sec                |
| Concurrent Agents     | 10,000+                    |
| Message Durability    | 30-day streaming retention |
