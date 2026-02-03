# Phase-Specific Rules

These rules define specialized behaviors for specific workflow phases. Currently, we have detailed rules for the Creative Phase.

## Creative Phase Rules

The Creative Phase (triggered by `/mb-design`) is where architectural and design decisions are explored and documented using Claude's "Think" tool methodology.

### Rules in This Category

- **[Creative Phase Architecture](creative-creative-phase-architecture.md)** - Architecture design exploration
- **[Creative Phase UI/UX](creative-creative-phase-uiux.md)** - UI/UX design exploration
- **[Optimized Creative Template](creative-optimized-creative-template.md)** - Token-optimized creative documentation

### When Creative Phase is Used

Creative Phase is triggered for **Level 3-4 tasks** when:
- Multiple valid architectural approaches exist
- UI/UX design decisions need exploration
- Algorithm selection requires analysis
- Integration patterns need evaluation
- Data model design needs consideration

### Creative Phase Methodology

Based on Claude's "Think" tool methodology:

1. **PROBLEM** - Define scope and constraints
2. **OPTIONS** - List alternative approaches
3. **ANALYSIS** - Compare options (tabular format)
4. **DECISION** - Select approach with rationale
5. **GUIDELINES** - Document implementation rules

### Documentation Format

Creative Phase documents are saved to:
```
memory-bank/creative/creative-[task_id]-[feature_name].md
```

### Token Optimization

Creative Phase uses **progressive documentation**:
- Tabular format for option comparison (~60% token reduction)
- "Detail-on-demand" approach
- Incremental refinement
- Focus on decision rationale

### Integration with Commands

Creative Phase rules are applied by:
- `/mb-design` - Executes creative exploration
- `/mb-plan` - Identifies components needing creative phase
- `/mb-archive` - Archives creative phase documents

## Future Phase Rules

Additional phase-specific rules may be added for:
- VAN Phase (initialization)
- PLAN Phase (planning)
- DO Phase (implementation)
- REFLECT Phase (reflection)
- ARCHIVE Phase (archiving)

Currently, these phases rely on Core and Level-specific rules.

## Related Rules

- **Core**: [Creative Phase Enforcement](../core/creative-phase-enforcement.md) - When to trigger
- **Core**: [Creative Phase Metrics](../core/creative-phase-metrics.md) - Success measurement
- **AI Quality**: [Rule #6 - Corner Cases](../ai-quality/context/06-corner-cases.md) - Related to option exploration
- **AI Quality**: [Rule #7 - Skeleton-First](../ai-quality/architecture/07-skeleton.md) - Related to architecture decisions

---

**Version**: Memory Bank System v2.0
**Last Updated**: 2026-01-17
