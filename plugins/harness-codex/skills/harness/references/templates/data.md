# Data Harness Template

Use this template for analytics, notebooks, dbt, ETL, ML pipeline, or data workflow repositories.

## Signals

- notebooks, `dbt_project.yml`, DAGs, SQL models, feature pipelines, or data validation scripts
- `requirements.txt`, `pyproject.toml`, `environment.yml`, or pipeline config
- schema docs, data dictionaries, metrics definitions, or warehouse-specific config

## Suggested AGENTS.md Additions

```markdown
## Data Rules

- Preserve metric definitions and schema contracts.
- Distinguish exploratory notebooks from production pipelines.
- Validate sample inputs, edge cases, and row-count or schema expectations.
- Avoid committing credentials, local data dumps, or generated private datasets.
- Record assumptions about data freshness and source quality.
```

## Suggested Skills

- `data-pipeline-change`: Use when changing ETL, dbt, DAG, or pipeline logic.
- `notebook-review`: Use when turning exploratory work into durable documentation or code.
- `metric-contract-guard`: Use when definitions, aggregates, or schema assumptions change.

## Verification Examples

```powershell
pytest
dbt compile
dbt test
python -m pytest
```

Prefer small sample-based checks when full data runs are expensive.
