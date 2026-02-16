# Claude Code Configuration

This directory contains Claude Code-specific configuration files for the Memory Bank System.

## Using Memory Bank with Claude Code

**Claude Code uses slash commands** - similar to Cursor IDE but with `/mb-` prefix.

See `documentation/claude/commands-reference.md` for command reference.

## Directory Structure

```
.claude/
├── agents/                     # 6 specialized AI roles
│   ├── architect.md            # System design, interfaces
│   ├── code-simplifier.md      # Code simplification (compliance)
│   ├── compliance.md           # Post-QA hardening workflow
│   ├── developer.md            # TDD, implementation
│   ├── planner.md              # Task breakdown, plans
│   └── reviewer.md             # QA, reflection
├── commands/                   # 10 slash command definitions
│   ├── mb-prd.md               # /mb-prd - Generate PRD
│   ├── mb-init.md              # /mb-init - Initialize task
│   ├── mb-plan.md              # /mb-plan - Create plan
│   ├── mb-design.md            # /mb-design - Explore designs
│   ├── mb-do.md                # /mb-do - Implement
│   ├── mb-compliance.md        # /mb-compliance - Post-QA hardening
│   ├── mb-reflect.md           # /mb-reflect - Review
│   ├── mb-archive.md           # /mb-archive - Archive
│   ├── mb-status.md            # /mb-status - Check status
│   └── mb-continue.md          # /mb-continue - Continue task
├── skills/                     # 7 knowledge modules
│   ├── ai-quality.md           # 15 AI development rules
│   ├── compliance.md           # Compliance workflow (7 steps)
│   ├── memory-bank-system.md  # File organization, task tracking
│   ├── performance.md          # Performance optimization
│   ├── security.md             # Security best practices
│   ├── tech-stack.md           # Tech stack guidance
│   └── testing.md              # Testing strategies
├── workflows/                  # Workflow descriptions
├── rules/                      # Core rules and principles
│   ├── ai-quality-principles.md      # AI Quality Rules summary
│   ├── ai-quality/                   # Detailed AI Quality Rules (15 rules)
│   │   ├── README.md                 # Rules overview
│   │   ├── foundation/               # Rules 1-3
│   │   ├── context/                  # Rules 4-6
│   │   ├── architecture/             # Rules 7-9
│   │   ├── quality/                  # Rules 10-12
│   │   └── technical/                # Rules 13-15
│   ├── memory-bank-paths.md          # File path definitions
│   ├── mcp-integration.md            # MCP server integration
│   └── git-push-restriction.md       # Git safety rules
└── guides/                     # Usage guides and examples
```

## Purpose

While Cursor IDE uses slash commands (`.cursor/commands/`) and MDC rule files (`.cursor/rules/`), Claude Code uses:
- **Slash commands** - Like Cursor, stored in `.claude/commands/` (e.g., `/mb-init`, `/mb-plan`)
- **Markdown rules** - Same principles as Cursor, converted to `.md` format (53 rules total)
- **Usage guides** - Examples and best practices

## Rule System

Claude Code has **complete parity** with Cursor IDE rules:

| Category | Count | Purpose |
|----------|-------|---------|
| **AI Quality** | 15 rules | Research-proven code quality rules |
| **Core** | 13 rules | Fundamental system behavior |
| **Levels** | 19 rules | Complexity-specific workflows (1-4) |
| **Phases** | 3 rules | Creative Phase specialization |
| **Standalone** | 3 rules | Git, MCP, file paths |
| **Total** | **53 rules** | Complete Memory Bank system |

**See**: `.claude/rules/README.md` for complete rule documentation (rules stay in .claude).

## Main Entry Point

The main configuration file for Claude Code is:
- **`CLAUDE.md`** (in project root) - Read by Claude Code on startup

This `.claude/` directory provides supporting configuration and rules that complement `CLAUDE.md`.

## Quick Start

**For first-time users:**

1. Commands are already installed in `.claude/commands/`
2. Read `documentation/claude/commands-reference.md` for command reference
3. Start Claude Code and use: `/mb-init`, `/mb-plan`, etc.

## Related Files

- `CLAUDE.md` - Main configuration (root level)
- `documentation/claude/INSTALLATION_GUIDE.md` - Installation and setup
- `documentation/claude/commands-reference.md` - Command reference
- `PLATFORM_COMPARISON.md` - Cursor vs Claude Code comparison (if at root)

## Version

Claude Code Configuration v2.0 - Compatible with Memory Bank System v2.0
