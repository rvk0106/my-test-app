# Deployment
> Tags: build, hosting, cdn, deploy, preview
> Scope: How the application is built and deployed
> Last updated: initialise

## Build
```bash
npm run build
# Runs: tsc -b && vite build
# Output: dist/
```

## Build Output
- Static files: `dist/`
- Entry: `index.html` (SPA)
- Assets: hashed filenames for cache busting (Vite default)

## Hosting
- Platform: Not configured
- URL: N/A
- Staging: N/A

## Deploy Process
Not configured. No CI/CD pipeline, no deploy scripts.

## Environment-Specific Config
No environment-specific configuration exists yet.

| Environment | API URL | Features |
|-------------|---------|----------|
| Development | N/A | Vite dev server with HMR |
| Staging | N/A | N/A |
| Production | N/A | N/A |

## Performance Budget
Not defined.

## Danger Zones (hard stop, ask first)
- Changing build config (bundler, output, targets)
- Modifying deployment pipeline
- Changing environment variables in production
- Updating Node.js version in CI

## Changelog
<!-- [PROJ-123] Migrated from Netlify to Vercel -->
