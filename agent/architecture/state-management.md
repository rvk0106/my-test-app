# State Management
> Tags: state, context, redux, zustand, hooks, server-state
> Scope: How application state is organized, stored, and accessed
> Last updated: initialise

## Current State
No state management library is installed. The only state in the app is a local `count` via `useState` in `App.tsx`.

## State Categories

| Category | Where | Examples |
|----------|-------|---------|
| **Local / UI state** | `useState`, `useReducer` in components | Form inputs, toggles, modals open/close, accordion state |
| **Shared / App state** | Not used | TBD — no Context or state library installed |
| **Server state** | Not used | TBD — no data-fetching library installed |
| **URL state** | Not used | TBD — no router installed |
| **Form state** | Not used | TBD — no forms exist |

## Rules
- ALWAYS use the simplest approach that works
- Local state FIRST — lift only when needed
- Server state belongs in a data-fetching library, NOT in global store
- URL state for anything that should survive refresh or be shareable
- Do NOT duplicate server data in client state

## State Library
- Library: None
- Location: N/A

## Server State
- Library: Not used
- Cache strategy: N/A
- Key convention: N/A

## State Decision Tree
```
Need state?
├── Only this component → useState / useReducer
├── Parent + few children → lift state + props
├── Many consumers across tree → Context / state library
├── Server data → data-fetching library (TanStack Query / SWR)
├── Should survive refresh → URL params (router)
└── Form fields → form library or local state
```

## Changelog
<!-- [PROJ-123] Migrated auth state from Redux to Context API -->
