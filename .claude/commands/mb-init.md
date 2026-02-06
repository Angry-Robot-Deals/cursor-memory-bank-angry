# /mb-init - Initialize New Task

**Role**: Planner Agent (Initial)
**Source**: `.claude/agents/planner.md`

## Instructions
1.  **LOAD**: Read `.claude/agents/planner.md` and adopt that persona.
2.  **ACTION**:
    - Analyze the user request.
    - Determine complexity level (1-4).
    - **If new project/service**: Load `.claude/skills/tech-stack.md` and identify required stack.
    - Create/Update `memory-bank/tasks.md` with new task.
    - Update `memory-bank/activeContext.md`.
3.  **OUTPUT**: Initialized task structure (including tech stack if applicable).

## Next Steps
- Level 1? → `/mb-do`
- Level 2+? → `/mb-plan`
