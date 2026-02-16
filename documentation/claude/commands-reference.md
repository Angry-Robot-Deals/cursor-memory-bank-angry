# Memory Bank Slash Commands for Claude Code

This directory contains slash command definitions for Memory Bank workflows in Claude Code.

## How It Works

Each `.md` file in `.claude/commands/` becomes a slash command:

- `mb-prd.md` → `/mb-prd`
- `mb-init.md` → `/mb-init`
- `mb-plan.md` → `/mb-plan`
- etc.

When you type the command in Claude Code, the markdown file is loaded and Claude follows those instructions.

## Available Commands

| Command | File | Phase | Description |
|---------|------|-------|-------------|
| `/mb-prd` | `mb-prd.md` | Pre-workflow | Generate Product Requirements Document |
| `/mb-init` | `mb-init.md` | VAN | Initialize new task |
| `/mb-plan` | `mb-plan.md` | PLAN | Create implementation plan |
| `/mb-design` | `mb-design.md` | CREATIVE | Explore design options (Level 3-4) |
| `/mb-do` | `mb-do.md` | DO | Implement changes with TDD |
| `/mb-compliance` | `mb-compliance.md` | COMPLIANCE | Post-QA hardening & PRD revalidation |
| `/mb-reflect` | `mb-reflect.md` | REFLECT | Review implementation |
| `/mb-archive` | `mb-archive.md` | ARCHIVE | Archive completed task |
| `/mb-status` | `mb-status.md` | Utility | Check current status |
| `/mb-continue` | `mb-continue.md` | Utility | Continue current task |

## Quick Start

```bash
# In Claude Code:
/mb-init Add user authentication
/mb-plan
/mb-design
/mb-do
/mb-compliance
/mb-reflect
/mb-archive
```

## Installation

These commands are **project-specific** (stored in `.claude/commands/`). They are automatically available when you run Claude Code in this project directory.

For **global commands** (available in all projects), copy files to `~/.claude/commands/`:

```bash
# Make commands available globally
cp -r .claude/commands/* ~/.claude/commands/
```

## Command Structure

Each command file contains:

1. **Title** - What the command does
2. **Instructions** - Step-by-step what Claude should do
3. **Memory Bank Integration** - Which files to read/write
4. **Rules to Follow** - Which rules and guidelines apply
5. **Examples** - Usage examples

## Two Ways to Work

### Option 1: Slash Commands (`.claude/commands/`)
```
/mb-init Add authentication
/mb-plan
/mb-do
```
- Fast and consistent
- Command-like experience
- Same as Cursor IDE style

Commands provide consistent, predictable workflow management for Memory Bank development.

## Documentation

- **Command reference**: This file (`documentation/claude/commands-reference.md`)
- **Setup guide**: `documentation/claude/INSTALLATION_GUIDE.md`
- **Agents**: `.claude/agents/` (6 roles: architect, code-simplifier, compliance, developer, planner, reviewer)
- **Skills**: `.claude/skills/` (7 modules: ai-quality, compliance, memory-bank-system, performance, security, tech-stack, testing)

## Testing Commands

After creating or modifying commands:

1. **Restart Claude Code** (commands are loaded at startup)
2. **Type `/mb` and press Tab** to see autocomplete
3. **Try a command**: `/mb-status`

## Notes

- **Prefix**: All Memory Bank commands use `/mb-` prefix
- **Arguments**: Most commands read context from `memory-bank/` files
- **Rules**: Commands follow Memory Bank workflow rules
- **Shared files**: Same `memory-bank/` directory works with both Cursor IDE and Claude Code

## Related

- **Cursor IDE commands**: `.cursor/commands/` (different format, same functionality)
- **Memory Bank files**: `memory-bank/` (shared between platforms)

---

**Ready to use!** Just type `/mb-` in Claude Code and start working. 🚀

## References

- [Claude Code Slash Commands Documentation](https://code.claude.com/docs/en/slash-commands)
- Memory Bank system docs and setup: see project root `README.md` and `documentation/claude/INSTALLATION_GUIDE.md` when this repo is the source; or your project's deployment docs.
