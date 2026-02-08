# Memory Bank v2.1 Installation Guide

## Quick Installation for Existing Projects

If you want to use Memory Bank v2.1 (Subagents & Skills architecture) in another project:

### Step 1: Copy Required Files

From your Memory Bank repository to your target project:

```bash
# Navigate to your target project
cd /path/to/your-project

# Copy Claude Code structure
cp -r /Users/ug/code/AI/cursor-memory-bank-angry/.claude .

# Copy main router
cp /Users/ug/code/AI/cursor-memory-bank-angry/CLAUDE.md .

# Copy Cursor IDE compatibility (if using Cursor)
cp /Users/ug/code/AI/cursor-memory-bank-angry/.cursorrules .

# Optional: Copy Cursor rules if using Cursor IDE
cp -r /Users/ug/code/AI/cursor-memory-bank-angry/.cursor .
```

### Step 2: Initialize Memory Bank

Create the Memory Bank structure:

```bash
# In your project directory
mkdir -p memory-bank/{tasks,creative,reflection,qa,reports,archive,prd,docs}

# Create core files
touch memory-bank/tasks.md
touch memory-bank/backlog.md
touch memory-bank/backlog-archive.md
touch memory-bank/activeContext.md
touch memory-bank/progress.md
touch memory-bank/projectbrief.md
```

### Step 3: Verify Installation

Check that structure is correct:

```bash
# Should show:
ls -d .claude/agents .claude/skills .claude/commands CLAUDE.md
# Output: .claude/agents .claude/skills .claude/commands CLAUDE.md

# Should show 4 agent files:
ls .claude/agents/
# Output: architect.md developer.md planner.md reviewer.md

# Should show 5 skill files:
ls .claude/skills/
# Output: ai-quality.md memory-bank-system.md performance.md security.md testing.md
```

### Step 4: Test Commands

In Claude Code (in your project directory):

```bash
# Start Claude Code
claude

# Try a command
/mb-status

# Should show Memory Bank status
```

---

## For New Projects

If starting a completely new project with Memory Bank:

### Option 1: Clone This Repository

```bash
git clone https://github.com/Angry-Robot-Deals/cursor-memory-bank-angry.git my-project
cd my-project
rm -rf .git
git init
```

### Option 2: Manual Setup

1. Create project directory
2. Follow "Step 1: Copy Required Files" above
3. Follow "Step 2: Initialize Memory Bank" above
4. Initialize git: `git init`

---

## Troubleshooting

### Error: "Agent type 'mb-reflect:mb-reflect' not found"

**Problem:** Claude Code can't find agents.

**Cause:** You're in a project without `.claude/agents/` directory.

**Solution:**
```bash
# Verify you're in the right project directory
pwd

# Check if .claude/agents/ exists
ls .claude/agents/

# If not, copy from Memory Bank repository (Step 1 above)
```

### Error: "memory-bank/reflection/: No such file or directory"

**Problem:** Memory Bank structure not initialized.

**Solution:**
```bash
# Create Memory Bank directories
mkdir -p memory-bank/{tasks,creative,reflection,qa,reports,archive,prd,docs}
```

### Commands Not Working

**Problem:** `/mb-*` commands not recognized.

**Cause:** Missing `.claude/commands/` directory.

**Solution:**
```bash
# Copy commands from Memory Bank repository
cp -r /path/to/cursor-memory-bank-angry/.claude/commands .claude/
```

---

## Project-Specific vs. Global Installation

### Project-Specific (Recommended)
- Install in each project directory
- Customize agents/skills per project
- Better isolation

### Global Installation (Advanced)
```bash
# Copy to Claude Code global directory
cp -r .claude/agents ~/.claude/agents
cp -r .claude/skills ~/.claude/skills
cp -r .claude/commands ~/.claude/commands
cp CLAUDE.md ~/.claude/
```

**Note:** Global installation makes agents/skills available in ALL projects.

---

## Verification Checklist

After installation, verify:

- [ ] `.claude/agents/` exists with 4 files
- [ ] `.claude/skills/` exists with 5 files
- [ ] `.claude/commands/` exists with 10 files
- [ ] `CLAUDE.md` exists in project root
- [ ] `memory-bank/` directory structure created
- [ ] Commands work: Try `/mb-status`

---

## Quick Example: Installing in Another Project

```bash
# Example: Install Memory Bank in "aether/local-env" project
cd /Users/ug/code/aether/local-env

# Copy structure
cp -r /Users/ug/code/AI/cursor-memory-bank-angry/.claude .
cp /Users/ug/code/AI/cursor-memory-bank-angry/CLAUDE.md .
cp /Users/ug/code/AI/cursor-memory-bank-angry/.cursorrules .

# Initialize Memory Bank
mkdir -p memory-bank/{tasks,creative,reflection,qa,reports,archive,prd,docs}
touch memory-bank/{tasks,backlog,backlog-archive,activeContext,progress,projectbrief}.md

# Verify
ls -d .claude/agents .claude/skills memory-bank/

# Start Claude Code
claude

# Test
/mb-status
```

---

**Quick Start:** Copy `.claude/`, `CLAUDE.md`, create `memory-bank/`, done! 🚀
