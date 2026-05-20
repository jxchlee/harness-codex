# Migration From Claude Harness

Claude Harness and Harness Codex share a workflow idea, but they use different runtime assumptions.

Claude Harness is built around Claude Code conventions such as `.claude/agents`, `.claude/skills`, and Claude-specific orchestration patterns. Harness Codex translates the useful parts into Codex-native primitives.

## Mapping

| Claude Harness | Harness Codex |
| --- | --- |
| `.claude/skills/<name>/SKILL.md` | `.agents/skills/<name>/SKILL.md` |
| `.claude/agents/<name>.md` | documented subagent role or local skill |
| slash command | `$skill-name` or natural language trigger |
| Claude team creation | Codex subagent guidance |
| recurring review routine | Codex automation recipe |

## Migration Steps

1. Read the Claude Harness files as source material.
2. Keep the workflow intent and domain knowledge.
3. Remove Claude-only tool calls or runtime assumptions.
4. Convert reusable workflows into Codex `SKILL.md` files.
5. Put durable project guidance in `AGENTS.md`.
6. Document optional subagent roles instead of forcing them into every session.
7. Suggest automations only when the user asks for recurring work.

## Compatibility Warning

Do not copy a Claude Harness directory into a Codex project and expect it to run unchanged.

The migration should be a translation, not a direct execution layer.

