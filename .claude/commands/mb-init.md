# Initialize New Task (VAN Phase)

You are working with the Memory Bank System. Initialize a new task following the VAN (Validate-Assess-Navigate) workflow.

## Instructions

1. **Create/verify Memory Bank structure** if it doesn't exist:
   ```
   memory-bank/
   ├── tasks.md
   ├── activeContext.md
   ├── progress.md
   ├── creative/
   ├── reflection/
   ├── archive/
   ├── prd/
   └── docs/
   ```

2. **Determine complexity level** (1-4) based on:
   - Level 1: Quick fixes, documentation updates (VAN → DO → REFLECT → ARCHIVE)
   - Level 2: Standard features (VAN → PLAN → DO → REFLECT → ARCHIVE)
   - Level 3: Complex features needing design exploration (VAN → PLAN → CREATIVE → DO → REFLECT → ARCHIVE)
   - Level 4: Architectural changes (VAN → PLAN → CREATIVE → DO → REFLECT → ARCHIVE with multiple iterations)

3. **Generate task ID** using format: `TASK-YYYYMMDD-NNN` (use sys8 MCP for timestamp)

4. **Update Memory Bank files**:
   - `memory-bank/tasks.md` - Add new task with complexity level and initial status
   - `memory-bank/activeContext.md` - Set as current active task
   - `memory-bank/progress.md` - Initialize progress tracking

5. **Route to next phase** based on complexity level

## Memory Bank Integration

- Read from: `memory-bank/prd/` (if PRD exists), codebase
- Write to: `memory-bank/tasks.md`, `memory-bank/activeContext.md`, `memory-bank/progress.md`
- MCP servers: MUST use sys8 for timestamps

## Rules to Follow

- Follow all rules in `.claude/rules/memory-bank-paths.md`
- Use MCP servers per `.claude/rules/mcp-integration.md`
- Follow AI Quality principles from `.claude/rules/ai-quality-principles.md`

## Example Usage

```
/mb-init Add user authentication with OAuth2 support
/mb-init Fix session timeout issue
/mb-init Use PRD: memory-bank/prd/PRD-DEV-001.md
```
