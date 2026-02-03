# Generate Product Requirements Document

You are working with the Memory Bank System. Generate a Product Requirements Document (PRD) for the task described in the user's message.

## Instructions

1. **Analyze the task description** provided by the user
2. **Scan the codebase** to identify affected modules and components
3. **Create a structured PRD document** with the following sections:
   - Task ID and title
   - Overview and objectives
   - Technical requirements
   - Affected components
   - Dependencies and constraints
   - Success criteria
4. **Save the PRD** to `memory-bank/prd/PRD-{TASK_ID}-{description}.md`
5. **Identify follow-up tasks** for Backlog (NEW)
6. **Add follow-up tasks to Backlog** if user approves (NEW)
7. **Suggest next steps** (usually running `/mb-init` to initialize the task)

## Backlog Integration

After generating PRD, identify potential follow-up tasks and offer to add them to Backlog.

### Identifying Follow-up Tasks

Look for:
- Related bug fixes mentioned in PRD
- Documentation updates needed
- Test coverage improvements
- Performance optimizations
- Future enhancements noted in PRD
- Integration tasks with other systems

### Adding to Backlog Workflow

1. **Present identified tasks:**
   ```
   Based on PRD-DEV-001, I identified these potential follow-up tasks:
   
   1. Add unit tests for new authentication flow
   2. Update API documentation for OAuth endpoints  
   3. Implement rate limiting for auth endpoints
   
   Would you like to add these to the Backlog?
   [Yes] [No] [Modify list]
   ```

2. **Generate Backlog items:**
   - Create `memory-bank/backlog.md` if not exists
   - Generate BACKLOG-XXXX IDs for each task
   - Set Source: PRD-{TASK_ID}
   - Set Priority: based on analysis (default: medium)
   - Set Complexity: based on analysis (default: Level 2)
   - Use sys8 MCP for creation date

3. **Update Backlog file:**
   - Add items to "Pending Items" section
   - Update Summary counts

4. **Confirm additions:**
   ```
   ✅ Added 3 tasks to Backlog:
   - BACKLOG-0001: Add unit tests for authentication
   - BACKLOG-0002: Update API documentation
   - BACKLOG-0003: Implement rate limiting
   
   Use /mb-init to start working on any of these tasks.
   ```

## Memory Bank Integration

- Read from: Codebase structure, existing documentation, `memory-bank/backlog.md`
- Write to: `memory-bank/prd/PRD-{TASK_ID}-{description}.md`, `memory-bank/backlog.md`
- MCP servers: Use sys8 for timestamps, context7 for library documentation

## Rules to Follow

- Follow all rules in `.claude/rules/memory-bank-paths.md`
- Follow Backlog rules in `.claude/rules/core/backlog-management.md`
- Use MCP servers per `.claude/rules/mcp-integration.md`
- Follow AI Quality principles from `.claude/rules/ai-quality-principles.md`

## Example Usage

**Generate PRD:**
```
/mb-prd DEV-001: Implement rate limiting for API endpoints
```

**Generate PRD and add follow-up tasks to Backlog:**
```
/mb-prd DEV-001: Implement user authentication with OAuth2

(After PRD generation, system identifies follow-up tasks)
(User confirms adding to Backlog)
```

## Example Output

```
✅ PRD Generated Successfully

📄 Document: memory-bank/prd/PRD-DEV-001-user-authentication.md
📊 Complexity Estimate: Level 3
🎯 Affected Modules: 4 (auth, api, database, frontend)
⚠️ Risks Identified: 2

📋 Backlog Updates:
- Added 3 follow-up tasks to Backlog:
  - BACKLOG-0001: Add OAuth error handling [high]
  - BACKLOG-0002: Create auth unit tests [medium]
  - BACKLOG-0003: Update login UI [medium]

Next Steps:
1. Review the PRD document
2. Run /mb-init to initialize the task (or select from Backlog)
3. Run /mb-plan to create implementation plan
```
