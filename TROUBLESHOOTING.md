# Memory Bank Troubleshooting Guide

> **New in v2.3:** All commands now use Agent Skills standard format with YAML frontmatter.

## Understanding Skills vs Commands vs Agents

### What's What?

| Term | What It Is | Location | Example |
|------|-----------|----------|---------|
| **Skill** | Knowledge module or command | `.claude/skills/` or `.claude/commands/` | `ai-quality.md` |
| **Agent** | Role/persona | `.claude/agents/` | `planner.md` |
| **Command** | Slash command (skill with frontmatter) | `.claude/commands/` | `mb-init.md` |

**Key Point:** In v2.3, commands ARE skills. They use Agent Skills standard format (YAML frontmatter).

### Agent Skills Standard Format

**All commands now have YAML frontmatter:**

```yaml
---
name: mb-reflect
description: Review completed task and create reflection document
---

# Command content here...
```

**Required fields:**
- `name`: Command name (without `/`)
- `description`: What it does (used by Claude for context)

**Optional fields:**
- `disable-model-invocation: true` - User must invoke manually (e.g., `/mb-archive`)

**Why this matters:** Claude Code uses this format to:
- Register slash commands
- Understand when to suggest commands
- Load command context automatically

---

## Common Claude Code Errors

### ❌ Error: "Agent type 'mb-reflect:mb-reflect' not found"

**Full Error:**
```
Error: Agent type 'mb-reflect:mb-reflect' not found. 
Available agents: Bash, general-purpose, statusline-setup, Explore, Plan...
```

**Root Cause Analysis:**

This error occurs when command file has **incorrect frontmatter format**.

**Correct format (v2.3):**
```yaml
---
name: mb-reflect
description: Review completed task
---
```

**Incorrect formats that cause this error:**
```yaml
# WRONG: Using context: fork with invalid agent type
---
name: mb-reflect
context: fork
agent: mb-reflect  # ← This causes error (not a valid agent type)
---
```

**Why this happens:**
- Commands in `~/.claude/commands/` or `.claude/commands/` create slash commands
- If frontmatter has `context: fork` + `agent: [name]`, Claude tries to run as subagent
- `mb-reflect` is not a valid subagent type (valid: `Bash`, `general-purpose`, `Explore`, etc.)

**Solution (v2.3+):**
All Memory Bank commands use correct format now (YAML frontmatter without `context: fork`).

**Still seeing this error?**

**Cause:** You're in a project that doesn't have Memory Bank v2.3 structure installed.

**Diagnosis:**
```bash
# Check if you're in the right project
pwd
# Should be in a project with Memory Bank

# Check if agents exist
ls .claude/agents/
# Should show: architect.md developer.md planner.md reviewer.md

# If directory doesn't exist, Memory Bank is not installed
```

**Solution:**

1. **Verify Project Location**
   ```bash
   # Make sure you're in a project with Memory Bank
   cd /path/to/project-with-memory-bank
   claude
   ```

2. **OR Install Memory Bank in Current Project**
   ```bash
   # Copy from Memory Bank repository
   cp -r /path/to/cursor-memory-bank-angry/.claude .
   cp /path/to/cursor-memory-bank-angry/CLAUDE.md .
   
   # Initialize Memory Bank structure
   mkdir -p memory-bank/{tasks,creative,reflection,qa,reports,archive}
   touch memory-bank/{tasks,backlog,activeContext,progress,projectbrief}.md
   ```

3. **Verify Installation**
   ```bash
   ls .claude/agents/     # Should show 4 agent files
   ls .claude/skills/     # Should show 5 skill files
   ls memory-bank/        # Should show directories
   ```

---

### ❌ Error: "memory-bank/reflection/: No such file or directory"

**Cause:** Memory Bank directory structure not initialized in this project.

**Solution:**
```bash
mkdir -p memory-bank/{tasks,creative,reflection,qa,reports,archive,prd,docs}
```

---

### ❌ Error: "ls: /Users/ug/code/aether/local-env/.claude/agents/: No such file or directory"

**Cause:** Claude Code is looking in a different project (`aether/local-env`) that doesn't have Memory Bank.

**Solution 1: Switch to Correct Project**
```bash
# Navigate to project with Memory Bank
cd /Users/ug/code/AI/cursor-memory-bank-angry

# Start Claude Code
claude

# Now commands should work
/mb-status
```

