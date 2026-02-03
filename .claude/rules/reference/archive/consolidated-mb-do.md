# Consolidated Rules for /mb-do (Implementation Phase)

This consolidated rules file combines all essential rules for the **BUILD/DO** phase of the Memory Bank workflow. It integrates critical safety rules with 8 foundational AI Quality Rules to guide implementation.

**Content Structure**: Git Safety + Rules #1, #2, #3, #8, #13, #14, #15
**Purpose**: Guide test-driven, iterative implementation with proper safety guardrails
**Size Reduction**: ~750 lines (28% reduction from original 900+ source lines)

---

## 🚨 CRITICAL: GIT PUSH RESTRICTION

**Priority**: MANDATORY - Non-negotiable
**Version**: 2.0.0
**Status**: ✅ ACTIVE - Critical enforcement rule

### The Rule: NEVER Push Without Explicit User Request

**NEVER execute `git push` unless the user explicitly requests it.**

### Why This Rule Exists

1. Give user full control over when code is pushed to remote
2. Allow user to review commits before they become public
3. Prevent accidental pushes that might break CI/CD pipelines
4. Allow user to amend, rebase, or squash commits before pushing
5. Prevent pushing sensitive information accidentally

### What IS Allowed (Without Permission)

✅ You MAY execute these git commands:
- `git status` - Check repository status
- `git diff` - View changes
- `git log` - View commit history
- `git add` - Stage files
- `git commit` - Commit changes locally
- `git branch` - Manage branches
- `git checkout` / `git switch` - Switch branches
- `git reset` - Unstage or undo commits locally
- `git stash` - Temporarily save changes

### What IS NOT Allowed (Without Permission)

❌ You MUST NOT execute these without explicit user request:
- `git push` - Push to remote
- `git push origin <branch>` - Push specific branch
- `git push -f` / `git push --force` - Force push
- `git push --all` - Push all branches
- Any command that transfers commits to remote repository

### Valid User Requests for Push

User MUST explicitly say one of these (or similar):
- "push the changes"
- "git push"
- "push to remote"
- "commit and push"
- "deploy the changes" (in git context)

### Invalid Implicit Requests

These do NOT count as explicit push requests:
- "commit the changes" → Only commit, DON'T push
- "save the changes" → Only commit, DON'T push
- "finish the task" → Only commit, DON'T push
- "done" → Only commit, DON'T push

### Examples

✅ **CORRECT: User asks only to commit**
```
User: "Commit the changes"
You should:
1. git add -A
2. git commit -m "..."
3. STOP HERE - Do not push
```

✅ **CORRECT: User explicitly asks to push**
```
User: "Commit and push"
You should:
1. git add -A
2. git commit -m "..."
3. git push origin <branch> ← OK, user explicitly requested
```

❌ **WRONG: Auto-pushing without permission**
```
User: "Commit the changes"
You should NOT:
1. git add -A
2. git commit -m "..."
3. ~~git push origin <branch>~~ ← WRONG! User didn't ask for push
```

### Enforcement

This rule is **MANDATORY** and **NON-NEGOTIABLE**.

Violation could result in:
- Unwanted code in remote repository
- Broken CI/CD pipelines
- Conflicts with team members' work
- Loss of ability to rewrite commit history

---

## RULE #1: STUBBING / DECOMPOSITION

> **Goal:** Reduce cognitive load and improve code quality by 35-40% through task decomposition.

**Principle**: Break complex tasks into small stubs (max 50 lines each) before implementing.

AI generates higher quality code when focused on one small unit at a time.

### How to Apply

**Step 1: Identify Complex Task**

```typescript
// ❌ PROBLEM: One massive function
async function migrateDatabase() {
  // 500+ lines of code doing multiple things:
  // - Connect to databases
  // - Create schema
  // - Migrate data
  // - Validate results
  // - Handle errors
  // - Log progress
}
```

**Step 2: Decompose into Stubs**

