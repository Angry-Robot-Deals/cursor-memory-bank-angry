# Claude Code Configuration

This directory contains Claude Code-specific configuration files for the Memory Bank System.

## Using Memory Bank with Claude Code

**Claude Code uses slash commands** - similar to Cursor IDE but with `/mb-` prefix.

See `.claude/commands/README.md` for command reference.

## Directory Structure

```
.claude/
├── README.md                   # This file
├── commands/                   # Slash command definitions
│   ├── README.md               # Command reference
│   ├── mb-prd.md               # /mb-prd - Generate PRD
│   ├── mb-init.md              # /mb-init - Initialize task
│   ├── mb-plan.md              # /mb-plan - Create plan
│   ├── mb-design.md            # /mb-design - Explore designs
│   ├── mb-do.md                # /mb-do - Implement
│   ├── mb-reflect.md           # /mb-reflect - Review
│   ├── mb-archive.md           # /mb-archive - Archive
│   ├── mb-status.md            # /mb-status - Check status
│   └── mb-continue.md          # /mb-continue - Continue task
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

**See**: [.claude/rules/README.md](rules/README.md) for complete rule documentation.

## Main Entry Point

The main configuration file for Claude Code is:
- **`CLAUDE.md`** (in project root) - Read by Claude Code on startup

This `.claude/` directory provides supporting documentation and rules that complement `CLAUDE.md`.

## Quick Start

**For first-time users:**

1. Commands are already installed in `.claude/commands/`
2. Read `.claude/commands/README.md` for command reference
3. Start Claude Code and use: `/mb-init`, `/mb-plan`, etc.

## Related Files

- `CLAUDE.md` - Main configuration (root level)
- `CLAUDE_CODE_SETUP.md` - Installation and usage guide
- `.claude/commands/README.md` - Command reference
- `PLATFORM_COMPARISON.md` - Cursor vs Claude Code comparison

## Version

Claude Code Configuration v2.0 - Compatible with Memory Bank System v2.0
