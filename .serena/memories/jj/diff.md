## jj diff - View changes, pre-merge check, conflict detection, change summary

### Command: Get specific changeset changes
```bash
# View changeset changes
jj diff -r $AGENT1_ID

# Git format
jj diff -r $AGENT1_ID --git

# Statistics only
jj diff -r $AGENT1_ID --stat

# File names only
jj diff -r $AGENT1_ID --name-only

# Specific file
jj diff -r $AGENT1_ID path/to/file
```

### Command: Pre-merge difference check between changesets
```bash
# Compare differences between changesets
jj interdiff --from $AGENT1_ID --to $AGENT2_ID

# File list only (check for conflict possibility)
jj interdiff --from $AGENT1_ID --to $AGENT2_ID --name-only

# Statistics
jj interdiff --from $AGENT1_ID --to $AGENT2_ID --stat
```

### Command: Post-merge conflict detection
```bash
# List conflict files (machine parsable)
jj resolve --list

# View conflict content
jj diff --git
```

### Command: Post-integration change summary
```bash
# Statistics of changes from main (file count, line count, etc.)
jj diff --from main --to @ --stat

# Detailed view
jj diff --from main --to @ --git

# File list only
jj diff --from main --to @ --name-only

# Type changes
jj diff --from main --to @ --types
```

**Note:** jj treats working copy as a commit, referenced by `@`. `--stat` provides equivalent functionality to Git.