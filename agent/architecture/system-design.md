# System Design
> Tags: architecture, pages, routes, layout, high-level
> Scope: How the application is structured at a high level
> Last updated: initialise

## Overview
A fresh React single-page application scaffolded with Vite. Currently displays the default Vite + React counter demo. No business logic, routing, or backend integration exists yet.

## Tech Stack
- Framework: Vite 8 + React 19
- Language: TypeScript 5.9 (strict mode)
- State management: None (local `useState` only)
- Styling: Vanilla CSS (global + component-level files)
- Router: Not used
- Data fetching: Not used
- Form handling: Not used
- Testing: Not configured

## Route / Page Structure
```
/                     → App.tsx (single page — counter demo)
```
No router is installed. The app renders a single component tree.

## Component Hierarchy
```
<StrictMode>
  <App />              → Counter demo with Vite + React logos
</StrictMode>
```
No providers, no layout components, no routing.

## Project Structure
```
src/
├── App.tsx             → Main (and only) component
├── App.css             → Component styles for App
├── main.tsx            → Entry point — createRoot + StrictMode
├── index.css           → Global styles (reset, typography, dark/light)
├── assets/
│   └── react.svg       → React logo
public/
└── vite.svg            → Vite logo (favicon + display)
```

## Key Data Flows
No data flows exist yet. The only state is a local `count` managed by `useState` in `App.tsx`.

## Changelog
<!-- [PROJ-123] Added settings page route -->