```typescript
// ✅ SOLUTION: Decomposed into focused stubs
async function migrateDatabase() {
  await initSourceConnection();
  await initTargetConnection();
  await createTargetSchema();
  await migrateUsers();
  await migrateOrders();
  await migrateProducts();
  await validateMigration();
  await generateReport();
}

// Each stub: single responsibility, max 50 lines
async function initSourceConnection() { /* TODO */ }
async function initTargetConnection() { /* TODO */ }
async function createTargetSchema() { /* TODO */ }
async function migrateUsers() { /* TODO */ }
async function migrateOrders() { /* TODO */ }
async function migrateProducts() { /* TODO */ }
async function validateMigration() { /* TODO */ }
async function generateReport() { /* TODO */ }
```

**Step 3: Implement One Stub at a Time**

```typescript
// Focus AI on ONE stub
async function migrateUsers() {
  const batchSize = 1000;
  let offset = 0;
  let hasMore = true;

  while (hasMore) {
    const users = await source.query(
      'SELECT * FROM users LIMIT $1 OFFSET $2',
      [batchSize, offset]
    );

    if (users.length === 0) {
      hasMore = false;
      continue;
    }

    await target.batchInsert('users', users);
    offset += batchSize;
    console.log(`Migrated ${offset} users`);
  }
}
// ~25 lines, single responsibility, clear input/output
```

### Quality Impact

```
Without Decomposition:
├── 500-line function
├── Multiple concerns mixed
├── Hard to test
├── AI loses focus
└── Quality: 60%

With Decomposition:
├── 10 × 50-line stubs
├── Single concern each
├── Easy to test
├── AI maintains focus
└── Quality: 95% (+35%)
```

### Verification Checklist

```
□ All stubs identified and named
□ Each stub has single responsibility
□ Each stub < 50 lines (estimated)
□ Each stub can be tested independently
□ Orchestrating function is clear and simple
□ Dependencies between stubs are minimal
□ Stub names are self-documenting
```

---

## RULE #2: TEST-DRIVEN DEVELOPMENT (TDD)

> **Goal:** Use tests as hallucination filters. Tests automatically reject non-working AI-generated code.

**Principle**: Write tests BEFORE implementation, not after.

Tests define "what success looks like" in executable form. AI writes code that must pass these tests.

### How to Apply

**Step 1: Define What Success Looks Like**

```markdown
## Method: addLike(videoId, ipAddress)

### Success Criteria
- Adds like to database
- Increments video like count
- Returns new count
- Does NOT add duplicate from same IP
- Handles database errors gracefully
```

**Step 2: Write Tests FIRST**

```typescript
describe('addLike', () => {
  // HAPPY PATH
  it('should add like from new IP', async () => {
    const result = await storage.addLike('video1', '192.168.1.1');
    expect(result.added).toBe(true);
    expect(result.count).toBe(1);
  });

  // EDGE CASE: Duplicate
  it('should not add duplicate from same IP', async () => {
    await storage.addLike('video1', '192.168.1.1');
    const result = await storage.addLike('video1', '192.168.1.1');
    expect(result.added).toBe(false);
    expect(result.count).toBe(1); // Still 1, not 2
  });

  // EDGE CASE: Concurrent
  it('should handle 100 concurrent likes from same IP', async () => {
    const promises = Array(100).fill(null)
      .map(() => storage.addLike('video1', '192.168.1.1'));
    await Promise.all(promises);

    const count = await storage.getLikeCount('video1');
    expect(count).toBe(1); // Only 1, not 100
  });

  // ERROR CASE: Invalid input
  it('should reject null IP address', async () => {
    await expect(storage.addLike('video1', null))
      .rejects.toThrow('IP address required');
  });

  // ERROR CASE: Database failure
  it('should handle database timeout gracefully', async () => {
    jest.spyOn(db, 'query').mockRejectedValue(new Error('timeout'));

    await expect(storage.addLike('video1', '192.168.1.1'))
      .rejects.toThrow('Database unavailable');
  });
});
```

**Step 3: Implement to Pass Tests**

