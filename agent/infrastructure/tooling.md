# Tooling
> Tags: bundler, linter, test, ci, formatter, quality
> Scope: Dev tools, CI/CD pipeline, quality checks
> Last updated: initialise

## Bundler
- Tool: Vite 8.0.0-beta.13
- Config: `vite.config.ts` (minimal — just `@vitejs/plugin-react`)
- Dev server: `npm run dev`
- Build: `npm run build` (runs `tsc -b && vite build`)
- Preview: `npm run preview`

## Linting
- ESLint 9: `npm run lint`
- Config: `eslint.config.js` (flat config format)
- Plugins: `@eslint/js`, `typescript-eslint`, `eslint-plugin-react-hooks`, `eslint-plugin-react-refresh`
- Auto-fix: `npm run lint -- --fix`
- Ignores: `dist/`

## Formatting
- Prettier: Not configured
- No `.prettierrc` or format script

## Type Checking
- TypeScript 5.9: `tsc -b` (runs as part of `npm run build`)
- Standalone check: `npx tsc --noEmit`
- Config: `tsconfig.json` → references `tsconfig.app.json` + `tsconfig.node.json`
- Strict mode: enabled

## Testing
- Framework: Not configured
- No test runner, no test files, no test scripts
- Recommendation: Add Vitest (pairs well with Vite) + React Testing Library

## Storybook
Not used.

## CI/CD
- Platform: Not configured
- `.github/` contains only `copilot-instructions.md` — no workflow files
- No CI pipeline, no automated checks

## Code Quality
- PR review required: Not defined
- Branch strategy: Not defined
- Commit convention: Not defined

## Available npm Scripts
```json
{
  "dev": "vite",
  "build": "tsc -b && vite build",
  "lint": "eslint .",
  "preview": "vite preview"
}
```

## Changelog
<!-- [PROJ-123] Migrated from CRA to Vite -->
