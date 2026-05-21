# Validation Checklist

Use this reference after generating or updating a project harness.

## File Structure

- `AGENTS.md` exists only when useful and does not duplicate large docs.
- Project-local skills live under `.agents/skills/*/SKILL.md` or the repo's existing Codex skill location.
- Harness docs live under `docs/harness/*` when the repo has docs.
- Claude files are not copied as executable Codex runtime files.

## Markdown

- Headings are clear and not overly nested.
- Tables render correctly.
- Code fences have matching backticks.
- Links to local files point to files that exist.

## Skill Frontmatter

Each generated skill has:

- `name`
- `description`
- a focused trigger scope
- concrete workflow steps
- verification guidance

## Codex Runtime Boundaries

- No generated Codex file assumes `TeamCreate`, `SendMessage`, or `TaskCreate`.
- Subagent guidance is manager-led and only used when the user explicitly asks for delegation or parallel work.
- Automations are suggestions unless the user explicitly asked to create recurring work.

## Final Report

Report:

- files created or changed
- how to invoke the harness or generated skills
- commands run and results
- validation not performed and why
- remaining risks or follow-up work
