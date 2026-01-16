# Core Rules

Core rules define the fundamental behavior of the Memory Bank System. These rules apply across all complexity levels and workflow phases.

## Rules in This Category

### System Architecture
- **[Hierarchical Rule Loading](hierarchical-rule-loading.md)** - Progressive rule loading for token optimization
- **[Optimization Integration](optimization-integration.md)** - Integration of optimization strategies
- **[Mode Transition Optimization](mode-transition-optimization.md)** - Efficient context transfer between phases

### Task Management
- **[Task Numbering System](task-numbering-system.md)** - Task ID format and assignment
- **[Task Context Tracking](task-context-tracking.md)** - Current task identification via activeContext.md
- **[Complexity Decision Tree](complexity-decision-tree.md)** - Task complexity assessment

### File Management
- **[Documentation Storage](documentation-storage.md)** - Where to store Memory Bank files
- **[Documentation Tasks Prohibition](documentation-tasks-prohibition.md)** - Never create documentation/tasks/ directory
- **[File Verification](file-verification.md)** - Verify file paths before operations

### Creative Phase
- **[Creative Phase Enforcement](creative-phase-enforcement.md)** - When to trigger creative phases
- **[Creative Phase Metrics](creative-phase-metrics.md)** - How to measure creative phase success

### Platform & Execution
- **[Platform Awareness](platform-awareness.md)** - Detect and adapt to OS/platform
- **[Command Execution](command-execution.md)** - How to execute workflow commands

## How These Rules Work

Core rules are **always active** and apply to all Memory Bank operations regardless of:
- Task complexity level (1-4)
- Current workflow phase (VAN/PLAN/CREATIVE/DO/REFLECT/ARCHIVE)
- Platform (Cursor IDE or Claude Code)

## Integration with Commands

Core rules are automatically enforced by all Claude Code commands:
- `/mb-init` → Uses complexity-decision-tree, task-numbering, platform-awareness
- `/mb-plan` → Uses documentation-storage, file-verification
- `/mb-design` → Uses creative-phase-enforcement, creative-phase-metrics
- `/mb-do` → Uses task-context-tracking, file-verification
- `/mb-reflect` → Uses documentation-storage
- `/mb-archive` → Uses documentation-storage, task-context-tracking

---

**Version**: Memory Bank System v2.0
**Last Updated**: 2026-01-17
