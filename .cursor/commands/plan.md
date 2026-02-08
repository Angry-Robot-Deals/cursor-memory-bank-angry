# PLAN Command - Task Planning

This command creates detailed implementation plans based on complexity level determined in VAN mode.

## Memory Bank Integration

Reads from:
- `memory-bank/tasks.md` - Task requirements and complexity level
- `memory-bank/activeContext.md` - Current project context
- `memory-bank/projectbrief.md` - Project foundation (if exists)

Updates:
- `memory-bank/tasks.md` - Adds detailed implementation plan

## Progressive Rule Loading

### Step 1: Load Core Rules
```
Load: .cursor/rules/isolation_rules/main.mdc
Load: .cursor/rules/isolation_rules/Core/memory-bank-paths.mdc
```

### Step 2: Load PLAN Mode Map
```
Load: .cursor/rules/isolation_rules/visual-maps/plan-mode-map.mdc
```

### Step 3: Load Complexity-Specific Planning Rules
Based on complexity level from `memory-bank/tasks.md`:

**Level 2:**
```
Load: .cursor/rules/isolation_rules/Level2/task-tracking-basic.mdc
Load: .cursor/rules/isolation_rules/Level2/workflow-level2.mdc
```

**Level 3:**
```
Load: .cursor/rules/isolation_rules/Level3/task-tracking-intermediate.mdc
Load: .cursor/rules/isolation_rules/Level3/planning-comprehensive.mdc
Load: .cursor/rules/isolation_rules/Level3/workflow-level3.mdc
```

**Level 4:**
```
Load: .cursor/rules/isolation_rules/Level4/task-tracking-advanced.mdc
Load: .cursor/rules/isolation_rules/Level4/architectural-planning.mdc
Load: .cursor/rules/isolation_rules/Level4/workflow-level4.mdc
```

### MANDATORY Load Rules:
```
Load: .cursor/rules/sys8-mcp-usage.mdc
Load: .cursor/rules/context7-mcp-usage.mdc
```

## Workflow

1. **Read Task Context**
   - Read `memory-bank/tasks.md` to get complexity level
   - Read `memory-bank/activeContext.md` for current context
   - Review codebase structure

2. **Detailed Design (Enhanced)**
   - **Component Breakdown**: List every modified and new file.
   - **Integration Points**: Define API endpoints, DB queries, Docker services.
   - **Data Flow**: Trace input -> processing -> output.
   - **Security Checks**: Validate input, check SQL injection risks, secrets handling.

3. **Create Implementation Plan**
   - **Level 2:** Document planned changes, files to modify, implementation steps
   - **Level 3:** Create comprehensive plan with components, dependencies, challenges
   - **Level 4:** Create phased implementation plan with architectural considerations
   
   **Mandatory Plan Sections:**
   - **Rollback Plan**: How to revert changes (git commands, migration down).
   - **Validation Checklist**: Specific checks (Yii2 patterns, Docker restart, etc.).

4. **Technology Validation** (Level 2-4)
   - Document technology stack selection
   - Create proof of concept if needed
   - Verify dependencies and build configuration

5. **Identify Creative Phases**
   - Flag components requiring design decisions
   - Document which components need creative exploration

6. **Update Memory Bank**
   - Update `memory-bank/tasks.md` with complete plan
   - Mark planning phase as complete

## Usage

Type `/plan` to start planning based on the task in `memory-bank/tasks.md`.

## Implementation Plan Template

The plan in `memory-bank/tasks.md` MUST follow this structure:

```markdown
# [Feature Name] Implementation Plan

## Overview
[Problem, goals, success criteria]

## Architecture Impact
- Components: [AIO/API/Content Generator/...]
- Databases: [stats/bi_aggregate]
- Docker: [services affected]

## Implementation Steps

### Step 1: [Name]
**Files:**
- `path/to/file1`
- `path/to/file2`

**Changes:**
```php
// Specific code examples
class Example extends ActiveRecord {
    // ...
}
```

**Rationale:** [why this step]

### Step 2: [Name]
...

## Database Migration

```php
// Migration code
public function safeUp() {
    // ...
}

public function safeDown() {
    // ...
}
```

## Testing

**Manual testing:**
1. [Step-by-step verification]
2. Check UI at http://aio-pro.co.local
3. Verify API response

**Automated tests:**
- Unit tests: [files/scenarios]
- Integration tests: [if needed]

## Deployment

```bash
# Commands to deploy
cd _docker/ && docker compose up -d --build
bash _docker/bin/deploy.sh
docker exec aether-aio bash -c "cd /var/www/aio && php yii migrate --interactive=0"
```

## Rollback

```bash
# How to revert
php yii migrate/down
# Restore from backup if needed
```

## Validation Checklist

- [ ] Code follows Yii2/Python patterns
- [ ] Reused existing utilities/models
- [ ] Database migration tested
- [ ] Docker services restart successfully
- [ ] Feature works as expected
- [ ] No regressions
- [ ] Input validation implemented
- [ ] SQL queries use query builder
```

## Next Steps

- **If creative phases identified:** Use `/creative` command
- **If no creative phases:** Proceed to `/do` command
