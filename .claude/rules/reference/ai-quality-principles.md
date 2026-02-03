# AI Quality Rules - Core Principles

These 5 pillars guide AI-assisted development, reducing bugs by 40-50% and improving code quality by 30-50%.

## The 5 Pillars of Quality AI Development

### 1️⃣ DECOMPOSITION (Rules #1, #3, #9)

**Principle**: Break complex tasks into small, focused units.

**Key Limits**:
- Max 50 lines per method
- Max 7-9 objects in working memory
- One responsibility per function

**Why**: AI loses focus with complexity. Small units = better output.

---

### 2️⃣ TEST-FIRST (Rules #2, #5, #6)

**Principle**: Tests are hallucination filters.

**Sequence**:
1. Write tests BEFORE code
2. Define "done" explicitly (DoD)
3. Cover corner cases upfront

**Why**: Tests catch AI mistakes. No tests = no safety net.

---

### 3️⃣ ARCHITECTURE-FIRST (Rules #7, #8)

**Principle**: Approve structure before coding.

**Approach**:
1. Create skeleton with stubs
2. Review architecture
3. Implement one method at a time

**Why**: Bad architecture = wasted work. Validate first.

---

### 4️⃣ FOCUSED WORK (Rules #10, #11, #12)

**Principle**: Narrow context improves quality.

**Practices**:
- Review one method at a time
- Define clear boundaries (what we DON'T do)
- Verify AI can solve before starting

**Why**: Broad context = scattered results. Focus = precision.

---

### 5️⃣ CONTEXT MANAGEMENT (Rules #4, #13, #14, #15)

**Principle**: Right information at right time.

**Elements**:
- Gather requirements BEFORE coding
- Document transaction isolation needs
- Structure Memory Bank hierarchically
- Engineer prompts carefully

**Why**: Bad context = bad output. Quality in = quality out.

---

## Quick Rule Reference

| # | Rule | One-Liner | When to Apply |
|---|------|-----------|---------------|
| 1 | Stubbing | Break into 50-line stubs | Planning, Implementation |
| 2 | TDD | Tests before code | Implementation |
| 3 | Method Size | Max 50 lines, 7-9 objects | Implementation |
| 4 | Requirements | Context before coding | Initialization, Planning |
| 5 | DoD | Explicit done criteria | Planning |
| 6 | Corner Cases | List boundaries first | Planning, Design |
| 7 | Skeleton | Architecture before code | Planning, Design |
| 8 | Iterative | One method at a time | Implementation |
| 9 | Cognitive | 7±2 objects max | Implementation |
| 10 | Review | Review one method only | Reflection |
| 11 | Boundaries | State what's out of scope | Planning |
| 12 | Complexity | Verify AI can solve | Initialization |
| 13 | Transaction | Explicit isolation levels | Implementation, Design |
| 14 | MB Structure | Hierarchical summaries | Initialization, Archive |
| 15 | Prompts | Structured prompt creation | All phases |

---

## Quality Checkpoint

Before proceeding with any phase, ask:

```
□ Is this task decomposed into small units?
□ Do I have tests/DoD defined?
□ Is the architecture approved?
□ Am I focused on one thing?
□ Do I have the right context?
```

**If NO to any**: Stop and address before coding.

---

## Applying These Rules with Commands

When working with Claude Code commands, these principles are automatically applied:

### Command-based workflow:
- `/mb-do` → Automatically enforces TDD, method size limits, and iterative development
- `/mb-plan` → Creates skeleton with stubs before implementation
- `/mb-design` → Explores architectural options before coding

### During implementation:
- **User**: `/mb-init Implement authentication system`
- **Assistant**: "I'll create an architectural skeleton with stubs for approval before implementing. This ensures we have the right structure before diving into details."

---

## Detailed Rules

The table above provides a quick reference for all 15 AI Quality Rules. For detailed explanations with code examples, implementation guides, and anti-patterns, see the full rule files:

### Foundation Rules (1-3)
- **Rule #1**: [Stubbing/Decomposition](ai-quality/foundation/01-stubbing.md) - Break into 50-line stubs
- **Rule #2**: [Test-Driven Development](ai-quality/foundation/02-tdd.md) - Tests before code
- **Rule #3**: [Method Size Limits](ai-quality/foundation/03-method-size.md) - Max 50 lines, 7-9 objects

### Context Rules (4-6)
- **Rule #4**: [Requirements Gathering](ai-quality/context/04-requirements.md) - Context before coding
- **Rule #5**: [Definition of Done](ai-quality/context/05-dod.md) - Explicit done criteria
- **Rule #6**: [Corner Cases](ai-quality/context/06-corner-cases.md) - List boundaries first

### Architecture Rules (7-9)
- **Rule #7**: [Skeleton-First Development](ai-quality/architecture/07-skeleton.md) - Architecture before code
- **Rule #8**: [Iterative Development](ai-quality/architecture/08-iterative.md) - One method at a time
- **Rule #9**: [Cognitive Load Management](ai-quality/architecture/09-cognitive-load.md) - 7±2 objects max

### Quality Rules (10-12)
- **Rule #10**: [Focused Code Review](ai-quality/quality/10-focused-review.md) - Review one method only
- **Rule #11**: [Task Boundaries](ai-quality/quality/11-boundaries.md) - State what's out of scope
- **Rule #12**: [Complexity Check](ai-quality/quality/12-complexity-check.md) - Verify AI can solve

### Technical Rules (13-15)
- **Rule #13**: [Transaction Isolation](ai-quality/technical/13-transaction.md) - Explicit isolation levels
- **Rule #14**: [Memory Bank Structure](ai-quality/technical/14-mb-structure.md) - Hierarchical summaries
- **Rule #15**: [Prompt Engineering](ai-quality/technical/15-prompt-engineering.md) - Structured prompts

Each detailed rule file includes:
- Core principle and goals
- Step-by-step implementation guide
- Real code examples (good and bad)
- Anti-patterns to avoid
- Quality impact measurements
- Verification checklists

**See also**: [ai-quality/README.md](ai-quality/README.md) for complete directory structure and usage guide.

---

## References

- Full principles document: See `CLAUDE.md` section "AI Quality Rules"
- Cursor equivalent: `.cursor/rules/isolation_rules/Core/AI-Quality/_principles.mdc`
- Research basis: See `creative_mode_think_tool.md`

---

*These principles reduce bugs by 40-50% and improve code quality by 30-50%.*
