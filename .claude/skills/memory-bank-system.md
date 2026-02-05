# Memory Bank System Rules

> **Core system rules for Memory Bank workflow and file organization**

## 📂 File Locations

**CRITICAL:** All Memory Bank files reside in `memory-bank/` directory.

### Core Files
- `tasks.md` - Active task tracking (ephemeral)
- `backlog.md` - Active task queue (v2.0 - performance optimized)
- `backlog-archive.md` - Historical completed/cancelled tasks
- `activeContext.md` - Current state
- `progress.md` - Overall progress
- `projectbrief.md` - Project overview
- `productContext.md` - Product requirements
- `systemPatterns.md` - System patterns
- `techContext.md` - Technical context
- `style-guide.md` - Code style guide

### Directories
- `prd/` - Product Requirements Documents
- `tasks/` - ALL operational task documentation
- `creative/` - Creative phase documents
- `reflection/` - Reflection documents
- `qa/` - QA reports
- `archive/` - Completed task archives
- `reports/` - Debug/diagnostic reports
- `docs/` - Memory Bank system documentation

---

## 🚨 Documentation Storage Rules

### MANDATORY: Task ID in ALL Report Filenames

**Format:** `[PREFIX]-[4-digit-number]` (e.g., `DEV-0053`, `FIN-0001`)

**Report Types:**
- QA reports: `qa-report-[task_id]-[phase].md`
- Test reports: `test-report-[task_id]-[component].md`
- Debug reports: `debug-[task_id]-[feature].md`
- Diagnostic: `diagnostic-[task_id]-[issue].md`
- Creative: `creative-[task_id]-[feature_name].md`

### Prohibited Locations

**NEVER create MD files (except README.md) in:**
- Application source directories
- Component directories (`frontend/src/`, `backend/src/`)
- Service root directories (except README.md)
- Any directory containing source code

---

## 🔢 Task Numbering System

### Format
```
[PREFIX]-[NUMBER]
```

**Examples:**
- `DEV-0053` (Development task #53)
- `FIN-0001` (Finance task #1)
- `QA-0008` (QA task #8)

### Auto-Generation
If user doesn't provide task ID, system automatically:
1. Determines prefix from task content/keywords
2. Scans existing tasks for same prefix
3. Generates next sequential number (4-digit with leading zeros)

### Task ID Extraction
Get current task ID from `memory-bank/activeContext.md` first line:
```markdown
**Current Task:** [TASK-ID] - [Task Title]
```

---

## 📋 Task Context Tracking

### Active Task Identification

`activeContext.md` MUST track current task:

```markdown
**Current Task:** [TASK-ID] - [Task Title]
- **Status**: [in_progress|completed|paused]
- **Started**: [Date]
- **Complexity**: Level [1-4]
- **Type**: [Type]
- **Priority**: [Priority]
- **Repository**: [Repository]
- **Branch**: [Branch name]
```

### Task Status Lifecycle
```
not_started → in_progress → completed → archived
     ↓              ↑
   paused ←────────┘
```

### Archive Command Behavior
`/archive` command:
1. Reads `activeContext.md` to get current task ID
2. Verifies task exists in `tasks.md`
3. Archives ONLY that specific task (not all completed)
4. Updates `activeContext.md` after archiving

---

## 🎯 Backlog Management (v2.0)

### Two-File Architecture

**Active Backlog** (`backlog.md`):
- Contains ONLY `pending` and `in_progress` items
- Performance optimized (~10x faster reads)
- Format: `BACKLOG-[4-digit-number]`

**Backlog Archive** (`backlog-archive.md`):
- Historical `completed` and `cancelled` items
- Rarely read during normal operations
- Provides historical reference

### When to Update
- Task completion: Move from `backlog.md` to `backlog-archive.md`
- New task: Add to `backlog.md` with `pending` status

---

## 📝 Documentation Tasks Prohibition

### CRITICAL PROHIBITION

**NEVER create `documentation/tasks/` directory!**

**Correct locations:**
- Operational task docs → `memory-bank/tasks/`
- Final archived tasks → `documentation/archive/` (if exists)
- Project documentation → `documentation/[category]/`

### File Type Routing

**Operational → memory-bank/tasks/**
- Implementation plans: `DEV-XXX-implementation-plan.md`
- Testing guides: `DEV-XXX-testing-guide.md`
- QA reports: `DEV-XXX-QA-*.md`
- Bug fix reports: `DEV-XXX-bug-fix.md`

**Final → documentation/**
- Archived tasks: `documentation/archive/archive-[task_id].md`
- API docs: `documentation/api/`
- Infrastructure: `documentation/infrastructure/`

---

## 🔄 Command Execution

### Platform Awareness

**Always detect platform first:**
```
- macOS/Linux → use forward slashes
- Windows → check for backslashes, adapt paths
```

**Safe command execution:**
1. Verify directory exists before operations
2. Use absolute paths for Memory Bank files
3. Handle both `/` and `\` path separators

### File Verification

**Optimized checks:**
- Use `ls` (fast) for existence checks
- Use `Read` only when content needed
- Avoid redundant file reads

---

## 🎨 Creative Phase Enforcement

### When Required
Complexity Level 3-4 tasks automatically trigger Creative Phase.

### Requirements
- Architectural decisions needed
- Multiple implementation approaches
- UI/UX design required
- Data model design

### Output
- `memory-bank/creative/creative-[task_id]-[feature_name].md`
- Must include task ID in filename

---

## 📊 Complexity Decision Tree

### Level 1 (Quick Fix)
- Single file change
- < 50 lines of code
- No architecture changes
- Flow: init → do → reflect → archive

### Level 2 (Enhancement)
- Few files (2-5)
- < 200 lines of code
- Minor refactoring
- Flow: init → plan → do → reflect → archive

### Level 3 (Feature)
- Multiple files (5-15)
- 200-1000 lines
- Requires design
- Flow: init → plan → **design** → do → reflect → archive

### Level 4 (Major Feature)
- Many files (15+)
- > 1000 lines
- Complex architecture
- Flow: init → plan → **design** → **phased implementation** → reflect → archive

---

## ⚙️ Mode Transition Optimization

### Automatic Transitions
- Level 3-4 → Auto-enter CREATIVE mode
- QA validation needed → Auto-enter QA mode
- Implementation done → Auto-suggest REFLECT mode

### Manual Transitions
- `/plan` → PLAN mode
- `/design` → CREATIVE mode
- `/do` → DO mode
- `/reflect` → REFLECT mode
- `/archive` → ARCHIVE mode

---

## 🚨 Critical Rules (Always Apply)

1. **Memory Bank is Truth** - Never work outside `memory-bank/`
2. **Task ID Required** - ALL reports must include task ID
3. **No documentation/tasks/** - This directory must NOT exist
4. **Context Tracking** - Always update `activeContext.md`
5. **Backlog v2.0** - Use two-file architecture (active + archive)

---

*These rules ensure clean organization and efficient workflow.*
