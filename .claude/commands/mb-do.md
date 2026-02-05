# /mb-do - Implementation Mode

**Role**: Developer Agent
**Source**: `.claude/agents/developer.md`

## Instructions
1.  **LOAD**: Read `.claude/agents/developer.md` and adopt that persona.
2.  **SKILL**: Read `.claude/skills/ai-quality.md`.
3.  **CONTEXT**: Read `memory-bank/tasks.md` (Implementation Plan).
4.  **ACTION**:
    - **TDD Loop**: Write test -> Fail -> Code -> Pass.
    - Implement one stub/method at a time.
    - Follow `memory-bank/patterns.md`.
5.  **OUTPUT**: Code changes + `progress.md` update.

## Next Steps
- Implementation done? → `/mb-reflect`
