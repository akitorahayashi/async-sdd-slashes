## jj bookmark - Create Git commits in colocated repository, manage linear history

### Command: Create Git commit for phase (colocated mode)
```bash
# After phase merge and fixes
jj bookmark create phase-1

# Push to create Git commit
jj git push --bookmark phase-1
```

### Command: Build linear phase history
```bash
# Phase 1
jj new main --no-edit -m "Phase 1 integration"
jj bookmark create phase-1

# Phase 2 (build on Phase 1, not main)
jj new phase-1 --no-edit -m "Phase 2 integration"
jj bookmark create phase-2

# Phase 3 (build on Phase 2)
jj new phase-2 --no-edit -m "Phase 3 integration"
jj bookmark create phase-3
```

### Command: Alternative - Move main bookmark forward
```bash
# After each phase completion
jj bookmark move main --to @

# Next phase builds on updated main
jj new main --no-edit -m "Next phase"
```

### Command: Create PR with all phase commits
```bash
# After all phases complete
jj bookmark create feature-complete
jj git push --bookmark feature-complete
```

**Note:** In colocated repos, bookmarks automatically create corresponding Git branches. Each phase becomes a separate Git commit with preserved commit message.