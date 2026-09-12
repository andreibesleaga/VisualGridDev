# 1. Introduction & Vision

> **Status: draft specification - not implemented and not validated.**
> This document proposes a design. No component described here has been built,
> deployed, or tested, and any figure quoted is a target rather than a
> measurement. Claims of "production ready" or "complete" inherited from earlier
> drafts are unsupported and are being retired.
> See [PROJECT_STATUS.md](../../PROJECT_STATUS.md) for the maturity boundary and known gaps.

VisualGridDev is a next-generation platform designed to unify visual programming, decentralized agent networks, edge AI, and cloud-native infrastructure. The goal is to build an evolutionary, self-healing system that uses AI agents and agentic programming, that adapts and scales across edge-to-cloud environments.

**Key Features of chosen tech stack:**

- Visual programming (Node-RED) - already proven opensource graphical programming language with extensive user base that has hardware and other systems integrations;
- Agent communication (A2A, MCP, ANP, ACP) - standard communication protocols between AI entities or AI and other systems;
- Local AI execution (SQLite-AI) - proven filebased SQL DB VM, combined with AI and embedded models, for best edge implementations;
- Streaming (Apache Kafka) - a widely used publish/subscribe system, cited as a candidate substrate;
- MAPE-K control loops - an established autonomic-computing model, named here as an
  intention. The shared Knowledge model is still undefined; see
  [ADR-0004](../../docs/adr/0004-self-evolution-sandboxing.md).
