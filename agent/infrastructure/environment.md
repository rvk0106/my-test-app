# Environment
> Tags: node, browser, runtime, versions
> Scope: Dev/runtime environment details
> Last updated: initialise

## Runtime
- Node.js: Not specified in package.json (recommend >= 18 LTS)
- Package manager: npm (package-lock.json present)
- Bundler: Vite 8.0.0-beta.13

## Browser Support
Not explicitly configured. Vite defaults to modern browsers supporting native ES modules.

| Browser | Minimum Version |
|---------|----------------|
| Chrome | Last 2 versions (Vite default) |
| Firefox | Last 2 versions (Vite default) |
| Safari | Last 2 versions (Vite default) |
| Edge | Last 2 versions (Vite default) |

## Framework
- React: 19.2.0
- TypeScript: ~5.9.3
- Router: Not installed

## Local Setup
```bash
git clone [repo]
cd my-test-app
npm install
npm run dev        # start Vite dev server
```

## Environment Variables
No environment variables are currently used.

| Variable | Purpose | Required | Example |
|----------|---------|----------|---------|
| N/A | N/A | N/A | N/A |

**Rules:**
- `.env.local` is gitignored — never commit secrets
- Prefix with `VITE_` to expose to client (Vite convention)
- NEVER put server-side secrets in client env vars — they ship in the bundle

## Changelog
<!-- [PROJ-123] Updated to Node 20 LTS -->
