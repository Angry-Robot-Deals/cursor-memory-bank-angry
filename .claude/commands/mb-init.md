# Initialize New Task (VAN Phase)

You are working with the Memory Bank System. Initialize a new task following the VAN (Validate-Assess-Navigate) workflow.

## Instructions

1. **Create/verify Memory Bank structure** if it doesn't exist:
   ```
   memory-bank/
   ├── tasks.md
   ├── activeContext.md
   ├── progress.md
   ├── backlog.md          # NEW: Pending task queue
   ├── creative/
   ├── reflection/
   ├── archive/
   ├── prd/
   └── docs/
   ```

2. **Check Backlog for pending tasks** (NEW):
   - Read `memory-bank/backlog.md` if exists
   - Parse for items with status `pending`
   - If pending items found:
     - Display summary: "📋 N pending items in Backlog"
     - Show list: ID, Title, Priority, Complexity
     - Prompt: "Select from Backlog or start new task?"
   - User can select BACKLOG-XXXX or describe new task

3. **Determine complexity level** (1-4) based on:
   - Level 1: Quick fixes, documentation updates (VAN → DO → REFLECT → ARCHIVE)
   - Level 2: Standard features (VAN → PLAN → DO → REFLECT → ARCHIVE)
   - Level 3: Complex features needing design exploration (VAN → PLAN → CREATIVE → DO → REFLECT → ARCHIVE)
   - Level 4: Architectural changes (VAN → PLAN → CREATIVE → DO → REFLECT → ARCHIVE with multiple iterations)

4. **Generate task ID** using format: `DEV-XXXX` (4-digit with leading zeros, use sys8 MCP for timestamp)

5. **Update Memory Bank files**:
   - `memory-bank/tasks.md` - Add new task with complexity level and initial status
   - `memory-bank/activeContext.md` - Set as current active task
   - `memory-bank/progress.md` - Initialize progress tracking
   - `memory-bank/backlog.md` - Update item status to `in_progress` (if selected from Backlog)

6. **Route to next phase** based on complexity level

## Backlog Integration

### Check Backlog on Start

```
if exists(memory-bank/backlog.md):
    pending_items = parse_pending_items()
    if pending_items.length > 0:
        display_summary()
        prompt_user_selection()
```

### Display Format

```
📋 Backlog Status: 3 pending items

| ID | Title | Priority | Complexity |
|----|-------|----------|------------|
| BACKLOG-0001 | Add error handling | high | Level 2 |
| BACKLOG-0002 | Unit tests | medium | Level 2 |
| BACKLOG-0003 | API documentation | low | Level 1 |

Options:
1. Select from Backlog: Enter ID (e.g., BACKLOG-0001)
2. Start new task: Describe your task
```

### When Selecting from Backlog

1. Find item by BACKLOG-XXXX ID
2. Update item status to `in_progress` in backlog.md
3. Extract task details (title, description, complexity)
4. Create entry in tasks.md
5. Set activeContext.md
6. Continue with complexity-based workflow

## Memory Bank Integration

- Read from: `memory-bank/prd/`, `memory-bank/backlog.md`, codebase
- Write to: `memory-bank/tasks.md`, `memory-bank/activeContext.md`, `memory-bank/progress.md`, `memory-bank/backlog.md`
- MCP servers: MUST use sys8 for timestamps

## Rules to Follow

- Follow all rules in `.claude/rules/memory-bank-paths.md`
- Follow Backlog rules in `.claude/rules/core/backlog-management.md`
- Use MCP servers per `.claude/rules/mcp-integration.md`
- Follow AI Quality principles from `.claude/rules/ai-quality-principles.md`

## Example Usage

**Start new task:**
```
/mb-init Add user authentication with OAuth2 support
```

**Select from Backlog:**
```
/mb-init
(System shows Backlog, user selects BACKLOG-0001)
```

**Use specific Backlog item:**
```
/mb-init BACKLOG-0001
```

**Use PRD:**
```
/mb-init Use PRD: memory-bank/prd/PRD-DEV-001.md
```
