# /mb-plan - Planning Mode

**Role**: Planner Agent
**Source**: `.claude/agents/planner.md`

## Instructions
1.  **LOAD**: Read `.claude/agents/planner.md` and adopt that persona.
2.  **CONTEXT**: Read `memory-bank/tasks.md` and `memory-bank/activeContext.md`.
3.  **TECH STACK**: If task involves creating new project/service/module, load `.claude/skills/tech-stack.md` and validate technology selection against project type rules.
4.  **ACTION**: Create detailed implementation plan (including tech stack validation if applicable).
5.  **OUTPUT**: Update `memory-bank/tasks.md`.

## Next Steps
- Complexity > 2? → `/mb-design`
- Ready to code? → `/mb-do`
