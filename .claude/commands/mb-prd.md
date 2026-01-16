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
5. **Suggest next steps** (usually running `/mb-init` to initialize the task)

## Memory Bank Integration

- Read from: Codebase structure, existing documentation
- Write to: `memory-bank/prd/PRD-{TASK_ID}-{description}.md`
- MCP servers: Use sys8 for timestamps, context7 for library documentation

## Rules to Follow

- Follow all rules in `.claude/rules/memory-bank-paths.md`
- Use MCP servers per `.claude/rules/mcp-integration.md`
- Follow AI Quality principles from `.claude/rules/ai-quality-principles.md`

## Example Usage

```
/mb-prd DEV-001: Implement rate limiting for API endpoints
```
