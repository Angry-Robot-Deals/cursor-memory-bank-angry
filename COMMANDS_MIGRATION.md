# Migration Guide: Custom Modes to Cursor 2.0 Commands

This document explains the migration from Cursor custom modes to Cursor 2.0 commands feature.

## Overview

The Memory Bank system previously used Cursor's custom modes feature, which has been deprecated. All workflows have been ported to Cursor 2.0's commands feature, which provides similar functionality with improved integration.

## What Changed

### Before (Custom Modes)
- Custom modes were configured in Cursor settings
- Each mode had its own instruction file in `custom_modes/`
- Modes were selected from a dropdown in the chat interface

### After (Commands)
- Commands are defined as Markdown files in `.cursor/commands/`
- Commands are triggered with `/` prefix in chat (e.g., `/van`)
- Same functionality, better integration with Cursor 2.0

## Command Mapping

| Old Custom Mode | New Command | Purpose |
|----------------|-------------|---------|
| VAN Mode | `/van` | Initialization & entry point |
| PLAN Mode | `/plan` | Task planning |
| CREATIVE Mode | `/creative` | Design decisions |
| BUILD Mode | `/build` | Code implementation |
| REFLECT Mode | `/reflect` | Task reflection |
| ARCHIVE Mode | `/archive` | Task archiving |

## Key Features Preserved

✅ **Progressive Rule Loading** - Commands still load rules progressively to optimize context  
✅ **Memory Bank Integration** - All commands read from and update `memory-bank/` directory  
✅ **Complexity-Based Workflows** - Level 1-4 workflows are preserved  
✅ **Mode Transitions** - Commands guide you to the next appropriate command  

## How to Use Commands

1. **Type `/` in the chat input** to see available commands
2. **Select a command** or type the command name (e.g., `/van`)
3. **Follow the workflow** - each command will guide you to the next step

## Example Workflow

```
1. /van "Initialize project for adding user authentication"
   → Determines Level 3 complexity
   → Routes to /plan

2. /plan
   → Creates detailed implementation plan
   → Identifies components needing creative phases
   → Routes to /creative

3. /creative
   → Explores design options for flagged components
   → Documents design decisions
   → Routes to /build

4. /build
   → Implements planned changes
   → Tests implementation
   → Routes to /reflect

5. /reflect
   → Reviews completed implementation
   → Documents lessons learned
   → Routes to /archive

6. /archive
   → Creates archive document
   → Updates Memory Bank
   → Ready for next task
```

## File Structure

```
.cursor/
  commands/
    van.md          # Initialization command
    plan.md         # Planning command
    creative.md     # Design command
    do.md           # Implementation command
    reflect.md      # Reflection command
    archive.md      # Archiving command
    README.md       # Commands documentation

custom_modes/       # Legacy files (kept for reference)
  van_instructions.md
  plan_instructions.md
  creative_instructions.md
  implement_instructions.md
  reflect_archive_instructions.md
```

## Benefits of Commands

1. **Better Integration** - Commands are native to Cursor 2.0
2. **Easier Discovery** - Type `/` to see all available commands
3. **Simpler Setup** - No need to configure custom modes in settings
4. **Same Functionality** - All workflows preserved exactly as before

## Migration Checklist

- [x] Create `.cursor/commands/` directory
- [x] Port VAN workflow to `/van` command
- [x] Port PLAN workflow to `/plan` command
- [x] Port CREATIVE workflow to `/creative` command
- [x] Port IMPLEMENT workflow to `/build` command
- [x] Port REFLECT workflow to `/reflect` command
- [x] Port ARCHIVE workflow to `/archive` command
- [x] Preserve progressive rule loading
- [x] Maintain Memory Bank integration
- [x] Create documentation

## Next Steps

1. **Test each command** to ensure they work correctly
2. **Remove custom modes** from Cursor settings (if still configured)
3. **Update project documentation** to reference commands instead of modes
4. **Train team members** on using commands instead of modes

## Support

If you encounter any issues with the commands, check:
- `.cursor/commands/README.md` for command documentation
- `memory-bank/tasks.md` for current task status
- Original `custom_modes/` files for reference (if needed)

