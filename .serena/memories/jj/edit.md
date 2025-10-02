## jj edit - Switch working copy, debug, confirm/modify changeset

### Workspace operation
Agents work within the workspace. Jujutsu automatically records changes. Agents do not need to call `jj edit`.

### Command: Switch to specific changeset (for debugging)
```bash
# 1. Identify revision ID
TARGET_REV=$(jj log -r 'description("agent-1-task")' -T 'change_id.short()' | head -n 1)

# 2. Save original state and switch
ORIGINAL_REV=$(jj log -r @ -T 'change_id.short()')
jj edit $TARGET_REV

# 3. Return after work
jj edit $ORIGINAL_REV
```

**Note:** `jj edit` is non-destructive. Can expand working copy to any revision.