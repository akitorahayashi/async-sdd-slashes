# Orchestrate Agent Execution

## Role

Engineering Manager

## Context

- `.tmp/requirements.md` defines the project scope
- `.tmp/tasks.md` contains the phase-based task breakdown
- `.tmp/prompts.md` contains activation prompts for each agent and phase

## Your task

### 0. Initialize environment

Checkout the target branch and initialize jj:
```bash
git checkout <target-branch>
jj git init --colocate
```

### 1. Prepare orchestration environment

- Read `.tmp/tasks.md` to understand phases, agent assignments, and dependencies
- Read `.tmp/prompts.md` to obtain activation prompts for each agent

### 2. Execute phases sequentially

For each phase in `.tmp/tasks.md`:

#### Phase initialization
Create parallel changesets for each active agent:
```bash
# For Phase 1, use 'main' as parent
# For Phase 2+, use previous phase bookmark (e.g., 'phase-1')
PARENT_BOOKMARK="main"  # or "phase-1", "phase-2", etc.

# Create changeset for each agent
jj new $PARENT_BOOKMARK --no-edit -m "Phase 1 Agent 1: [task description]"
AGENT1_ID=$(jj log -r @ --no-graph -T 'change_id.short()')

jj new $PARENT_BOOKMARK --no-edit -m "Phase 1 Agent 2: [task description]"
AGENT2_ID=$(jj log -r @ --no-graph -T 'change_id.short()')

jj new $PARENT_BOOKMARK --no-edit -m "Phase 1 Agent 3: [task description]"
AGENT3_ID=$(jj log -r @ --no-graph -T 'change_id.short()')
```

#### Agent activation
Activate agents in parallel by providing their prompts from `.tmp/prompts.md`

Monitor completion using operation log:
```bash
# Poll for agent completion
jj op log -T 'json{
  "hostname": hostname,
  "description": description,
  "end_time": end_time
} ++ "\n"'
```

#### Phase completion and integration
Once all agents complete, review and merge their work:
```bash
# Optional: Check for potential conflicts before merge
jj interdiff --from $AGENT1_ID --to $AGENT2_ID --name-only
jj interdiff --from $AGENT1_ID --to $AGENT3_ID --name-only

# Merge all agent changesets
jj new $AGENT1_ID $AGENT2_ID $AGENT3_ID -m "Phase 1 integration"

# Check for conflicts
jj resolve --list

# If conflicts exist, resolve them then verify
jj diff --git  # Review conflict resolution
```

After merge resolution:
- Verify build passes
- Run all tests

Record phase completion:
```bash
# Get change summary from main
jj diff --from main --to @ --stat

# Update checkboxes in .tmp/tasks.md with ✅ for completed agent tasks

# Create bookmark for this phase and push to Git
jj bookmark create phase-1
jj git push --bookmark phase-1
```

#### Before next phase
- Ensure build and tests succeed
- Git commit for this phase is now created
- Next phase will use `PARENT_BOOKMARK="phase-1"` in initialization

### 3. Final verification

- Run comprehensive build and test suite
- Verify all `.tmp/tasks.md` checkboxes are ✅

### 4. CodeRabbit review and refinement

Run AI code review with project context:
```bash
# --config provides additional instructions to CodeRabbit AI
# --type all reviews both committed and uncommitted changes
# --base main compares against main branch
coderabbit review --plain \
  --type all \
  --config .tmp/requirements.md \
  --config .tmp/design.md \
  --config .tmp/tasks.md \
  --base main
```

Review the output and if issues are identified:
- Create new phase with refinement tasks in `.tmp/tasks.md`
- Generate prompts in `.tmp/prompts.md` for fix agents
- Return to Step 2 to execute refinement phase (using last phase bookmark as parent)
- Re-run CodeRabbit review after fixes

Iterate until CodeRabbit review passes or issues are acceptable.

### 5. Create PR

After all phases complete and CodeRabbit review passes:
```bash
# Create final bookmark for PR
jj bookmark create feature-complete

# Push to create PR branch
jj git push --bookmark feature-complete
```

All phase commits are now in Git with linear history: `main -> phase-1 -> phase-2 -> ... -> feature-complete`

Create PR on GitHub/GitLab using the `feature-complete` branch.

## Notes

### jj Commands Reference
The snippets above cover basic orchestration workflow. **For detailed command options and advanced usage:** Use `mcp__serena__search_for_pattern` to search memories (e.g., "jj new --no-edit", "jj op log JSON", "revset", "heads()").

**If you need additional jj commands not covered above:** Stop execution and inform the user about the missing command/scenario so they can update the reference documentation.

### Workflow Principles
- Maximize parallelism within phases
- Use `jj op log` for reliable completion detection
- Handle conflicts at phase boundaries
- Every phase must pass build and tests before proceeding

