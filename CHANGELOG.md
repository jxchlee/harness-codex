# Changelog

## 0.7.0 - 2026-05-21

| Date | Change | Target | Reason |
| --- | --- | --- | --- |
| 2026-05-21 | Expanded Claude Harness migration rules with file conversion and Agent Team rewriting guidance. | `docs/migration-from-claude-harness.md`, `plugins/harness-codex/skills/harness/references/claude-migration.md` | Make migration practical instead of only conceptual. |
| 2026-05-21 | Added before/after Claude-to-Codex migration examples. | `docs/examples/claude-to-codex/*` | Show how Claude runtime assumptions become Codex manager-led delegation guidance. |
| 2026-05-21 | Bumped plugin version to 0.7.0. | `plugins/harness-codex/.codex-plugin/plugin.json` | Mark the migration examples release. |

## 0.6.0 - 2026-05-21

| Date | Change | Target | Reason |
| --- | --- | --- | --- |
| 2026-05-21 | Added safe automation recipes for test health, dependency review, documentation drift, and harness drift. | `plugins/harness-codex/skills/harness/references/automation-recipes.md` | Support recurring maintenance suggestions without silently creating risky automation. |
| 2026-05-21 | Added testing guidance for manifests, trigger prompts, dry runs, and with-skill comparisons. | `plugins/harness-codex/skills/harness/references/testing-guide.md` | Make Harness Codex and generated harnesses easier to validate. |
| 2026-05-21 | Bumped plugin version to 0.6.0. | `plugins/harness-codex/.codex-plugin/plugin.json` | Mark the automation and testing release. |

## 0.5.0 - 2026-05-21

| Date | Change | Target | Reason |
| --- | --- | --- | --- |
| 2026-05-21 | Documented Codex subagent capability boundaries. | `plugins/harness-codex/skills/harness/references/codex-subagent-capabilities.md` | Make unsupported Claude Agent Team assumptions explicit. |
| 2026-05-21 | Added six adapted agent design patterns for Codex manager-led delegation. | `plugins/harness-codex/skills/harness/references/agent-design-patterns.md` | Preserve the useful Harness architecture vocabulary without pretending Codex has the same runtime. |
| 2026-05-21 | Bumped plugin version to 0.5.0. | `plugins/harness-codex/.codex-plugin/plugin.json` | Mark the Codex subagent pattern release. |

## 0.4.0 - 2026-05-21

| Date | Change | Target | Reason |
| --- | --- | --- | --- |
| 2026-05-21 | Added a base `AGENTS.md` template and domain templates for frontend, backend, data, and research repositories. | `plugins/harness-codex/skills/harness/references/templates/*` | Give new harness runs practical starting points without hardcoding every project. |
| 2026-05-21 | Added a validation checklist for generated harness files. | `plugins/harness-codex/skills/harness/references/validation-checklist.md` | Make generated instructions and skills easier to review. |
| 2026-05-21 | Bumped plugin version to 0.4.0. | `plugins/harness-codex/.codex-plugin/plugin.json` | Mark the template release. |

## 0.3.0 - 2026-05-21

| Date | Change | Target | Reason |
| --- | --- | --- | --- |
| 2026-05-21 | Converted `SKILL.md` into a concise routing layer with Progressive Disclosure pointers. | `plugins/harness-codex/skills/harness/SKILL.md` | Keep the main skill small and make future expansion maintainable. |
| 2026-05-21 | Added reference files for inspection, planning, skill writing, `AGENTS.md`, Claude migration, and evolution feedback. | `plugins/harness-codex/skills/harness/references/*` | Load detailed guidance only when needed. |
| 2026-05-21 | Bumped plugin version to 0.3.0. | `plugins/harness-codex/.codex-plugin/plugin.json` | Mark the Progressive Disclosure release. |

## 0.2.0 - 2026-05-21

| Date | Change | Target | Reason |
| --- | --- | --- | --- |
| 2026-05-21 | Added Phase 0 audit and Phase 7 evolution loop to the harness skill. | `plugins/harness-codex/skills/harness/SKILL.md` | Make Harness Codex an evolving system instead of a one-time generator. |
| 2026-05-21 | Documented Codex subagent boundaries and Claude Agent Team incompatibilities. | `plugins/harness-codex/skills/harness/SKILL.md`, docs | Prevent Claude-only `TeamCreate`/`SendMessage`/`TaskCreate` assumptions from leaking into Codex. |
| 2026-05-21 | Bumped plugin version to 0.2.0. | `plugins/harness-codex/.codex-plugin/plugin.json` | Mark the depth-first audit/evolution release. |

## 0.1.0 - 2026-05-20

| Date | Change | Target | Reason |
| --- | --- | --- | --- |
| 2026-05-20 | Created installable Codex plugin marketplace structure and initial `harness` skill. | plugin and docs | Establish the minimum usable Codex-native port. |
