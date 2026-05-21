# Before: Claude Harness Excerpt

```markdown
## Team Orchestration

Use TeamCreate to create a research team:

- analyst
- verifier
- writer

Use TaskCreate to assign shared tasks. Agents should use SendMessage to coordinate findings and update the shared task queue.

Generated files:

- `.claude/agents/analyst.md`
- `.claude/agents/verifier.md`
- `.claude/agents/writer.md`
- `.claude/skills/research-orchestrator/SKILL.md`

Add this to CLAUDE.md:

Use the research-orchestrator skill for research tasks.
```
```

This is valid Claude Harness source material, but it assumes Claude Agent Team runtime behavior that Codex should not copy directly.
