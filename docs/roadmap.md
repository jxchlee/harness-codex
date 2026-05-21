# Roadmap

## 0.1: Installable Plugin

- Add plugin marketplace metadata.
- Add plugin manifest.
- Add the main `harness` skill.
- Document installation and usage.

## 0.2: Audit And Evolution Loop

- Add Phase 0 audit for existing `AGENTS.md`, `.agents/skills/*`, `.codex/skills/*`, `docs/harness/*`, and Claude migration source files.
- Add drift detection and run-mode selection: new build, extension, maintenance, or migration.
- Add Codex subagent boundary guidance so Claude-only Agent Team primitives are not assumed.
- Add Phase 7 evolution loop for change history, feedback, and follow-up harness updates.
- Start a repository changelog for harness changes.

## 0.3: Progressive Disclosure

- Keep `SKILL.md` concise and move detailed guidance into `references/`.
- Add reference files for inspection, plan format, skill writing, AGENTS.md guidance, and Claude migration.
- Document when each reference should be loaded.

## 0.4: Project Harness Templates

- Add templates for `AGENTS.md`.
- Add templates for common project-local skills.
- Add examples for frontend, backend, data, and research repositories.
- Add validation checklists.

## 0.5: Codex Subagent Patterns

- Document Codex-supported manager-led subagent delegation patterns.
- Map Claude Harness team architecture patterns to Codex-supported equivalents.
- Mark unsupported Claude Agent Team behavior explicitly.

## 0.6: Automation Recipes

- Add safe automation prompt examples.
- Add daily and weekly check recipes.
- Document when not to automate.

## 0.7: Claude Harness Migration

- Add conversion examples.
- Add before/after samples.
- Add compatibility warnings for Claude-specific assumptions.
