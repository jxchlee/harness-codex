# Codex Subagent Capabilities

Use this reference before recommending subagent orchestration in Codex.

## Summary

Codex supports manager-led subagent delegation. The current Codex session acts as the manager: it decides whether delegation is appropriate, gives each subagent a bounded task, reviews the returned result, and integrates or rejects the work.

Do not model Codex as a Claude-style autonomous Agent Team runtime.

## Supported Pattern

Codex can support:

- explicit user-requested subagent use
- parallel independent subtasks
- bounded exploration tasks
- bounded implementation tasks with clear file ownership
- manager-reviewed integration
- manager-maintained task plans

## Unsupported Assumptions

Do not assume Codex provides:

- `TeamCreate`
- `SendMessage`
- `TaskCreate`
- direct subagent-to-subagent messaging
- autonomous shared task queues
- implicit shared memory across agents
- background agents that pick up work without manager assignment

## Delegation Rules

Only recommend subagents when the user explicitly asks for delegation, parallel agent work, subagents, or a multi-agent run.

Good Codex subagent tasks are:

- concrete
- bounded
- self-contained
- useful in parallel with manager work
- assigned clear read/write scope
- easy to review from a final report or changed files

Avoid delegation when:

- the manager's next step is blocked on the result
- the task is too ambiguous
- the implementation would require multiple agents to edit the same files
- the user asked for a quick direct answer
- the task can be done locally with less coordination cost

## Manager Responsibilities

The manager must:

1. Define the goal and acceptance criteria.
2. Split work into non-overlapping tasks.
3. Assign file ownership for implementation tasks.
4. Tell workers they are not alone in the codebase and must not revert others' edits.
5. Review subagent output before integrating it.
6. Run the narrowest useful verification.
7. Report results, remaining risks, and changed files.

## Data Sharing

Prefer explicit data sharing:

- manager plan messages
- file-based artifacts in agreed paths
- final subagent reports
- manager summaries between phases

Do not rely on implicit shared memory. If shared state matters, write it down in a plan, issue, checklist, or project-local document.
