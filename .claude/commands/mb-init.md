# /mb-init - Initialize New Task

**Role**: Planner Agent (Initial)
**Source**: `.claude/agents/planner.md`

## Instructions
1.  **LOAD**: Read `.claude/agents/planner.md` and adopt that persona.
2.  **ACTION**:
    - Analyze the user request.
    - Determine complexity level (1-4).
    - Create/Update `memory-bank/tasks.md` with new task.
    - Update `memory-bank/activeContext.md`.
3.  **OUTPUT**: Initialized task structure.

## Next Steps
- Level 1? → `/mb-do`
- Level 2+? → `/mb-plan`
