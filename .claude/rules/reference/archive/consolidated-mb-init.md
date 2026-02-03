# Consolidated Rules for /mb-init Command
## Initialization & Task Foundation

This consolidated file combines critical rules for the initialization phase (/mb-init):
- **Rule #4**: Requirements Gathering (context before coding)
- **Rule #5**: Definition of Done (explicit completion criteria)
- **Rule #6**: Corner Cases (boundary conditions documentation)
- **Rule #11**: Task Boundaries (scope management)
- **Reference**: Memory Bank file paths and structure

Together these rules establish the foundation for all subsequent work phases.

---

## RULE #4: REQUIREMENTS GATHERING

**Goal:** Increase AI accuracy by 50% by providing complete context BEFORE coding.

**Core Principle:**
Gather ALL requirements (context, expected results, DoD, boundaries) BEFORE ANY code is written. AI output quality is directly proportional to input quality.

### How to Apply

#### Step 1: Document Context

```markdown
## Context

### Current State
- System: E-commerce platform
- Module: Payment processing
- Technology: Node.js, PostgreSQL
- Related files: /src/payments/*.ts

### Problem Statement
Users report duplicate charges when clicking "Pay" multiple times quickly.
Need to implement idempotency to prevent duplicate payments.

### Constraints
- Must work with existing payment gateway (Stripe)
- Cannot change database schema (only new tables allowed)
- Response time < 500ms
```

#### Step 2: Define Expected Results

```markdown
## Expected Results

### Happy Path
| Input | Expected Output |
|-------|-----------------|
| First payment request | Payment processed, return success |
| Same idempotency key | Return cached result, no new charge |

### Edge Cases
| Input | Expected Output |
|-------|-----------------|
| Expired idempotency key (>24h) | Allow new payment |
| Different amount, same key | Return error |
| Database timeout | Retry with backoff |

### Error Cases
| Input | Expected Output |
|-------|-----------------|
| Invalid payment data | 400 Bad Request |
| Payment declined | Return decline reason |
| Gateway timeout | 503 Service Unavailable |
```

#### Step 3: Define Done

```markdown
## Definition of Done

### Functional
- [ ] Duplicate requests return cached result
- [ ] Different amounts with same key return error
- [ ] Keys expire after 24 hours

### Quality
- [ ] All tests pass (unit + integration)
- [ ] Response time < 500ms (p99)
- [ ] Code reviewed

### Documentation
- [ ] API documented
- [ ] Error codes documented
```

#### Step 4: Set Boundaries

```markdown
## Boundaries (Out of Scope)

### ❌ What We DON'T Do
- Refactoring existing payment code
- Changing Stripe integration
- Adding new payment methods
- Modifying checkout UI
- Database schema migration

### Rationale
- Existing code is stable, don't touch
- Stripe integration is tested and working
- New methods require business approval
- UI changes need design review
- Schema changes need DBA approval
```

### Requirements Quality Checklist

**Context Quality**
- [ ] Problem is clearly stated
- [ ] Existing state is documented
- [ ] Technology stack is specified
- [ ] Related files/modules identified
- [ ] Constraints are explicit

**Expected Results Quality**
- [ ] Happy path has concrete example
- [ ] At least 3 edge cases listed
- [ ] At least 2 error cases listed
- [ ] Input/output pairs are specific
- [ ] No vague descriptions ("should work")

**DoD Quality**
- [ ] Each criterion is testable
- [ ] No subjective criteria
- [ ] All stakeholder needs covered
- [ ] Quality requirements included
- [ ] Documentation requirements included

**Boundaries Quality**
- [ ] Explicitly states what's excluded
- [ ] Rationale provided for exclusions
- [ ] No ambiguous scope
- [ ] Prevents scope creep

---

## RULE #5: DEFINITION OF DONE (DoD)

**Goal:** Create explicit, testable completion criteria that auto-generate test cases.

**Core Principle:**
DoD must be so precise that tests can be auto-generated from it. If you can't write a test for a DoD criterion, it's too vague.

### DoD Categories

**Functional DoD** - What the code must DO
- [Action verb] + [specific behavior] + [conditions]
- User can [action] when [condition]
- System returns [specific output] for [specific input]

