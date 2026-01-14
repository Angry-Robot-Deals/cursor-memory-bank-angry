# ARCHIVE Command - Task Archiving

This command creates comprehensive archive documentation and updates the Memory Bank for future reference.                                                      

## Memory Bank Integration

Reads from:
- `memory-bank/tasks.md` - Complete task details and checklists
- `memory-bank/reflection/reflection-[task_id].md` - Reflection document
- `memory-bank/progress.md` - Implementation status
- `memory-bank/creative/creative-*.md` - Creative phase documents (Level 3-4)

Creates:
- Archive document in location determined by **Archive Location Priority** (see below)

Updates:
- `memory-bank/tasks.md` - Mark task as COMPLETE
- `memory-bank/progress.md` - Add archive reference
- `memory-bank/activeContext.md` - Reset for next task

## Archive Location Priority

**CRITICAL:** Before creating the archive document, determine the correct location using this priority order:

1. **First priority:** If `./documentation/` directory exists → save to `documentation/archive/`
   - Create `archive/` subdirectory if it doesn't exist
   - Example: `documentation/archive/archive-[task_id].md`

2. **Second priority:** Else if `./doc/` directory exists → save to `doc/archive/`
   - Create `archive/` subdirectory if it doesn't exist
   - Example: `doc/archive/archive-[task_id].md`

3. **Fallback:** Else → save to `memory-bank/archive/`
   - This is the default location if neither `documentation/` nor `doc/` directories exist
   - Example: `memory-bank/archive/archive-[task_id].md`

**Implementation Note:** Check for directory existence at runtime before creating the archive document. Use the first available option in the priority order above.

## Progressive Rule Loading

### Step 1: Load Core Rules
```
Load: $HOME/.cursor/rules/isolation_rules/main.mdc
Load: $HOME/.cursor/rules/isolation_rules/Core/memory-bank-paths.mdc
```

### Step 2: Load ARCHIVE Mode Map
```
Load: $HOME/.cursor/rules/isolation_rules/visual-maps/archive-mode-map.mdc
```

### Step 3: Complexity-Specific Archive Rules
Based on complexity level from `memory-bank/tasks.md`:

### MANDATORY Load Rules:
```
Load: $HOME/.cursor/rules/sys8-mcp-usage.mdc
```

**Level 1:**
```
Load: $HOME/.cursor/rules/isolation_rules/Level1/quick-documentation.mdc
```

**Level 2:**
```
Load: $HOME/.cursor/rules/isolation_rules/Level2/archive-basic.mdc
```

**Level 3:**
```
Load: $HOME/.cursor/rules/isolation_rules/Level3/archive-intermediate.mdc
```

**Level 4:**
```
Load: $HOME/.cursor/rules/isolation_rules/Level4/archive-comprehensive.mdc
```

## Workflow

1. **Verify Reflection Complete**
   - Check that `memory-bank/reflection/reflection-[task_id].md` exists
   - Verify reflection is complete
   - If not complete, return to `/reflect` command

2. **Determine Archive Location**
   - Check if `./documentation/` directory exists
   - If not, check if `./doc/` directory exists
   - If neither exists, use `memory-bank/archive/` as fallback
   - Create `archive/` subdirectory if needed

3. **Create Archive Document**

   **Level 1:**
   - Create quick summary
   - Update `memory-bank/tasks.md` marking task complete

   **Level 2:**
   - Create basic archive document
   - Document changes made
   - Update `memory-bank/tasks.md` and `memory-bank/progress.md`

   **Level 3-4:**
   - Create comprehensive archive document
   - Include: Metadata, Summary, Requirements, Implementation details, Testing, Lessons Learned, References                                                     
   - Archive creative phase documents
   - Document code changes
   - Document testing approach
   - Summarize lessons learned
   - Update all Memory Bank files

4. **Archive Document Structure**
   ```
   # TASK ARCHIVE: [Task Name]
   
   ## METADATA
   - Task ID, dates, complexity level
   
   ## SUMMARY
   Brief overview of the task
   
   ## REQUIREMENTS
   What the task needed to accomplish
   
   ## IMPLEMENTATION
   How the task was implemented
   
   ## TESTING
   How the solution was verified
   
   ## LESSONS LEARNED
   Key takeaways from the task
   
   ## REFERENCES
   Links to related documents (reflection, creative phases, etc.)
   ```

5. **Update Memory Bank**
   - Create archive document in the determined location (see Archive Location Priority above)
   - Mark task as COMPLETE in `memory-bank/tasks.md`
   - Update `memory-bank/progress.md` with archive reference (use correct path based on location)
   - Reset `memory-bank/activeContext.md` for next task
   - Clear completed task details from `memory-bank/tasks.md` (keep structure)

## Usage

Type `/archive` to archive the completed task after reflection is done.

## Next Steps

After archiving complete, use `/van` command to start the next task.
