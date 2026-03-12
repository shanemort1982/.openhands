---
name: safe-file-editing
type: repo
version: 1.0.0
agent: CodeActAgent
---

# Safe File Editing Rules

## CRITICAL: No Large File Rewrites

When editing files, especially HTML, CSS, JS, and other frontend files:

1. **NEVER rewrite entire files in a single operation.** Do not use `create` to replace an existing file. Do not use a single `str_replace` that replaces more than ~100 lines at once.

2. **Always use small, targeted `str_replace` edits.** Each edit should change 5-30 lines. If a file needs 10+ changes, make them as 10 separate `str_replace` calls.

3. **NEVER delete and recreate a file** to rewrite it. Always edit in place with small incremental changes.

4. **If you need to make many changes to a large file**, break them into multiple small edits across multiple tool calls. This is safer and prevents crashes.

5. **Before editing, verify context.** Use `view` with line ranges to see the exact lines you need to change, then craft precise `str_replace` calls with enough context for unique matching.

## Why This Matters

Large file operations can cause agent crashes, wasting the user's time and compute. Small edits are:
- More reliable (less likely to crash)
- Easier to verify (user can review each change)
- Safer to undo (if something goes wrong)