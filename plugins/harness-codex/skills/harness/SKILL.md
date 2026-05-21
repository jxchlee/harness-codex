---
name: harness
description: Use when the user says harness, 하네스, 하네스 사용, project harness, automation harness, or asks Codex to organize reusable project instructions, skills, subagent workflows, review loops, or automation suggestions for a repository.
---

# Harness

Harness mode is a guided workflow for shaping and maintaining a small Codex-native operating layer for a repository. It helps Codex understand how the project works, then propose or create project instructions, local skills, review checklists, subagent delegation guidance, and optional automation ideas.

Do not assume Claude `.claude/*` files can run directly in Codex. Preserve the workflow idea, but express the result using Codex-native files and behavior.

## Progressive Disclosure

Keep this `SKILL.md` as the routing layer. Load references only when needed:

- Read `references/inspection-checklist.md` when auditing or inspecting a repository.
- Read `references/plan-format.md` before proposing a harness plan.
- Read `references/skill-writing-guide.md` before creating or updating project-local skills.
- Read `references/agents-md-guide.md` before creating or updating `AGENTS.md`.
- Read `references/claude-migration.md` when `.claude/*`, `CLAUDE.md`, `TeamCreate`, `SendMessage`, or `TaskCreate` appears.
- Read `references/evolution-loop.md` before recording changes or handling feedback.
- Read `references/validation-checklist.md` before final verification of generated harness files.
- Read `references/templates/agents-md-base.md` when drafting a new `AGENTS.md`.
- Read one domain template when the repository clearly matches it: `templates/frontend.md`, `templates/backend.md`, `templates/data.md`, or `templates/research.md`.

If this file approaches 500 lines, move detailed guidance into `references/` and leave a pointer here. Reference files over 300 lines should include a table of contents.

## Default Workflow

0. Audit the existing harness state before designing anything new.
1. Inspect the repository before proposing edits.
2. Identify the project domain, languages, package managers, test commands, docs, and existing agent instructions.
3. Find repeated workflows, risky areas, and places where Codex would benefit from project-specific guidance.
4. Propose the smallest useful harness before editing.
5. If the user asked for implementation, create or update project-local files.
6. Verify the generated files are valid Markdown or JSON. Use `references/validation-checklist.md`.
7. Close the loop: record changes, ask for feedback, and identify whether the harness itself should evolve.

## Phase 0: Existing Harness Audit

Start every harness run by checking whether the target repository already has harness artifacts. Use `references/inspection-checklist.md` for the audit checklist, drift checks, and run-mode classification.

Report the audit result before broad edits. Classify the run as one of:

- New build
- Extension
- Maintenance
- Migration

## Files To Consider

Create only the files that fit the user's request and the repository's shape:

- `AGENTS.md`
- `.agents/skills/<skill-name>/SKILL.md`
- `.codex/skills/<skill-name>/SKILL.md` when the project already uses Codex-local skills
- `docs/harness/overview.md`
- `docs/harness/workflows.md`
- `docs/harness/automation-recipes.md`
- `docs/harness/CHANGELOG.md`

Do not create recurring automations unless the user explicitly asks for them.

Do not spawn subagents unless the user explicitly asks for delegation, parallel agent work, or subagents.

## Codex Subagent Boundary

Codex supports manager-led subagent delegation when the user explicitly asks for delegation, parallel agent work, or subagents. Treat the current Codex session as the manager: it decomposes work, assigns bounded tasks, reviews results, and integrates changes.

Do not describe Codex as having Claude-style Agent Teams by default. Do not generate instructions that assume `TeamCreate`, `SendMessage`, `TaskCreate`, autonomous shared task queues, or implicit shared memory across agents exist in Codex. Read `references/claude-migration.md` when translating Claude Harness material.

## Harness Plan

Before editing, produce a concise plan. Use `references/plan-format.md` for the required fields and examples.

The plan must include:

- audit result and selected run mode
- project summary
- detected commands
- proposed `AGENTS.md` guidance
- proposed skills
- subagent guidance only if requested or clearly useful
- optional automation recipes
- files to create or edit

If the repo clearly matches a supported domain, include the selected domain template and why. If no domain template fits cleanly, use only the base guidance.

## Generated Files

Before creating or updating project-local skills, read `references/skill-writing-guide.md`.

Before creating or updating `AGENTS.md`, read `references/agents-md-guide.md`.

Before drafting a new `AGENTS.md`, read `references/templates/agents-md-base.md`.

Use domain templates only when they fit the repository:

- `references/templates/frontend.md` for frontend UI apps
- `references/templates/backend.md` for APIs, services, workers, and CLIs
- `references/templates/data.md` for analytics, ETL, dbt, notebooks, and ML pipelines
- `references/templates/research.md` for research, experiments, evaluations, and literature workflows

When migrating Claude Harness files, read `references/claude-migration.md` and translate intent rather than copying Claude-only runtime assumptions.

## Phase 7: Evolution Loop

At the end of any implemented harness change, read `references/evolution-loop.md`, record what changed, summarize future trigger phrases, and identify whether user feedback should update instructions, skills, docs, validation, or subagent guidance.

Treat repeated feedback, repeated verification failures, or repeated manual workarounds as evolution triggers.

## KO Invocation Examples

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
