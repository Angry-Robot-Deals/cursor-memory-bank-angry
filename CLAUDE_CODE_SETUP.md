# Claude Code Setup Guide

This guide explains how to use Memory Bank System with **Claude Code** (claude.ai/code) - Anthropic's official CLI tool for Claude.

## What is Claude Code?

Claude Code is Anthropic's command-line interface that allows you to interact with Claude AI directly in your terminal.

### Key Difference from Cursor IDE

**⚠️ IMPORTANT**: Claude Code uses different slash command prefixes than Cursor IDE!

- **Cursor IDE**: Uses slash commands (`/van`, `/plan`, `/creative`, etc.)
- **Claude Code**: Uses **`/mb-` prefix** (`/mb-init`, `/mb-plan`, `/mb-design`, etc.)

The slash `/` is reserved for system commands like `/help`, `/clear`, `/tasks` in both platforms.

### How It Works

Claude Code uses **slash commands** with `/mb-` prefix:

```bash
/mb-init Add authentication
/mb-plan
/mb-design
/mb-do
```

Claude reads `CLAUDE.md` at startup and understands Memory Bank methodology, following the appropriate workflow through these commands.

## Installation

### Prerequisites

1. **Claude Code CLI** - Install from [claude.ai/code](https://claude.ai/code)
2. **Project with Memory Bank System** - This repository or your own project with Memory Bank installed

### Setup Steps

#### 1. Install Claude Code

Follow the official installation instructions at [claude.ai/code](https://claude.ai/code).

Verify installation:
```bash
claude --version
```

#### 2. Copy CLAUDE.md to Your Project

The `CLAUDE.md` file is already included in this repository. When you use Claude Code in this project, it will automatically read `CLAUDE.md` to understand the Memory Bank System.

For new projects:
```bash
# Copy CLAUDE.md to your project root
cp /path/to/cursor-memory-bank/CLAUDE.md /path/to/your-project/
```

#### 3. Copy Claude Code Rules and Commands

Claude Code has its own directory structure optimized for slash commands:

```bash
# Copy the .claude directory structure
cp -r /path/to/cursor-memory-bank/.claude /path/to/your-project/
```

This provides Claude Code with access to:
- Slash commands (`.claude/commands/`)
- Workflow guides (`.claude/workflows/`)
- Core rules (`.claude/rules/`)
- MCP server integration guidelines

**Optional**: You can also copy `.cursor/` for additional context, but `.claude/` is specifically designed for Claude Code.

#### 4. Initialize Memory Bank Structure

Create the `memory-bank/` directory structure:

```bash
mkdir -p memory-bank/{creative,reflection,archive,tasks,qa,reports,prd,docs}
```

Or let Claude Code create it for you on first use.

## Usage with Claude Code

### Starting Claude Code

Navigate to your project directory and start Claude Code:

```bash
cd /path/to/your-project
claude
```

### Using Slash Commands

Claude Code uses Memory Bank slash commands with `/mb-` prefix:

#### Available Commands

| Command | Purpose | Example |
|---------|---------|---------|
| `/mb-prd` | Generate Product Requirements Document | `/mb-prd Add email notifications` |
| `/mb-init` | Initialize new task | `/mb-init Add user authentication` |
| `/mb-plan` | Create implementation plan | `/mb-plan` |
| `/mb-design` | Explore design options | `/mb-design` |
| `/mb-do` | Implement changes | `/mb-do` |
| `/mb-compliance` | Post-QA hardening & PRD revalidation | `/mb-compliance` |
| `/mb-reflect` | Review completed work | `/mb-reflect` |
| `/mb-archive` | Archive completed task | `/mb-archive` |
| `/mb-status` | Check current task status | `/mb-status` |
| `/mb-continue` | Continue current task | `/mb-continue` |

#### Example Workflow

**1. Generate PRD (Optional):**
```bash
/mb-prd Implement rate limiting for API endpoints
```

**2. Initialize Task:**
```bash
/mb-init Add OAuth2 authentication
```

**3. Create Plan:**
```bash
/mb-plan
```

**4. Explore Design (if needed):**
```bash
/mb-design
```

**5. Implement:**
```bash
/mb-do
```

**6. Compliance (Post-QA hardening):**
```bash
/mb-compliance
```

**7. Reflect:**
```bash
/mb-reflect
```

**8. Archive:**
```bash
/mb-archive
```

### Working with Memory Bank Files

Claude Code automatically:
- ✅ Reads from `memory-bank/tasks.md`, `activeContext.md`, etc.
- ✅ Updates files based on workflow progress
- ✅ Follows file naming conventions
- ✅ Maintains task context across sessions
- ✅ Uses sys8 and context7 MCP servers (if configured)

### MCP Server Integration

Claude Code supports MCP servers. Configure them in your Claude Code settings:

**sys8 MCP** (system operations):
```json
{
  "mcpServers": {
    "sys8": {
      "command": "npx",
      "args": [
        "tsx",
        "$HOME/code/AI/mcp/sys8/src/index.ts"
      ]
    }
  }
}
```

**context7 MCP** (library documentation):
```json
{
  "mcpServers": {
    "context7": {
      "command": "npx",
      "args": ["-y", "@context7/mcp-server"]
    }
  }
}
```

## Key Differences: Cursor vs Claude Code

| Feature | Cursor IDE | Claude Code |
|---------|-----------|-------------|
| **Interface** | Graphical IDE | Command-line |
| **Commands** | `/van`, `/plan`, etc. | `/mb-init`, `/mb-plan`, etc. |
| **Rules Loading** | Automatic via .mdc files | Via CLAUDE.md + .claude/ |
| **Memory Bank** | ✅ Automatic | ✅ Automatic |
| **MCP Servers** | ✅ Supported | ✅ Supported |
| **Workflow** | Command-driven | Command-driven |
| **Setup** | Copy .cursor folder | Copy CLAUDE.md + .claude folder |
| **Project vs global** | Project: `.cursor/` in repo; Global: see memory-bank/docs/DEPLOYMENT.md | Project: `.claude/` in repo; Global: copy to `~/.claude/` |

## Best Practices for Claude Code

### 1. Use Slash Commands
```bash
/mb-init Add new feature
/mb-plan
/mb-design
```

### 2. Check Task Status
```bash
/mb-status
```

### 3. Continue Work
```bash
/mb-continue
```

### 4. Follow Workflow Order
```bash
/mb-init → /mb-plan → /mb-design → /mb-do → /mb-reflect → /mb-archive
```

### 5. Use PRD for Complex Features
```bash
/mb-prd Complex feature description
# Then reference the PRD when initializing
/mb-init Use PRD: memory-bank/prd/PRD-*.md
```

## Workflow Examples

### Complete Feature Development

```bash
# Session 1: PRD and Planning
/mb-prd Add email notification system
# Review generated PRD, then:
/mb-init Use PRD: memory-bank/prd/PRD-email-notifications.md
/mb-plan

# Session 2: Design and Implementation
/mb-continue
/mb-design
/mb-do

# Session 3: Review and Archive
/mb-reflect
/mb-archive
```

### Quick Bug Fix (Level 1)

```bash
/mb-init Fix login timeout issue in session management
/mb-do
/mb-reflect
/mb-archive
```

## Troubleshooting

### Issue: Commands not recognized

**Solution:**
- Ensure `.claude/commands/` directory exists
- Use `/mb-` prefix (not `/van`, `/plan`, etc.)
- Check that `CLAUDE.md` is in project root

### Issue: Memory Bank files not being created

**Solution:**
- Check if `memory-bank/` directory exists
- Run: `/mb-init` to initialize structure
- Verify file permissions

### Issue: MCP servers not being used

**Solution:**
- Verify MCP server configuration in Claude Code settings
- Check MCP server status
- Ensure servers are properly installed

### Issue: Workflow seems out of sync

**Solution:**
- Check `memory-bank/activeContext.md` for current task
- Run: `/mb-status` to check current status
- Use: `/mb-continue` to resume workflow

## Migrating from Cursor to Claude Code

If you're already using Memory Bank in Cursor:

1. **Your Memory Bank files are compatible** - No changes needed
2. **Continue existing tasks** - Claude Code can read your current tasks
3. **Use `/mb-` commands** - Instead of `/plan`, use `/mb-plan`
4. **Same workflow** - All phases work identically

## Advanced Usage

### Check Task Status

```bash
/mb-status
```

### Continue Interrupted Work

```bash
/mb-continue
```

### Generate PRD Before Starting

```bash
/mb-prd Feature description
# Then use the PRD
/mb-init Use PRD: memory-bank/prd/PRD-*.md
```

## Support and Resources

- **Documentation**: See `README.md` for complete Memory Bank overview
- **Claude setup & commands**: `documentation/claude/` (INSTALLATION_GUIDE.md, commands-reference.md, COMMANDS_QUICK_START.md)
- **Cursor commands reference**: `documentation/cursor/commands-reference.md`
- **Cursor Commands**: If using Cursor, see `COMMANDS_README.md`
- **Platform Comparison**: See `PLATFORM_COMPARISON.md`
- **AI Quality Rules**: See `.cursor/rules/isolation_rules/Core/AI-Quality/`

## Version Compatibility

- **Claude Code**: Any version
- **Memory Bank System**: v2.0+
- **CLAUDE.md**: Automatically updated with system

---

**Remember:** Claude Code uses slash commands with `/mb-` prefix. Use these commands to follow the Memory Bank methodology and maintain structured development workflows!
