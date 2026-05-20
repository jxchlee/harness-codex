# Architecture

Harness Codex is intentionally small. Version 0.1 is a Codex plugin that ships one skill named `harness`.

The skill's job is to help Codex generate a project-local harness for the repository currently being worked on.

## Components

### Marketplace

`.agents/plugins/marketplace.json` makes this repository usable as a Codex plugin marketplace.

### Plugin

`plugins/harness-codex/.codex-plugin/plugin.json` describes the plugin metadata and points Codex at the plugin's skills directory.

### Skill

`plugins/harness-codex/skills/harness/SKILL.md` is the main reusable workflow. It tells Codex how to inspect a project and generate Codex-native instructions, skills, and automation suggestions.

## Generated Project Harness

When the skill runs in another repository, it may generate:

- `AGENTS.md`
- `.agents/skills/*/SKILL.md`
- `docs/harness/*`

These generated files belong to the target project, not to the Harness Codex plugin itself.

## Boundaries

Harness Codex should not:

- run Claude `.claude/*` files directly
- create large agent hierarchies by default
- create recurring automations without explicit user approval
- introduce MCP servers before the basic skill workflow is proven

## Compatibility Model

Claude Harness concepts are translated into Codex concepts:

| Claude Harness concept | Codex equivalent |
| --- | --- |
| `.claude/skills/*` | `.agents/skills/*/SKILL.md` |
| `.claude/agents/*` | documented subagent roles or project-local skills |
| slash commands | `$skill-name` and natural language triggers |
| team orchestration | Codex subagents when explicitly requested |
| recurring routines | Codex automations |

