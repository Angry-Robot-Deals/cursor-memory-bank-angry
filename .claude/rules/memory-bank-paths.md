# Memory Bank File Paths

**Critical:** All Memory Bank files must be located in the `memory-bank/` directory at project root.

## Core Files

- **`memory-bank/tasks.md`** - Active task tracking (ephemeral, cleared after archival)
- **`memory-bank/activeContext.md`** - Current focus and active task ID
- **`memory-bank/progress.md`** - Implementation status
- **`memory-bank/projectbrief.md`** - Project foundation
- **`memory-bank/productContext.md`** - Product requirements
- **`memory-bank/systemPatterns.md`** - Architectural decisions
- **`memory-bank/techContext.md`** - Technology stack

## Generated Files

### PRD Documents
- **Location**: `memory-bank/prd/`
- **Format**: `PRD-[task_id]-[description].md`
- **Example**: `memory-bank/prd/PRD-DEV-001-notification-system.md`

### Task-Specific Documentation
- **Location**: `memory-bank/tasks/`
- **Format**: `DEV-[task_id]-[description].md`
- **Example**: `memory-bank/tasks/DEV-001-implementation-plan.md`

### Creative Phase Documents
- **Location**: `memory-bank/creative/`
- **Format**: `creative-[task_id]-[feature_name].md`
- **Example**: `memory-bank/creative/creative-DEV-001-oauth-integration.md`

### Reflection Documents
- **Location**: `memory-bank/reflection/`
- **Format**: `reflection-[task_id].md`
- **Example**: `memory-bank/reflection/reflection-DEV-001.md`

### Archive Documents
- **Location**: `memory-bank/archive/`
- **Format**: `archive-[task_id].md`
- **Example**: `memory-bank/archive/archive-DEV-001.md`

### QA Reports
- **Location**: `memory-bank/qa/`
- **Format**: `qa-report-[task_id]-[phase].md`
- **Example**: `memory-bank/qa/qa-report-DEV-001-phase3.md`

### Debug/Diagnostic Reports
- **Location**: `memory-bank/reports/`
- **Format**: `debug-[task_id]-[feature].md` or `diagnostic-[task_id]-[issue].md`
- **Example**: `memory-bank/reports/debug-DEV-001-session-timeout.md`

## Task ID Format

**Format**: `[PREFIX]-[number]`
- **Prefix**: Usually `DEV`, `FIN`, `QA`, etc.
- **Number**: 3-4 digit number (e.g., `001`, `0053`)
- **Examples**: `DEV-001`, `DEV-0053`, `FIN-0042`

**To get current task ID**: Read `memory-bank/activeContext.md`

## Critical Rules

### ✅ DO
- Create all Memory Bank files in `memory-bank/` directory
- Use task ID in ALL report filenames
- Read `activeContext.md` to get current task ID
- Follow naming conventions exactly

### ❌ DON'T
- Create Memory Bank files outside `memory-bank/` directory
- Create `documentation/tasks/` directory (should NOT exist)
- Create Markdown files in application source directories (except README.md)
- Omit task ID from report filenames

## File Verification

Before creating or editing Memory Bank files, verify:
1. Path starts with `memory-bank/`
2. Parent directory exists
3. Task ID is included in filename (for task-specific files)
4. File follows naming convention

## References

- Full path definitions: See `CLAUDE.md` section "Memory Bank Directory Structure"
- Cursor equivalent: `.cursor/rules/isolation_rules/Core/memory-bank-paths.mdc`
