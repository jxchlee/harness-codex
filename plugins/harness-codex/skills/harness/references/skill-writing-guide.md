# Skill Writing Guide

Use this reference before creating or updating project-local Codex skills.

## Location

Prefer the local convention already used by the repository:

- `.agents/skills/<skill-name>/SKILL.md`
- `.codex/skills/<skill-name>/SKILL.md` when the project already uses Codex-local skills

## Frontmatter

Every skill must start with a clear frontmatter block:

```markdown
---
name: test-runner
description: Use when validating code changes in this repository, especially before final responses or commits.
---
```

## Writing Rules

- Make each skill specific to one repeated workflow.
- Include concrete steps and verification.
- Avoid broad, vague "do everything" skills.
- Explain why important constraints exist.
- Keep the main `SKILL.md` focused; move long details into `references/`.
- Prefer scripts for deterministic repeatable work when the repo benefits from them.

## Description Rules

The description should include:

- what the skill does
- when it should trigger
- relevant natural-language trigger phrases
- cases that should not trigger when confusion is likely

Avoid overclaiming. A skill should trigger reliably for its real workflow, not for every adjacent task.

## Minimal Skill Body

```markdown
# Test Runner

Use this skill when validating code changes in this repository.

1. Inspect the changed files.
2. Choose the narrowest meaningful test command.
3. Run the command from the repository root.
4. Report command, result, and any residual risk.
```