```typescript
// NOW implement - AI has clear success criteria
async function addLike(videoId: string, ipAddress: string): Promise<LikeResult> {
  // Validation (satisfies error test)
  if (!ipAddress) {
    throw new Error('IP address required');
  }

  try {
    return await db.transaction(async (tx) => {
      // Check duplicate (satisfies edge case)
      const existing = await tx.query(
        'SELECT id FROM likes WHERE video_id = $1 AND ip_address = $2',
        [videoId, ipAddress]
      );

      if (existing.rows.length > 0) {
        const count = await getCount(tx, videoId);
        return { added: false, count };
      }

      // Insert with constraint (satisfies concurrent test)
      await tx.query(
        `INSERT INTO likes (video_id, ip_address)
         VALUES ($1, $2)
         ON CONFLICT (video_id, ip_address) DO NOTHING`,
        [videoId, ipAddress]
      );

      const count = await getCount(tx, videoId);
      return { added: true, count };
    });
  } catch (error) {
    // Handle DB errors (satisfies error test)
    if (error.message.includes('timeout')) {
      throw new Error('Database unavailable');
    }
    throw error;
  }
}
```

### Test Case Categories

**Happy Path (Required)**
Basic successful operation with valid inputs.

**Edge Cases (Required)**
Boundary conditions and unusual but valid inputs.

**Error Cases (Required)**
Invalid inputs and failure scenarios.

### Quality Impact

```
Without TDD:
├── Code written first
├── Tests written after (or never)
├── AI hallucinations undetected
├── Edge cases missed
└── Bug rate: High

With TDD:
├── Tests define success
├── Code must pass tests
├── Hallucinations filtered out
├── Edge cases covered
└── Bug rate: -40-50%
```

### Verification Checklist

Before implementation is complete:
```
□ All happy path tests pass
□ All edge case tests pass
□ All error case tests pass
□ Test coverage ≥ 80%
□ No skipped tests
□ Tests are independent (no shared state)
□ Tests are deterministic (no flaky tests)
```

---

## RULE #3: METHOD SIZE LIMITS

> **Goal:** Prevent quality degradation by keeping methods within AI's effective context window.

**Principle**: Maximum 50 lines per method. Maximum 7-9 objects in working memory.

AI (like humans) loses focus when tracking too many things. Small methods = high quality.

### The 7±2 Rule (Miller's Law)

Human (and AI) working memory can hold 7±2 items simultaneously.

**Quality vs Object Count**

```
Objects    Quality    Status
───────────────────────────────────
  1-5      100%       ✅ Ideal
  6-7       95%       ✅ Good
  8-9       85%       ⚠️ Acceptable limit
 10-12      70%       ❌ Refactor needed
 13-15      50%       ❌ High bug risk
  15+       30%       ❌ Certain problems
```

### What Counts as an Object

| Type | Example | Count |
|------|---------|-------|
| Parameters | `function(a, b, c)` | 3 objects |
| Local variables | `let x, y, z` | 3 objects |
| Properties accessed | `user.name, user.email` | 2 objects |
| Return values | `return { data, error }` | 2 objects |
| Loop variables | `for (let i...)` | 1 object |
| Conditions | `if (a && b)` | 2 objects |

### How to Stay Within Limits

**Strategy 1: Extract to Helper Functions**

```typescript
// ❌ BAD: 12 objects
async function createUser(name, email, age, country, city, street, zip, phone) {
  let validation, user, address, result;  // 12 total!
}

// ✅ GOOD: 6 objects each
async function createUser(userData: UserData) {
  const validation = validateUser(userData);  // 1, 2
  const address = createAddress(userData);    // 3
  const user = await saveUser(userData, address);  // 4, 5
  return formatResult(user);  // 6
}
```

**Strategy 2: Use Config Objects**

```typescript
// ❌ BAD: 8 parameters
function sendEmail(to, from, subject, body, cc, bcc, attachments, priority) {}

// ✅ GOOD: 1 config object
function sendEmail(config: EmailConfig) {
  const { to, subject, body } = config;  // 4 objects
}
```

**Strategy 3: Early Returns**

