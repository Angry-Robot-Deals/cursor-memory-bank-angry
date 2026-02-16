---
name: compliance
description: Post-QA hardening workflow (7 steps): change set vs PRD/task, code simplification, references/dead code, test coverage, linters, test run, optional hardening. Use with /mb-compliance or any post-implementation review.
---

# Compliance Workflow Skill

> **Self-contained in .claude.** Use when running /mb-compliance or any post-QA hardening flow. No external spec file required.

## Inputs (when present in project)

- **Current task:** From activeContext (task ID, title) if project has memory-bank; else from context.
- **PRD or task description:** From project prd/ or tasks if present.
- **Base branch:** Default `main` or `master`.
- **Changed files:** From Git diff (current vs base) if repo; else from task context.

## Steps (execute in order, best-effort)

1. **Change set & PRD/task alignment** — Get diff; re-check changes align with PRD/task; report drift.
2. **Code simplification** — Apply Code Simplifier principles below (and optionally `.claude/agents/code-simplifier.md`) to **recently modified code** only.
3. **References and dead code** — Check refs; flag/remove unused variables and imports; optional dead code.
4. **Test coverage** — If project requires tests: verify coverage of changed code; report gaps; suggest or add tests.
5. **Linters and formatters** — Run linters (fix or document); run formatter (e.g. Prettier); apply.
6. **Test execution** — Run test suite; report pass/fail; list failures if any.
7. **Optional hardening** — Error handling consistency; dependency audit if lockfile changed; security scan if project has it.

## Output — Report structure

Write report with these sections:

1. PRD alignment (ok | drift)
2. Simplification applied (yes | no + summary)
3. References/unused (fixed | reported)
4. Coverage (ok | gaps)
5. Lint/format (run + fixes)
6. Tests (pass | fail)
7. Optional (done | skipped)
8. Remaining risks/follow-ups

**Report path:** If project has `memory-bank/reports/`, write `memory-bank/reports/compliance-report-[task_id]-[date].md` (sys8 for date YYYY-MM-DD). Otherwise output report in chat only.

## Error handling

- No Git → infer changed files from task context.
- No PRD → use task description from context/tasks.
- Step failure → record in report; continue all steps; list all failures at end.

## Code Simplifier principles (for step 2)

1. **Preserve functionality** — Do not change what the code does; only how.
2. **Apply project standards** — Follow project coding standards (e.g. CLAUDE.md, style guide).
3. **Enhance clarity** — Reduce nesting; clear names; no nested ternaries (prefer switch or if/else); clarity over brevity.
4. **Maintain balance** — Avoid over-simplification; keep code debuggable and extendable.
5. **Scope** — Focus on recently modified code only unless instructed otherwise.
