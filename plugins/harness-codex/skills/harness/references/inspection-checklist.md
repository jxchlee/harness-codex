# Inspection Checklist

Use this reference when auditing or inspecting a target repository.

## Phase 0 Audit

Look for existing harness artifacts:

- `AGENTS.md`
- `.agents/skills/*/SKILL.md`
- `.codex/skills/*/SKILL.md`
- `docs/harness/*`
- `.claude/agents/*`, `.claude/skills/*`, or `CLAUDE.md` as migration source material only

Classify the run before planning edits:

| State | Signal | Action |
| --- | --- | --- |
| New build | No Codex harness artifacts exist | Propose the smallest useful starting harness. |
| Extension | Codex harness artifacts exist and the user asks for more capability | Reuse existing conventions and update only affected files. |
| Maintenance | User asks for audit, drift check, cleanup, sync, or repair | Report drift first, then propose targeted fixes. |
| Migration | Claude harness artifacts exist | Translate intent into Codex-native files; do not execute Claude-only runtime assumptions. |

## Drift Checks

When artifacts already exist, compare references for drift:

- `AGENTS.md` mentions skills that do not exist
- skill files exist but are not mentioned by project instructions
- docs describe commands or workflows that no longer match the repo
- Claude harness files appear to have been copied without Codex translation

Report drift before broad edits.

## Repository Inspection

Look for:

- package files such as `package.json`, `pyproject.toml`, `Cargo.toml`, `go.mod`, `pom.xml`, or `build.gradle`
- test and lint commands
- framework conventions
- entry points and deployment files
- existing `AGENTS.md`, `.agents/`, `.codex/`, `.claude/`, or docs
- large or risky modules
- repeated manual workflows mentioned in docs or scripts

Use fast file search tools such as `rg` or `rg --files` when available.

## Phase Selection For Existing Harnesses

For extension or maintenance work, run only the phases that fit the change:

| Change type | Inspect | Design | Write | Verify | Evolve |
| --- | --- | --- | --- | --- | --- |
| Add/update project instructions | Required | Light | `AGENTS.md` or docs | Required | Record change |
| Add/update a skill | Required | Required | `.agents/skills/*` | Required | Record trigger feedback |
| Add subagent guidance | Required | Required | docs or skill guidance | Required | Note Codex limits |
| Migrate Claude harness | Required | Required | Codex-native files | Required | Record compatibility gaps |
| Audit/repair drift | Required | Only if needed | Targeted fixes | Required | Record issue and fix |
