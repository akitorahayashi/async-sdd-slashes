## jj op / jj operation - Track operation history, audit, detect agent completion

### Command: Obtain operation log in JSON format
```bash
jj op log -T 'json{
  "id": id,
  "user": user,
  "hostname": hostname,
  "start_time": start_time,
  "end_time": end_time,
  "description": description,
  "tags": tags
} ++ "\n"'
```
- `id`: Unique ID of operation
- `user`, `hostname`: Executing user/host (identify agent/workspace)
- `description`: Detailed executed command (e.g., `describe commit 1234abcd`)
- `tags`: Operation tags (e.g., `workspace_id`)

### Detecting agent operation completion: op log vs log
**`jj op log` is the most reliable**
- `jj log`: Commit state history (difficult to determine operation completion timing)
- `jj op log`: Records all operation history (foundation of concurrent processing model, reliable completion detection)

**Detection method:** Poll `jj op log`, confirm new log where `hostname`/`tags` match agent, and `description` includes target operation.