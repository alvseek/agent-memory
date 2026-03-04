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

### 2. Run the setup script
```bash
bash control-files/setup-scripts/setup-claude-code.sh
```
This configures your identity, compiles the global CLAUDE.md, installs slash commands, and sets up hooks + permissions. See the [Setup Guide](control-files/SETUP.md) for details or manual alternatives.

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
