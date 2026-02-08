# Quick Start: Cursor vs Claude Code

Choose your platform and get started in 5 minutes!

## 🎯 Which Platform Are You Using?

<table>
<tr>
<th width="50%">🖥️ Cursor IDE</th>
<th width="50%">💻 Claude Code</th>
</tr>
<tr>
<td>

**Visual IDE with slash commands**

Use if you:
- Work in a visual IDE
- Prefer point-and-click
- Want autocomplete
- Work in a team

</td>
<td>

**Command-line with slash commands**

Use if you:
- Work in terminal
- Prefer CLI tools
- Work on remote servers
- Want command consistency

</td>
</tr>
</table>

---

## 🚀 Cursor IDE Quick Start

### 1. Install
```bash
# Copy .cursor folder to your project
cp -r cursor-memory-bank/.cursor /path/to/project/
```

### 2. Use Commands
Type `/` in Cursor chat to see commands:

```
/prd Add notifications             # Optional: Generate PRD
/van Add user authentication       # Initialize task
/plan                              # Create plan
/creative                          # Explore designs (if needed)
/do                                # Implement
/reflect                           # Review
/archive                           # Archive

# Helper commands (use anytime):
/status                            # Check current status
/continue                          # Resume work
```

### 3. Done! 🎉
**Read more**: [README.md](README.md) | [COMMANDS_README.md](COMMANDS_README.md)

---

## 🚀 Claude Code Quick Start

### 1. Install
```bash
# Copy CLAUDE.md and .claude folder
cp cursor-memory-bank/CLAUDE.md /path/to/project/
cp -r cursor-memory-bank/.claude /path/to/project/
```

### 2. Use Commands
```bash
claude
# Then use slash commands:
/mb-init Add user authentication
/mb-plan
/mb-do
```

### 3. Done! 🎉
**Read more**: [CLAUDE_CODE_SETUP.md](CLAUDE_CODE_SETUP.md) | [.claude/commands/README.md](.claude/commands/README.md)

---

## ⚠️ Critical Difference

<table>
<tr>
<th>Cursor IDE</th>
<th>Claude Code</th>
</tr>
<tr>
<td>

**Uses slash commands**
```
/van Add authentication
/plan
/do
```

✅ Type `/` to see commands
✅ Autocomplete helps
✅ Fast and consistent

</td>
<td>

**Uses `/mb-` commands**
```
/mb-init Add authentication
/mb-plan
/mb-do
```

⚠️ **Use `/mb-` prefix** (not `/van`, `/plan`)
✅ Consistent command syntax
✅ Same as Cursor IDE
✅ Fast and reliable

</td>
</tr>
</table>

### Common Mistake 😅

**In Claude Code:**
```
❌ /van Add authentication          (WRONG - Cursor syntax!)
✅ /mb-init Add authentication      (CORRECT - Claude Code syntax)
```

**Why?** Claude Code uses `/mb-` prefix for Memory Bank commands, while Cursor uses direct command names.

---

## 📋 Side-by-Side Comparison

| Action | Cursor IDE | Claude Code |
|--------|-----------|-------------|
| **New Task** | `/van Add auth` | `/mb-init Add auth` |
| **Plan** | `/plan` | `/mb-plan` |
| **Design** | `/creative` | `/mb-design` |
| **Build** | `/do` | `/mb-do` |
| **Review** | `/reflect` | `/mb-reflect` |
| **Archive** | `/archive` | `/mb-archive` |
| **Status** | `/status` | `/mb-status` |
| **Continue** | `/continue` | `/mb-continue` |

---

## 💡 Pro Tips

### Cursor IDE Tips
1. **Type `/` to discover** - See all available commands
2. **Use autocomplete** - Start typing command name
3. **Check status anytime** - Use `/status` to see where you are
4. **Resume easily** - Use `/continue` after breaks
5. **Visual guides** - See workflow maps in `.cursor/rules/visual-maps/`

### Claude Code Tips
1. **Use `/mb-` prefix** - `/mb-init`, `/mb-plan`, `/mb-do`
2. **Check status** - `/mb-status` shows current task
3. **Continue work** - `/mb-continue` resumes workflow
4. **Generate PRD** - `/mb-prd` for complex features
5. **Follow workflow** - `/mb-init` → `/mb-plan` → `/mb-do`

---

## 🔄 Can I Use Both?

**Yes!** Memory Bank files are 100% compatible.

**Example workflow:**
```bash
# Morning: Plan in Cursor IDE
Cursor> /van Add caching
Cursor> /plan

# Afternoon: Implement via Claude Code on server
ssh remote
claude
/mb-continue

# Evening: Review in Cursor IDE
Cursor> /reflect
Cursor> /archive
```

All using the same `memory-bank/` files! 🎉

---

## 📚 Next Steps

### For Cursor Users
- **Full Guide**: [README.md](README.md)
- **Command Reference**: [COMMANDS_README.md](COMMANDS_README.md)
- **Migration**: [COMMANDS_MIGRATION.md](COMMANDS_MIGRATION.md)

### For Claude Code Users
- **Full Guide**: [CLAUDE_CODE_SETUP.md](CLAUDE_CODE_SETUP.md)
- **Command Reference**: [.claude/commands/README.md](.claude/commands/README.md)
- **Workflows**: [.claude/workflows/workflow-overview.md](.claude/workflows/workflow-overview.md)

### For Both
- **Platform Comparison**: [PLATFORM_COMPARISON.md](PLATFORM_COMPARISON.md)
- **Project Structure**: [PROJECT_STRUCTURE.md](PROJECT_STRUCTURE.md)
- **Optimizations**: [MEMORY_BANK_OPTIMIZATIONS.md](MEMORY_BANK_OPTIMIZATIONS.md)

---

## ❓ Need Help?

**Cursor IDE:**
- Type `/help` in chat
- Check `.cursor/commands/README.md`
- Review [README.md](README.md)

**Claude Code:**
- Type `/help` in Claude Code (system help)
- Read [CLAUDE_CODE_SETUP.md](CLAUDE_CODE_SETUP.md)
- Read [.claude/commands/README.md](.claude/commands/README.md)

**General:**
- [PLATFORM_COMPARISON.md](PLATFORM_COMPARISON.md) - Detailed comparison
- GitHub Issues - Report problems
- Community forums - Ask questions

---

**Version**: Memory Bank System v2.0
**Last Updated**: 2025-01-14

**Ready to start?** Pick your platform above and follow the quick start! 🚀
