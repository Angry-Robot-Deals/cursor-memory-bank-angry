# AI Quality Rules - Detailed Reference

This directory contains the complete 15 AI Quality Rules with detailed examples, code samples, and implementation guidelines.

## Structure

```
ai-quality/
├── foundation/       # Rules 1-3: Core building blocks
├── context/          # Rules 4-6: Information gathering
├── architecture/     # Rules 7-9: Structure and design
├── quality/          # Rules 10-12: Code quality
└── technical/        # Rules 13-15: Technical practices
```

## The 15 Rules

### Foundation Rules (1-3)
1. **[Stubbing/Decomposition](foundation/01-stubbing.md)** - Break into 50-line stubs
2. **[Test-Driven Development](foundation/02-tdd.md)** - Tests before code
3. **[Method Size Limits](foundation/03-method-size.md)** - Max 50 lines, 7-9 objects

### Context Rules (4-6)
4. **[Requirements Gathering](context/04-requirements.md)** - Context before coding
5. **[Definition of Done](context/05-dod.md)** - Explicit done criteria
6. **[Corner Cases](context/06-corner-cases.md)** - List boundaries first

### Architecture Rules (7-9)
7. **[Skeleton-First](architecture/07-skeleton.md)** - Architecture before code
8. **[Iterative Development](architecture/08-iterative.md)** - One method at a time
9. **[Cognitive Load](architecture/09-cognitive-load.md)** - 7±2 objects max

### Quality Rules (10-12)
10. **[Focused Review](quality/10-focused-review.md)** - Review one method only
11. **[Task Boundaries](quality/11-boundaries.md)** - State what's out of scope
12. **[Complexity Check](quality/12-complexity-check.md)** - Verify AI can solve

### Technical Rules (13-15)
13. **[Transaction Isolation](technical/13-transaction.md)** - Explicit isolation levels
14. **[Memory Bank Structure](technical/14-mb-structure.md)** - Hierarchical summaries
15. **[Prompt Engineering](technical/15-prompt-engineering.md)** - Structured prompts

## Usage

Each rule file contains:
- **Core Principle**: What the rule is about
- **Rule Specification**: Formal definition
- **How to Apply**: Step-by-step guide with examples
- **Code Examples**: Real-world implementation
- **Anti-Patterns**: What NOT to do
- **Quality Impact**: Measurable benefits
- **Verification Checklist**: How to verify compliance

## Quick Reference

For a quick overview, see:
- **[AI Quality Principles](../ai-quality-principles.md)** - One-page summary with all rules
- **[Quick Reference Table](../ai-quality-principles.md#quick-rule-reference)** - When to apply each rule

## Integration with Commands

These rules are automatically applied by Claude Code commands:
- `/mb-init` → Rules 4, 12, 14
- `/mb-plan` → Rules 1, 5, 6, 11
- `/mb-design` → Rules 6, 7, 9
- `/mb-do` → Rules 2, 3, 7, 8, 13
- `/mb-reflect` → Rule 10
- `/mb-archive` → Rule 14

## Benefits

Following these rules leads to:
- **40-50% reduction in bugs**
- **30-50% improvement in code quality**
- **Better AI-generated code accuracy**
- **Fewer refactoring cycles**
- **Clearer, more maintainable code**

---

**Version**: Memory Bank System v2.0
**Last Updated**: 2026-01-17
