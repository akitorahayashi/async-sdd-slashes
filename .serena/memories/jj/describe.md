## jj describe - Update changeset description, record agent work, multi-line messages

### Recording agent work: describe vs commit
**Always use `jj describe` when agent work is completed**
- `jj describe`: Update metadata of current changeset (optimal for recording agent work)
- `jj commit`: Create new changeset (inappropriate to use after agent completion, generates empty changeset)

### Command: Record multi-line message
```bash
AGENT_REPORT=$'Task completion report\n\n- File A modification completed\n- Module B added'
jj describe -m "$AGENT_REPORT"
```
**Note:** Use `$'...\n...'` syntax (bash/zsh) to include line breaks.