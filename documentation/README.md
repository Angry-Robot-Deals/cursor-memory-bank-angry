# Project documentation

Documentation that does **not** live in agent config folders (`.cursor`, `.claude`) so agents do not load it as rules.

## Contents

- **`claude/`** – Claude Code: setup, installation, command reference, quick start
  - `README.md` – Overview of .claude layout (6 agents, 7 skills, 10 commands including /mb-compliance)
  - `INSTALLATION_GUIDE.md` – Installing Memory Bank (Claude)
  - `commands-reference.md` – Slash commands (/mb-prd, /mb-init, /mb-plan, /mb-design, /mb-do, /mb-compliance, /mb-reflect, /mb-archive, /mb-status, /mb-continue)
  - `COMMANDS_QUICK_START.md` – Quick start for commands
  - `guides-README.md` – Guides placeholder
- **`cursor/`** – Cursor IDE: command reference (documentation only)
  - `commands-reference.md` – Overview of /van, /plan, /build, /compliance, /reflect, /archive, etc.
- **`archive/`** – Archived task docs (if used)
- **`historical/`** – Historical docs (if used)

Agent config stays in `.cursor/` and `.claude/`; only rules, commands, and minimal pointers (e.g. `DOCS.txt`) remain there.
