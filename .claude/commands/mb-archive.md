---
name: mb-archive
description: Archive completed task with comprehensive documentation and Memory Bank updates
disable-model-invocation: true
---

# /mb-archive - Archive Task

Complete and archive current task.

## Steps
1. Create archive document with:
   - Task summary
   - Implementation details
   - Reflection insights
2. Update Backlog (if from Backlog)
3. Reset `activeContext.md`
4. Clear `tasks.md`

## Read
- `memory-bank/tasks.md`
- `memory-bank/reflection/reflection-[task_id].md`
- `memory-bank/creative/*.md` (Level 3-4)

## Write
- `memory-bank/archive/archive-[task_id].md`
- `memory-bank/backlog.md` (if applicable)
- `memory-bank/backlog-archive.md` (if applicable)
- `memory-bank/tasks.md` (clear)
- `memory-bank/activeContext.md` (reset)

## Next
Ready for new task → `/mb-init`
