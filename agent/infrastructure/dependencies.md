# Dependencies
> Tags: npm, packages, runtime, devDependencies, external
> Scope: All dependencies the project relies on
> Last updated: initialise

## Dependency Philosophy
- Prefer small, focused packages over monolithic ones
- Evaluate bundle size impact before adding (use bundlephobia.com)
- Keep dependencies up to date — audit regularly
- Every dependency must be justified

## Core Dependencies (package.json)
| Package | Version | Purpose | Bundle Impact |
|---------|---------|---------|---------------|
| `react` | ^19.2.0 | UI library | Core |
| `react-dom` | ^19.2.0 | DOM renderer | Core |

## Dev Dependencies
| Package | Purpose |
|---------|---------|
| `@vitejs/plugin-react` (^5.1.1) | Vite plugin for React (Babel-based HMR + JSX) |
| `vite` (^8.0.0-beta.13) | Bundler and dev server |
| `typescript` (~5.9.3) | Type checking |
| `@types/react` (^19.2.7) | React type definitions |
| `@types/react-dom` (^19.2.3) | React DOM type definitions |
| `@types/node` (^24.10.1) | Node.js type definitions |
| `eslint` (^9.39.1) | Linter |
| `@eslint/js` (^9.39.1) | ESLint recommended JS rules |
| `typescript-eslint` (^8.48.0) | TypeScript ESLint integration |
| `eslint-plugin-react-hooks` (^7.0.1) | React hooks linting rules |
| `eslint-plugin-react-refresh` (^0.4.24) | React Refresh / HMR linting |
| `globals` (^16.5.0) | Global variable definitions for ESLint |

## Not Installed (notable absences)
- No test framework (Vitest, Jest)
- No React Testing Library
- No router (React Router, TanStack Router)
- No data-fetching library (TanStack Query, SWR)
- No state management library
- No CSS framework (Tailwind, styled-components)
- No form library
- No Prettier
- No `eslint-plugin-jsx-a11y`

## External Services / APIs
- Backend API: None
- Auth provider: None
- Analytics: None
- Error tracking: None
- CDN: None

## Adding Dependencies
Before adding a new package:
1. Check if the feature can be done with vanilla JS/React
2. Check bundle size at bundlephobia.com
3. Check maintenance status (last release, open issues, downloads)
4. Check for tree-shaking support
5. Prefer packages with TypeScript types included
6. Document the justification in this file

## Changelog
<!-- [PROJ-123] Added @tanstack/react-query for server state -->
