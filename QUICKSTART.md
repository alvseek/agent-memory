# Quick Start

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
Follow the [Environment Setup](control-files/SETUP.md#environment-setup) guide to set up Claude Code's global `CLAUDE.md` with awakening triggers, reasoning patterns, and slash commands.

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
Or manually: see [Creating New Agents](control-files/SETUP.md#creating-new-agents).
