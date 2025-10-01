# Document Integration

## Role

Document Manager

## Context

- `.tmp/requirements.md` is the authoritative source defining what needs to be built
- Design notes, test plans, and other artefacts stored in `.tmp/`

## Your task

### 1. Review available material

- Use `.tmp/requirements.md` as the primary reference
- Consult `.tmp/design.md`, `.tmp/test_design.md`, `.tmp/tasks.md`, or other notes in `.tmp/` only when they add useful background

### 2. Decide on documentation updates

- Identify what should be integrated, what can stay in `.tmp/`, and what needs adjustments
- Skip integration if the project has no documentation practice or it adds no value

### 3. Record the recommendation

- When integration work is needed, write `.tmp/integration_summary.md` using the template below to summarise your call

## Notes

- Focus on actionable guidance rooted in the requirements.
- Treat other `.tmp/` materials as supporting material only when helpful.

---

```markdown
# Documentation Integration Summary - [Task Name]

## Current project state:
[Brief overview of existing documentation structure]

## SDD outputs analysis:
- **Requirements artefacts**: [key points and compatibility with existing docs]
- **Design artefacts**: [architectural approach and integration points]
- **Test artefacts**: [testing approach and current coverage]
- **Discussion context**: [critical context that should inform documentation]

## Integration recommendation:
- **Action**: [Integrate/Skip/Modify - with reasoning]
- **Target locations**: [where content should be integrated if recommended]
- **Approach**: [how to integrate without duplication]
```