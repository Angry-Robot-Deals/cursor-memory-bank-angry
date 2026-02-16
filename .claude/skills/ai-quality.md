---
name: ai-quality
description: Five pillars of AI-assisted development (decomposition, test-first, architecture-first, focused work, context). Use for TDD, stubbing, method size limits, DoD, and code quality decisions.
---

# AI Quality & Best Practices

> **TL;DR:** These 5 pillars guide AI-assisted development. Apply them consistently for 30-50% better code quality and 40-50% fewer bugs.

## 🎯 THE 5 PILLARS OF QUALITY AI DEVELOPMENT

### 1️⃣ DECOMPOSITION (Rules #1, #3, #9)
> **Break complex tasks into small, focused units.**

```
KEY LIMITS:
├── Max 50 lines per method
├── Max 7-9 objects in working memory
└── One responsibility per function
```

**Why:** AI loses focus with complexity. Small units = better output.

---

### 2️⃣ TEST-FIRST (Rules #2, #5, #6)
> **Tests are hallucination filters. Mock edges, not logic.**

```
SEQUENCE:
1. Write tests BEFORE code
2. Define "done" explicitly (DoD)
3. Cover corner cases upfront
4. STRICT mocking: edges only, NO data fitting
```

**Why:** Tests catch AI mistakes. No tests = no safety net.

---

### 3️⃣ ARCHITECTURE-FIRST (Rules #7, #8)
> **Approve structure before coding.**

```
APPROACH:
1. Create skeleton with stubs
2. Review architecture
3. Implement one method at a time
```

**Why:** Bad architecture = wasted work. Validate first.

---

### 4️⃣ FOCUSED WORK (Rules #10, #11, #12)
> **Narrow context improves quality.**

```
PRACTICES:
├── Review one method at a time
├── Define clear boundaries (what we DON'T do)
└── Verify AI can solve before starting
```

**Why:** Broad context = scattered results. Focus = precision.

---

### 5️⃣ CONTEXT MANAGEMENT (Rules #4, #13, #14, #15)
> **Right information at right time.**

```
ELEMENTS:
├── Gather requirements BEFORE coding
├── Document transaction isolation needs
├── Structure Memory Bank hierarchically
└── Engineer prompts carefully
```

**Why:** Bad context = bad output. Quality in = quality out.

---

## 📋 QUICK RULE REFERENCE

| # | Rule | One-Liner | Mode |
|---|------|-----------|------|
| 1 | Stubbing | Break into 50-line stubs | PLAN, BUILD |
| 2 | TDD | Tests before code (Strict Mocking) | BUILD |
| 3 | Method Size | Max 50 lines, 7-9 objects | BUILD |
| 4 | Requirements | Context before coding | VAN, PLAN |
| 5 | DoD | Explicit done criteria | PLAN |
| 6 | Corner Cases | List boundaries first | PLAN, CREATIVE |
| 7 | Skeleton | Architecture before code | PLAN, CREATIVE |
| 8 | Iterative | One method at a time | BUILD |
| 9 | Cognitive | 7±2 objects max | BUILD |
| 10 | Review | Review one method only | REFLECT |
| 11 | Boundaries | State what's out of scope | PLAN |
| 12 | Complexity | Verify AI can solve | VAN |
| 13 | Transaction | Explicit isolation levels | BUILD, CREATIVE |
| 14 | MB Structure | Hierarchical summaries | VAN, ARCHIVE |
| 15 | Prompts | Structured prompt creation | ALL |

---

## ✅ QUALITY CHECKPOINT

Before proceeding, ask:

```
□ Is this task decomposed into small units?
□ Do I have tests/DoD defined?
□ Is the architecture approved?
□ Am I focused on one thing?
□ Do I have the right context?
```

**If NO to any:** Stop and address before coding.

---

## 🚩 COMMON MISTAKES

### ❌ DON'T
- Write code before tests
- Create methods > 50 lines
- Track > 9 objects per method
- Review entire features at once
- Start without clear requirements
- Skip corner case analysis

### ✅ DO
- Tests → Code → Review → Next
- Keep methods small and focused
- One method at a time
- Define boundaries explicitly
- Document requirements upfront

---

*These principles reduce bugs by 40-50% and improve code quality by 30-50%.*
