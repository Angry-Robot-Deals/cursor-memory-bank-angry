# Memory Bank Commands

This directory contains Cursor 2.0 commands that replace the deprecated custom modes feature. Each command implements a specific phase of the Memory Bank workflow with progressive rule loading to optimize context usage.

**Version 2.0**: Commands now integrate with MCP servers (context7 and sys8) for enhanced accuracy and security.

**MCP Servers**:
- **context7**: [https://github.com/upstash/context7](https://github.com/upstash/context7) - Library documentation
- **sys8**: [https://github.com/Angry-Robot-Deals/mcp-sys8](https://github.com/Angry-Robot-Deals/mcp-sys8) - System operations

## Available Commands

### `/van` - Initialization & Entry Point
**Purpose:** Initialize Memory Bank, detect platform, determine task complexity, and route to appropriate workflows.

**When to use:** 
- Starting a new task or project
- Initializing Memory Bank structure
- Determining task complexity

**Next steps:**
- Level 1 tasks → `/do`
- Level 2-4 tasks → `/plan`

### `/plan` - Task Planning
**Purpose:** Create detailed implementation plans based on complexity level.

**When to use:**
- After `/van` determines Level 2-4 complexity
- Need to create structured implementation plan

**Next steps:**
- Creative phases identified → `/creative`
- No creative phases → `/do`

### `/creative` - Design Decisions
**Purpose:** Perform structured design exploration for components requiring creative phases.

**When to use:**
- After `/plan` identifies components needing design decisions
- Need to explore architecture, UI/UX, or algorithm options

**Next steps:**
- After all creative phases complete → `/do`

### `/do` - Code Implementation
**Purpose:** Implement planned changes following the implementation plan and creative decisions with AI Quality Rules.

**When to use:**
- After planning is complete (and creative phases if needed)
- Ready to start coding

**What it does:**
- Applies test-driven development (TDD) approach
- Enforces method size limits (max 50 lines)
- Manages cognitive load (7±2 objects per method)
- Follows iterative development cycle
- Applies relevant AI Quality Rules automatically

**Next steps:**
- After implementation complete → `/reflect`

### `/reflect` - Task Reflection
**Purpose:** Facilitate structured reflection on completed implementation.

**When to use:**
- After `/do` completes implementation
- Need to document lessons learned and process improvements

**Next steps:**
- After reflection complete → `/archive`

### `/archive` - Task Archiving
**Purpose:** Create comprehensive archive documentation and update Memory Bank.

**When to use:**
- After `/reflect` completes reflection
- Ready to finalize task documentation

**Next steps:**
- After archiving complete → `/van` (for next task)

### `/status` - Check Current Status
**Purpose:** Check the status of the current task and workflow progress.

**When to use:**
- Anytime you want to see current task status
- After returning to a project
- To understand where you are in the workflow

**What it shows:**
- Current task ID and description
- Complexity level
- Current phase
- What's completed, what's remaining
- Suggested next steps

### `/continue` - Continue Current Task
**Purpose:** Resume work on the current task from the last checkpoint.

**When to use:**
- After a break or interruption
- When resuming work on an active task
- To automatically determine and continue from current phase

**What it does:**
- Reads current task state
- Determines current phase
- Automatically resumes work in appropriate phase
- Shows context of where you left off

## Command Workflow

### Main Workflow
```
/van → /plan → /creative → /do → /reflect → /archive
  ↓       ↓        ↓         ↓         ↓          ↓
Level 1  Level   Level    Level    Level     Level
tasks    2-4     3-4      1-4      1-4       1-4
```

### Helper Commands
```
/status   - Check current task status (anytime)
/continue - Resume work from current phase (anytime)
```

## Progressive Rule Loading

Each command implements progressive rule loading to optimize context usage:

1. **Core Rules** - Always loaded (main.mdc, memory-bank-paths.mdc)
2. **Mode-Specific Rules** - Loaded based on command (mode maps)
3. **Complexity-Specific Rules** - Loaded based on task complexity level
4. **Specialized Rules** - Lazy loaded only when needed (e.g., creative phase types)

This approach reduces initial token usage by ~70% compared to loading all rules at once.

## Memory Bank Integration

All commands read from and update files in the `memory-bank/` directory:

- **tasks.md** - Source of truth for task tracking
- **activeContext.md** - Current project focus
- **progress.md** - Implementation status
- **projectbrief.md** - Project foundation
- **creative/** - Creative phase documents
- **reflection/** - Reflection documents
- **archive/** - Archive documents

## Usage Examples

### Starting a New Task
```
/van Initialize project for adding user authentication feature
```

### Planning a Feature
```
/plan
```

### Exploring Design Options
```
/creative
```

### Implementing Changes
```
/do
```

### Reflecting on Completion
```
/reflect
```

### Archiving Completed Task
```
/archive
```

### Checking Task Status
```
/status
```

### Resuming Work
```
/continue
```

## Migration from Custom Modes

These commands replace the previous custom modes:
- **VAN Mode** → `/van` command
- **PLAN Mode** → `/plan` command
- **CREATIVE Mode** → `/creative` command
- **BUILD Mode** → `/do` command (renamed for clarity)
- **REFLECT Mode** → `/reflect` command
- **ARCHIVE Mode** → `/archive` command

The functionality remains the same, but now uses Cursor 2.0's commands feature instead of custom modes.

## MCP Server Setup

### Required MCP Servers

Memory Bank v2.0 integrates with two MCP servers for optimal functionality:

#### context7 MCP Server
**Purpose**: Library documentation and code examples

**Required For**:
- All library/framework/package-related tasks
- API documentation needs
- Code example requirements
- Version-specific documentation

**Tools Provided**:
- `resolve-library-id`: Resolves library names to Context7-compatible IDs
- `get-library-docs`: Retrieves up-to-date library documentation

**Where to Find**:
- Search GitHub for "context7 MCP server"
- Check official MCP server registry
- Check Cursor community resources

#### sys8 MCP Server
**Purpose**: System operations

**Required For**:
- Date and time operations
- Operating system information
- Mathematical calculations
- Random string generation
- String hashing operations

**Tools Provided**:
- `get_current_datetime`: Secure date/time operations
- `get_os_version`: Cross-platform OS information
- `calculate_math_expression`: Safe mathematical evaluation
- `random_string`: Cryptographically secure random strings
- `hash_string`: Secure string hashing

**Where to Find**:
- Search GitHub for "sys8 MCP server"
- Check official MCP server registry
- Check Cursor community resources

### Configuration

MCP servers are configured in Cursor's MCP settings. Configuration can be:
- Project-specific: `.cursor/mcp.json`
- Global: Cursor settings

#### Example Configuration

```json
{
  "mcpServers": {
    "context7": {
      "command": "npx",
      "args": ["-y", "@context7/mcp-server"]
    },
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

**Note**: Actual installation commands may vary. Check the specific MCP server documentation for exact setup instructions.

### Benefits

- **Accuracy**: Up-to-date documentation and secure operations
- **Security**: Cryptographically secure random strings and hashing
- **Consistency**: Unified interface for system operations
- **Error Prevention**: Built-in validation prevents common mistakes
- **Version Support**: Exact library version documentation

### Troubleshooting

If MCP servers are not available:
- Memory Bank will continue to work but with reduced functionality
- Library documentation may be outdated
- System operations may use less secure methods
- Check MCP server configuration in Cursor settings
- Verify MCP servers are installed and accessible

