# Installing Memory Bank v2.1 in Your Project

## Quick Install (5 minutes)

### Step 1: Copy Files
```bash
# From Memory Bank repository to your project
cd /your/project/directory

# Copy Claude Code structure
cp -r /path/to/cursor-memory-bank-angry/.claude .
cp /path/to/cursor-memory-bank-angry/CLAUDE.md .

# Optional: Copy Cursor IDE support
cp /path/to/cursor-memory-bank-angry/.cursorrules .
```

### Step 2: Initialize Memory Bank
```bash
# Create directory structure
mkdir -p memory-bank/{tasks,creative,reflection,qa,reports,archive,prd,docs}

# Create core files
touch memory-bank/tasks.md
touch memory-bank/backlog.md
touch memory-bank/backlog-archive.md
touch memory-bank/activeContext.md
touch memory-bank/progress.md
touch memory-bank/projectbrief.md
```

### Step 3: Verify
```bash
ls .claude/agents/    # Should show 4 files
ls .claude/skills/    # Should show 5 files
ls memory-bank/       # Should show directories

# Test in Claude Code
claude
/mb-status
```

---

## What Gets Installed

### Claude Code Structure
```
.claude/
├── agents/           (4 specialized AI roles)
├── skills/           (5 knowledge modules)
├── commands/         (10 workflow commands)
├── guides/
└── settings.local.json

CLAUDE.md             (lean router, <1KB)
```

### Memory Bank Structure
```
memory-bank/
├── tasks.md          (active task tracking)
├── backlog.md        (task queue)
├── activeContext.md  (current state)
├── progress.md       (build status)
├── tasks/            (task documentation)
├── creative/         (design docs)
├── reflection/       (review docs)
├── archive/          (completed tasks)
└── [other dirs]
```

---

## Troubleshooting

### "Agent type not found"
**Problem:** `.claude/agents/` directory missing

**Fix:**
```bash
cp -r /path/to/cursor-memory-bank-angry/.claude/agents .claude/
```

### "memory-bank/reflection/: No such file or directory"
**Problem:** Memory Bank not initialized

**Fix:**
```bash
mkdir -p memory-bank/reflection
```

### Commands Not Working
**Problem:** Missing `.claude/commands/`

**Fix:**
```bash
cp -r /path/to/cursor-memory-bank-angry/.claude/commands .claude/
```

---

## Example: Install in "aether/local-env"

```bash
cd /Users/ug/code/aether/local-env

# Copy structure
cp -r /Users/ug/code/AI/cursor-memory-bank-angry/.claude .
cp /Users/ug/code/AI/cursor-memory-bank-angry/CLAUDE.md .

# Initialize Memory Bank
mkdir -p memory-bank/{tasks,creative,reflection,qa,reports,archive}
touch memory-bank/{tasks,backlog,activeContext,progress,projectbrief}.md

# Verify
ls .claude/agents/     # architect.md developer.md planner.md reviewer.md
ls .claude/skills/     # 5 skill files
ls memory-bank/        # directories present

# Start Claude Code
claude

# Test
/mb-status
```

**Now Memory Bank v2.1 will work in your project!** 🚀

---

See main `README.md` for full documentation.
