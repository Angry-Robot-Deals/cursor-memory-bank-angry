# Level-Specific Rules

These rules define workflows and behaviors for different task complexity levels (1-4). Each level has its own workflow, documentation requirements, and quality standards.

## Complexity Levels Overview

| Level | Type | Duration | Documentation | Examples |
|-------|------|----------|---------------|----------|
| **Level 1** | Quick Fix | < 1 hour | Minimal | Bug fixes, typos, config changes |
| **Level 2** | Enhancement | 1-4 hours | Basic | Small features, refactoring |
| **Level 3** | Feature | 1-2 days | Comprehensive | New features, integrations |
| **Level 4** | System | 1+ weeks | Enterprise-grade | Major systems, architecture changes |

## Level 1: Quick Fix Pipeline

**Workflow**: `/mb-init` → `/mb-do` → `/mb-reflect` → `/mb-archive`

**Rules**:
- **[Workflow Level 1](level1-workflow-level1.md)** - Complete workflow definition
- **[Optimized Workflow](level1-optimized-workflow-level1.md)** - Token-optimized version
- **[Quick Documentation](level1-quick-documentation.md)** - Minimal documentation requirements

**Characteristics**:
- No planning phase required
- Ultra-compact documentation
- Consolidated Memory Bank updates
- 3-phase workflow (skip PLAN/CREATIVE)

## Level 2: Enhancement Pipeline

**Workflow**: `/mb-init` → `/mb-plan` → `/mb-do` → `/mb-reflect` → `/mb-archive`

**Rules**:
- **[Workflow Level 2](level2-workflow-level2.md)** - Complete workflow definition
- **[Task Tracking Basic](level2-task-tracking-basic.md)** - Basic task documentation
- **[Reflection Basic](level2-reflection-basic.md)** - Basic reflection requirements
- **[Archive Basic](level2-archive-basic.md)** - Basic archiving process

**Characteristics**:
- Requires planning phase
- Balanced 4-phase workflow
- Simplified planning templates
- No creative phase needed

## Level 3: Feature Development Pipeline

**Workflow**: `/mb-init` → `/mb-plan` → `/mb-design` → `/mb-do` → `/mb-reflect` → `/mb-archive`

**Rules**:
- **[Workflow Level 3](level3-workflow-level3.md)** - Complete workflow definition
- **[Planning Comprehensive](level3-planning-comprehensive.md)** - Detailed planning requirements
- **[Implementation Intermediate](level3-implementation-intermediate.md)** - Implementation standards
- **[Task Tracking Intermediate](level3-task-tracking-intermediate.md)** - Intermediate task documentation
- **[Reflection Intermediate](level3-reflection-intermediate.md)** - Intermediate reflection
- **[Archive Intermediate](level3-archive-intermediate.md)** - Intermediate archiving

**Characteristics**:
- Full 5-phase workflow
- Creative phase for design decisions
- Optimized creative templates
- Comprehensive documentation

## Level 4: Enterprise System Pipeline

**Workflow**: `/mb-init` → `/mb-plan` → `/mb-design` → `/mb-do` → `/mb-reflect` → `/mb-archive`

**Rules**:
- **[Workflow Level 4](level4-workflow-level4.md)** - Complete workflow definition
- **[Architectural Planning](level4-architectural-planning.md)** - Architecture-first approach
- **[Phased Implementation](level4-phased-implementation.md)** - Multi-phase implementation
- **[Task Tracking Advanced](level4-task-tracking-advanced.md)** - Advanced task documentation
- **[Reflection Comprehensive](level4-reflection-comprehensive.md)** - Comprehensive reflection
- **[Archive Comprehensive](level4-archive-comprehensive.md)** - Enterprise archiving

**Characteristics**:
- Advanced 6-phase workflow
- Multiple creative phases possible
- Tiered documentation templates
- Enhanced governance controls

## How Level Selection Works

Level is determined automatically by `/mb-init` based on:
1. **Scope**: Files/modules affected
2. **Complexity**: Technical challenges
3. **Duration**: Estimated time
4. **Risk**: Impact on system
5. **Dependencies**: Integration points

See [Core/complexity-decision-tree.md](../core/complexity-decision-tree.md) for the decision algorithm.

## Token Optimization by Level

Each level uses progressively more context as needed:

```
Level 1: ~500 tokens   (minimal rules)
Level 2: ~1500 tokens  (basic rules)
Level 3: ~3000 tokens  (comprehensive rules)
Level 4: ~5000 tokens  (enterprise rules)
```

This approach ensures you only load rules needed for your task's complexity.

---

**Version**: Memory Bank System v2.0
**Last Updated**: 2026-01-17
