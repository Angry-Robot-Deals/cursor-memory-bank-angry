# AI Quality Rules (15 Rules, 5 Pillars)

Reduce bugs 40-50%, improve quality 30-50%.

---

## Pillar 1: DECOMPOSITION

### Rule #1: Stubbing
Break complex tasks into max 50-line stubs before implementing.
```
❌ One 500-line function
✅ 10 × 50-line focused functions
```

### Rule #3: Method Size
- Max 50 lines per method
- Max 7-9 objects in working memory
- One responsibility per function

### Rule #9: Cognitive Load
Keep within 7±2 objects. Use:
- Config objects instead of many parameters
- Early returns to reduce nesting
- Helper functions to extract complexity

---

## Pillar 2: TEST-FIRST

### Rule #2: TDD
Write tests BEFORE implementation.
```
1. Define success criteria
2. Write tests (they fail)
3. Implement (tests pass)
4. Refactor (tests still pass)
```

### Rule #5: Definition of Done
Make DoD testable:
```
❌ "Like system works correctly"
✅ "addLike(videoId, ip) returns {added: false} if like exists"
```

### Rule #6: Corner Cases
Document before coding:
- Input validation (null, empty, too long)
- Boundary values (0, max, negative)
- Concurrency (race conditions)
- External failures (timeout, unavailable)

---

## Pillar 3: ARCHITECTURE-FIRST

### Rule #7: Skeleton First
Create structure before implementation:
```
1. Create class/module skeleton
2. Add method stubs with signatures
3. Review architecture
4. Implement one method at a time
```

### Rule #8: Iterative Development
For each stub:
```
Write tests → Implement → Run tests → Review → Next
```
Never batch. One method at a time.

---

## Pillar 4: FOCUSED WORK

### Rule #10: Focused Review
Review one method at a time. Broad context = scattered results.

### Rule #11: Task Boundaries
Explicitly state what's OUT of scope:
```markdown
### ❌ NOT in this task:
- Refactoring existing code
- Adding new dependencies
- UI changes
```

### Rule #12: Complexity Check
Before starting, verify task is solvable. If too complex, decompose.

---

## Pillar 5: CONTEXT MANAGEMENT

### Rule #4: Requirements Gathering
Gather ALL requirements BEFORE coding:
- Context (system, module, tech)
- Expected results (happy path, edge cases)
- Definition of Done
- Boundaries

### Rule #13: Transaction Isolation
Always explicit:
```typescript
await tx.query('SET TRANSACTION ISOLATION LEVEL SERIALIZABLE');
```
Test with 100 concurrent requests.

### Rule #14: Memory Bank Structure
Hierarchy by detail level:
- Project brief → Low detail
- Module docs → Medium detail
- Active task → High detail

### Rule #15: Prompt Engineering
Structure: Context → Task → Expected Results → DoD → Boundaries

---

## Quick Reference

| # | Rule | One-liner |
|---|------|-----------|
| 1 | Stubbing | Max 50-line stubs |
| 2 | TDD | Tests before code |
| 3 | Method Size | Max 50 lines, 7-9 objects |
| 4 | Requirements | Context before coding |
| 5 | DoD | Testable criteria |
| 6 | Corner Cases | List boundaries first |
| 7 | Skeleton | Architecture before code |
| 8 | Iterative | One method at a time |
| 9 | Cognitive | 7±2 objects max |
| 10 | Review | One method only |
| 11 | Boundaries | State out of scope |
| 12 | Complexity | Verify solvable |
| 13 | Transaction | Explicit isolation |
| 14 | MB Structure | Hierarchical detail |
| 15 | Prompts | Structured format |

---

## Checkpoint

Before proceeding:
```
□ Task decomposed into small units?
□ Tests/DoD defined?
□ Architecture approved?
□ Focused on one thing?
□ Right context loaded?
```
