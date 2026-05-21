# Architecture

Harness Codex is intentionally small. Version 0.3 is a Codex plugin that ships one skill named `harness`.

The skill's job is to help Codex audit, generate, and maintain a project-local harness for the repository currently being worked on.

## Components

### Marketplace

`.agents/plugins/marketplace.json` makes this repository usable as a Codex plugin marketplace.

### Plugin

`plugins/harness-codex/.codex-plugin/plugin.json` describes the plugin metadata and points Codex at the plugin's skills directory.

### Skill

`plugins/harness-codex/skills/harness/SKILL.md` is the main reusable workflow. It tells Codex how to audit an existing harness, inspect a project, and generate Codex-native instructions, skills, review loops, subagent guidance, and automation suggestions.

Version 0.3 uses Progressive Disclosure:

- `SKILL.md` is the routing layer and should stay under 500 lines.
- Detailed guidance lives under `plugins/harness-codex/skills/harness/references/`.
- The main skill tells Codex when to read each reference file.
- Reference files over 300 lines should include a table of contents.

## Generated Project Harness

When the skill runs in another repository, it may generate:

- `AGENTS.md`
- `.agents/skills/*/SKILL.md`
- `.codex/skills/*/SKILL.md` when the project already uses Codex-local skills
- `docs/harness/*`

The audit/evolution layer treats the generated harness as an evolving project asset. A run starts with Phase 0 audit, chooses a run mode, and ends with Phase 7 evolution:

| Phase | Purpose |
| --- | --- |
| Phase 0 audit | Detect existing harness artifacts, drift, and migration source files before planning new work. |
| Main workflow | Inspect, design, write, and verify only the smallest useful Codex-native changes. |
| Phase 7 evolution | Record changes, collect feedback, and decide what should update next. |

These generated files belong to the target project, not to the Harness Codex plugin itself.

## Boundaries

Harness Codex should not:

- run Claude `.claude/*` files directly
- create large agent hierarchies by default
- create recurring automations without explicit user approval
- introduce MCP servers before the basic skill workflow is proven
- assume Claude Agent Team primitives such as `TeamCreate`, `SendMessage`, or `TaskCreate` exist in Codex

## Compatibility Model

Claude Harness concepts are translated into Codex concepts:

| Claude Harness concept | Codex equivalent |
| --- | --- |
| `.claude/skills/*` | `.agents/skills/*/SKILL.md` |
| `.claude/agents/*` | documented subagent roles or project-local skills |
| slash commands | `$skill-name` and natural language triggers |
| team orchestration | Codex manager-led subagent delegation when explicitly requested |
| recurring routines | Codex automations |

Codex does not provide Claude-style autonomous Agent Teams as a default runtime. Harness Codex should translate team architecture ideas into manager-led delegation patterns and make unsupported behavior explicit.
