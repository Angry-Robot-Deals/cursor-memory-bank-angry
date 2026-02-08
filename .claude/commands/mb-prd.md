---
name: mb-prd
description: Generate Product Requirements Document with technology stack selection and design exploration
---

# /mb-prd - Generate PRD

Create Product Requirements Document with detailed design exploration.

## Steps
1. **Context Gathering**:
   - Analyze task description.
   - Scan codebase for affected modules.
   - Read relevant code files (Models, Controllers, Configs).
   - Identify constraints (Database, Performance, Security).

2. **Solution Exploration**:
   - **If new project/service/module**: Load `.claude/skills/tech-stack.md` and select stack.
   - Generate **2-3 distinct technical approaches**.
   - Evaluate Pros/Cons for each.
   - Check for security risks and anti-patterns.

3. **User Consultation**:
   - Present approaches to user if significant architectural decisions are needed.
   - Wait for approval before finalizing PRD.

4. **Create PRD**:
   - Overview & objectives
   - Technical requirements (including selected approach)
   - **Technology stack** (from tech-stack rules if applicable)
   - Affected components
   - Success criteria

5. **Backlog**:
   - Identify follow-up tasks for Backlog.

## Read
- Codebase structure
- `memory-bank/backlog.md`
- `.claude/skills/tech-stack.md` (when new project/service creation is involved)
- Relevant source code files

## Write
- `memory-bank/prd/PRD-[task_id]-[description].md`
- `memory-bank/backlog.md` (follow-up tasks)

## Usage
```
/mb-prd [task description]
```

## Next
→ `/mb-init Use PRD: memory-bank/prd/PRD-XXX.md`
