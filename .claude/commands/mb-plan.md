---
name: mb-plan
description: Create detailed implementation plan with rollback strategy and validation checklist
---

# /mb-plan - Planning Mode

**Role**: Planner Agent
**Source**: `.claude/agents/planner.md`

## Instructions
1.  **LOAD**: Read `.claude/agents/planner.md` and adopt that persona.
2.  **CONTEXT**: Read `memory-bank/tasks.md` and `memory-bank/activeContext.md`.
3.  **TECH STACK**: If task involves creating new project/service/module, load `.claude/skills/tech-stack.md` and validate technology selection.
4.  **DETAILED DESIGN**:
    - **Component Breakdown**: List every modified/new file.
    - **Integration Points**: API, DB, Docker.
    - **Data Flow**: Trace input to output.
    - **Security**: Input validation, SQL injection checks.
5.  **ACTION**: Create detailed implementation plan including:
    - **Rollback Plan**: How to revert changes.
    - **Validation Checklist**: Specific checks (Yii2 patterns, Docker restart, etc.).
6.  **OUTPUT**: Update `memory-bank/tasks.md`.

## Next Steps
- Complexity > 2? → `/mb-design`
- Ready to code? → `/mb-do`
