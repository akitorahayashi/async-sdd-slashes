## jj resolve - Conflict resolution, interactive merge, conflict detection

### Command: List conflicts (machine parsable)
```bash
jj resolve --list
```
**Output format:** `<filepath>    <conflict-type>` (tab/space separated, one per line)

### Command: Interactive conflict resolution
```bash
# Resolve specific file with external merge tool
jj resolve <filename>

# Resolve all conflicts sequentially
jj resolve

# Use specific merge tool
jj resolve --tool <NAME>

# Resolve multiple files
jj resolve file1 file2

# Use fileset notation
jj resolve "glob:**/*.rs"
```

### Command: Manual conflict resolution
**No `--mark` command needed.** Simply edit conflict markers and save file. Jujutsu automatically detects resolution.

### Conflict marker format
```
<<<<<<< Conflict 1 of 1
%%%%%%% Changes from base to side #1
-old_line
+new_line
+++++++ Contents of side #2
ANOTHER_VERSION
>>>>>>> Conflict 1 of 1 ends
```

**Note:** Conflicts can coexist with commits. No need to resolve immediately. Partial conflict resolution is supported.