**Edge Cases DoD** - Boundary conditions to handle
- Handles [boundary value]: [expected behavior]
- Concurrent [operation] results in [expected outcome]
- Invalid [input type] returns [specific error]

**Quality DoD** - Non-functional requirements
- Performance: [metric] < [threshold]
- Test coverage: ≥ [percentage]%
- Method size: < [N] lines
- Security: [specific requirement]

**Documentation DoD** - Documentation requirements
- API endpoints documented
- Error codes explained
- Examples provided
- Changelog updated

### DoD → Test Transformation

```typescript
// DoD Item: "Concurrent addLike from same IP results in only 1 like"
//     ↓
// Test: "should result in only 1 like for concurrent requests from same IP"
//     ↓
it('should result in only 1 like for concurrent requests from same IP', async () => {
  const promises = Array(100).fill(null)
    .map(() => storage.addLike('video1', '192.168.1.1'));
  await Promise.all(promises);
  const count = await storage.getLikeCount('video1');
  expect(count).toBe(1);
});
```

### DoD Item Quality Checklist

**Ask**: "Can I write a test that passes/fails based on this criterion?"
- YES → Good DoD item
- NO → Rewrite to be specific

**Anti-Patterns**:
- ❌ "Like system works correctly" (vague)
- ❌ "Should work" (not testable)
- ✅ "addLike(videoId, ip) returns {added: false} if like exists from same IP" (specific, testable)

---

## RULE #6: CORNER CASES DOCUMENTATION

**Goal:** List all corner cases and boundary conditions BEFORE writing tests or code.

**Core Principle:**
Document every corner case explicitly before implementation. Undocumented cases = undiscovered bugs. AI cannot handle cases it doesn't know about.

### Corner Case Categories

#### 1. Input Validation

| Case | Input | Expected | Priority |
|------|-------|----------|----------|
| Null value | null | Error: "Value required" | High |
| Empty string | "" | Error: "Value cannot be empty" | High |
| Whitespace only | "   " | Error: "Value cannot be empty" | Medium |
| Too long | "a" × 10001 | Error: "Max 10000 chars" | Medium |
| Invalid type | 123 (number) | Error: "Must be string" | High |
| SQL injection | "'; DROP TABLE" | Escaped, safe | Critical |

#### 2. Boundary Values

| Case | Value | Expected | Notes |
|------|-------|----------|-------|
| Minimum | 0 | Accept or reject based on spec | |
| Maximum | MAX_INT | Accept or handle overflow | |
| Negative | -1 | Error or special handling | |
| Just under min | min - 1 | Reject | |
| Just over max | max + 1 | Reject | |
| Exact boundary | exactly min/max | Accept | |

#### 3. Concurrency

| Case | Scenario | Expected | Mitigation |
|------|----------|----------|------------|
| Double submit | User clicks twice fast | Only 1 processed | Idempotency key |
| Race condition | 100 simultaneous writes | Consistent state | Transaction lock |
| Deadlock | A waits B, B waits A | Timeout, retry | Lock ordering |
| Stale read | Read during write | Consistent data | Isolation level |

#### 4. External Dependencies

| Case | Scenario | Expected | Fallback |
|------|----------|----------|----------|
| Timeout | DB takes > 30s | Timeout error | Retry with backoff |
| Unavailable | Service down | Graceful degrade | Cache / queue |
| Rate limited | Too many requests | 429 error | Exponential backoff |
| Malformed response | Invalid JSON | Parse error | Default value |

#### 5. State Transitions

| Current State | Action | Expected | Invalid? |
|--------------|--------|----------|----------|
| PENDING | approve() | APPROVED | No |
| PENDING | reject() | REJECTED | No |
| APPROVED | approve() | Error | Yes |
| REJECTED | approve() | Error | Yes |
| COMPLETED | update() | Error | Yes |

### Common Corner Cases Checklist

**Numeric Values**
- [ ] Zero
- [ ] Negative
- [ ] Maximum integer
- [ ] Minimum integer
- [ ] Float precision issues
- [ ] Division by zero
- [ ] Overflow

**Strings**
- [ ] Empty string
- [ ] Null
- [ ] Whitespace only
- [ ] Very long string
- [ ] Unicode characters
- [ ] Special characters
- [ ] SQL injection patterns
- [ ] XSS patterns

