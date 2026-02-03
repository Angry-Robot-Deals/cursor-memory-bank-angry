# Memory Bank System v2.0

Token-optimized task management for Claude Code. Commands in `.claude/commands/`, rules in `.claude/rules/`.

## Commands

| Command | Purpose | When |
|---------|---------|------|
| `/mb-prd` | Generate PRD from task description | Optional, before init |
| `/mb-init` | Initialize task, set complexity 1-4 | Start here |
| `/mb-plan` | Create implementation plan | Level 2-4 |
| `/mb-design` | Design decisions (5-phase) | Level 3-4 |
| `/mb-do` | Implement with TDD | All levels |
| `/mb-reflect` | Review & lessons learned | All levels |
| `/mb-archive` | Archive task, cleanup | All levels |
| `/mb-status` | Show current status | Anytime |
| `/mb-continue` | Resume current task | Anytime |

**Workflows:**
- Level 1: init → do → reflect → archive
- Level 2: init → plan → do → reflect → archive
- Level 3-4: init → plan → design → do → reflect → archive

## Critical Rules

### 1. MCP Servers (MANDATORY)

**sys8** - Use for ALL system operations:
- `get_current_datetime` - timestamps
- `get_os_version` - platform info

**context7** - Use for ALL library docs:
- `resolve-library-id` → `get-library-docs`

**NEVER** use `Date()`, hardcode timestamps, or hallucinate library APIs.

### 2. Git Push (MANDATORY)

**NEVER** push without explicit user request ("push", "git push", "commit and push").

Allowed: `git add`, `git commit`, `git status`, `git diff`, `git log`
Forbidden: `git push` (without permission)

### 3. File Paths (MANDATORY)

All Memory Bank files in `memory-bank/`:
- `tasks.md` - Active task (source of truth)
- `activeContext.md` - Current task ID
- `progress.md` - Status tracking
- `backlog.md` - Pending queue
- `prd/PRD-[id]-[desc].md` - Requirements
- `creative/creative-[id]-[name].md` - Design docs
- `reflection/reflection-[id].md` - Reviews
- `archive/archive-[id].md` - Completed tasks

**Task ID format:** `DEV-XXXX` (4-digit). Get from `activeContext.md`.

**NEVER** create files outside `memory-bank/` or in `documentation/tasks/`.

### 4. Task Context (MANDATORY)

- `activeContext.md` identifies CURRENT task
- Archive only current task, not all completed
- System auto-assigns task IDs if not provided

## AI Quality (5 Pillars)

1. **Decomposition** - Max 50 lines/method, 7-9 objects
2. **Test-First** - TDD always, DoD explicit
3. **Architecture-First** - Skeleton before code
4. **Focused Work** - One thing at a time
5. **Context Management** - Right info at right time

See `.claude/rules/ai-quality-principles.md` for 15 detailed rules.

## Quick Reference

**Starting a task:**
```
/mb-init [task description]
```

**With PRD:**
```
/mb-prd [task description]
/mb-init Use PRD: memory-bank/prd/PRD-XXX.md
```

**Check status:**
```
/mb-status
```

## Project Type

This is a workflow configuration project. No build/test commands.
- Claude Code config: `CLAUDE.md`, `.claude/`
- Cursor IDE config: `.cursor/`
- Shared: `memory-bank/`

## Details

- Setup: `CLAUDE_CODE_SETUP.md`
- Commands: `.claude/commands/README.md`
- Rules: `.claude/rules/`
- Comparison: `PLATFORM_COMPARISON.md`
