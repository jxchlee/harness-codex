# Migration From Claude Harness

Claude Harness and Harness Codex share a workflow idea, but they use different runtime assumptions.

Claude Harness is built around Claude Code conventions such as `.claude/agents`, `.claude/skills`, and Claude-specific orchestration patterns. Harness Codex translates the useful parts into Codex-native primitives.

## Mapping

| Claude Harness | Harness Codex |
| --- | --- |
| `.claude/skills/<name>/SKILL.md` | `.agents/skills/<name>/SKILL.md` |
| `.claude/agents/<name>.md` | documented subagent role or local skill |
| slash command | `$skill-name` or natural language trigger |
| Claude team creation | Codex manager-led subagent guidance |
| recurring review routine | Codex automation recipe |

## Migration Steps

1. Read the Claude Harness files as source material.
2. Keep the workflow intent and domain knowledge.
3. Remove Claude-only tool calls or runtime assumptions.
4. Convert reusable workflows into Codex `SKILL.md` files.
5. Put durable project guidance in `AGENTS.md`.
6. Document optional subagent roles instead of forcing them into every session.
7. Suggest automations only when the user asks for recurring work.

## File Conversion Guide

| Claude Harness source | Harness Codex target | Rule |
| --- | --- | --- |
| `.claude/skills/<name>/SKILL.md` | `.agents/skills/<name>/SKILL.md` | Preserve the workflow, rewrite trigger wording and runtime assumptions. |
| `.claude/agents/<name>.md` | `docs/harness/subagents.md` or project-local skills | Treat as role documentation unless Codex subagents are explicitly requested. |
| `CLAUDE.md` harness pointer | `AGENTS.md` harness pointer | Keep the pointer short and link to detailed docs. |
| Claude orchestrator skill | Codex workflow skill or `docs/harness/workflows.md` | Replace team messaging with manager-led delegation. |
| Claude hooks or slash commands | Documentation or explicit commands | Do not install hidden recurring behavior. |

## Unsupported Claude Runtime Assumptions

Do not translate these Claude Harness concepts as if Codex provides the same runtime:

- `TeamCreate`
- `SendMessage`
- `TaskCreate`
- autonomous shared task queues
- implicit shared memory between agents

In Codex, model the current session as the manager. The manager may delegate to subagents only when the user explicitly asks for delegation, parallel agent work, or subagents. The manager owns task decomposition, result review, conflict resolution, and final integration.

When preserving a Claude Harness team pattern, translate it as documentation or as a manager-led delegation plan unless Codex explicitly supports the needed runtime behavior.

## Examples

See the before/after migration examples:

- `docs/examples/claude-to-codex/before-claude.md`
- `docs/examples/claude-to-codex/after-codex.md`
- `docs/examples/claude-to-codex/README.md`

## Compatibility Warning

Do not copy a Claude Harness directory into a Codex project and expect it to run unchanged.

The migration should be a translation, not a direct execution layer.