**Collections**
- [ ] Empty array
- [ ] Single element
- [ ] Duplicate elements
- [ ] Very large collection
- [ ] Nested structures

**Concurrency**
- [ ] Simultaneous read
- [ ] Simultaneous write
- [ ] Read during write
- [ ] Multiple writers
- [ ] Deadlock scenarios
- [ ] Timeout scenarios

### Corner Cases → Tests

From corner case table:
```markdown
| Double submit | User clicks twice | Only 1 processed |
```

Becomes test:
```typescript
it('should process only once for double submit', async () => {
  const key = 'unique-key';
  const [result1, result2] = await Promise.all([
    process(data, key),
    process(data, key)
  ]);

  expect(result1.id).toBe(result2.id);  // Same result
});
```

---

## RULE #11: TASK BOUNDARIES

**Goal:** Prevent scope creep and wasted effort by explicitly stating what is NOT included.

**Core Principle:**
Explicitly define what is OUT OF SCOPE. Negative constraints are as important as positive requirements. Without boundaries, AI (and humans) will expand scope indefinitely.

### Boundary Categories

**Feature Boundaries** - What features are NOT included
```markdown
### ❌ Features Out of Scope
- [Feature A] - Planned for Phase 2
- [Feature B] - Requires design approval
- [Feature C] - Different team responsibility
- [Feature D] - Not in current sprint
```

**Technical Boundaries** - What technical work is NOT included
```markdown
### ❌ Technical Out of Scope
- Performance optimization (after MVP)
- Code refactoring (tech debt backlog)
- Infrastructure changes (ops team)
- Database migration (DBA approval needed)
- Test coverage improvements (QA sprint)
```

**Time Boundaries** - What won't be done in this iteration
```markdown
### ❌ Not in This Iteration
- Edge case X (handle in v1.1)
- Feature enhancement Y (next sprint)
- Bug fix Z (separate ticket)
```

### Boundary Template

```markdown
## Task: [Task Name]

### ✅ IN SCOPE (What We Do)
1. [Specific deliverable 1]
2. [Specific deliverable 2]
3. [Specific deliverable 3]

### ❌ OUT OF SCOPE (What We Don't Do)

#### Features Excluded
- [Feature] - Reason: [Why excluded]
- [Feature] - Reason: [Why excluded]

#### Technical Work Excluded
- [Tech work] - Reason: [Why excluded]

#### Deferred Items
- [Item] - Will be done: [When/ticket#]

### Rationale
[Brief explanation of why these boundaries exist]
```

### Common Scope Creep Triggers

| Trigger | AI Tendency | Boundary |
|---------|-------------|----------|
| "Make it work" | Add all features | "Only basic functionality" |
| "Handle errors" | Every possible error | "Only listed error cases" |
| "Optimize" | Premature optimization | "Basic implementation first" |
| "Clean code" | Massive refactoring | "Only new code quality" |
| "Good UX" | Animations, polish | "Functional UI only" |

### Benefits of Boundaries

**Without Boundaries**:
```
Task: "Implement likes"
AI Response:
├── Like functionality ✓
├── Unlike functionality (not asked)
├── Like animations (not asked)
├── Caching layer (not asked)
└── 3x scope, 3x time, 3x bugs
```

**With Boundaries**:
```
Task: "Implement likes"
Boundaries: "NOT: unlike, animations, caching"
AI Response:
├── Like functionality ✓
└── Done. Clean, focused, correct.
```

### Boundary Enforcement