```typescript
// ❌ BAD: Nested conditions add mental load
function process(data) {
  if (data) {
    if (data.valid) {
      if (data.items) {
        // Deep nesting
      }
    }
  }
}

// ✅ GOOD: Early returns reduce active objects
function process(data) {
  if (!data) return null;
  if (!data.valid) throw new Error('Invalid');
  if (!data.items) return [];
  // Now only valid case, fewer objects to track
}
```

### Size Limits Reference

| Metric | Limit | Why |
|--------|-------|-----|
| **Lines per method** | ≤50 | Fits in context window |
| **Objects in scope** | 7-9 | Miller's Law (working memory) |
| **Parameters** | ≤5 | Reduces call complexity |
| **Nesting depth** | ≤3 | Maintains readability |

### Verification Checklist

Before considering method complete:
```
□ Method ≤ 50 lines
□ ≤ 7-9 objects in scope
□ ≤ 5 parameters
□ ≤ 3 nesting levels
□ Single responsibility
□ Clear method name
□ Testable in isolation
□ No "and" in method name
```

---

## RULE #8: ITERATIVE DEVELOPMENT CYCLE

> **Goal:** Maximize quality by implementing, testing, and reviewing one method at a time.

**Principle**: For each stub: Write tests → Implement → Run tests → Review → Next stub.

Breaking the cycle or batching steps reduces quality. Each step must complete before the next.

### The Cycle

```
┌─────────────────────────────────────────────────────────────┐
│                  ITERATIVE DEVELOPMENT CYCLE                │
├─────────────────────────────────────────────────────────────┤
│                                                             │
│   ┌─────────┐    ┌─────────┐    ┌─────────┐               │
│   │  WRITE  │───▶│IMPLEMENT│───▶│  TEST   │               │
│   │  TESTS  │    │  CODE   │    │  (RUN)  │               │
│   └─────────┘    └─────────┘    └────┬────┘               │
│        ▲                             │                     │
│        │                             ▼                     │
│        │                      ┌─────────────┐              │
│        │                      │   GREEN?    │              │
│        │                      └──────┬──────┘              │
│        │                     YES     │    NO               │
│        │                    ┌────────┴────────┐            │
│        │                    ▼                 ▼            │
│        │              ┌─────────┐       ┌─────────┐        │
│        │              │ REVIEW  │       │   FIX   │        │
│        │              └────┬────┘       └────┬────┘        │
│        │                   │                 │             │
│        │                   ▼                 │             │
│        │              ┌─────────┐            │             │
│        └──────────────│  NEXT   │◀───────────┘             │
│                       │ METHOD  │                          │
│                       └─────────┘                          │
│                                                             │
└─────────────────────────────────────────────────────────────┘
```

### Quality Comparison

| Approach | Context Window | Quality | Debug Time |
|----------|---------------|---------|------------|
| All at once | Cluttered | 60% | High |
| Batch 3-4 methods | Moderate | 75% | Medium |
| **One at a time** | **Clean** | **95%** | **Low** |

### Why One at a Time?

```
Clean Context Window:
├── AI focuses on ONE thing
├── No confusion between methods
├── Full attention to edge cases
└── Better error messages

Isolated Errors:
├── Bug in addItem? Only affects addItem
├── Easy to pinpoint issues
├── Simple to fix and re-test
└── No cascading failures

Human Checkpoints:
├── Review after each method
├── Catch issues early
├── Course-correct if needed
└── Maintain control
```

### Practical Workflow for 5-Method Class

```
SKELETON (Chat 0): Create class with 5 stubs

METHOD 1 - addItem:
├── Chat 1: Write tests
├── Chat 2: Implement
└── Chat 3: Review

METHOD 2 - getItem:
├── Chat 4: Write tests
├── Chat 5: Implement
└── Chat 6: Review

METHOD 3 - updateItem:
├── Chat 7: Write tests
├── Chat 8: Implement
└── Chat 9: Review

METHOD 4 - deleteItem:
├── Chat 10: Write tests
├── Chat 11: Implement
└── Chat 12: Review

METHOD 5 - listItems:
├── Chat 13: Write tests
├── Chat 14: Implement
└── Chat 15: Review

INTEGRATION (Chat 16):
└── Integration tests & final review
```

