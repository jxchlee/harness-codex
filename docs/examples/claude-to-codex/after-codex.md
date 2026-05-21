# After: Harness Codex Equivalent

```markdown
## Harness

Use the research harness when the user asks for reusable research workflows, source validation, or research automation suggestions.

Details:

- `docs/harness/overview.md`
- `docs/harness/workflows.md`
- `docs/harness/CHANGELOG.md`
```

Optional subagent guidance can live in `docs/harness/workflows.md`:

```markdown
## Research Workflow

Default mode: manager-led single-session workflow.

Use Codex subagents only when the user explicitly asks for delegation, parallel agent work, or subagents.

Suggested roles:

- analyst: gather and summarize source material
- verifier: check claims against cited sources
- writer: produce the final synthesis

Manager responsibilities:

1. Assign bounded tasks.
2. Keep ownership clear.
3. Route findings between roles.
4. Review outputs before integration.
5. Report sources, uncertainty, and remaining gaps.
```

Reusable workflow details can become `.agents/skills/research-synthesis/SKILL.md`:

```markdown
---
name: research-synthesis
description: Use when synthesizing source-backed research notes, validating claims, or turning research findings into a concise report.
---

# Research Synthesis

1. Identify the research question.
2. Separate source evidence from interpretation.
3. Track citations and dates.
4. Mark inferred claims clearly.
5. Summarize findings, gaps, and residual uncertainty.
```
