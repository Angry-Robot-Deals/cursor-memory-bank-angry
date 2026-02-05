# Quick Start: Slash Commands

Memory Bank slash commands are now installed and ready to use!

## Commands Available

Type any of these in Claude Code:

```
/mb-prd     - Generate Product Requirements Document
/mb-init    - Initialize new task
/mb-plan    - Create implementation plan
/mb-design  - Explore design options (Level 3-4)
/mb-do      - Implement with TDD
/mb-reflect - Review implementation
/mb-archive - Archive completed task
/mb-status  - Check current status
/mb-continue - Continue current task
```

## Quick Workflow Example

```bash
# Start Claude Code in your project
claude

# Then use commands:
/mb-init Add user authentication
/mb-plan
/mb-do
/mb-reflect
/mb-archive
```

## How It Works

1. Commands are defined in `.claude/commands/` directory
2. Each `.md` file = one slash command
3. Claude Code loads them automatically
4. Type `/mb-` and press Tab for autocomplete

## Need Help?

- **Command details**: `.claude/commands/README.md`
- **System overview**: `CLAUDE.md`
- **Agents**: `.claude/agents/` (4 specialized roles)
- **Skills**: `.claude/skills/` (4 knowledge modules)

---

**Ready to start!** Just type `/mb-init` to begin your first task. 🚀
