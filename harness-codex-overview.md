# Harness Codex Overview

Invocation examples: [KO](#ko-invocation-examples) | [EN](#en-invocation-examples)

Harness Codex is a Codex-native adaptation of the Claude Harness idea: a guided workflow skill that helps Codex audit a repository, propose a lightweight project harness, and optionally create domain-specific skills, subagent guidance, review loops, and repeatable work plans.

The goal is not to run Claude's `.claude/*` harness files directly. The goal is to preserve the useful workflow pattern and express it using Codex-native primitives:

- Codex plugins
- Codex skills
- `AGENTS.md` project instructions
- manager-led subagent delegation patterns
- automations for recurring checks or follow-up work

## Intended User Experience

A user should be able to install Harness Codex from a GitHub-backed Codex plugin marketplace and then invoke it naturally inside Codex.

Example install flow:

```bash
codex plugin marketplace add jxchlee/harness-codex
```

After installing the plugin, the user can start a Codex session and use either KO or EN invocation examples.

### KO Invocation Examples

```text
하네스 사용해서 이 프로젝트에 맞는 자동화/스킬 구조를 제안해줘.
```

```text
하네스로 이 프로젝트의 AGENTS.md와 필요한 skills를 제안해줘.
```

### EN Invocation Examples

```text
$harness
Analyze this repository and create a Codex harness plan for it.
```

```text
Use harness mode to analyze this repo and propose project-specific Codex skills.
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

1. Audit existing harness files, including `AGENTS.md`, `.agents/skills/*`, `.codex/skills/*`, `docs/harness/*`, and Claude migration source files.
2. Inspect the repository structure, package files, tests, docs, and existing agent instructions.
3. Identify the project's domain, development workflows, risky areas, and recurring tasks.
4. Propose a small set of Codex-native skills or instructions that would help this project.
5. If the user asks for edits, create or update project files such as `AGENTS.md`, `.agents/skills/*/SKILL.md`, and docs.
6. Recommend optional automations, such as daily test health checks or dependency review.
7. Verify generated files are valid, record changes, and keep changes scoped.

The skill should be conservative. It should not generate a huge agent hierarchy by default. It should start with the smallest useful harness and expand only when the repository clearly needs more structure.

## Claude Harness Concepts And Codex Equivalents

| Claude Harness concept | Codex equivalent |
| --- | --- |
| `.claude/agents/*` | Codex subagent usage patterns documented in `AGENTS.md` or skills |
| `.claude/skills/*` | `.agents/skills/*/SKILL.md` or plugin-provided `skills/*/SKILL.md` |
| Claude team orchestration | Codex manager-led subagents, used only when explicitly requested or when the user asks for delegation |
| Slash commands | Skill triggers, `$skill-name`, and natural language |
| Long-running project routines | Codex automations |
| Project memory/instructions | `AGENTS.md` |

Codex does not provide Claude-style Agent Teams as the default runtime. Harness Codex should not emit `TeamCreate`, `SendMessage`, or `TaskCreate` assumptions unless it is explicitly documenting Claude source material as unsupported or as migration input.

## Current Version Scope

Version 0.6 focuses on making the harness lifecycle useful after the first run while keeping detailed guidance behind Progressive Disclosure, providing starter templates, documenting Codex-supported subagent patterns, and adding automation/testing guidance:

- Provide one plugin: `harness-codex`
- Provide one main skill: `harness`
- Audit existing harness artifacts before planning new ones
- Generate a project-specific harness plan
- Optionally generate or update `AGENTS.md`
- Optionally generate or update local `.agents/skills/*` skills
- Record changes and feedback for later harness evolution
- Keep `SKILL.md` as a routing layer and load `references/` files only when needed
- Provide a base `AGENTS.md` template
- Provide frontend, backend, data, and research starter templates
- Provide a validation checklist for generated harness files
- Provide Codex subagent capability boundaries
- Map six Claude Harness team patterns to Codex manager-led delegation patterns
- Provide safe automation recipes for recurring checks
- Provide should-trigger and should-not-trigger testing guidance
- Document installation and usage

It should avoid adding custom MCP servers, complex scripts, or hidden automation until the basic skill flow is proven.

## Invocation Examples

### KO

```text
하네스 사용. 이 코드베이스에서 반복되는 개발/검증 작업을 Codex skill로 정리해줘.
```

```text
하네스로 이 프로젝트의 AGENTS.md와 필요한 skills를 제안해줘.
```

```text
이 repo에 맞는 자동화 하네스 계획을 제안해줘.
```

### EN

```text
$harness
Create a minimal Codex harness plan for this repo.
```

```text
Use harness mode to analyze the repo and suggest subagent roles, but do not edit files yet.
```

```text
Use harness mode to propose Codex skills and automation ideas for this repo.
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

### 0.2: Audit And Evolution Loop

- Add Phase 0 audit
- Add drift detection and run-mode selection
- Add Codex subagent boundary guidance
- Add Phase 7 evolution loop and changelog

### 0.3: Progressive Disclosure

- Split detailed guidance into `references/`
- Keep the main `SKILL.md` compact
- Document when to load each reference

### 0.4: Project Harness Templates

- Add templates for `AGENTS.md`
- Add templates for common project skills
- Add validation checklist
- Add examples for frontend, backend, data, and research repos

### 0.5: Codex Subagent Patterns

- Document supported manager-led delegation patterns
- Map Claude Harness team patterns to Codex-supported equivalents

### 0.6: Automation Guidance

- Add documented automation recipes
- Add prompts for daily/weekly checks
- Add safe criteria for when to suggest automations

### 0.7: Migration From Claude Harness

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