**In Planning**:
- [ ] Scope defined (what we do)
- [ ] Boundaries defined (what we don't)
- [ ] Rationale for boundaries documented
- [ ] Stakeholders agree on boundaries

**In Implementation**:
```markdown
"Remember: We're NOT doing [X, Y, Z] in this task.
Focus only on [A, B, C]."
```

**In Review**:
- Is implementation within boundaries?
- Were any out-of-scope items added?
- Are boundaries still appropriate?

---

## MEMORY BANK FILE PATHS & STRUCTURE

**Critical Reference**: All Memory Bank files MUST be located in `memory-bank/` directory at project root.

### Core Files

- **`memory-bank/tasks.md`** - Active task (highest detail)
- **`memory-bank/activeContext.md`** - Current focus
- **`memory-bank/progress.md`** - Status tracking
- **`memory-bank/projectbrief.md`** - Project overview (high level)
- **`memory-bank/productContext.md`** - Product info
- **`memory-bank/systemPatterns.md`** - Patterns used
- **`memory-bank/techContext.md`** - Tech decisions
- **`memory-bank/style-guide.md`** - Code standards

### Generated Files

| Directory | Format | Purpose |
|-----------|--------|---------|
| `memory-bank/prd/` | `PRD-[task_id]-[description].md` | Product Requirements Docs |
| `memory-bank/tasks/` | `DEV-[task_id]-[description].md` | Task-specific docs |
| `memory-bank/creative/` | `creative-[task_id]-[feature].md` | Design decisions |
| `memory-bank/reflection/` | `reflection-[task_id].md` | Task learnings |
| `memory-bank/archive/` | `archive-[task_id].md` | Completed tasks |
| `memory-bank/qa/` | `qa-report-[task_id]-[phase].md` | QA reports |
| `memory-bank/reports/` | `debug-[task_id]-[feature].md` | Debug reports |

### Task ID Format

**Format**: `[PREFIX]-[4-digit-number]`
- **Prefix**: Usually `DEV`, `FIN`, `QA`, etc.
- **Examples**: `DEV-001`, `DEV-0053`, `FIN-0042`

**How to get current task ID**: Read `memory-bank/activeContext.md`

### Critical Rules for Memory Bank

**✅ DO**:
- Create all Memory Bank files in `memory-bank/` directory
- Use task ID in ALL report filenames
- Read `activeContext.md` to get current task ID
- Follow naming conventions exactly

**❌ DON'T**:
- Create Memory Bank files outside `memory-bank/` directory
- Create `documentation/tasks/` directory (should NOT exist)
- Create Markdown files in application source directories (except README.md)
- Omit task ID from report filenames

### Context Hierarchy

```
                    DETAIL LEVEL
SCOPE               Low ◀─────────────▶ High
────────────────────────────────────────────
Full Project        ████░░░░░░░░░░░░░░░░░
                    Technologies, purpose

Module/Folder       ████████░░░░░░░░░░░░░
                    Interfaces, key functions

Specific File       ████████████████░░░░░
                    Implementation details

Single Method       ████████████████████
                    Full code, edge cases
```

### Context Loading Strategy

**When Starting New Task**:
1. projectbrief.md → Understand project
2. activeContext.md → Current state
3. tasks.md → Task details
4. [relevant rules] → If needed

**When Deep in Implementation**:
1. tasks.md → Task focus
2. activeContext.md → Working files
3. [specific module docs if saved]

---

## INITIALIZATION PHASE VERIFICATION CHECKLIST

Before starting implementation phase (/mb-do):

```
REQUIREMENTS GATHERING
□ Context is complete and specific
□ Expected results have concrete examples
□ DoD is testable and explicit
□ Boundaries clearly exclude scope creep
□ Complexity is assessed as solvable
□ All stakeholders' needs are captured
□ No ambiguous or vague requirements

DEFINITION OF DONE
□ Each DoD item is specific and testable
□ Happy path tests defined
□ Edge case tests defined
□ Error case tests defined
□ Quality requirements measurable

CORNER CASES
□ Input validation cases documented
□ Boundary values identified
□ Concurrency scenarios listed
□ External dependency failures covered
□ Invalid state transitions documented
□ Security attack vectors considered
□ Each corner case has expected behavior

TASK BOUNDARIES
□ In-scope items clearly listed
□ Out-of-scope items explicitly stated
□ Reasons for exclusions documented
□ Deferred items tracked (ticket numbers)
□ Boundaries are specific, not vague
□ All stakeholders agree on boundaries

MEMORY BANK STRUCTURE
□ Current task ID identified in activeContext.md
□ Appropriate Memory Bank files created/updated
□ File paths follow naming conventions
□ All necessary context is documented

READY FOR IMPLEMENTATION
□ All 5 verification sections above complete
□ Ready to proceed to /mb-do phase
```

---

*Foundation laid. Ready to build with confidence.*
