# AGENTS.md Guide

Use this reference before creating or updating `AGENTS.md`.

## Purpose

`AGENTS.md` should provide durable project instructions that Codex and other agents can load at the start of a session.

## Rules

- Capture repository-specific commands and conventions.
- Keep instructions durable and concise.
- Do not duplicate generic Codex behavior.
- Include safety notes only when they are specific to the project.
- Preserve existing user-authored instructions.
- Link to authority documents instead of duplicating them.

## Harness Pointer

Prefer a short harness pointer in `AGENTS.md` and put detailed harness history in `docs/harness/CHANGELOG.md` when the repo has docs.

Example:

```markdown
## Harness

Use the project harness when the user asks for repository workflow design, reusable Codex skills, automation suggestions, or harness maintenance.

Details:
- `docs/harness/overview.md`
- `docs/harness/CHANGELOG.md`
```

If the repo has no docs folder and the user wants a tiny harness, a short change table in `AGENTS.md` is acceptable.

## Avoid

- Long generated inventories that duplicate the filesystem
- Claude-only runtime commands
- Hidden recurring automation rules without user approval
- Broad claims that every task must use the harness