### Verification Checklist

For each method iteration:
```
□ Tests written first
□ Tests run (initially failing)
□ Implementation written
□ Tests pass (all green)
□ Code reviewed
□ < 50 lines confirmed
□ Edge cases covered
□ Ready for next method
```

---

## RULE #13: TRANSACTION ISOLATION

> **Goal:** Prevent data corruption by explicitly specifying transaction isolation levels and testing for race conditions.

**Principle**: Always explicitly specify transaction isolation level. Never assume defaults. Test for race conditions.

Implicit defaults cause subtle bugs. Explicit specification ensures correct behavior.

### Isolation Levels Reference

| Level | Dirty Read | Non-Repeatable | Phantom | Performance |
|-------|------------|----------------|---------|-------------|
| READ UNCOMMITTED | ✓ | ✓ | ✓ | Fastest |
| READ COMMITTED | ✗ | ✓ | ✓ | Fast |
| REPEATABLE READ | ✗ | ✗ | ✓ | Medium |
| SERIALIZABLE | ✗ | ✗ | ✗ | Slowest |

### When to Use Each

```markdown
READ COMMITTED (Default)
├── Most CRUD operations
├── Read-only queries
└── When eventual consistency OK

REPEATABLE READ
├── Reports that read same data twice
├── Calculations based on multiple reads
└── When consistency within transaction needed

SERIALIZABLE
├── Financial transactions
├── Inventory management
├── Like/vote deduplication
└── Any "check-then-insert" pattern
```

### How to Apply

**Step 1: Explicit Isolation in Code**

```typescript
// ❌ BAD: Implicit isolation (uses database default)
async function addLike(videoId: string, ip: string) {
  return await db.transaction(async (tx) => {
    // What isolation level? Who knows!
    const existing = await tx.query(/*...*/);
    // Race condition possible!
    if (!existing) {
      await tx.query('INSERT...');
    }
  });
}

// ✅ GOOD: Explicit isolation
async function addLike(videoId: string, ip: string) {
  return await db.transaction(async (tx) => {
    // Explicit: I know what I'm doing
    await tx.query('SET TRANSACTION ISOLATION LEVEL SERIALIZABLE');

    const existing = await tx.query(
      'SELECT id FROM likes WHERE video_id = $1 AND ip = $2',
      [videoId, ip]
    );

    if (existing.rows.length > 0) {
      return { added: false };
    }

    await tx.query(
      'INSERT INTO likes (video_id, ip) VALUES ($1, $2)',
      [videoId, ip]
    );

    return { added: true };
  });
}
```

**Step 2: Add Database Constraints**

```sql
-- Additional protection: unique constraint
ALTER TABLE likes
ADD CONSTRAINT unique_like_per_ip
UNIQUE (video_id, ip_address);
```

**Step 3: Concurrent Test (MANDATORY)**

```typescript
// MANDATORY: Test with 100 concurrent operations
describe('addLike concurrency', () => {
  it('should handle 100 simultaneous likes from same IP', async () => {
    const videoId = 'test-video';
    const ipAddress = '192.168.1.1';

    // Fire 100 concurrent requests
    const promises = Array(100).fill(null)
      .map(() => storage.addLike(videoId, ipAddress));

    // Wait for all to complete
    const results = await Promise.all(promises);

    // Count how many actually added
    const addedCount = results.filter(r => r.added).length;

    // Verify: Only 1 should succeed
    expect(addedCount).toBe(1);

    // Verify database state
    const count = await storage.getLikeCount(videoId);
    expect(count).toBe(1);
  });

  it('should handle concurrent likes from different IPs', async () => {
    const videoId = 'test-video';

    // 100 different IPs
    const promises = Array(100).fill(null)
      .map((_, i) => storage.addLike(videoId, `192.168.1.${i}`));

    await Promise.all(promises);

    // All 100 should succeed
    const count = await storage.getLikeCount(videoId);
    expect(count).toBe(100);
  });
});
```

### Common Race Condition Patterns

