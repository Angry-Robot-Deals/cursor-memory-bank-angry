# BACKLOG MANAGEMENT RULES

## Overview

The Memory Bank system supports a Backlog for storing pending tasks that are not yet active. The Backlog provides a queue of future work items that can be added by PRD and VAN commands, selected and activated by VAN command.

## Backlog File

### Active Backlog (v2.0)
**Location:** `memory-bank/backlog.md`
**Template:** `.cursor/templates/backlog-template.md`
**Contains:** Pending and in-progress tasks only
**Purpose:** Fast reads (~10x performance improvement)

### Archive Backlog (v2.0)
**Location:** `memory-bank/backlog-archive.md`
**Template:** `.cursor/templates/backlog-archive-template.md`
**Contains:** Completed and cancelled tasks
**Purpose:** Historical reference

## Backlog Item Format

```markdown
### BACKLOG-XXXX: {Task Title}

| Field | Value |
|-------|-------|
| **Status** | pending |
| **Priority** | high |
| **Complexity** | Level 2 |
| **Created** | YYYY-MM-DD |
| **Source** | PRD-DEV-0001 |
| **Tags** | feature, enhancement |

**Description:**
Brief but comprehensive description of what needs to be done.

**Acceptance Criteria:**
- [ ] Criterion 1
- [ ] Criterion 2

**Notes:**
Additional context, references.

---
```

## Backlog ID Format

**Format:** `BACKLOG-[4-digit-number]` (e.g., `BACKLOG-0001`, `BACKLOG-0042`)

**Generation:**
1. Scan existing IDs in `memory-bank/backlog.md`
2. Find maximum number
3. Generate next (max + 1) with 4-digit zero padding

## Statuses

| Status | Description |
|--------|-------------|
| `pending` | Waiting to be worked on |
| `in_progress` | Currently active (moved to tasks.md) |
| `completed` | Finished successfully |
| `cancelled` | No longer needed |

## Priority Levels

- `critical` - Blocking other work
- `high` - Important, address soon
- `medium` - Standard priority (default)
- `low` - Nice to have

## Command Integration

### /mb-prd (PRD Command)

After generating PRD:
1. Identify potential follow-up tasks
2. Prompt: "Add related tasks to Backlog?"
3. Collect task descriptions (1-N)
4. Generate BACKLOG-XXXX IDs
5. Add to `memory-bank/backlog.md`
6. Update summary counts

### /mb-init (VAN Command)

On initialization:
1. Check if `memory-bank/backlog.md` exists
2. Parse for pending items
3. If pending items exist:
   - Display summary: "📋 N pending items in Backlog"
   - List: ID, Title, Priority, Complexity
   - Prompt: "Select from Backlog or start new?"
4. When selecting from Backlog:
   - Update item status to `in_progress`
   - Create entry in `memory-bank/tasks.md`
   - Update `memory-bank/activeContext.md`

### /mb-status (STATUS Command)

Display:
- Current active task
- Backlog summary (counts by status)
- List of pending items

### /mb-archive (ARCHIVE Command)

When archiving:
- Check if task originated from Backlog
- Update Backlog item status to `completed`
- Move to "Archived Items" section

## Operations

### Adding to Backlog

```
1. Ensure backlog.md exists (create from template if not)
2. Generate next BACKLOG-XXXX ID
3. Use sys8 MCP for creation date
4. Set status: pending
5. Set default priority: medium (if not specified)
6. Add to "Pending Items" section
7. Update Summary counts
```

### Selecting from Backlog

```
1. Find item by BACKLOG-XXXX ID
2. Verify status is "pending"
3. Update status to "in_progress"
4. Move to "In Progress Items" section
5. Create task in tasks.md
6. Update activeContext.md
7. Update Summary counts
```

### Completing Backlog Item

```
1. Find item by related task ID
2. Update status to "completed"
3. Add completion date
4. Move to "Archived Items" section
5. Update Summary counts
```

## Error Handling

**Missing Backlog:**
- Create from template: `memory-bank/backlog.md`

**Invalid ID:**
- Show available pending items
- Request valid selection

**Item already active:**
- Show current active task
- Request different selection

---

**Version:** 1.0.0
**Created:** 2026-02-03
