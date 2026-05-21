# Testing Guide

Use this reference when validating Harness Codex itself or generated project harnesses.

## Validation Layers

1. Manifest validation
2. Markdown structure validation
3. Skill trigger review
4. Generated file consistency
5. Optional with-skill vs without-skill comparison

## Manifest Validation

For Harness Codex:

```powershell
Get-Content .agents/plugins/marketplace.json | ConvertFrom-Json | Out-Null
Get-Content plugins/harness-codex/.codex-plugin/plugin.json | ConvertFrom-Json | Out-Null
```

## Markdown Structure

Check:

- `SKILL.md` has frontmatter
- references mentioned by `SKILL.md` exist
- code fences are balanced
- generated skill files have `name` and `description`
- local links point to existing files

## Should-Trigger Tests

Use realistic prompts. The harness should trigger for:

- `하네스 사용해서 이 프로젝트 구조를 정리해줘.`
- `Create a minimal Codex harness plan for this repo.`
- `Audit this repo's existing harness and suggest improvements.`
- `Convert this Claude harness into Codex-native skills.`
- `Suggest project-local Codex skills for repeated workflows.`
- `Design a subagent workflow for this repo.`

## Should-Not-Trigger Tests

The harness should not take over when the user asks for:

- a simple factual answer unrelated to repo workflow
- a one-line command explanation
- a direct bug fix that does not need reusable workflow design
- image generation
- product or travel recommendations
- unrelated web research

## With-Skill Vs Without-Skill Comparison

Use only when the user wants to evaluate harness value.

Method:

1. Run one response with the harness skill.
2. Run a baseline response without reading the harness skill.
3. Compare:
   - project-specificity
   - correctness of generated files
   - trigger quality
   - verification clarity
   - unsupported runtime assumptions

Do not overstate results from small comparisons. Treat them as local quality checks, not universal benchmarks.

## Dry Run

For a dry run, ask:

```text
$harness
Analyze this repo and suggest a harness plan, but do not edit files yet.
```

Expected output:

- audit result
- selected run mode
- detected commands
- recommended files
- verification plan
- Codex subagent limits if delegation is discussed
