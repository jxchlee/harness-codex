# Harness Plan Format

Use this reference before proposing a harness plan.

## Required Fields

Keep the plan short enough for the user to review. Include:

- audit result and selected run mode
- project summary
- detected commands
- repeated workflows or risky areas
- proposed `AGENTS.md` guidance
- proposed skills
- subagent guidance only if requested or clearly useful
- optional automation recipes
- files to create or edit
- narrow verification command

## Plan Template

```markdown
**Harness Plan**

- Run mode: New build | Extension | Maintenance | Migration
- Project summary: ...
- Detected commands: ...
- Proposed guidance: ...
- Proposed skills: ...
- Optional automation: ...
- Files to change: ...
- Verification: ...
```

## Planning Rules

- Plan before broad edits.
- Prefer one useful skill over many speculative skills.
- Keep generated files small and reviewable.
- Preserve existing user-authored instructions.
- If implementation is not explicitly requested, stop at the plan.
