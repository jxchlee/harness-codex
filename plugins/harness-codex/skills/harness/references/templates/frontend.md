# Frontend Harness Template

Use this template for React, Next.js, Vue, Svelte, or similar UI repositories.

## Signals

- `package.json`
- `src/`, `app/`, `pages/`, `components/`, or `routes/`
- Vite, Next.js, Nuxt, Storybook, Playwright, Cypress, Vitest, or Jest config
- CSS modules, Tailwind, design-system packages, or component libraries

## Suggested AGENTS.md Additions

```markdown
## Frontend Rules

- Match existing component, routing, and styling patterns.
- Keep UI changes scoped to the requested flow.
- Prefer accessible controls and semantic HTML.
- Verify responsive behavior for changed screens.
- Run the narrowest relevant lint, typecheck, unit, or browser test.
```

## Suggested Skills

- `frontend-change`: Use when implementing UI behavior, component changes, or page-level frontend work.
- `browser-verify`: Use when a visual or interactive change needs browser validation.
- `design-system-guard`: Use when changing shared components or tokens.

## Verification Examples

```powershell
npm run lint
npm run typecheck
npm test
npm run test:e2e
```

Choose commands from the repo. Do not invent scripts that are not present.
