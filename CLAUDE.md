# CLAUDE.md

This file provides guidance to **Claude Code** (claude.ai/code) when working with code in this repository.

> **Note:** This is the configuration file specifically for **Claude Code** - Anthropic's official CLI tool. If you're using **Cursor IDE**, the system uses `.cursor/commands/` and `.cursor/rules/` files instead. Both platforms are fully supported! See `PLATFORM_COMPARISON.md` for details.

## Overview

This is the **Memory Bank System v2.0** - a token-optimized, hierarchical task management system that works with both **Cursor IDE** and **Claude Code**. The system uses specialized workflows to guide AI through structured development, integrating mandatory MCP (Model Context Protocol) server usage and 15 AI Quality Rules for improved code quality.

## Architecture

Memory Bank is a **command-based workflow system** that transforms development into a structured, phase-based process using Cursor 2.0 commands. Each command reads from and writes to a shared **Memory Bank** directory (`memory-bank/`) to maintain persistent context across workflow phases.

### Core Concepts

1. **Hierarchical Rule Loading**: Rules are loaded progressively based on mode and task complexity, achieving ~70% token reduction compared to loading all rules at once
2. **Adaptive Complexity Model**: Workflow adapts based on task complexity (Levels 1-4), from quick bug fixes to enterprise features
3. **Command-Based Phases**: Seven specialized commands form an integrated workflow graph
4. **Mandatory MCP Integration**: All commands must query sys8 and context7 MCP servers before starting work
5. **AI Quality Rules**: 15 research-proven rules embedded in workflows (TDD, method size limits, skeleton-first architecture, etc.)

### The Seven Workflow Commands

Memory Bank operates through these commands (located in `.claude/commands/`):

0. **`/mb-prd`** - Product Requirements Document Generator (OPTIONAL, pre-workflow)
   - Runs BEFORE `/mb-init` to prepare detailed requirements
   - Transforms brief task descriptions into structured PRD documents
   - Analyzes codebase to identify affected modules and subsystems
   - Estimates complexity level and identifies risks
   - Creates `memory-bank/prd/PRD-{TASK_NUMBER}-{description}.md`

1. **`/mb-init`** - Initialization & Entry Point
   - Detects platform and OS
   - Creates/verifies Memory Bank structure
   - Analyzes task requirements (or reads from PRD if generated)
   - Determines complexity level (1-4)
   - Routes to appropriate workflow

2. **`/mb-plan`** - Task Planning (Level 2-4)
   - Creates implementation plans based on complexity
   - Validates technology stack
   - Identifies components needing design decisions
   - Updates `memory-bank/tasks.md`

3. **`/mb-design`** - Design Decisions (Level 3-4)
   - Explores design options for flagged components
   - Based on Claude's "Think" tool methodology
   - Uses progressive documentation (5-phase process)
   - Creates `memory-bank/creative/creative-[feature_name].md`

4. **`/mb-do`** - Code Implementation (All Levels)
   - Implements planned changes
   - Enforces test-driven development (TDD)
   - Phases must pass tests before proceeding
   - Documents execution in `memory-bank/tasks.md` and `memory-bank/progress.md`

5. **`/mb-reflect`** - Task Reflection (All Levels)
   - Reviews completed implementation
   - Documents lessons learned
   - Creates `memory-bank/reflection/reflection-[task_id].md`

6. **`/mb-archive`** - Task Archiving (All Levels)
   - Creates comprehensive archive documentation
   - Archives creative phase documents
   - Resets `memory-bank/activeContext.md`
   - Creates `memory-bank/archive/archive-[task_id].md`

Plus two helper commands:

7. **`/mb-status`** - Check Current Status
   - Shows current task information
   - Displays workflow progress
   - Suggests next steps

8. **`/mb-continue`** - Continue Current Task
   - Resumes work on active task
   - Determines current phase
   - Continues from last checkpoint

