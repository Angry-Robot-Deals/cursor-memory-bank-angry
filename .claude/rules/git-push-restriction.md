# Git Push Restriction Rule

## 🚨 CRITICAL: Never Push Without Explicit User Request

**Version**: 2.0.0
**Last Updated**: 2025-01-19
**Priority**: CRITICAL

## The Rule

**NEVER execute `git push` unless the user explicitly requests it.**

## Why This Rule Exists

1. Give user full control over when code is pushed to remote
2. Allow user to review commits before they become public
3. Prevent accidental pushes that might break CI/CD pipelines
4. Allow user to amend, rebase, or squash commits before pushing
5. Prevent pushing sensitive information accidentally

## What IS Allowed (Without Permission)

✅ You MAY execute these git commands:
- `git status` - Check repository status
- `git diff` - View changes
- `git log` - View commit history
- `git add` - Stage files
- `git commit` - Commit changes locally
- `git branch` - Manage branches
- `git checkout` / `git switch` - Switch branches
- `git reset` - Unstage or undo commits locally
- `git stash` - Temporarily save changes

## What IS NOT Allowed (Without Permission)

❌ You MUST NOT execute these without explicit user request:
- `git push` - Push to remote
- `git push origin <branch>` - Push specific branch
- `git push -f` / `git push --force` - Force push
- `git push --all` - Push all branches
- Any command that transfers commits to remote repository

## Valid User Requests for Push

User MUST explicitly say one of these (or similar):
- "push the changes"
- "git push"
- "push to remote"
- "commit and push"
- "deploy the changes" (in git context)

## Invalid Implicit Requests

These do NOT count as explicit push requests:
- "commit the changes" → Only commit, DON'T push
- "save the changes" → Only commit, DON'T push
- "finish the task" → Only commit, DON'T push
- "done" → Only commit, DON'T push

## Examples

### ✅ CORRECT: User asks only to commit

**User**: "Commit the changes"

**You should**:
1. `git add -A`
2. `git commit -m "..."`
3. **STOP HERE** - Do not push

### ✅ CORRECT: User explicitly asks to push

**User**: "Commit and push"

**You should**:
1. `git add -A`
2. `git commit -m "..."`
3. `git push origin <branch>` ← OK, user explicitly requested

### ❌ WRONG: Auto-pushing without permission

**User**: "Commit the changes"

**You should NOT**:
1. `git add -A`
2. `git commit -m "..."`
3. ~~`git push origin <branch>`~~ ← WRONG! User didn't ask for push

## Asking for Permission

If unsure whether to push, you MAY ask:

**Example**:
> "Changes committed locally. Would you like me to push them to the remote repository?"

Then wait for user response.

## Integration with Memory Bank

When documenting commits in Memory Bank files:
- Record commit hashes
- Note that changes are "committed locally"
- Do NOT record push status unless user explicitly requested push

## Enforcement

This rule is **MANDATORY** and **NON-NEGOTIABLE**.

Violation could result in:
- Unwanted code in remote repository
- Broken CI/CD pipelines
- Conflicts with team members' work
- Loss of ability to rewrite commit history

## References

- Cursor equivalent: `.cursor/rules/git-push-restriction.mdc`
