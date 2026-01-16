# MCP Server Integration Rules

**Priority**: MANDATORY

All Memory Bank workflows MUST use MCP (Model Context Protocol) servers before any work.

## Required MCP Servers

### 1. sys8 MCP Server (System Operations)

**Purpose**: Secure system operations

**Required Tools**:
- `get_current_datetime` - For ALL date/time fields in Memory Bank documents
- `get_os_version` - For platform-specific decisions
- `calculate_math_expression` - For safe math operations
- `random_string` - For cryptographically secure random strings
- `hash_string` - For secure hashing

**NEVER**:
- ❌ Use JavaScript `new Date()` or `Date.now()`
- ❌ Hardcode dates or timestamps
- ❌ Use Node.js `os` module directly
- ❌ Use `Math.random()` for security-sensitive operations

**ALWAYS**:
- ✅ Call sys8 `get_current_datetime` for timestamps
- ✅ Call sys8 `get_os_version` for OS information
- ✅ Use sys8 tools for all system operations

---

### 2. context7 MCP Server (Library Documentation)

**Purpose**: Up-to-date library documentation and code examples

**Required Tools**:
- `resolve-library-id` - Resolve library names to Context7 IDs
- `get-library-docs` - Get up-to-date library documentation

**NEVER**:
- ❌ Rely on outdated training data for library APIs
- ❌ Use generic or hallucinated API methods
- ❌ Assume library APIs based on old versions

**ALWAYS**:
- ✅ Call `resolve-library-id` first to get correct library ID
- ✅ Call `get-library-docs` with resolved library ID
- ✅ Use fetched documentation for accurate code

---

## Integration Workflow

**Before ANY work in ANY phase**:

1. **Query sys8 MCP FIRST**:
   ```
   - Call get_current_datetime for current date/time
   - Call get_os_version for OS/platform info
   ```

2. **Query context7 MCP SECOND** (when libraries involved):
   ```
   - Call resolve-library-id for all libraries mentioned
   - Call get-library-docs for all libraries/frameworks used
   ```

3. **Include MCP Results in Context**:
   ```
   - All sys8 results (date/time, OS) must inform decisions
   - All context7 results (docs) must guide implementation
   ```

**This is MANDATORY - no exceptions.**

---

## Date/Time Stamp Requirements

When updating ANY timestamp fields in Memory Bank documents:

**Required Fields**:
- "Last Updated" in any Memory Bank document
- "Date Completed" in archive documents
- "Date Archived" in archive documents
- "Date" in reflection documents
- "Timestamp" in progress.md
- ANY other date/time fields

**Process**:
1. Call sys8 MCP `get_current_datetime` BEFORE writing timestamp
2. Use the datetime value returned by sys8 MCP
3. Format consistently using sys8 response formats

**Example**:
```
User: "Update tasks.md with current progress"

You should:
1. Call sys8 get_current_datetime
2. Get response: { datetime: "2025-01-14T20:30:00Z", ... }
3. Use in file: "Last Updated: 2025-01-14T20:30:00Z"
```

---

## Library Documentation Workflow

When implementing features using external libraries:

1. **Identify Libraries**:
   - User mentions library/framework/package
   - Implementation requires external dependencies

2. **Resolve Library ID**:
   ```
   Call context7 resolve-library-id with library name
   Get Context7-compatible library ID
   ```

3. **Fetch Documentation**:
   ```
   Call context7 get-library-docs with library ID
   Use mode='code' for APIs (default)
   Use mode='info' for concepts
   Specify topic parameter if needed
   ```

4. **Use Documentation**:
   - Write accurate code based on fetched docs
   - Use correct API methods (not hallucinated)
   - Follow version-specific patterns

---

## Error Handling

If MCP server tool call fails:

1. **Report Error**: Clearly inform user
2. **Don't Fall Back**: Do NOT silently use alternative methods
3. **Ask Permission**: Before using non-MCP approaches
4. **Document**: Why MCP was not used (if permission granted)

---

## Configuration

MCP servers are configured in Claude Code settings.

**Verify Configuration**:
```
User: "Are MCP servers configured?"

You should:
1. Check if sys8 tools are accessible
2. Check if context7 tools are accessible
3. Report configuration status
```

---

## Benefits

### sys8 MCP:
- ✅ Consistency across all system operations
- ✅ Security (cryptographic randomness, safe evaluation)
- ✅ Cross-platform compatibility
- ✅ Accurate timestamps

### context7 MCP:
- ✅ Up-to-date library APIs
- ✅ Version-specific documentation
- ✅ No API hallucinations
- ✅ Working code examples

---

## Examples

### Example 1: Creating PRD Document

```
User: "Generate a PRD for task DEV-001"

You should:
1. Call sys8 get_current_datetime → Get timestamp
2. Create PRD with "Created: {timestamp}"
3. If libraries mentioned, call context7 for docs
```

### Example 2: Implementing with React

```
User: "Implement user profile component with React hooks"

You should:
1. Call context7 resolve-library-id('react')
2. Call context7 get-library-docs with React ID, topic='hooks'
3. Use fetched hook documentation for accurate implementation
```

---

## References

- Full MCP integration rules: See `CLAUDE.md` section "MCP Server Integration"
- Cursor equivalents: `.cursor/rules/sys8-mcp-usage.mdc`, `.cursor/rules/context7-mcp-usage.mdc`
