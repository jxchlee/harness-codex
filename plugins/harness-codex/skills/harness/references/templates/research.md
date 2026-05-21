# Research Harness Template

Use this template for research repos, paper notes, experiments, evaluation suites, or long-form investigation projects.

## Signals

- `docs/`, `papers/`, `experiments/`, `notebooks/`, `evals/`, or citation files
- experiment logs, benchmark scripts, datasets, or literature review notes
- README that describes research questions rather than production deployment

## Suggested AGENTS.md Additions

```markdown
## Research Rules

- Separate source evidence from interpretation.
- Preserve citations, dates, and experiment parameters.
- Mark claims that are inferred rather than directly observed.
- Keep generated summaries traceable to source files or URLs.
- Do not overwrite raw experiment outputs without explicit instruction.
```

## Suggested Skills

- `research-synthesis`: Use when combining notes, sources, and experiment outputs into a concise finding.
- `experiment-review`: Use when checking methodology, parameters, and reproducibility.
- `citation-guard`: Use when claims need source attribution or date-sensitive verification.

## Verification Examples

```powershell
pytest
python scripts/run_eval.py
```

For non-code research, verification can be a source coverage check, citation check, or reproducibility note.
