## jj git init - Initialize existing Git project, colocated repository

### Command: Recommended initialization (coexist with Git)
```bash
jj git init --colocate
```
- `--colocate`: Coexist .git and .jj in the same directory (recommended)
- Automatically import existing Git commits
- Can mix use jj and git commands

### Command: Specify external Git repository
```bash
jj git init --git-repo=<path/to/git/repo>
```

### Advantages of colocated repository
- Existing Git toolchain (IDE, build tools) works as is
- Can introduce Jujutsu features gradually
- Import Git's HEAD, share working copy
- **Automatic sync**: Every jj command automatically synchronizes with Git

**Note:** Git staging area and merge conflict states are ignored. For large repositories, use `jj util gc` to improve performance.