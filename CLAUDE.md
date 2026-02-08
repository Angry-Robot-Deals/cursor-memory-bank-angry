# Memory Bank System v2.1 (Subagents)

**Concept**: A lightweight router that delegates to specialized Agents.

## 🤖 Agents (Roles)
Use these slash commands to switch context:

| Role | Command | Focus |
|------|---------|-------|
| **Planner** | `/mb-plan` | Task breakdown, Backlog management |
| **Architect** | `/mb-design` | System design, Interfaces, Data models |
| **Developer** | `/mb-do` | TDD, Implementation, Refactoring |
| **Reviewer** | `/mb-reflect` | QA, Security check, Validation |

## 🧠 Skills (Knowledge)
Agents automatically load these, or request them via:
- `/load-skill ai-quality` - 15 AI development rules
- `/load-skill memory-bank-system` - File organization, task tracking
- `/load-skill security` - Security best practices
- `/load-skill performance` - Performance optimization
- `/load-skill testing` - Testing strategies

## 📂 Core Memory (Always Loaded)
- `memory-bank/activeContext.md` (Current State)
- `memory-bank/tasks.md` (Current Plan)

## 🚨 Critical Rules (Global)
1.  **Memory Bank is Truth**: Never work outside `memory-bank/`.
2.  **No Git Push**: Never push without explicit user request.
3.  **MCP Mandatory**: Always use `sys8` (time/os) and `context7` (docs).

## Quick Start
```bash
/mb-init "New task description"  # Starts with Planner
```

## 🔧 Installation & Troubleshooting

### First Time in This Project?
See `.claude/INSTALLATION_GUIDE.md` for setup instructions.

### Error: "Agent type not found"?
**Cause:** Missing `.claude/agents/` directory.
**Fix:** Copy Memory Bank structure to your project (see INSTALLATION_GUIDE.md).

### Error: "memory-bank/[dir] not found"?
**Cause:** Memory Bank not initialized.
**Fix:** `mkdir -p memory-bank/{tasks,creative,reflection,qa,reports,archive}`
