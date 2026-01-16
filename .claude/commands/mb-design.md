# Explore Design Options (CREATIVE Phase)

You are working with the Memory Bank System. Explore multiple design approaches for components flagged during planning.

## Instructions

This phase is ONLY for Level 3-4 tasks with architectural decisions.

1. **Read planning output** from `memory-bank/tasks.md` to identify components needing design exploration

2. **Follow 5-phase creative process**:
   - **Phase 1: Divergent Exploration** - Generate 3-5 distinct design options
   - **Phase 2: Analysis** - Analyze pros/cons of each option
   - **Phase 3: Synthesis** - Combine best aspects
   - **Phase 4: Validation** - Test against requirements
   - **Phase 5: Decision** - Select recommended approach with rationale

3. **Create creative documentation**:
   - File: `memory-bank/creative/creative-{task_id}-{component}.md`
   - Include all 5 phases
   - Provide clear recommendation

4. **Update Memory Bank files**:
   - `memory-bank/tasks.md` - Add design decisions section
   - `memory-bank/progress.md` - Update phase to CREATIVE

5. **Ready for implementation** - Move to DO phase

## Memory Bank Integration

- Read from: `memory-bank/tasks.md`, `memory-bank/activeContext.md`
- Write to: `memory-bank/creative/creative-{task_id}-{component}.md`, `memory-bank/tasks.md`
- MCP servers: Use sys8 for timestamps, context7 for architecture patterns

## Rules to Follow

- Follow all rules in `.claude/rules/memory-bank-paths.md`
- Use MCP servers per `.claude/rules/mcp-integration.md`
- Follow AI Quality principles from `.claude/rules/ai-quality-principles.md`

## Example Usage

```
/mb-design
```
