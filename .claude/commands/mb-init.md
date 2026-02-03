# /mb-init - Initialize Task

Start new task or select from Backlog.

## Steps
1. Check `memory-bank/backlog.md` for pending items
2. Create/verify Memory Bank structure
3. Determine complexity (1-4)
4. Generate task ID: `DEV-XXXX`
5. Update `tasks.md` and `activeContext.md`

## Complexity Routing
- Level 1: → `/mb-do`
- Level 2-4: → `/mb-plan`

## Read
- `memory-bank/backlog.md`
- `memory-bank/prd/` (if PRD provided)

## Write
- `memory-bank/tasks.md`
- `memory-bank/activeContext.md`
- `memory-bank/progress.md`

## Usage
```
/mb-init [task description]
/mb-init BACKLOG-0001
/mb-init Use PRD: memory-bank/prd/PRD-XXX.md
```
