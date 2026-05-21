# AGENTS.md Base Template

Use this template as a starting point. Preserve existing project instructions and merge only the sections that fit.

```markdown
# Agent Instructions

## Project Scope

- Describe the product or repository in one sentence.
- Name the main source directories.
- Name any directories that are experiments, generated output, or non-authority examples.

## Authority And References

- List the documents or files that should be read before planning.
- Prefer links to source-of-truth documents over copied policy text.
- State whether README files are authoritative or only entry points.

## Build And Verification

- Standard build command:
  ```powershell
  <build command>
  ```
- Standard test command:
  ```powershell
  <test command>
  ```
- Run the narrowest meaningful verification for the active change.

## Editing Rules

- Preserve user changes.
- Keep unrelated work out of the current change.
- Follow existing project structure and naming.
- Do not introduce secrets into committed files.

## Harness

Use the project harness when the user asks for repository workflow design, reusable Codex skills, automation suggestions, or harness maintenance.

Harness details:
- `docs/harness/overview.md`
- `docs/harness/CHANGELOG.md`
```

## Notes

If the target repository already has an `AGENTS.md`, do not replace it wholesale. Add only the missing durable guidance or a short harness pointer.
