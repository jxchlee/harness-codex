# Evolution Loop

Use this reference before recording changes or handling feedback after a harness run.

## Closeout Steps

At the end of any implemented harness change:

1. Record what changed in `docs/harness/CHANGELOG.md` when available, or in the smallest appropriate project-local change log.
2. Summarize which trigger phrases should invoke the harness or generated skills later.
3. Ask for targeted feedback only when it would change the harness design.
4. Identify whether any feedback should update instructions, skills, docs, validation, or subagent guidance.

## Feedback Matrix

| Feedback signal | Update target |
| --- | --- |
| "The skill did not trigger" | Skill `description` and invocation examples |
| "The output missed a required step" | Skill workflow or `AGENTS.md` guidance |
| "The same manual fix is repeated" | Add or refine a project-local skill |
| "Subagent work conflicted" | Tighten ownership boundaries and manager review steps |
| "Docs and behavior diverged" | Run Phase 0 drift repair |

## Evolution Triggers

Treat these as signals that the harness itself should change:

- repeated user feedback
- repeated verification failures
- repeated manual workarounds
- recurring confusion about when a skill should trigger
- drift between docs and actual repo behavior
