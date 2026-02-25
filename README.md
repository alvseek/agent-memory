# Agent Memory

A 5-layer memory architecture that gives AI agents persistent memory across sessions. Agents remember past work, learn from mistakes through reasoning patterns, and grow domain expertise over time.

This repository is your **private agent data** — where each agent stores its identity, episodes, knowledge base, and emotional milestones. It includes [control-files/](control-files/) as a git submodule: the **shared procedures, templates, and protocols** that teach agents how to manage their own memory (planning workflows, memory updates, archiving, and more).

It comes with a ready-to-use **Meta agent** — a built-in agent that helps you create new domain agents, modify existing ones, and manage the memory system. See the [Quick Start](QUICKSTART.md) to get up and running.

## Repository Structure

```
agent-memory/
├── control-files/           ← Public submodule (shared procedures & templates)
├── agent-meta/              ← Meta agent (manages other agents)
│   ├── agent-core-memory.md
│   ├── agent-memory-index.md
│   ├── episodes/
│   └── knowledge-base/
├── agent-[domain]/          ← Your domain agents (created as needed)
│   └── (same structure)
├── QUICKSTART.md            ← Getting started guide
├── CONTRIBUTING.md          ← Contribution guidelines
├── LICENSE                  ← CC BY 4.0
└── README.md                ← This file
```

## Documentation

- [Architecture Overview](control-files/README.md) — 5-layer memory architecture, repository design, automation features
- [Setup Guide](control-files/SETUP.md) — Environment configuration and creating new agents
- [Architecture Details](control-files/ARCHITECTURE.md) — File structure, loading flow, memory layers
- [Contributing](CONTRIBUTING.md) — How to contribute to this template repo
- [Contributing to Control Files](control-files/CONTRIBUTING.md) — How to contribute to the shared procedures and templates

## License

This project is licensed under [CC BY 4.0](LICENSE). Your private agent data (episodes, knowledge bases, identity files) is yours.
