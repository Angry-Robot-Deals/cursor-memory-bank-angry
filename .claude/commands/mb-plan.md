# Create Implementation Plan (PLAN Phase)

You are working with the Memory Bank System. Create a detailed implementation plan for the current task.

## Instructions

1. **Read current task** from `memory-bank/tasks.md` and `memory-bank/activeContext.md`

2. **Review codebase structure** to understand:
   - Existing patterns and architecture
   - Related components that will be affected
   - Testing infrastructure
   - Dependencies

3. **Create detailed implementation plan** including:
   - Step-by-step implementation approach
   - Files to be created/modified
   - Testing strategy (TDD required)
   - Components requiring design decisions (flag for CREATIVE phase if Level 3-4)
   - Risk assessment
   - Rollback strategy

4. **Update Memory Bank files**:
   - `memory-bank/tasks.md` - Add implementation plan section
   - `memory-bank/progress.md` - Update phase to PLAN

5. **Determine next phase**:
   - If Level 3-4 and design exploration needed → Suggest CREATIVE phase
   - Otherwise → Ready for DO phase

## Memory Bank Integration

- Read from: `memory-bank/tasks.md`, `memory-bank/activeContext.md`, codebase
- Write to: `memory-bank/tasks.md`, `memory-bank/progress.md`
- MCP servers: Use sys8 for timestamps, context7 for library docs

## Rules to Follow

- Follow all rules in `.claude/rules/memory-bank-paths.md`
- Use MCP servers per `.claude/rules/mcp-integration.md`
- Follow AI Quality principles from `.claude/rules/ai-quality-principles.md`
- Follow TDD principle per `.claude/rules/ai-quality-principles.md`

## Example Usage

```
/mb-plan
```