**Solution 2: Install Memory Bank in Current Project**
```bash
# If you want to use Memory Bank in aether/local-env:
cd /Users/ug/code/aether/local-env

# Copy Memory Bank structure
cp -r /Users/ug/code/AI/cursor-memory-bank-angry/.claude .
cp /Users/ug/code/AI/cursor-memory-bank-angry/CLAUDE.md .

# Initialize Memory Bank
mkdir -p memory-bank/{tasks,creative,reflection,qa,reports,archive}
touch memory-bank/{tasks,backlog,activeContext,progress,projectbrief}.md

# Verify
ls .claude/agents/
ls memory-bank/

# Restart Claude Code
claude
```

---

### ❌ Commands Show Up But Don't Work

**Problem:** Commands exist but behavior is wrong.

**Possible Causes:**

1. **Missing YAML Frontmatter (Pre-v2.3)**
   ```bash
   # Check if commands have frontmatter
   head -5 .claude/commands/mb-reflect.md
   # Should start with:
   # ---
   # name: mb-reflect
   # description: ...
   # ---
   ```
   
   **Fix:** Update to v2.3 (all commands have proper frontmatter).

2. **Missing Agents/Skills**
   ```bash
   # Verify agents exist
   ls .claude/agents/
   # Should show: architect.md developer.md planner.md reviewer.md
   
   # Verify skills exist
   ls .claude/skills/
   # Should show 5 skill files
   ```

3. **Corrupted CLAUDE.md**
   ```bash
   # Check CLAUDE.md size
   wc -l CLAUDE.md
   # Should be ~37 lines, <1KB
   
   # If wrong, copy fresh version
   cp /path/to/cursor-memory-bank-angry/CLAUDE.md .
   ```

4. **Wrong Claude Code Version**
   ```bash
   claude --version
   # Should be recent version (2026+)
   ```

---

## Verification Commands

### Check Installation
```bash
# In your project directory
ls .claude/agents/     # Should show 4 files
ls .claude/skills/     # Should show 5 files
ls .claude/commands/   # Should show 10+ files
ls memory-bank/        # Should show directories
cat CLAUDE.md          # Should be ~37 lines
```

### Test Commands in Claude Code
```bash
claude                 # Start Claude Code
/mb-status            # Should show status (even if no active task)
/mb-init "Test task"  # Should initialize a task
```

---

## Quick Fix Script

Save this as `install-memory-bank.sh`:

```bash
#!/bin/bash
# Quick install Memory Bank v2.1 in current project

echo "Installing Memory Bank v2.1..."

# Set source path (adjust this!)
SOURCE="/Users/ug/code/AI/cursor-memory-bank-angry"

# Copy structure
cp -r "$SOURCE/.claude" .
cp "$SOURCE/CLAUDE.md" .
cp "$SOURCE/.cursorrules" .

# Initialize Memory Bank
mkdir -p memory-bank/{tasks,creative,reflection,qa,reports,archive,prd,docs}
touch memory-bank/tasks.md
touch memory-bank/backlog.md
touch memory-bank/backlog-archive.md
touch memory-bank/activeContext.md
touch memory-bank/progress.md
touch memory-bank/projectbrief.md

# Verify
echo "✅ Installation complete!"
echo ""
echo "Verification:"
ls .claude/agents/ | wc -l | xargs echo "Agents:"
ls .claude/skills/ | wc -l | xargs echo "Skills:"
ls memory-bank/ | wc -l | xargs echo "Memory Bank dirs:"
echo ""
echo "Start Claude Code: claude"
echo "Test command: /mb-status"
```

Usage:
```bash
chmod +x install-memory-bank.sh
./install-memory-bank.sh
```

---

## Getting Help

1. **Installation Issues:** See `INSTALLATION.md`
2. **Command Reference:** See `COMMANDS_README.md`
3. **Quick Start:** See `QUICK_START.md`
4. **Main Docs:** See `README.md`

---

**Most Common Issue:** Running Claude Code in wrong project directory!

**Quick Check:**
```bash
pwd                    # Verify you're in the right project
ls .claude/agents/     # Verify agents exist
ls memory-bank/        # Verify Memory Bank initialized
```