### Workflow Paths by Complexity

**Optional PRD Generation** (for complex or unclear requirements):
- `/mb-prd` → `/mb-init` → [continue with complexity-based workflow]

**Core Workflows:**
- **Level 1 (Quick Fix)**: `/mb-init` → `/mb-do` → `/mb-reflect` → `/mb-archive`
- **Level 2 (Enhancement)**: `/mb-init` → `/mb-plan` → `/mb-do` → `/mb-reflect` → `/mb-archive`
- **Level 3-4 (Feature/System)**: `/mb-init` → `/mb-plan` → `/mb-design` → `/mb-do` → `/mb-reflect` → `/mb-archive`

**With PRD (Recommended for complex tasks):**
- **Level 3-4**: `/mb-prd` → `/mb-init` → `/mb-plan` → `/mb-design` → `/mb-do` → `/mb-reflect` → `/mb-archive`

## Memory Bank Directory Structure

All Memory Bank files reside in `memory-bank/` at project root:

```
memory-bank/
├── tasks.md              # Source of truth for active task tracking
├── backlog.md            # Pending task queue (NEW in v2.1)
├── activeContext.md      # Current focus and active task ID
├── progress.md           # Implementation status
├── projectbrief.md       # Project foundation
├── productContext.md     # Product requirements
├── systemPatterns.md     # Architectural decisions
├── techContext.md        # Technology stack
├── prd/                  # Product Requirements Documents (PRD-XXX-*.md)
│   └── archive/          # Archived/completed PRDs
├── creative/             # Design decision documents
├── reflection/           # Task reflection documents
├── archive/              # Completed task archives
├── tasks/                # Task-specific documentation (DEV-XXX-*.md)
├── qa/                   # QA reports
├── reports/              # Debug/diagnostic reports
└── docs/                 # Documentation about Memory Bank system
```

### Backlog System (v2.0 - Performance Optimized)

The Backlog (`memory-bank/backlog.md`) provides a queue for future tasks:

- **Adding tasks**: `/mb-prd` and `/mb-init` can add tasks to Backlog
- **Selecting tasks**: `/mb-init` shows pending items and allows selection
- **Format**: `BACKLOG-XXXX` items with priority, complexity, description
- **Statuses**: `pending` → `in_progress` → `completed`

Example Backlog entry:
```markdown
### BACKLOG-0001: Implement error handling
| Field | Value |
|-------|-------|
| **Status** | pending |
| **Priority** | high |
| **Complexity** | Level 2 |
| **Created** | 2026-02-03 |
| **Source** | PRD-DEV-0001 |
```

### Critical File Paths

**NEVER** create Memory Bank files outside the `memory-bank/` directory. All operational documentation must follow these patterns:

- PRD documents: `memory-bank/prd/PRD-[task_id]-[description].md`
- Task tracking: `memory-bank/tasks.md` (ephemeral, cleared after archival)
- Task-specific docs: `memory-bank/tasks/DEV-[task_id]-*.md`
- QA reports: `memory-bank/qa/qa-report-[task_id]-[phase].md`
- Debug reports: `memory-bank/reports/debug-[task_id]-[feature].md`
- Creative docs: `memory-bank/creative/creative-[task_id]-[feature_name].md`
- Reflections: `memory-bank/reflection/reflection-[task_id].md`
- Archives: `memory-bank/archive/archive-[task_id].md`

**Task ID Format**: `[PREFIX]-[4-digit-number]` (e.g., `DEV-0053`, `FIN-0001`)
- Get current task ID from `memory-bank/activeContext.md`
- System auto-assigns task IDs during initialization if not provided

## Rule System Architecture

Rules for Claude Code are located in `.claude/` directory and organized for command-based interaction:

### Core Rules (Always Referenced)
- `.claude/rules/memory-bank-paths.md` - File path definitions
- `.claude/rules/ai-quality-principles.md` - 5 pillars of AI quality
- `.claude/rules/mcp-integration.md` - MCP server integration
- `.claude/rules/git-push-restriction.md` - Git push safety rules

