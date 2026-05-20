# Harness Codex Overview

Harness Codex is a Codex-native adaptation of the Claude Harness idea: a guided workflow skill that helps Codex analyze a repository, propose a lightweight project harness, and optionally create domain-specific skills, subagent guidance, review loops, and repeatable work plans.

The goal is not to run Claude's `.claude/*` harness files directly. The goal is to preserve the useful workflow pattern and express it using Codex-native primitives:

- Codex plugins
- Codex skills
- `AGENTS.md` project instructions
- subagent delegation patterns
- automations for recurring checks or follow-up work

## Intended User Experience

A user should be able to install Harness Codex from a GitHub-backed Codex plugin marketplace and then invoke it naturally inside Codex.

Example install flow:

```bash
codex plugin marketplace add jxchlee/harness-codex
```

After installing the plugin, the user can start a Codex session and say:

```text
$harness
Analyze this repository and create a Codex harness plan for it.
```

or:

```text
하네스 사용해서 이 프로젝트에 맞는 자동화/스킬 구조를 제안해줘.
```

The plugin should expose a `harness` skill whose description is broad enough for Codex to trigger it when the user says "harness", "하네스", "하네스 사용", "project harness", "automation harness", or asks Codex to organize reusable project workflows.

## Repository Shape

The repo should be structured as a Codex plugin marketplace:

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
|   `-- migration-from-claude-harness.md
`-- README.md
```

## Core Skill Behavior

The `harness` skill should guide Codex through a repeatable workflow:

1. Inspect the repository structure, package files, tests, docs, and existing agent instructions.
2. Identify the project's domain, development workflows, risky areas, and recurring tasks.
3. Propose a small set of Codex-native skills or instructions that would help this project.
4. If the user asks for edits, create or update project files such as `AGENTS.md`, `.agents/skills/*/SKILL.md`, and docs.
5. Recommend optional automations, such as daily test health checks or dependency review.
6. Verify generated files are valid and keep changes scoped.

The skill should be conservative. It should not generate a huge agent hierarchy by default. It should start with the smallest useful harness and expand only when the repository clearly needs more structure.

## Claude Harness Concepts And Codex Equivalents

| Claude Harness concept | Codex equivalent |
| --- | --- |
| `.claude/agents/*` | Codex subagent usage patterns documented in `AGENTS.md` or skills |
| `.claude/skills/*` | `.agents/skills/*/SKILL.md` or plugin-provided `skills/*/SKILL.md` |
| Claude team orchestration | Codex subagents, used only when explicitly requested or when the user asks for delegation |
| Slash commands | Skill triggers, `$skill-name`, and natural language |
| Long-running project routines | Codex automations |
| Project memory/instructions | `AGENTS.md` |

## First Version Scope

Version 0.1 should focus on being useful, installable, and easy to understand:

- Provide one plugin: `harness-codex`
- Provide one main skill: `harness`
- Generate a project-specific harness plan
- Optionally generate `AGENTS.md`
- Optionally generate local `.agents/skills/*` skills
- Document installation and usage

It should avoid adding custom MCP servers, complex scripts, or hidden automation until the basic skill flow is proven.

## Invocation Examples

```text
$harness
Create a minimal Codex harness plan for this repo.
```

```text
하네스 사용. 이 코드베이스에서 반복되는 개발/검증 작업을 Codex skill로 정리해줘.
```

```text
Use harness mode to analyze the repo and suggest subagent roles, but do not edit files yet.
```

```text
하네스로 이 프로젝트의 AGENTS.md와 필요한 skills를 만들어줘.
```

## Safety And Editing Rules

Harness Codex should follow Codex's normal collaboration rules:

- Read the codebase before editing.
- Preserve user changes.
- Keep generated files small and reviewable.
- Prefer project-local conventions.
- Do not create recurring automations unless the user asks for them.
- Do not spawn subagents unless the user explicitly asks for delegation or parallel agent work.
- Explain what will be generated before making broad changes.

## Suggested Roadmap

### 0.1: Installable Guided Skill

- Add `.agents/plugins/marketplace.json`
- Add `plugins/harness-codex/.codex-plugin/plugin.json`
- Add `plugins/harness-codex/skills/harness/SKILL.md`
- Add README installation instructions

### 0.2: Project Harness Templates

- Add templates for `AGENTS.md`
- Add templates for common project skills
- Add validation checklist
- Add examples for frontend, backend, data, and research repos

### 0.3: Automation Guidance

- Add documented automation recipes
- Add prompts for daily/weekly checks
- Add safe criteria for when to suggest automations

### 0.4: Migration From Claude Harness

- Add a guide for converting `.claude/agents/*` and `.claude/skills/*`
- Add mapping examples
- Add compatibility warnings

## Open Questions

- Should Harness Codex start in planning mode by default, then edit only when asked?
- Should Korean trigger language be included directly in the skill description?
- Should this repo support only plugin installation, or also copy-paste project-local skills?
- Should the generated harness be minimal by default, with an explicit "expand" command?

## Recommended Default

Start with a minimal, Codex-native plugin that provides a single excellent `harness` skill.

That skill should analyze a repository and then offer to create:

- `AGENTS.md`
- one or more `.agents/skills/*/SKILL.md` files
- optional documentation under `docs/harness/`

This gives users the feeling of "download and say 하네스 사용" without pretending Claude Harness files can run unchanged inside Codex.

