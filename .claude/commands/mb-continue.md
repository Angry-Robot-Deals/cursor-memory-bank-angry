---
name: mb-continue
description: Resume work on current task from last checkpoint with context awareness
---

# /mb-continue - Resume Task

Continue from where you left off.

## Steps
1. Read current state
2. Determine phase (VAN/PLAN/DESIGN/DO/REFLECT)
3. Show context summary
4. Resume appropriate action

## Read
- `memory-bank/activeContext.md`
- `memory-bank/tasks.md`
- `memory-bank/progress.md`

## Write
Depends on current phase

## Routing
- No active task → suggest `/mb-init`
- In PLAN → continue planning
- In DO → continue implementation
- Ready for ARCHIVE → suggest `/mb-archive`