### Workflow Guides
- `.claude/workflows/workflow-overview.md` - Complete workflow phases guide

### Cursor IDE Equivalents
Cursor IDE has similar commands but with different names:
- Cursor uses: `/van`, `/plan`, `/creative`, `/do`, `/reflect`, `/archive`
- Claude Code uses: `/mb-init`, `/mb-plan`, `/mb-design`, `/mb-do`, `/mb-reflect`, `/mb-archive`
- Both platforms share the same Memory Bank principles and files

## Critical System Rules

### 1. MCP Server Integration (MANDATORY)

**All commands MUST query MCP servers before any work:**

1. **sys8 MCP Server** (system operations):
   - `get_current_datetime` - For ALL date/time fields in Memory Bank documents
   - `get_os_version` - For platform-specific decisions
   - `calculate_math_expression` - For safe math operations
   - `random_string` - For cryptographically secure random strings
   - `hash_string` - For secure hashing

2. **context7 MCP Server** (library documentation):
   - `resolve-library-id` - Resolve library names to Context7 IDs
   - `get-library-docs` - Get up-to-date library documentation
   - Use for ALL external libraries/frameworks to prevent API hallucinations

**NEVER** use JavaScript `Date()`, Node.js `os` module, or outdated training data for library APIs without MCP queries.

### 2. Git Push Restriction (MANDATORY)

**NEVER execute `git push` unless explicitly requested by the user.**

Valid user requests for push:
- "push the changes"
- "git push"
- "commit and push"
- "push to remote"
- "deploy the changes" (in git context)

Invalid implicit requests (do NOT push):
- "commit the changes" → Only commit, don't push
- "save the changes" → Only commit, don't push
- "finish the task" → Only commit, don't push

**Allowed without permission:**
- ✅ `git commit`, `git add`, `git status`, `git diff`, `git log`, `git branch`, `git checkout`, `git stash`

**Forbidden without explicit request:**
- ❌ `git push`, `git push origin <branch>`, `git push -f`, `git push --force`, `git push --all`

See: `.claude/rules/git-push-restriction.md` (version 2.0.0, updated 2025-01-19)

### 3. Documentation Storage Rules (MANDATORY)

**NEVER create `documentation/tasks/` directory** - it should NOT exist.
- ALL operational task docs go to `memory-bank/tasks/`
- ALL report filenames MUST include task ID
- NEVER create MD files in application source directories (except README.md)

See: `.claude/rules/memory-bank-paths.md` for complete file path definitions

### 4. Task Context Tracking (MANDATORY)

- `memory-bank/activeContext.md` MUST always identify the CURRENT task
- Archive phase archives ONLY the current task (not all completed tasks)
- System auto-assigns unique task numbers during initialization if not provided

See: `.claude/rules/memory-bank-paths.md` for task ID format and tracking

## AI Quality Rules (15 Rules, 5 Pillars)

Memory Bank integrates 15 research-proven AI Quality Rules that reduce bugs by 40-50% and improve code quality by 30-50%:

### The 5 Pillars

