# Harness Codex

Usage examples: [KO](#ko-usage) | [EN](#en-usage)

Harness Codex is a Codex-native guided workflow skill for shaping a lightweight project harness. It helps Codex inspect a repository, propose useful project instructions, and optionally create small, reviewable skills, review loops, subagent guidance, and automation suggestions.

This project adapts the workflow idea behind Claude Harness into Codex primitives:

- Codex plugins
- Codex skills
- `AGENTS.md`
- project-local `.agents/skills/*/SKILL.md`
- optional Codex automations

It does not run Claude `.claude/*` files directly. Harness Codex is a small Codex-native workflow layer, not a compatibility runtime for Claude Code.

## Original Source And Attribution

Harness Codex is inspired by the Claude Harness / agent harness pattern, especially the upstream Harness repository:

- [revfactory/harness](https://github.com/revfactory/harness) - the upstream Harness repository for a Claude Code team architecture factory.
- The broader Claude Code harness convention of combining skills, agents, hooks, project instructions, and repeatable review workflows.

This repository is an independent Codex-native adaptation. It translates the useful workflow concepts into Codex plugin and skill conventions instead of copying Claude-specific runtime behavior.

## What It Does

When invoked in a Codex session, the `harness` skill guides Codex to:

1. Inspect the current repository.
2. Identify languages, package managers, tests, docs, risky areas, and repeated workflows.
3. Propose the smallest useful project harness.
4. Optionally create or update `AGENTS.md`, project-local skills, and `docs/harness/*`.
5. Suggest optional automations only when they fit the project and the user asks for recurring work.
6. Keep generated changes small and reviewable.

## What It Does Not Do

- It does not execute Claude `.claude/*` files.
- It does not install Claude hooks or slash commands.
- It does not create large agent hierarchies by default.
- It does not create recurring automations without explicit user approval.
- It does not replace project-specific judgment; it gives Codex a structured way to discover and document that judgment.

## Install

After this repository is pushed to GitHub, add it as a Codex plugin marketplace:

```bash
codex plugin marketplace add jxchlee/harness-codex
```

If your Codex setup expects a full Git URL, use:

```bash
codex plugin marketplace add https://github.com/jxchlee/harness-codex.git
```

Then install the `harness-codex` plugin from the Codex plugin marketplace UI or CLI flow.

## Use

In a Codex session, invoke the skill directly:

```text
$harness
Create a minimal Codex harness plan for this repo.
```

### KO Usage

```text
하네스 사용해서 이 프로젝트 구조를 정리해줘.
```

```text
하네스로 AGENTS.md와 필요한 Codex skills를 제안해줘.
```

```text
이 repo에 맞는 자동화 하네스 계획을 제안해줘.
```

### EN Usage

```text
Use harness mode to analyze this repo and propose project-specific Codex skills.
```

```text
Use harness mode to suggest Codex skills and automation ideas for this repo.
```

If you want Codex to edit files, say so explicitly:

```text
$harness
Analyze this repo and create AGENTS.md plus one useful project-local skill.
```

If you only want a plan:

```text
$harness
Analyze this repo and suggest a harness plan, but do not edit files yet.
```

## Expected Output

Depending on the request and repository shape, Harness Codex may propose or create:

- `AGENTS.md`
- `.agents/skills/<skill-name>/SKILL.md`
- `docs/harness/overview.md`
- `docs/harness/workflows.md`
- `docs/harness/automation-recipes.md`

By default, it starts small and avoids creating a large agent hierarchy unless the repository clearly benefits from it.

## Example Workflow

```text
$harness
Analyze this TypeScript app and create a minimal Codex harness.
```

Codex should then:

1. Inspect files such as `package.json`, tests, source directories, docs, and existing agent instructions.
2. Summarize the project shape and detected commands.
3. Propose a small harness plan.
4. Create files only if the user requested implementation.
5. Validate generated Markdown and JSON.
6. Summarize what changed and how to use it later.

## Repository Layout

```text
harness-codex/
|-- .agents/
|   `-- plugins/
|       `-- marketplace.json
|-- plugins/
|   `-- harness-codex/
|       |-- .codex-plugin/
|       |   `-- plugin.json
|       `-- skills/
|           `-- harness/
|               `-- SKILL.md
|-- docs/
|   |-- architecture.md
|   |-- installation.md
|   |-- migration-from-claude-harness.md
|   `-- roadmap.md
|-- harness-codex-overview.md
`-- README.md
```

## Local Validation

Before publishing, validate the plugin metadata:

```powershell
Get-Content .agents/plugins/marketplace.json | ConvertFrom-Json | Out-Null
Get-Content plugins/harness-codex/.codex-plugin/plugin.json | ConvertFrom-Json | Out-Null
```

The main skill should live at:

```text
plugins/harness-codex/skills/harness/SKILL.md
```

It should include frontmatter like:

```markdown
---
name: harness
description: Use when the user says harness, project harness, automation harness, or asks Codex to organize reusable project instructions, skills, subagent workflows, review loops, or automation suggestions for a repository.
---
```

The actual bundled skill may include additional natural-language trigger phrases.

## Design Principle

Harness Codex should feel like "download it, say use harness, and let Codex help structure the work." Under the hood, it plans first, keeps generated changes reviewable, and stays Codex-native.
