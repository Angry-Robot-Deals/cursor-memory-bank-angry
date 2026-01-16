# Archive Task (ARCHIVE Phase)

You are working with the Memory Bank System. Archive the completed task and prepare for the next one.

## Instructions

1. **Create comprehensive archive document**:
   - File: `memory-bank/archive/archive-{task_id}.md`
   - Include:
     - Task ID and description
     - Complexity level and workflow path
     - Implementation plan (from tasks.md)
     - Design decisions (from creative/ if Level 3-4)
     - Implementation summary
     - Reflection insights
     - Final status and outcomes
     - Key metrics (time, files changed, tests added)

2. **Archive creative phase documents** (if Level 3-4):
   - Move `memory-bank/creative/creative-{task_id}-*.md` references to archive
   - Or keep them as reference for similar future tasks

3. **Update Memory Bank files**:
   - `memory-bank/tasks.md` - Move task to "Completed Tasks" section
   - `memory-bank/activeContext.md` - Reset to empty (ready for next task)
   - `memory-bank/progress.md` - Mark as archived

4. **Clean up**:
   - Remove temporary files if any
   - Update task list
   - Prepare for next task

5. **Provide summary**:
   - What was accomplished
   - What files were created/modified
   - Archived documentation location
   - System ready for next task

## Memory Bank Integration

- Read from: All memory-bank/ files for current task
- Write to: `memory-bank/archive/archive-{task_id}.md`, update tasks.md, reset activeContext.md
- MCP servers: Use sys8 for timestamps

## Rules to Follow

- Follow all rules in `.claude/rules/memory-bank-paths.md`
- Use MCP servers per `.claude/rules/mcp-integration.md`
- Preserve all important information in archive
- Make archive searchable and well-organized

## Example Usage

```
/mb-archive
```
