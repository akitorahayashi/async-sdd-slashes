# Break Down Tasks

## Role

Engineering Manager

## Context

- `.tmp/requirements.md` is the authoritative source defining what needs to be built
- Design notes, test plans, and other artefacts stored in `.tmp/`

## Your task

### 1. Gather the inputs

- Start from `.tmp/requirements.md` as the core brief
- Use `.tmp/design.md`, `.tmp/test_design.md`, or other notes in `.tmp/` only to supplement the plan when they exist

### 2. Design phases and agent usage

- Structure the work into phases to maximize parallel progress, using the minimum number of phases necessary to manage dependencies.
- Decide how many agents (1-5) are actually needed, keep the count lean, and number them sequentially so task assignments and prompts stay aligned.
- Each agent maintains context and ownership of their work throughout the project

### 3. Build `.tmp/tasks.md`

- Compose the breakdown using the template at the end of this command.
- Maximize opportunities for parallel work - agents can work simultaneously even on shared files.
- Note any critical coordination points between phases if needed.

---

## Example: .tmp/tasks.md Template

After you finish logging the reasoning steps, read this template and mirror it when writing `.tmp/tasks.md`. Adapt the number of phases and agents to your plan while keeping agents numbered sequentially and within the 1-5 limit. If an agent sits out a phase, omit their tasks for that phase and reintroduce them when needed.

```markdown
# Task Breakdown - [Task Name]

## Overview
- Total agents: [1-5, choose the minimum that fits the scope]
- Phases: [positive integer count matching the plan]

## All Tasks Summary

Fill in each phase using the ownership decisions captured in `.tmp/tasks.think.md`. Use the `- [ ] [Task summary] (Agent X)` format for every line.

Before any agent begins, ensure they do all of the following:
- Read `.tmp/requirements.md` for the definitive brief.
- Review the relevant sections in `.tmp/design.md` for implementation details and file paths.
- Study this file (`.tmp/tasks.md`) to understand sequencing and ownership.
- Work in parallel with other agents - the orchestrator will handle any conflicts that arise.
- Adhere to existing project conventions.
- update `.tmp/tasks.md` checkboxes with ✅ for completed tasks in your task.

### Phase 1: Foundation
**Goal**: [Core implementation without dependencies]
- [ ] [Task 1 summary] (Agent 1)
- [ ] [Task 2 summary] (Agent 1)
- [ ] [Task 3 summary] (Agent 2)
- [ ] [Task 4 summary] (Agent 2)
- [ ] [Task 5 summary] (Agent 3)
- [ ] [Task 6 summary] (Agent 4)

### Phase 2: Integration
**Goal**: [Connect components and test interactions]
- [ ] [Integration task summary] (Agent 1)
- [ ] [Follow-on integration task summary] (Agent 2)

### Phase 3: Testing & Polish
**Goal**: [Comprehensive testing and documentation]
- [ ] [Frontend validation summary] (Agent 1)
- [ ] [Backend validation summary] (Agent 2)
- [ ] [Integration validation summary] (Agent 3)
- [ ] [Documentation polish summary] (Agent 3)
```