1. **DECOMPOSITION** (Rules #1, #3, #9)
   - Max 50 lines per method
   - Max 7-9 objects in working memory
   - One responsibility per function

2. **TEST-FIRST** (Rules #2, #5, #6)
   - Write tests BEFORE code (TDD)
   - Define "done" explicitly (DoD)
   - Cover corner cases upfront

3. **ARCHITECTURE-FIRST** (Rules #7, #8)
   - Create skeleton with stubs before implementation
   - Review architecture before coding
   - Implement one method at a time

4. **FOCUSED WORK** (Rules #10, #11, #12)
   - Review one method at a time
   - Define clear boundaries (what we DON'T do)
   - Verify AI can solve before starting

5. **CONTEXT MANAGEMENT** (Rules #4, #13, #14, #15)
   - Gather requirements BEFORE coding
   - Document transaction isolation needs
   - Structure Memory Bank hierarchically
   - Engineer prompts carefully

See: `.claude/rules/ai-quality-principles.md` for full details

## Token Optimization Features

Version 2.0 includes these optimizations:

1. Hierarchical rule loading (~70% token reduction)
2. Progressive creative phase documentation (~60% token reduction)
3. Context preservation during mode transitions (~40% token reduction)
4. Differential Memory Bank updates (~30% token reduction)
5. Complexity-based template scaling (varies by level)

## Common Development Patterns

### Starting a New Task

**Option 1: Direct Start (for simple/clear requirements)**
```bash
# 1. Initialize with /mb-init
/mb-init Add user authentication with OAuth2 support

# 2. System determines complexity and routes you
# Level 1: Goes to /mb-do
# Level 2-4: Goes to /mb-plan

# 3. Follow the workflow
/mb-plan          # If Level 2-4
/mb-design        # If Level 3-4 with design decisions
/mb-do            # Implementation (all levels)
/mb-reflect       # Review (all levels)
/mb-archive       # Archive and cleanup (all levels)
```

**Option 2: With PRD (recommended for complex/unclear requirements)**
```bash
# 1. Generate detailed requirements first
/mb-prd DEV-001: Add notification system for account expiry warnings

# 2. Review generated PRD: memory-bank/prd/PRD-DEV-001-notification-system.md

# 3. Initialize with PRD reference
/mb-init Use PRD: memory-bank/prd/PRD-DEV-001-notification-system.md

# 4. Continue with normal workflow
/mb-plan          # If Level 2-4
/mb-design        # If Level 3-4 with design decisions
/mb-do            # Implementation (all levels)
/mb-reflect       # Review (all levels)
/mb-archive       # Archive and cleanup (all levels)
```

### Test-Driven Development Flow

All `/mb-do` implementations enforce TDD:

1. Extract success criteria from current phase in `memory-bank/tasks.md`
2. Write test cases covering each success criterion
3. Execute all tests
4. **GATE**: All tests MUST pass before phase completion
5. Document test results in `memory-bank/tasks.md`
6. If tests fail: fix implementation, re-run tests, repeat

### Progressive Creative Phase

For Level 3-4 features requiring design decisions:

1. **PROBLEM**: Define scope
2. **OPTIONS**: List alternatives
3. **ANALYSIS**: Compare options (tabular format)
4. **DECISION**: Select approach
5. **GUIDELINES**: Document implementation rules

## File Naming Conventions

### Claude Code Configuration
- Workflows: `.claude/workflows/*.md`
- Rules: `.claude/rules/*.md`
- Configuration: `CLAUDE.md` (project root)

### Cursor IDE Configuration
- Commands: `.cursor/commands/[command-name].md`
- Rules: `.cursor/rules/isolation_rules/[Category]/[rule-name].mdc`
- Templates: `.cursor/templates/*.md`

### Memory Bank Files (Shared by Both Platforms)
- PRD Documents: `memory-bank/prd/PRD-[task_id]-[description].md`
- Memory Bank Tasks: `memory-bank/tasks/DEV-[task_id]-[description].md`
- Creative Docs: `memory-bank/creative/creative-[task_id]-[feature_name].md`
- Reflections: `memory-bank/reflection/reflection-[task_id].md`
- Archives: `memory-bank/archive/archive-[task_id].md`

## Project Type

This is a **dual-platform AI workflow configuration project** - not a traditional software project with code to build or test. It consists of:

**For Claude Code:**
- Configuration file (`CLAUDE.md`)
- Workflow guides (`.claude/workflows/*.md`)
- Rule files (`.claude/rules/*.md`)

**For Cursor IDE:**
- Command definitions (`.cursor/commands/*.md`)
- Hierarchical rule files (`.cursor/rules/isolation_rules/**/*.mdc`)
- Global templates (`.cursor/templates/*.md`)

**Shared:**
- Documentation files (README.md, guides, release notes)
- Example Memory Bank structure
- Platform comparison and setup guides

**There are no build commands, test suites, or runtime code to execute.** The "product" is the Memory Bank workflow system itself, which users install in their own projects.

## Important Implementation Notes

1. **Memory Bank MUST exist before ANY operation** - `/mb-init` creates it if missing
2. **Always read `memory-bank/activeContext.md`** to get current task ID before creating any files
3. **Query MCP servers first** - sys8 for date/time/OS, context7 for library docs
4. **Never hardcode timestamps** - use sys8 `get_current_datetime`
5. **Never hallucinate library APIs** - use context7 `get-library-docs`
6. **Follow TDD strictly in `/mb-do` mode** - tests before code, all tests must pass
7. **Keep methods under 50 lines** - decompose complex logic
8. **Create skeletons before implementation** - approve architecture first
9. **Never push to git** unless user explicitly requests it
10. **Task context is critical** - `activeContext.md` identifies the current task being worked on

## Key Documentation Files

### For Claude Code Users
- `CLAUDE_CODE_SETUP.md` - Complete setup and usage guide
- `.claude/workflows/workflow-overview.md` - Workflow phases reference
- `.claude/rules/` - Core rules and principles

### For Cursor IDE Users
- `README.md` - Complete system overview and installation
- `COMMANDS_README.md` - Detailed command usage guide
- `COMMANDS_MIGRATION.md` - Migration from custom modes to commands

### For Both Platforms
- `PLATFORM_COMPARISON.md` - Compare Cursor vs Claude Code
- `MEMORY_BANK_OPTIMIZATIONS.md` - Token optimization details
- `creative_mode_think_tool.md` - Creative phase methodology
- `memory_bank_upgrade_guide.md` - Architecture benefits
- `RELEASE_NOTES.md` - Version history

## Using This File with Claude Code

When you start Claude Code in this repository, it automatically reads this `CLAUDE.md` file to understand:
- The Memory Bank System architecture
- Workflow phases and rules
- File naming conventions
- Critical system rules
- AI Quality Rules

### ⚠️ Important: No Slash Commands!

**Important:** Claude Code uses different command names than Cursor IDE!

In Claude Code, the slash `/` is reserved for system commands (`/help`, `/clear`, `/tasks`).

**Instead, use slash commands with `/mb-` prefix**, and Claude will follow the appropriate Memory Bank workflow automatically.

### Example Usage

**Cursor IDE uses these commands:**
```bash
/van Add user authentication
/plan
/creative
/do
```

**Claude Code uses `/mb-` commands:**
```bash
/mb-init Add user authentication
/mb-plan
/mb-design
/mb-do
```

Both achieve the same result - just different command prefixes!

Claude Code will automatically:
1. Recognize which workflow phase you want
2. Follow the appropriate rules from `.claude/`
3. Create/update Memory Bank files
4. Guide you through subsequent phases
5. Maintain context across sessions

**See**:
- `CLAUDE_CODE_SETUP.md` - Complete setup guide
- `.claude/commands/README.md` - Command reference guide

## Platform Support

Memory Bank System supports two platforms:

| Platform | Interface | Command Style | Setup Guide |
|----------|-----------|---------------|-------------|
| **Claude Code** | CLI | Natural language | `CLAUDE_CODE_SETUP.md` |
| **Cursor IDE** | GUI | Slash commands (`/van`, `/plan`) | `README.md` |

See `PLATFORM_COMPARISON.md` for a detailed comparison.

## Version Information

This is Memory Bank System v2.0 with:
- Dual-platform support (Cursor IDE + Claude Code)
- Mandatory MCP server integration
- Enhanced accuracy and improved security
- 15 AI Quality Rules
