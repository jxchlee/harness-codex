# Backend Harness Template

Use this template for API, service, worker, CLI, or server repositories.

## Signals

- API routes, controllers, services, workers, or command handlers
- `package.json`, `pyproject.toml`, `go.mod`, `Cargo.toml`, `.csproj`, `pom.xml`, or `build.gradle`
- database migrations, queues, OpenAPI specs, integration tests

## Suggested AGENTS.md Additions

```markdown
## Backend Rules

- Keep public API and data contract changes explicit.
- Prefer existing service boundaries and dependency patterns.
- Update tests near changed behavior.
- Treat auth, authorization, migrations, and external calls as high-risk areas.
- Run the narrowest relevant build and test command.
```

## Suggested Skills

- `api-change`: Use when changing endpoints, request/response shapes, or service behavior.
- `data-contract-guard`: Use when schema, migration, or serialized payloads change.
- `integration-test-runner`: Use when validating behavior across service boundaries.

## Verification Examples

```powershell
dotnet test
npm test
pytest
go test ./...
cargo test
```

Choose commands from the repo. For contract changes, include focused tests or document residual risk.
