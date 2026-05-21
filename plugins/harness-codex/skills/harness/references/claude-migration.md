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

## File Conversion

Convert files by intent:

| Source | Convert to | Notes |
| --- | --- | --- |
| `.claude/skills/<name>/SKILL.md` | `.agents/skills/<name>/SKILL.md` | Preserve trigger intent, rewrite Claude-only tool assumptions. |
| `.claude/agents/<name>.md` | `docs/harness/subagents.md` or a project-local skill | Use as role guidance; do not assume reusable agent definitions are executable in Codex. |
| `CLAUDE.md` harness pointer | `AGENTS.md` harness pointer | Keep it short and link to `docs/harness/*`. |
| Claude orchestrator skill | Codex workflow skill or `docs/harness/workflows.md` | Replace team messaging with manager-led delegation. |
| Claude hooks or slash commands | Documentation or explicit commands | Do not install hidden recurring behavior. |

## Rewriting Agent Teams

When a Claude Harness says:

```text
TeamCreate(...)
TaskCreate(...)
SendMessage(...)
```

Rewrite it as:

```text
Manager session:
1. Split work into bounded tasks.
2. Spawn subagents only if the user explicitly asked for delegation or parallel work.
3. Assign non-overlapping ownership.
4. Collect results.
5. Review and integrate.
```

If the user did not ask for subagents, document the roles as optional guidance instead of invoking them.

## Before/After Examples

See:

- `docs/examples/claude-to-codex/before-claude.md`
- `docs/examples/claude-to-codex/after-codex.md`
- `docs/examples/claude-to-codex/README.md`

The migration should be a translation, not a direct execution layer.
