# Project Structure

This document explains the directory structure of the Memory Bank System with dual-platform support.

## Overview

Memory Bank supports **two AI platforms**:
1. **Cursor IDE** - Graphical IDE with slash commands
2. **Claude Code** - Command-line tool with slash commands

## Directory Structure

```
cursor-memory-bank/
├── CLAUDE.md                        # Claude Code main configuration
├── README.md                        # Main documentation (Cursor-focused)
├── CLAUDE_CODE_SETUP.md            # Claude Code setup guide
├── PLATFORM_COMPARISON.md          # Platform comparison guide
├── COMMANDS_README.md              # Cursor commands documentation
├── COMMANDS_MIGRATION.md           # Cursor migration guide
│
├── .claude/                        # Claude Code Configuration
│   ├── README.md                   # Claude Code config overview
│   ├── workflows/                  # Natural language workflow guides
│   │   └── workflow-overview.md   # Complete workflow reference
│   ├── rules/                      # Core rules for Claude Code
│   │   ├── memory-bank-paths.md   # File path definitions
│   │   ├── ai-quality-principles.md  # AI Quality Rules
│   │   ├── mcp-integration.md     # MCP server integration
│   │   └── git-push-restriction.md   # Git safety rules
│   └── guides/                     # Additional guides (placeholder)
│
├── .cursor/                        # Cursor IDE Configuration
│   ├── commands/                   # Slash commands (/van, /plan, etc.)
│   │   ├── van.md
│   │   ├── plan.md
│   │   ├── creative.md
│   │   ├── do.md
│   │   ├── reflect.md
│   │   ├── archive.md
│   │   └── prd.md
│   ├── rules/                      # Cursor-specific rules
│   │   └── isolation_rules/        # Hierarchical rule system
│   │       ├── main.mdc            # Main rule file
│   │       ├── Core/               # Core rules (always loaded)
│   │       ├── Level1-4/           # Complexity-specific rules
│   │       ├── Phases/             # Phase-specific rules
│   │       └── visual-maps/        # Workflow visualizations
│   └── templates/                  # Global templates
│       └── prd-template.md         # PRD document template
│
└── memory-bank/                    # Shared Memory Bank Files
    ├── tasks.md                    # Active task tracking
    ├── activeContext.md            # Current task context
    ├── progress.md                 # Implementation progress
    ├── projectbrief.md             # Project foundation
    ├── productContext.md           # Product requirements
    ├── systemPatterns.md           # Architecture patterns
    ├── techContext.md              # Technology stack
    ├── prd/                        # Product Requirements Documents
    ├── creative/                   # Design decision documents
    ├── reflection/                 # Task reflections
    ├── archive/                    # Completed task archives
    ├── tasks/                      # Task-specific docs
    ├── qa/                         # QA reports
    └── reports/                    # Debug/diagnostic reports
```

## Platform-Specific Files

### For Cursor IDE Users

**Required:**
- `.cursor/commands/*.md` - Slash commands
- `.cursor/rules/isolation_rules/**/*.mdc` - Hierarchical rules

**Documentation:**
- `README.md` - Main installation guide
- `COMMANDS_README.md` - Command reference
- `COMMANDS_MIGRATION.md` - Migration from custom modes

### For Claude Code Users

**Required:**
- `CLAUDE.md` - Main configuration file (root level)
- `.claude/workflows/*.md` - Workflow guides
- `.claude/rules/*.md` - Core rules

**Documentation:**
- `CLAUDE_CODE_SETUP.md` - Installation and usage guide
- `.claude/README.md` - Configuration overview

### Shared by Both Platforms

**Memory Bank Files:**
- All files in `memory-bank/` directory
- PRD documents, creative docs, reflections, archives
- Task tracking and progress files

**Documentation:**
- `PLATFORM_COMPARISON.md` - Compare platforms
- `MEMORY_BANK_OPTIMIZATIONS.md` - Token optimization details
- `creative_mode_think_tool.md` - Creative phase methodology
- `memory_bank_upgrade_guide.md` - Architecture benefits
- `RELEASE_NOTES.md` - Version history

## Key Differences

### Configuration Location

| Aspect | Cursor IDE | Claude Code |
|--------|-----------|-------------|
| **Main Config** | `.cursor/commands/*.md` | `CLAUDE.md` |
| **Rules** | `.cursor/rules/isolation_rules/**/*.mdc` | `.claude/rules/*.md` |
| **Format** | MDC (Cursor-specific) | Markdown |
| **Structure** | Hierarchical (progressive loading) | Flat (modular) |

### Command Style

| Aspect | Cursor IDE | Claude Code |
|--------|-----------|-------------|
| **Syntax** | Slash commands | Natural language |
| **Example** | `/van Initialize task` | "Initialize a new task" |
| **Discovery** | Type `/` to see list | Ask "What can I do?" |

## Installation Paths

### Cursor IDE
```bash
# Copy .cursor folder
cp -r cursor-memory-bank/.cursor /path/to/project/
```

### Claude Code
```bash
# Copy CLAUDE.md and .claude folder
cp cursor-memory-bank/CLAUDE.md /path/to/project/
cp -r cursor-memory-bank/.claude /path/to/project/
```

### Both Platforms
```bash
# Copy everything
cp -r cursor-memory-bank/.cursor /path/to/project/
cp cursor-memory-bank/CLAUDE.md /path/to/project/
cp -r cursor-memory-bank/.claude /path/to/project/
```

## File Compatibility

**✅ 100% Compatible:**
- All `memory-bank/` files
- PRD documents
- Creative phase documents
- Reflection documents
- Archive documents

**⚠️ Platform-Specific:**
- `.cursor/` files (Cursor IDE only)
- `.claude/` files (Claude Code only)
- `CLAUDE.md` (Claude Code entry point)

## Switching Between Platforms

You can freely switch between Cursor IDE and Claude Code:

1. **Same project** - Both platforms use the same `memory-bank/` files
2. **No conversion needed** - Files are standard Markdown
3. **Context preserved** - Task state maintained across platforms

**Example:**
```bash
# Morning: Work in Cursor IDE
cursor .

# Afternoon: Switch to Claude Code on remote server
ssh remote-server
cd project
claude
# Continue where you left off!
```

## Development Workflow

### Typical Cursor IDE Workflow
```
/van → /plan → /creative → /do → /reflect → /archive
```

### Typical Claude Code Workflow
```
"Initialize task" → "Create plan" → "Explore design" →
"Implement" → "Reflect" → "Archive"
```

### Hybrid Workflow
```
Cursor: /van, /plan
Claude Code: "Continue with creative phase"
Cursor: /do, /reflect
Claude Code: "Archive completed task"
```

## Quick Reference

| Need | Platform | File/Command |
|------|----------|--------------|
| Add new command | Cursor | Create `.cursor/commands/name.md` |
| Add new rule | Cursor | Create `.cursor/rules/isolation_rules/.../rule.mdc` |
| Add workflow guide | Claude Code | Create `.claude/workflows/guide.md` |
| Add rule | Claude Code | Create `.claude/rules/rule.md` |
| Update main config | Claude Code | Edit `CLAUDE.md` |
| Share between platforms | Both | Use `memory-bank/` files |

## Support

- **Cursor IDE**: See `README.md` and `COMMANDS_README.md`
- **Claude Code**: See `CLAUDE_CODE_SETUP.md` and `.claude/README.md`
- **Platform Comparison**: See `PLATFORM_COMPARISON.md`

---

**Version**: Memory Bank System v2.0 with dual-platform support
