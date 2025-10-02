## jj log - Monitor progress, JSON output, head filtering, revset

### Command: Obtain log in JSON format (all revisions)
```bash
jj log -r "all()" --no-graph -T 'json{
  "change_id": change_id.short(),
  "commit_id": commit_id.short(),
  "parents": parents.map(|c| c.commit_id().short()),
  "description": description,
  "author": author,
  "timestamp": committer.timestamp()
}'
```
- `-r "all()"`: Target all revisions
- `--no-graph`: Disable graph display (for parsing)
- `-T 'json{...}'`: Specify JSON template

### Command: Filter only heads (agent final deliverables)
```bash
jj log -r "heads(all())" --no-graph -T 'json{...}'
```
- `heads(all())`: Select only revisions with no children (heads)

**Note:** Template functions: `author.email()`, `description.first_line()`, etc. are available.