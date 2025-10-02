## jj rebase - Adjust dependencies, update base branch

### Command: Rebase to latest main
```bash
# Rebase current commit to main
jj rebase -d main

# Rebase specific commit to main
jj rebase -s <phase_commit> -d main
```

### Command: Rebase subtree
```bash
# Rebase commit and all descendants
jj rebase -s <commit> -d <new_parent>
```

### Automatic descendant rebasing
**Descendants are automatically rebased** when parent is rebased. No manual intervention needed for Phase 2, 3, etc.

### Conflict handling during rebase
**Rebase always succeeds, even with conflicts.** Conflicts are recorded in commits:
1. Rebase completes with conflicts recorded
2. Create fix commit: `jj new <conflicted_commit>`
3. Resolve conflicts
4. Squash fix into conflicted commit: `jj squash`

**No `--continue` command needed.** Unified conflict resolution workflow.

**Note:** This design allows flexible conflict resolution timing without blocking rebase operations.