**Pattern 1: Check-Then-Insert**
```typescript
// ❌ RACE CONDITION
// Request A: Check → Not exists → INSERT
// Request B: Check → Not exists → INSERT (both insert!)

// ✅ SAFE: Use SERIALIZABLE
await tx.query('SET TRANSACTION ISOLATION LEVEL SERIALIZABLE');
```

**Pattern 2: Read-Modify-Write**
```typescript
// ❌ RACE CONDITION
// Request A: Read balance=100 → Update to 90
// Request B: Read balance=100 → Update to 80 (overwrites A!)

// ✅ SAFE: Use SELECT FOR UPDATE
const result = await tx.query(
  'SELECT balance FROM accounts WHERE id = $1 FOR UPDATE',
  [accountId]
);
```

**Pattern 3: Counter Increment**
```typescript
// ❌ RACE CONDITION
// Request A: Read count=5 → Write count=6
// Request B: Read count=5 → Write count=6 (lost increment!)

// ✅ SAFE: Atomic increment
await tx.query(
  'UPDATE counters SET value = value + 1 WHERE id = $1',
  [counterId]
);
```

### Isolation Decision Guide

```
OPERATION TYPE                    → ISOLATION LEVEL
──────────────────────────────────────────────────────
Simple read                       → READ COMMITTED
Multiple reads, same data         → REPEATABLE READ
Check-then-insert                 → SERIALIZABLE + CONSTRAINT
Financial transaction             → SERIALIZABLE
Inventory update                  → SERIALIZABLE + FOR UPDATE
Read-modify-write                 → SELECT FOR UPDATE
Counter increment                 → Atomic UPDATE
```

### Verification Checklist

```
□ Isolation level explicitly set in code
□ Unique constraints added where needed
□ Race condition patterns identified
□ SELECT FOR UPDATE used appropriately
□ Concurrent test written (100+ requests)
□ Test verifies final state is correct
□ Timeout handling implemented
□ Transaction scope is minimal
```

---

## RULE #14: MEMORY BANK STRUCTURE

> **Goal:** Optimize context usage by organizing information hierarchically with appropriate detail levels.

**Principle**: Organize context hierarchically: less detail for broader scope, more detail for narrower focus.

Don't dump everything into context. Structure information so AI loads only what it needs.

### Hierarchy Principle

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

### Memory Bank File Structure

```
memory-bank/
├── tasks.md              # Active task (highest detail)
├── activeContext.md      # Current focus
├── progress.md           # Status tracking
├── projectbrief.md       # Project overview (low detail)
├── productContext.md     # Product info
├── systemPatterns.md     # Patterns used
├── techContext.md        # Tech decisions
├── style-guide.md        # Code standards
├── creative/             # Design decisions
│   └── creative-[name].md
├── reflection/           # Review learnings
│   └── reflection-[id].md
└── archive/              # Completed tasks
    └── archive-[id].md
```

### Detail by File Type

