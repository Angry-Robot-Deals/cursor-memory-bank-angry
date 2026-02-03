# Memory Bank Workflows

## Command Flow

```
/mb-prd (optional) → /mb-init → /mb-plan → /mb-design → /mb-do → /mb-reflect → /mb-archive
```

## By Complexity

| Level | Type | Flow |
|-------|------|------|
| 1 | Quick fix | init → do → reflect → archive |
| 2 | Enhancement | init → plan → do → reflect → archive |
| 3-4 | Feature | init → plan → design → do → reflect → archive |

## Phase Summary

| Phase | Command | Purpose | Output |
|-------|---------|---------|--------|
| PRD | `/mb-prd` | Requirements | `prd/PRD-XXX.md` |
| Init | `/mb-init` | Start task | `tasks.md`, `activeContext.md` |
| Plan | `/mb-plan` | Implementation plan | `tasks.md` updated |
| Design | `/mb-design` | Design decisions | `creative/creative-XXX.md` |
| Do | `/mb-do` | Implement (TDD) | Code + tests |
| Reflect | `/mb-reflect` | Review | `reflection/reflection-XXX.md` |
| Archive | `/mb-archive` | Complete | `archive/archive-XXX.md` |

## Helper Commands

| Command | Purpose |
|---------|---------|
| `/mb-status` | Show current state |
| `/mb-continue` | Resume from checkpoint |

## Key Rules

1. **MCP servers** - sys8 for time, context7 for libs
2. **TDD** - Tests before code in `/mb-do`
3. **No git push** - Without explicit request
4. **Memory Bank** - All files in `memory-bank/`

See `.claude/rules/essential.md` for full rules.
