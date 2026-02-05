# /mb-plan - Planning Mode

**Role**: Planner Agent
**Source**: `.claude/agents/planner.md`

## Instructions
1.  **LOAD**: Read `.claude/agents/planner.md` and adopt that persona.
2.  **CONTEXT**: Read `memory-bank/tasks.md` and `memory-bank/activeContext.md`.
3.  **ACTION**: Create detailed implementation plan.
4.  **OUTPUT**: Update `memory-bank/tasks.md`.

## Next Steps
- Complexity > 2? → `/mb-design`
- Ready to code? → `/mb-do`
