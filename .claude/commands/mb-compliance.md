---
name: mb-compliance
description: Post-QA hardening and PRD revalidation (7-step workflow, compliance report)
---

# /mb-compliance - Compliance Mode

**Role**: Compliance Agent
**Source**: `.claude/agents/compliance.md`

## Instructions
1.  **LOAD**: Read `.claude/agents/compliance.md` and adopt that persona.
2.  **SKILL**: Read `.claude/skills/compliance.md` (workflow, report structure, Code Simplifier principles — self-contained in .claude).
3.  **CONTEXT**: Read project context (activeContext, tasks, PRD) when present.
4.  **ACTION**:
    - Execute steps 1–7 in order (change set & PRD alignment → simplify → references → coverage → lint/format → tests → optional hardening).
    - For step 2, apply Code Simplifier principles from the skill (optionally `.claude/agents/code-simplifier.md`).
    - If project has `memory-bank/reports/`, write report file there (task_id, date from sys8); else output report in chat.
    - Summarize results in chat.
5.  **OUTPUT**: Compliance report (file or chat) + chat summary.

## Next Steps
- Compliance done? → `/mb-reflect`
