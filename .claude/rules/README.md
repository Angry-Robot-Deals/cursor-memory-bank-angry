# Claude Code Rules

This directory contains all rules for the Memory Bank System when used with Claude Code. These rules are automatically applied by Claude Code commands and workflow phases.

## Directory Structure

```
.claude/rules/
├── README.md                        # This file
│
├── ai-quality-principles.md         # Quick reference for all 15 AI Quality Rules
│
├── ai-quality/                      # Detailed AI Quality Rules (15 rules)
│   ├── README.md                    # AI Quality Rules overview
│   ├── foundation/                  # Rules 1-3: Core building blocks
│   ├── context/                     # Rules 4-6: Information gathering
│   ├── architecture/                # Rules 7-9: Structure and design
│   ├── quality/                     # Rules 10-12: Code quality
│   └── technical/                   # Rules 13-15: Technical practices
│
├── core/                            # Core System Rules (13 rules)
│   ├── README.md                    # Core rules overview
│   ├── command-execution.md
│   ├── complexity-decision-tree.md
│   ├── creative-phase-enforcement.md
│   ├── creative-phase-metrics.md
│   ├── documentation-storage.md
│   ├── documentation-tasks-prohibition.md
│   ├── file-verification.md
│   ├── hierarchical-rule-loading.md
│   ├── mode-transition-optimization.md
│   ├── optimization-integration.md
│   ├── platform-awareness.md
│   ├── task-context-tracking.md
│   └── task-numbering-system.md
│
├── levels/                          # Level-Specific Rules (19 rules)
│   ├── README.md                    # Levels overview
│   ├── level1-*.md                  # Level 1 (Quick Fix) - 3 rules
│   ├── level2-*.md                  # Level 2 (Enhancement) - 4 rules
│   ├── level3-*.md                  # Level 3 (Feature) - 6 rules
│   └── level4-*.md                  # Level 4 (System) - 6 rules
│
├── phases/                          # Phase-Specific Rules (3 rules)
│   ├── README.md                    # Phases overview
│   └── creative-*.md                # Creative Phase rules
│
├── git-push-restriction.md          # Git safety rule (never push without permission)
├── mcp-integration.md               # MCP server integration requirements
└── memory-bank-paths.md             # File path definitions
```

## Rule Categories

### 1. AI Quality Rules (15 rules)
**Purpose**: Research-proven rules that improve AI-generated code quality by 30-50%

**Categories**:
- Foundation (1-3): Decomposition, TDD, Method Size
- Context (4-6): Requirements, DoD, Corner Cases
- Architecture (7-9): Skeleton-First, Iterative, Cognitive Load
- Quality (10-12): Focused Review, Boundaries, Complexity Check
- Technical (13-15): Transactions, MB Structure, Prompts

**See**: [ai-quality/README.md](ai-quality/README.md)

### 2. Core Rules (13 rules)
**Purpose**: Fundamental system behavior that applies across all levels and phases

**Categories**:
- System Architecture: Hierarchical loading, optimization, transitions
- Task Management: Numbering, context tracking, complexity assessment
- File Management: Storage rules, verification, prohibitions
- Creative Phase: Enforcement and metrics
- Platform: Awareness and command execution

**See**: [core/README.md](core/README.md)

### 3. Level-Specific Rules (19 rules)
**Purpose**: Workflows and behaviors adapted to task complexity

**Levels**:
- Level 1 (3 rules): Quick fixes, minimal documentation
- Level 2 (4 rules): Enhancements, basic documentation
- Level 3 (6 rules): Features, comprehensive documentation
- Level 4 (6 rules): Systems, enterprise documentation

**See**: [levels/README.md](levels/README.md)

### 4. Phase-Specific Rules (3 rules)
**Purpose**: Specialized behaviors for specific workflow phases

**Currently**:
- Creative Phase: Architecture, UI/UX, optimized templates

**See**: [phases/README.md](phases/README.md)

### 5. Standalone Rules (3 rules)
**Purpose**: Critical cross-cutting concerns

- **git-push-restriction.md**: Never push to remote without explicit permission
- **mcp-integration.md**: Mandatory MCP server usage (sys8, context7)
- **memory-bank-paths.md**: File path definitions for Memory Bank

## How Rules Are Applied

### By Command

Each Claude Code command automatically applies relevant rules:

| Command | Core Rules | Level Rules | Phase Rules | AI Quality |
|---------|-----------|-------------|-------------|------------|
| `/mb-init` | ✓ All | ✓ Selected | - | Rules 4,12,14 |
| `/mb-plan` | ✓ All | ✓ Selected | - | Rules 1,5,6,11 |
| `/mb-design` | ✓ All | ✓ Selected | ✓ Creative | Rules 6,7,9 |
| `/mb-do` | ✓ All | ✓ Selected | - | Rules 2,3,7,8,13 |
| `/mb-reflect` | ✓ All | ✓ Selected | - | Rule 10 |
| `/mb-archive` | ✓ All | ✓ Selected | - | Rule 14 |

### By Complexity Level

Rules are progressively loaded based on task complexity:

```
Level 1: Core + Level1 + AI Quality (quick reference)
Level 2: Core + Level2 + AI Quality (summary)
Level 3: Core + Level3 + Creative Phase + AI Quality (detailed)
Level 4: Core + Level4 + Creative Phase + AI Quality (comprehensive)
```

This hierarchical approach reduces token usage by ~70% compared to loading all rules at once.

## Quick Reference

### For Quick Tasks (Level 1)
- Read: [levels/level1-workflow-level1.md](levels/level1-workflow-level1.md)
- Apply: Minimal documentation, fast workflow

### For Standard Features (Level 2-3)
- Read: [levels/level2-workflow-level2.md](levels/level2-workflow-level2.md) or [levels/level3-workflow-level3.md](levels/level3-workflow-level3.md)
- Apply: Balanced documentation, full workflow

### For Complex Systems (Level 4)
- Read: [levels/level4-workflow-level4.md](levels/level4-workflow-level4.md)
- Apply: Enterprise documentation, advanced workflow

### For AI Quality
- Read: [ai-quality-principles.md](ai-quality-principles.md) - Quick reference table
- Detailed: [ai-quality/README.md](ai-quality/README.md) - Full rules with examples

## Total Rule Count

- **AI Quality Rules**: 15
- **Core Rules**: 13
- **Level Rules**: 19 (3+4+6+6)
- **Phase Rules**: 3
- **Standalone Rules**: 3
- **Total**: 53 rules

All rules are available as standalone Markdown files for easy reference and integration.

## Differences from Cursor IDE

| Aspect | Cursor IDE | Claude Code |
|--------|-----------|-------------|
| **Format** | `.mdc` (MDC format) | `.md` (Markdown) |
| **Location** | `.cursor/rules/isolation_rules/` | `.claude/rules/` |
| **YAML Frontmatter** | Yes (for progressive loading) | No (not needed) |
| **Content** | Identical | Identical |
| **Integration** | Automatic via Cursor | Automatic via Claude Code |

Both platforms share the same Memory Bank principles and achieve the same token optimization.

---

**Version**: Memory Bank System v2.0
**Last Updated**: 2026-01-17

**See Also**:
- [CLAUDE.md](../../CLAUDE.md) - Main Claude Code configuration
- [CLAUDE_CODE_SETUP.md](../../CLAUDE_CODE_SETUP.md) - Setup guide
- [.claude/commands/README.md](../commands/README.md) - Command reference
