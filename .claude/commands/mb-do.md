# Implement Changes (DO Phase)

You are working with the Memory Bank System. Implement the planned changes following Test-Driven Development.

## Instructions

1. **Read implementation context**:
   - `memory-bank/tasks.md` - Implementation plan
   - `memory-bank/creative/*.md` - Design decisions (if Level 3-4)
   - `memory-bank/activeContext.md` - Current task context

2. **Follow TDD strictly** (AI Quality Rule #1):
   - Write tests BEFORE implementation code
   - Run tests to verify they fail (Red)
   - Implement minimal code to pass tests (Green)
   - Refactor while keeping tests green (Refactor)
   - Repeat for each feature/component

3. **Implement following plan**:
   - Create/modify files as specified in plan
   - Follow design decisions from CREATIVE phase
   - Maintain code quality (follow all AI Quality Rules)
   - Add appropriate error handling
   - Update documentation

4. **Verify implementation**:
   - All tests pass
   - Code follows project patterns
   - No security vulnerabilities introduced
   - Performance is acceptable

5. **Update Memory Bank files**:
   - `memory-bank/tasks.md` - Mark implementation complete
   - `memory-bank/progress.md` - Update phase to DO, track progress

6. **Do NOT push to git** - Follow `.claude/rules/git-push-restriction.md`

## Memory Bank Integration

- Read from: `memory-bank/tasks.md`, `memory-bank/creative/`, `memory-bank/activeContext.md`
- Write to: Codebase, test files, `memory-bank/tasks.md`, `memory-bank/progress.md`
- MCP servers: Use sys8 for timestamps, context7 for library usage

## Rules to Follow

- **CRITICAL**: Follow TDD strictly - tests BEFORE code
- Follow all rules in `.claude/rules/memory-bank-paths.md`
- Use MCP servers per `.claude/rules/mcp-integration.md`
- Follow all 15 AI Quality Rules from `.claude/rules/ai-quality-principles.md`
- DO NOT push to git per `.claude/rules/git-push-restriction.md`

## Example Usage

```
/mb-do
```
