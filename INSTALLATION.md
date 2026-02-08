# Memory Bank v2.4 Installation Guide

> **New in v2.4:** Enhanced Design Process (6-phase workflow) in `/prd` and `/plan`. All commands follow Agent Skills standard.

## 🎯 Where to Install?

Choose installation location based on your needs:

| Installation Type | Location | Use When | Benefits | Trade-offs |
|------------------|----------|----------|----------|------------|
| **Project-level** (Recommended) | `.claude/` in project | Project-specific customization | Isolated, version-controlled, team sharing | Install per project |
| **User-level** (Global) | `~/.claude/` in home | Available in ALL projects | One-time setup, always available | Changes affect all projects |

### Decision Tree

```
Do you need project-specific agents/skills?
├─ YES → Project-level installation (.claude/)
└─ NO → Do you use Memory Bank in multiple projects?
   ├─ YES → User-level installation (~/.claude/)
   └─ NO → Project-level installation (.claude/)
```

---

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

## Project-Level Installation (Recommended)

**Best for:**
- Project-specific customization
- Team collaboration (committed to git)
- Different Memory Bank configurations per project

**Location:** `.claude/` in project directory

**Install:**
```bash
cd /path/to/your-project

# Copy structure (as shown above in Quick Installation)
cp -r /path/to/cursor-memory-bank-angry/.claude .
cp /path/to/cursor-memory-bank-angry/CLAUDE.md .

# Initialize Memory Bank
mkdir -p memory-bank/{tasks,creative,reflection,qa,reports,archive,prd,docs}
touch memory-bank/{tasks,backlog,backlog-archive,activeContext,progress,projectbrief}.md
```

**Benefits:**
- ✅ Version-controlled with project
- ✅ Team members get same configuration
- ✅ Customize agents/skills per project
- ✅ Isolated from other projects

**Trade-offs:**
- ❌ Need to install in each project
- ❌ Updates require manual sync

---

## User-Level Installation (Global)

**Best for:**
- Using Memory Bank in many projects
- Personal workflow consistency
- Quick access without per-project setup

**Location:** `~/.claude/` in home directory

**Install:**
```bash
# Copy to global Claude Code directory
cp -r /path/to/cursor-memory-bank-angry/.claude/agents ~/.claude/agents
cp -r /path/to/cursor-memory-bank-angry/.claude/skills ~/.claude/skills
cp -r /path/to/cursor-memory-bank-angry/.claude/commands ~/.claude/commands
cp /path/to/cursor-memory-bank-angry/CLAUDE.md ~/.claude/CLAUDE.md

# Create Memory Bank in each project you use it
cd /path/to/your-project
mkdir -p memory-bank/{tasks,creative,reflection,qa,reports,archive,prd,docs}
touch memory-bank/{tasks,backlog,backlog-archive,activeContext,progress,projectbrief}.md
```

**Benefits:**
- ✅ Available in ALL projects automatically
- ✅ One-time setup
- ✅ Consistent workflow everywhere
- ✅ Easier to maintain/update

**Trade-offs:**
- ❌ Changes affect all projects
- ❌ Not version-controlled with project
- ❌ Team members need separate installation
- ❌ Still need `memory-bank/` per project

**Important:** Even with user-level installation, each project needs its own `memory-bank/` directory structure!

---

## Hybrid Installation (Advanced)

**Scenario:** User-level agents/skills, project-level customizations.

```bash
# Install base system globally
cp -r .claude/agents ~/.claude/agents
cp -r .claude/skills ~/.claude/skills
cp -r .claude/commands ~/.claude/commands

# In specific projects, override/extend as needed
cd /path/to/special-project
mkdir -p .claude/skills
cp ~/.claude/skills/ai-quality.md .claude/skills/
# Edit .claude/skills/ai-quality.md for project-specific rules
```

**Use case:** Core workflow globally, project-specific tweaks locally.

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
