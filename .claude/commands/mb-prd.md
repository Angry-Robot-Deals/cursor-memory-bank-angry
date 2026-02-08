---
name: mb-prd
description: Generate Product Requirements Document with technology stack selection
---

# /mb-prd - Generate PRD

Create Product Requirements Document.

## Steps
1. Analyze task description
2. Scan codebase for affected modules
3. **If new project/service/module**: Load `.claude/skills/tech-stack.md` and select stack based on project type
4. Create PRD with:
   - Overview & objectives
   - Technical requirements
   - **Technology stack** (from tech-stack rules if applicable)
   - Affected components
   - Success criteria
5. Identify follow-up tasks for Backlog

## Read
- Codebase structure
- `memory-bank/backlog.md`
- `.claude/skills/tech-stack.md` (when new project/service creation is involved)

## Write
- `memory-bank/prd/PRD-[task_id]-[description].md`
- `memory-bank/backlog.md` (follow-up tasks)

## Usage
```
/mb-prd [task description]
```

## Next
→ `/mb-init Use PRD: memory-bank/prd/PRD-XXX.md`
