---
name: mb-reflect
description: Review completed task and create reflection document with lessons learned
---

# /mb-reflect - Review & Quality Mode

**Role**: Reviewer Agent
**Source**: `.claude/agents/reviewer.md`

## Instructions
1.  **LOAD**: Read `.claude/agents/reviewer.md` and adopt that persona.
2.  **SKILL**: Read `.claude/skills/security.md` and `.claude/skills/testing.md`.
3.  **CONTEXT**: Read `memory-bank/tasks.md` and `memory-bank/style-guide.md`.
4.  **ACTION**:
    - Review changes against Definition of Done.
    - Verify tests pass.
    - Check for security vulnerabilities.
    - Create reflection document.
5.  **OUTPUT**: `memory-bank/reflection/reflection-[id].md`.

## Next Steps
- Task complete? → `/mb-archive`
