# Automation Recipes

Use this reference when the user asks for recurring checks, scheduled workflows, automation suggestions, or project maintenance routines.

Do not create recurring automations unless the user explicitly asks for them.

## Automation Safety

Good automation candidates are:

- deterministic
- reversible or read-only
- already done manually more than once
- cheap enough to run repeatedly
- easy to validate from logs or output
- scoped to the repository, not the user's whole machine

Avoid automating:

- destructive cleanup
- credential rotation
- production deploys
- payment, billing, or account actions
- broad filesystem changes
- workflows that require human judgment at every step

## Recipe: Daily Test Health

Purpose: detect broken tests early.

```text
Trigger: daily or before a work session
Steps:
1. Pull or inspect latest branch state if the user requested it.
2. Run the repository's standard fast test command.
3. Summarize failures by file, test name, and likely owner.
4. Do not auto-fix unless the user asks.
```

Generated harness suggestion:

```markdown
## Daily Test Health

Run the fastest reliable test command and report failures. Do not change files unless the user explicitly asks for fixes.
```

## Recipe: Weekly Dependency Review

Purpose: identify outdated or risky dependencies without automatically upgrading them.

```text
Trigger: weekly or before a release
Steps:
1. Inspect package manager files.
2. Run the repo's dependency audit command if present.
3. Summarize high-risk findings.
4. Propose upgrades separately from applying them.
```

## Recipe: Documentation Drift Check

Purpose: detect mismatch between docs and actual commands or files.

```text
Trigger: after setup, command, or workflow changes
Steps:
1. Read AGENTS.md, README, docs/harness, and package/build files.
2. Compare documented commands with actual scripts or project files.
3. Report stale commands and missing docs.
4. Update docs only if the user asks or the task includes docs maintenance.
```

## Recipe: Harness Drift Check

Purpose: keep generated harness files aligned.

```text
Trigger: after adding skills, removing workflows, or migrating Claude files
Steps:
1. Run Phase 0 audit.
2. Check AGENTS.md pointers against existing skills and docs.
3. Check skill descriptions against current trigger examples.
4. Record any fixes in docs/harness/CHANGELOG.md or CHANGELOG.md.
```

## Automation Proposal Format

When proposing automation, include:

- name
- trigger
- commands or checks
- files read
- files written
- safety boundary
- expected output
- when not to run it
