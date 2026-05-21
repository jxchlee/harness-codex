# Installation

Invocation examples: [KO](#ko-invocation-examples) | [EN](#en-invocation-examples)

Harness Codex is designed to be installed as a Codex plugin from a GitHub-backed marketplace repository.

At this stage, it is a guided workflow skill. It helps Codex analyze a project and propose or create a small harness when the user asks.

## Add The Marketplace

```bash
codex plugin marketplace add jxchlee/harness-codex
```

Then install the plugin:

```bash
codex plugin add harness-codex@jxchlee-harness-codex
```

You can verify installation with:

```bash
codex plugin list
```

Expected status:

```text
harness-codex@jxchlee-harness-codex (installed, enabled)
```

## Known Install Issue

On at least one Windows Codex CLI environment, `codex plugin add harness-codex@jxchlee-harness-codex` failed with:

```text
Error: failed to parse plugin.json: expected value at line 1 column 1
```

In that environment, the plugin manifest itself parsed successfully with PowerShell `ConvertFrom-Json`, and Codex recognized the plugin after the marketplace cache was copied into the local plugin cache and `config.toml` was updated. Keep this as a CLI compatibility issue until it is reproduced or resolved upstream.

## Invoke The Skill

Use the direct skill name:

```text
$harness
Create a minimal Codex harness plan for this repo.
```

### KO Invocation Examples

```text
하네스 사용해서 이 프로젝트에 맞는 Codex 스킬과 자동화 제안을 만들어줘.
```

```text
하네스로 AGENTS.md와 필요한 Codex skills를 제안해줘.
```

### EN Invocation Examples

```text
Use harness mode to analyze this repo and propose project-specific Codex skills.
```

```text
Use harness mode to suggest a harness plan, but do not edit files yet.
```

## Local Development

From this repository root, the important files are:

```text
.agents/plugins/marketplace.json
plugins/harness-codex/.codex-plugin/plugin.json
plugins/harness-codex/skills/harness/SKILL.md
```

Before publishing, validate that the JSON files parse correctly.

PowerShell:

```powershell
Get-Content .agents/plugins/marketplace.json | ConvertFrom-Json | Out-Null
Get-Content plugins/harness-codex/.codex-plugin/plugin.json | ConvertFrom-Json | Out-Null
```
