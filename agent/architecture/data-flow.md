# Data Flow & API Integration
> Tags: api, fetch, data, caching, mutations, server-state
> Scope: How data moves between the server and the UI
> Last updated: initialise

## Current State
No API integration exists. No HTTP client, no data-fetching library, no backend connection.

## API Client
- Library: Not used
- Base URL: N/A
- Auth: N/A
- Location: N/A

## Data Fetching Pattern
- Library: Not used
- Pattern: N/A

## Mutation Pattern
Not applicable — no mutations exist.

## Data Flow Diagram
```
App.tsx
  └── useState(count)  → local state only, no server interaction
```

## Caching Strategy
Not applicable — no server data.

## Real-Time Data
Not used.

## Authentication Flow
Not implemented.

## Environment Variables
- No environment variables are currently used
- Vite convention: prefix with `VITE_` to expose to client
- `.env.local` should be gitignored for secrets

## Changelog
<!-- [PROJ-123] Added TanStack Query for server state management -->
