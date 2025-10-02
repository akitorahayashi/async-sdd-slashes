## jj new - Create new changeset, start parallel work, obtain revision ID

### Command: Non-interactive changeset creation
```bash
jj new main --no-edit -m "description"
```
- `--no-edit`: No working copy switching (mandatory for scripts and non-interactive execution)
- `-m`: Specify changeset description directly

### Command: Create changeset for parallel agents (same parent)
```bash
jj new main --no-edit -m "agent1 task"
jj new main --no-edit -m "agent2 task"
jj new main --no-edit -m "agent3 task"
```

### Command: Obtain revision ID (change ID)
```bash
NEW_CHANGE_ID=$(jj log -r @ --no-graph -T 'change_id.short()')
```
**Note:** `jj new` does not directly output JSON. Parse standard error output or obtain afterwards with `jj log`. Change ID is immutable, unlike commit ID.