| File | Scope | Detail Level | Token Target |
|------|-------|--------------|--------------|
| projectbrief.md | Entire project | Low | 500-1000 |
| productContext.md | Product features | Low-Medium | 500-800 |
| systemPatterns.md | Architecture | Medium | 800-1200 |
| techContext.md | Technology | Medium | 800-1200 |
| activeContext.md | Current focus | Medium-High | 500-1000 |
| tasks.md | Active task | High | 1000-2000 |
| creative/*.md | Design decision | High | 1000-1500 |

### Context Loading Strategy

**When Starting New Task**
```
LOAD ORDER:
1. projectbrief.md      # Understand project
2. activeContext.md     # Current state
3. tasks.md             # Task details
4. [relevant rules]     # If needed
```

**When Deep in Implementation**
```
LOAD ORDER:
1. tasks.md             # Task focus
2. activeContext.md     # Working files
3. [specific module docs if saved]
```

### Token Budgeting

```
CONTEXT BUDGET: 15,000-30,000 tokens

Project Context:     3,000 tokens
├── projectbrief.md    500
├── productContext.md  500
├── systemPatterns.md  1,000
└── techContext.md     1,000

Task Context:        5,000 tokens
├── tasks.md           2,000
├── activeContext.md   1,000
└── creative/*.md      2,000

Rules:               5,000 tokens
├── _principles.mdc    1,000
├── Category summaries 2,000
└── Specific rules     2,000

Code:                7,000 tokens
└── Relevant files

TOTAL:              ~20,000 tokens
```

### Verification Checklist

```
□ projectbrief.md is current
□ activeContext.md reflects NOW
□ tasks.md has active task only
□ No stale information
□ Files are appropriately sized
□ Hierarchy is maintained
□ Summaries exist for key modules
□ Archive is organized
```

---

## RULE #15: PROMPT ENGINEERING

> **Goal:** Maximize AI output quality through structured, focused prompts with clear context and expectations.

**Principle**: Structure prompts with: Context → Task → Expected Results → DoD → Boundaries.

Good prompts produce good results. Bad prompts produce hallucinations and waste.

### Prompt Structure

```markdown
## 1. CONTEXT
[Brief background - what AI needs to know]
[Reference Memory Bank if detailed context exists]

## 2. TASK
[Specific, focused action to perform]
[One thing at a time]

## 3. EXPECTED RESULTS
[Concrete examples with inputs/outputs]
[Happy path and edge cases]

## 4. DEFINITION OF DONE
[Explicit, testable success criteria]
[Checklist format]

## 5. BOUNDARIES
[What NOT to do]
[Scope limitations]
```

### Implementation Prompt Template

```markdown
## Context
Module: User authentication
File: /src/auth/validate.ts
Related: See Memory Bank auth-overview

## Task
Implement validateToken() method.

## Expected Results
- Valid token → returns {valid: true, userId: "123"}
- Expired token → throws TokenExpiredError
- Invalid token → throws InvalidTokenError

## Definition of Done
- [ ] All 3 test cases pass
- [ ] Method < 30 lines
- [ ] Errors have clear messages

## Boundaries
- NOT implementing token refresh (separate task)
- NOT changing JWT library
- NOT adding new dependencies
```

### Prompt Quality Checklist

Before sending a prompt:
```
□ Is the task specific and focused?
□ Is context minimal but sufficient?
□ Are expected results concrete (examples)?
□ Is DoD testable and explicit?
□ Are boundaries clear (what NOT to do)?
□ Is prompt < 500 words?
□ Would I know if response is correct?
```

### Good vs Bad Prompts

**❌ BAD: Vague**
```
"Make the authentication better"
Problems:
- What does "better" mean?
- Which part of auth?
- No success criteria
```

**✅ GOOD: Specific**
```
"Implement validateToken() that:
- Returns userId for valid tokens
- Throws TokenExpiredError for expired
- Throws InvalidTokenError for malformed

Tests must pass. Method < 30 lines."
```

---

## Quick Reference Checklist

**Before Starting Implementation**
```
□ Task is decomposed into stubs (Rule #1)
□ Tests written first (Rule #2)
□ Each method ≤ 50 lines, ≤9 objects (Rule #3)
□ One method at a time iteratively (Rule #8)
□ Transaction isolation explicitly set (Rule #13)
□ Memory Bank structure is hierarchical (Rule #14)
□ Prompts follow 5-part structure (Rule #15)
□ Git push never without user request (GIT RULE)
```

**During Implementation**
```
□ Following iterative cycle (test→implement→test→review)
□ Each stub gets own focused implementation
□ All tests passing before moving on
□ Isolation levels explicitly specified
□ Concurrent tests included for shared data
□ Context organized in Memory Bank
```

**Before Completing Implementation**
```
□ All tests pass (green)
□ Code reviewed one method at a time
□ Size limits maintained
□ No uncommitted changes
□ Ready for merge (NOT pushed without user request)
```

---

**Version**: 2.0.0 (Consolidated from 8 source rules)
**Last Updated**: 2026-01-28
**Purpose**: Guide implementation phase (BUILD/DO) with safety and quality rules
**Size Reduction**: 750 lines (~28% from original 900+ lines)
