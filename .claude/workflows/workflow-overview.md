# Memory Bank Workflows for Claude Code

This document describes the seven workflow phases of Memory Bank System for use with Claude Code.

## Workflow Phases

Unlike Cursor IDE which uses slash commands (`/van`, `/plan`, etc.), Claude Code uses `/mb-` prefix commands (`/mb-init`, `/mb-plan`, etc.).

### Phase 0: PRD Generation (Optional)

**When**: Before starting a complex task with unclear requirements

**Command Examples**:
```bash
/mb-prd DEV-001: Add notification system
/mb-prd Implement rate limiting
/mb-prd Add caching feature
```

**What Happens**:
1. Analyzes task description
2. Scans codebase for affected modules
3. Creates structured PRD with problem statement, scope, risks
4. Saves to `memory-bank/prd/PRD-{TASK_ID}-{description}.md`

**Output**: `memory-bank/prd/PRD-{TASK_ID}-{description}.md`

---

### Phase 1: VAN (Initialization)

**When**: Starting a new task

**Command Examples**:
```bash
/mb-init Add user authentication
/mb-init Fix session timeout issue
/mb-init Add OAuth2 support
/mb-init Use PRD: memory-bank/prd/PRD-DEV-001-notifications.md
```

**What Happens**:
1. Detects platform and OS
2. Creates/verifies Memory Bank structure
3. Analyzes task requirements
4. Determines complexity level (1-4)
5. Updates `memory-bank/tasks.md` and `activeContext.md`

**Next Phase**:
- Level 1 → DO (Phase 4)
- Level 2-4 → PLAN (Phase 2)

---

### Phase 2: PLAN (Planning)

**When**: After VAN for Level 2-4 tasks

**Command Examples**:
```bash
/mb-plan
```

**What Happens**:
1. Reads task context from `memory-bank/tasks.md`
2. Reviews codebase structure
3. Creates detailed implementation plan
4. Validates technology stack (Level 2-4)
5. Identifies components needing creative phases
6. Updates `memory-bank/tasks.md` with plan

**Next Phase**:
- Creative phases identified → CREATIVE (Phase 3)
- No creative phases → DO (Phase 4)

---

### Phase 3: CREATIVE (Design Decisions)

**When**: After PLAN for Level 3-4 tasks with design decisions needed

**Command Examples**:
```bash
/mb-design
```

**What Happens**:
1. Reads components flagged for creative work
2. Explores multiple design options (5-phase process):
   - Problem: Define scope
   - Options: List alternatives
   - Analysis: Compare options
   - Decision: Select approach
   - Guidelines: Document implementation rules
3. Creates `memory-bank/creative/creative-{task_id}-{feature_name}.md`

**Next Phase**: DO (Phase 4)

---

### Phase 4: DO (Implementation)

**When**: After PLAN (and optionally CREATIVE)

**Command Examples**:
```bash
/mb-do
```

**What Happens**:
1. Reads implementation plan
2. Reads creative phase documents (if Level 3-4)
3. Implements changes systematically following AI Quality Rules
4. **Enforces TDD**: Tests before code, all tests must pass
5. Documents execution in `memory-bank/tasks.md` and `progress.md`

**Test-Driven Gate**: All tests MUST pass before phase completion

**Next Phase**: REFLECT (Phase 5)

---

### Phase 5: REFLECT (Review)

**When**: After DO (implementation complete)

**Command Examples**:
```bash
/mb-reflect
```

**What Happens**:
1. Reviews completed implementation
2. Compares against original plan
3. Documents what went well
4. Documents challenges encountered
5. Documents lessons learned
6. Creates `memory-bank/reflection/reflection-{task_id}.md`

**Next Phase**: ARCHIVE (Phase 6)

---

### Phase 6: ARCHIVE (Archiving)

**When**: After REFLECT

**Command Examples**:
```bash
/mb-archive
```

**What Happens**:
1. Reads reflection document and task details
2. Creates comprehensive archive document
3. Archives creative phase documents (Level 3-4)
4. Moves task from active to completed
5. Resets `memory-bank/activeContext.md` for next task
6. Creates `memory-bank/archive/archive-{task_id}.md`

**Next Phase**: Ready for new task (back to Phase 0 or 1)

---

## Workflow Paths by Complexity

### Level 1: Quick Bug Fix
```
VAN → DO → REFLECT → ARCHIVE
```

### Level 2: Simple Enhancement
```
VAN → PLAN → DO → REFLECT → ARCHIVE
```

### Level 3-4: Feature/System
```
VAN → PLAN → CREATIVE → DO → REFLECT → ARCHIVE
```

### With PRD (Recommended for complex tasks)
```
PRD → VAN → PLAN → CREATIVE → DO → REFLECT → ARCHIVE
```

---

## Continuing Work

**Resume Current Task**:
- "Continue the current task"
- "What's the status of the active task?"
- "Resume where we left off"

**Check Status**:
- "What phase are we in?"
- "Show me the current task status"
- "What's next in the workflow?"

---

## Key Principles

1. **Be Explicit**: Clearly state which phase you want
2. **Reference Files**: Mention Memory Bank files when needed
3. **Ask for Guidance**: Claude will guide you through phases
4. **Trust the Process**: Each phase builds on the previous one

---

## References

- Full workflow details: See `CLAUDE.md`
- Cursor equivalent: `.cursor/commands/*.md`
