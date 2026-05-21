# Agent Design Patterns

Use this reference when the user asks for subagents, parallel agent work, multi-agent planning, or a Codex adaptation of Claude Harness team patterns.

First read `codex-subagent-capabilities.md`.

## Pattern Selection

| Pattern | Use when | Codex support |
| --- | --- | --- |
| Pipeline | Work has sequential dependent phases | Supported as manager-led phases |
| Fan-out/Fan-in | Independent subtasks can run in parallel | Supported when user explicitly asks for parallel agents |
| Producer-Reviewer | One agent produces, another independently reviews | Supported with manager review between roles |
| Supervisor | A central manager dynamically distributes work | Supported only as the current Codex session managing subagents |
| Hierarchical Delegation | Managers delegate to sub-managers recursively | Simplify; nested subagent teams are not a default Codex pattern |
| Expert Pool | Different specialists are invoked as needed | Supported as selective manager-led delegation |

## Pipeline

Use for sequential work:

```text
Manager
  -> analysis
  -> implementation
  -> verification
  -> final integration
```

Codex implementation:

- Keep the phase plan in the manager session.
- Delegate only phases that are independent enough to review later.
- Save intermediate artifacts in files when later phases need them.

## Fan-out/Fan-in

Use for independent parallel work such as separate code areas, independent research angles, or multiple test surfaces.

Codex implementation:

- Ask for explicit user permission to use parallel subagents.
- Assign each subagent a disjoint task and file scope.
- Collect results in the manager session.
- Resolve conflicts manually before final output.

## Producer-Reviewer

Use when quality risk is high and independent review is useful.

Codex implementation:

- Producer creates a patch, plan, or artifact.
- Reviewer inspects behavior, tests, risks, and missing coverage.
- Manager decides what to integrate.

Do not let the reviewer blindly rewrite the producer's work. Review findings should lead to manager-approved changes.

## Supervisor

Use when work needs active coordination across several bounded tasks.

Codex implementation:

- The current Codex session is the supervisor.
- The supervisor owns the plan, task assignment, and integration.
- Subagents do not self-assign from a shared task queue.

## Hierarchical Delegation

Claude Harness can describe recursive delegation. Codex should simplify this unless the user explicitly asks for a deeper structure and the environment supports it.

Codex implementation:

- Prefer one manager layer.
- Split work into smaller direct tasks instead of creating sub-managers.
- Document hierarchy as a plan if needed, not as an assumed runtime.

## Expert Pool

Use when only some specialists are needed depending on what the repository contains.

Codex implementation:

- Detect signals from the repo.
- Invoke only the expert roles that match the active task.
- Keep unused roles as documented options, not active agents.

Example role signals:

| Signal | Candidate expert |
| --- | --- |
| UI routes and components | Frontend specialist |
| API contracts and persistence | Backend/API specialist |
| Migrations and schemas | Data contract specialist |
| Tests and CI failures | Verification specialist |
| Security-sensitive code | Security reviewer |

## Recommendation Format

When recommending a pattern, include:

- selected pattern
- why it fits
- why other patterns were not chosen
- Codex support level
- subagent roles, only if explicitly requested
- manager integration and verification steps
