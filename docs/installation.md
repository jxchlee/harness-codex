# Installation

Harness Codex is designed to be installed as a Codex plugin from a GitHub-backed marketplace repository.

At this stage, it is a guided workflow skill. It helps Codex analyze a project and propose or create a small harness when the user asks.

## Add The Marketplace

```bash
codex plugin marketplace add jxchlee/harness-codex
```

Then install the `harness-codex` plugin from the Codex plugin UI or CLI flow.

## Invoke The Skill

Use the direct skill name:

```text
$harness
Create a minimal Codex harness plan for this repo.
```

Or use natural language:

```text
하네스 사용해서 이 프로젝트에 맞는 Codex 스킬과 자동화 제안을 만들어줘.
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

