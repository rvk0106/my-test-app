# Design Patterns & Standards
> Tags: patterns, conventions, typescript, quality, hooks
> Scope: Coding patterns and quality standards for this React project
> Last updated: initialise

## Core Principles
- Agents are collaborators, not autonomous engineers
- Plan first → execute in small phases → verify → human review
- No scope creep, no unrelated refactors

## TypeScript Standards
- Strict mode enabled (`"strict": true` in `tsconfig.app.json`)
- Target: ES2022
- Module: ESNext with bundler resolution
- `noUnusedLocals`: true
- `noUnusedParameters`: true
- `erasableSyntaxOnly`: true
- `noFallthroughCasesInSwitch`: true
- `noUncheckedSideEffectImports`: true
- `verbatimModuleSyntax`: true
- No `any` — use `unknown` and narrow, or proper generics
- No `@ts-ignore` — fix the type instead
- `interface` for object shapes, `type` for unions/intersections

```tsx
// CORRECT
interface UserListProps {
  users: User[];
  onSelect: (user: User) => void;
}

const UserList: React.FC<UserListProps> = ({ users, onSelect }) => { ... };

// WRONG
const UserList = ({ users, onSelect }: any) => { ... };
```

## Hooks Rules
- Only call hooks at the top level (never inside conditions/loops)
- Always include all dependencies in useEffect/useMemo/useCallback
- Clean up side effects (return cleanup function from useEffect)
- Extract complex logic into custom hooks

```tsx
// CORRECT — clean dependency array and cleanup
useEffect(() => {
  const controller = new AbortController();
  fetchData(id, { signal: controller.signal });
  return () => controller.abort();
}, [id]);

// WRONG — missing dependency, no cleanup
useEffect(() => {
  fetchData(id);
}, []);
```

## Custom Hooks
- Prefix with `use` (e.g. `useAuth`, `useDebounce`, `useMediaQuery`)
- Location: `src/hooks/` (shared) or co-located with feature component
- Return clear interface (not raw state)
- Handle loading, error, and success states

## Event Handlers
- Prefix with `handle` in the component: `handleClick`, `handleSubmit`
- Prefix with `on` in props: `onClick`, `onSubmit`

## File Naming
- Components: `PascalCase.tsx` (e.g. `UserCard.tsx`)
- Hooks: `camelCase.ts` (e.g. `useAuth.ts`)
- Utils: `camelCase.ts` (e.g. `formatDate.ts`)
- Types: `camelCase.ts` or `PascalCase.ts`
- Tests: `*.test.tsx` or `*.spec.tsx`
- Constants: `SCREAMING_SNAKE_CASE` for values, `camelCase` for files

## Import Order
```tsx
// 1. React / framework
import { useState, useEffect } from 'react';
// 2. Third-party libraries
// 3. Internal shared (hooks, utils, types, context)
// 4. Relative (siblings, children)
import './App.css';
```

## ESLint Configuration
- Flat config (`eslint.config.js`)
- Plugins: `@eslint/js`, `typescript-eslint`, `eslint-plugin-react-hooks`, `eslint-plugin-react-refresh`
- Targets: `**/*.{ts,tsx}` files
- Ignores: `dist/`

## Prettier
Not configured — no `.prettierrc` file exists.

## Performance Patterns
- `React.memo` — only for components that re-render with same props
- `useMemo` — only for expensive computations
- `useCallback` — only when passing callbacks to memoized children
- Don't optimize prematurely — profile first, optimize second
- Code splitting with `React.lazy` for route-level components

## Quality Checklist
- [ ] TypeScript types for all props and API responses
- [ ] Tests with React Testing Library for new components
- [ ] Accessibility attributes (see `architecture/accessibility.md`)
- [ ] Responsive at all breakpoints (see `architecture/styling.md`)
- [ ] Loading + error states for async operations
- [ ] No console errors or warnings
- [ ] ESLint pass (`npm run lint`)
- [ ] Build succeeds (`npm run build`)

## Changelog
<!-- [PROJ-123] Added custom hooks naming convention -->
