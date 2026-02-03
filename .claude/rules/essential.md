# Essential Rules for Claude Code

All critical rules in one file. MANDATORY for all operations.

---

## 1. MCP Servers (MANDATORY)

### sys8 - System Operations
**ALWAYS use for:**
- `get_current_datetime` - ALL timestamps
- `get_os_version` - Platform info
- `calculate_math_expression` - Safe math
- `random_string` - Secure random
- `hash_string` - Hashing

**NEVER:** Use `Date()`, hardcode timestamps, use Node.js `os` directly.

### context7 - Library Docs
**ALWAYS use for:**
- `resolve-library-id` - Get library ID first
- `get-library-docs` - Then get docs

**NEVER:** Rely on training data for library APIs. Always verify.

---

## 2. Git Push Restriction (MANDATORY)

**NEVER push without explicit user request.**

### Allowed (no permission needed)
✅ `git add`, `git commit`, `git status`, `git diff`, `git log`, `git branch`, `git checkout`, `git stash`

### Forbidden (need explicit request)
❌ `git push`, `git push origin`, `git push -f`, `git push --force`

### Valid push requests
- "push the changes"
- "git push"
- "commit and push"
- "push to remote"

### Invalid (do NOT push)
- "commit the changes" → only commit
- "save the changes" → only commit
- "finish the task" → only commit

---

## 3. Memory Bank Paths (MANDATORY)

**All files in `memory-bank/` directory.**

### Core Files
| File | Purpose |
|------|---------|
| `tasks.md` | Active task (source of truth) |
| `activeContext.md` | Current task ID |
| `progress.md` | Status tracking |
| `backlog.md` | Pending queue |
| `backlog-archive.md` | Completed queue items |

### Generated Files
| Pattern | Location |
|---------|----------|
| PRD | `prd/PRD-[id]-[desc].md` |
| Creative | `creative/creative-[id]-[name].md` |
| Reflection | `reflection/reflection-[id].md` |
| Archive | `archive/archive-[id].md` |
| Tasks docs | `tasks/DEV-[id]-[desc].md` |
| QA reports | `qa/qa-report-[id]-[phase].md` |
| Debug | `reports/debug-[id]-[feature].md` |

### Task ID Format
- Format: `[PREFIX]-[4-digit-number]`
- Example: `DEV-0053`, `FIN-0001`
- Get from: `memory-bank/activeContext.md`
- Auto-generated if not provided

### Prohibited
❌ Creating files outside `memory-bank/`
❌ Creating `documentation/tasks/` directory
❌ Creating MD files in source directories (except README.md)

---

## 4. Task Context (MANDATORY)

- `activeContext.md` MUST identify current task
- Format: `**Current Task:** [TASK-ID] - [Title]`
- Archive only current task (not all completed)
- Update on task start, complete, and archive

---

## 5. Backlog Management

### File Locations
- Active: `memory-bank/backlog.md` (pending, in_progress)
- Archive: `memory-bank/backlog-archive.md` (completed, cancelled)

### Item Format
```markdown
### BACKLOG-XXXX: [Title]
| Field | Value |
|-------|-------|
| **Status** | pending |
| **Priority** | high/medium/low |
| **Complexity** | Level 1-4 |
| **Created** | YYYY-MM-DD |
```

### Statuses
- `pending` → `in_progress` → `completed`/`cancelled`

---

## 6. Documentation Storage

### Correct Locations
- Task docs → `memory-bank/tasks/`
- QA reports → `memory-bank/qa/`
- Debug reports → `memory-bank/reports/`
- Archives → `memory-bank/archive/`

### Wrong Locations
❌ `documentation/tasks/` (should NOT exist)
❌ Source code directories
❌ Project root (except README.md)

---

## 7. Complexity Levels

| Level | Type | Workflow |
|-------|------|----------|
| 1 | Quick fix | init → do → reflect → archive |
| 2 | Enhancement | init → plan → do → reflect → archive |
| 3 | Feature | init → plan → design → do → reflect → archive |
| 4 | System | init → plan → design → do → reflect → archive (iterations) |

---

## Quick Checklist

Before any operation:
- [ ] sys8 MCP for timestamps
- [ ] context7 MCP for library docs (if needed)
- [ ] Task ID from activeContext.md
- [ ] Files in memory-bank/ only
- [ ] No git push without permission
