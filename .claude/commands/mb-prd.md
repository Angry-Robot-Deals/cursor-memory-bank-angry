# /mb-prd - Generate PRD

Create Product Requirements Document.

## Steps
1. Analyze task description
2. Scan codebase for affected modules
3. Create PRD with:
   - Overview & objectives
   - Technical requirements
   - Affected components
   - Success criteria
4. Identify follow-up tasks for Backlog

## Read
- Codebase structure
- `memory-bank/backlog.md`

## Write
- `memory-bank/prd/PRD-[task_id]-[description].md`
- `memory-bank/backlog.md` (follow-up tasks)

## Usage
```
/mb-prd [task description]
```

## Next
→ `/mb-init Use PRD: memory-bank/prd/PRD-XXX.md`
