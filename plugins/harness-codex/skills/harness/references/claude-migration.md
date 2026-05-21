# Claude Harness Migration

Use this reference when `.claude/*`, `CLAUDE.md`, `TeamCreate`, `SendMessage`, or `TaskCreate` appears.

## Mapping

| Claude Harness concept | Codex-native adaptation |
| --- | --- |
| `.claude/skills/*` | `.agents/skills/*/SKILL.md` or plugin skills |
| `.claude/agents/*` | Documented subagent roles or project-local skills |
| `CLAUDE.md` | `AGENTS.md` |
| Slash commands | `$skill-name` and natural language triggers |
| Agent Team runtime | Manager-led subagent delegation, only when explicitly requested |
| Team member messaging | Manager summarizes and routes information |
| Shared task queue | Manager-maintained plan or project-local task document |

## Unsupported Claude Runtime Assumptions

Do not generate instructions that assume these Claude-specific primitives exist in Codex:

- `TeamCreate`
- `SendMessage`
- `TaskCreate`
- autonomous shared task queues
- implicit shared memory across agents

In Codex, the current session is the manager. It decomposes work, assigns bounded tasks, reviews results, and integrates changes.

## Migration Steps

1. Read Claude Harness files as source material.
2. Preserve workflow intent and domain knowledge.
3. Remove Claude-only tool calls or runtime assumptions.
4. Convert reusable workflows into Codex `SKILL.md` files.
5. Put durable project guidance in `AGENTS.md`.
6. Document optional subagent roles instead of forcing them into every session.
7. Suggest automations only when the user asks for recurring work.

The migration should be a translation, not a direct execution layer.
