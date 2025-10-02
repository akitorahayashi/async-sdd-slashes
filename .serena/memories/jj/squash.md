## jj squash - Consolidate changes, integrate modifications

### Command: Squash to parent (default)
```bash
# Move changes from current commit to parent
jj squash -r <revision>
```

### Command: Squash between specific commits
```bash
# Move changes from source to target
jj squash --from <source_commit> --into <target_commit>

# Multiple sources
jj squash --from commit1 --from commit2 --into target

# Squash specific files only
jj squash --from source --into target file1 file2
```

### Command: Control commit message
```bash
# Specify new message
jj squash -m "Combined changes"

# Use destination message
jj squash --use-destination-message
```

### squash vs new (merge)
- **`jj new A B`**: Merge commits, create new commit (preserves both parents)
- **`jj squash`**: Move changes, source becomes empty (linear history)

**Note:** Empty commits after squash are automatically abandoned unless `--keep-emptied` is used.