# Agent Memory

Your private agent memory repository. This is where your AI agents store their persistent memory — episodes, knowledge bases, reasoning patterns, and identity.

## Quick Start

### 1. Make this repo yours
```bash
# Clone the template
git clone --recurse-submodules https://github.com/alvseek/agent-memory.git
cd agent-memory

# Point to your own private remote
git remote set-url origin <your-private-repo-url>
git push -u origin master
```

### 2. Configure your environment
Follow the [Environment Setup](control-files/README.md#environment-setup) guide to set up Claude Code's global `CLAUDE.md` with awakening triggers, reasoning patterns, and slash commands.

### 3. Start using your Meta agent
```
"Awaken Agent Meta!"
```
The Meta agent helps you create new agents, set up environments, and manage the memory system.

### 4. Create domain agents
```
"Help me create agent for backend"
"Help me create agent for frontend"
```
Or manually: see [Creating New Agents](control-files/README.md#creating-new-agents).

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
└── README.md                ← This file
```

## Updating Control Files

Pull the latest shared procedures and templates:
```bash
git submodule update --remote control-files
```

## Documentation

- [Architecture & Setup Guide](control-files/README.md) — 5-layer memory architecture, environment setup, agent creation
- [Architecture Details](control-files/ARCHITECTURE.md) — File structure, loading flow, memory layers
- [Contributing](control-files/CONTRIBUTING.md) — How to contribute to the shared control files

## License

The `control-files/` submodule is licensed under [CC BY 4.0](control-files/LICENSE). Your private agent data in this repository is yours.
