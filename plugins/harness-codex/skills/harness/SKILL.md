---
name: harness
description: Use when the user says harness, 하네스, 하네스 사용, project harness, automation harness, or asks Codex to organize reusable project instructions, skills, subagent workflows, review loops, or automation suggestions for a repository.
---

# Harness

Invocation examples: [KO](#ko-invocation-examples) | [EN](#en-invocation-examples)

Harness mode is a guided workflow for shaping a small Codex-native operating layer for a repository. It helps Codex understand how the project works, then propose or create project instructions, local skills, review checklists, and optional automation ideas.

Do not assume Claude `.claude/*` files can run directly in Codex. Preserve the workflow idea, but express the result using Codex-native files and behavior.

## Default Workflow

1. Inspect the repository before proposing edits.
2. Identify the project domain, languages, package managers, test commands, docs, and existing agent instructions.
3. Find repeated workflows, risky areas, and places where Codex would benefit from project-specific guidance.
4. Propose the smallest useful harness before editing.
5. If the user asked for implementation, create or update project-local files.
6. Verify the generated files are valid Markdown or JSON.
7. Summarize what changed and how to invoke the harness later.

## Files To Consider

Create only the files that fit the user's request and the repository's shape:

- `AGENTS.md`
- `.agents/skills/<skill-name>/SKILL.md`
- `docs/harness/overview.md`
- `docs/harness/workflows.md`
- `docs/harness/automation-recipes.md`

Do not create recurring automations unless the user explicitly asks for them.

Do not spawn subagents unless the user explicitly asks for delegation, parallel agent work, or subagents.

## Repository Inspection Checklist

Look for:

- package files such as `package.json`, `pyproject.toml`, `Cargo.toml`, `go.mod`, `pom.xml`, or `build.gradle`
- test and lint commands
- framework conventions
- entry points and deployment files
- existing `AGENTS.md`, `.agents/`, `.codex/`, `.claude/`, or docs
- large or risky modules
- repeated manual workflows mentioned in docs or scripts

Use fast file search tools such as `rg` or `rg --files` when available.

## Harness Plan Format

When planning before edits, produce a concise plan with:

- project summary
- detected commands
- proposed `AGENTS.md` guidance
- proposed skills
- optional automation recipes
- files to create or edit

Keep the plan short enough for the user to review.

## Generated Skill Guidelines

When creating project-local skills:

- Use a clear `name` and `description` frontmatter block.
- Make each skill specific to one repeated workflow.
- Include concrete steps and verification.
- Avoid broad, vague "do everything" skills.
- Prefer one useful skill over many speculative skills.

Example:

```markdown
---
name: test-runner
description: Use when validating code changes in this repository, especially before final responses or commits.
---

# Test Runner

Run the repository's standard checks in this order...
```

## AGENTS.md Guidelines

When creating or updating `AGENTS.md`:

- Capture repository-specific commands and conventions.
- Keep instructions durable and concise.
- Do not duplicate generic Codex behavior.
- Include safety notes only when they are specific to the project.
- Preserve existing user-authored instructions.

## Claude Harness Migration

If a project contains Claude Harness files:

- Treat `.claude/skills/*` as source material for Codex skills.
- Treat `.claude/agents/*` as source material for documented subagent roles or local skills.
- Do not copy Claude-only tool calls as executable Codex instructions.
- Convert slash-command language into skill triggers and natural language examples.
- Explain compatibility gaps clearly.

## KO Invocation Examples

These phrases should trigger this skill when available:

```text
하네스 사용해서 이 프로젝트 구조를 정리해줘.
```

```text
하네스로 AGENTS.md와 필요한 Codex skills를 제안해줘.
```

```text
이 repo에 맞는 자동화 하네스를 만들어줘.
```

## EN Invocation Examples

These phrases should trigger this skill when available:

```text
Use harness mode to analyze this repo and propose project-specific Codex skills.
```

```text
Use harness mode to suggest a harness plan, but do not edit files yet.
```

```text
$harness
Create a minimal Codex harness plan for this repo.
```

## Output Style

When the task is complete, include:

- files created or changed
- how to invoke the harness
- any commands that were run
- any validation that could not be performed

Keep the final response concise.
