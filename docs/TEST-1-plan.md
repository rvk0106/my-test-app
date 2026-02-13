# TEST-1 — User Features Architecture Plan

## Context Loaded
- architecture/system-design.md
- architecture/component-design.md
- architecture/patterns.md
- architecture/styling.md
- architecture/accessibility.md
- architecture/data-flow.md
- architecture/state-management.md
- architecture/error-handling.md
- architecture/glossary.md
- infrastructure/security.md

## Ticket Metadata
- **ID:** TEST-1
- **Title:** User Features
- **Scope:** Registration & login, KYC verification, Wallet (deposit/withdraw), Bet placement, Bet history, Real-time odds display, Notifications

## Requirements

### Features
1. **Registration & Login** — user account creation and authentication
2. **KYC Verification** — identity verification flow
3. **Wallet** — deposit and withdraw funds
4. **Bet Placement** — place bets on events
5. **Bet History** — view past bets and outcomes
6. **Real-time Odds Display** — live odds that update in real time
7. **Notifications** — alerts for bet outcomes, account events, etc.

### Constraints
- Fresh Vite 8 + React 19 + TypeScript 5.9 scaffold — everything must be built from scratch
- No backend exists — frontend architecture must assume a REST/WebSocket API will be provided
- WCAG 2.1 AA compliance required
- Mobile-first responsive design
- TypeScript strict mode, no `any`

### Non-goals
- Backend/API implementation (frontend only)
- Payment processor integration (wallet UI only, assumes API handles payment logic)
- Admin panel or back-office features
- Internationalization (can be added later)

## Design References
- None provided in ticket — request mockups/wireframes before execution if available

## Danger Zones (require human approval before execution)
- **Authentication state management** — token storage, session handling, protected routes
- **API integration and error handling** — HTTP client setup, auth headers, error interceptors
- **Environment variables** — API URLs, WebSocket endpoints
- **Third-party library integrations** — router, state management, data fetching, form handling, WebSocket client

## Current State
- Single `App.tsx` counter demo, no routing, no state management, no API layer, no components, no tests
- Dependencies: React 19, Vite 8, TypeScript 5.9, ESLint
- No CSS Modules, no design tokens, no breakpoint system

## Architecture Decisions

### Routing
- **Library:** React Router v7 (standard for React SPAs)
- **Strategy:** Lazy-loaded route components with `React.lazy` + `Suspense` for code splitting

### State Management
- **Local/UI state:** `useState` / `useReducer` (forms, toggles, modals)
- **Server state:** TanStack Query v5 (caching, background refetching, optimistic updates)
- **Auth state:** React Context + `useReducer` (single global concern, no external library needed)
- **URL state:** React Router (search params for filters, pagination)

### Data Fetching
- **HTTP client:** Custom fetch wrapper or axios (to be decided — flag for human review)
- **Server state:** TanStack Query for all API calls
- **Real-time:** WebSocket client for live odds and notifications
- **Auth:** Bearer token in Authorization header; token stored in memory + httpOnly refresh cookie (server-side concern)

### Styling
- **Method:** CSS Modules (component-scoped, no runtime cost, built into Vite)
- **Design tokens:** CSS custom properties in `:root` (colors, spacing, typography, shadows)
- **Responsive:** Mobile-first with defined breakpoints (480px, 768px, 1024px, 1280px)
- **Theme:** Light/dark via CSS custom properties + `prefers-color-scheme`

### Form Handling
- **Library:** React Hook Form (lightweight, performant, TypeScript-friendly)
- **Validation:** Zod schemas (composable, type-safe, shared with API response validation)

### Testing
- **Runner:** Vitest (native Vite integration)
- **Component testing:** React Testing Library
- **Accessibility:** eslint-plugin-jsx-a11y + axe-core

### Project Structure (target)
```
src/
├── api/                    # HTTP client, API service functions
│   ├── client.ts           # Configured fetch/axios instance
│   ├── auth.ts             # Auth API calls
│   ├── wallet.ts           # Wallet API calls
│   ├── bets.ts             # Betting API calls
│   └── notifications.ts   # Notification API calls
├── components/
│   ├── common/             # Reusable UI (Button, Input, Card, Modal, Toast, Spinner)
│   ├── layout/             # Header, Footer, Sidebar, PageLayout
│   ├── auth/               # LoginForm, RegisterForm, ProtectedRoute
│   ├── kyc/                # KYCForm, DocumentUpload, KYCStatus
│   ├── wallet/             # DepositForm, WithdrawForm, TransactionList, BalanceCard
│   ├── betting/            # BetSlip, OddsDisplay, EventCard, BetConfirmation
│   ├── history/            # BetHistoryList, BetDetail, HistoryFilters
│   └── notifications/      # NotificationList, NotificationItem, NotificationBell
├── hooks/                  # Shared custom hooks
│   ├── useAuth.ts
│   ├── useWallet.ts
│   ├── useBets.ts
│   ├── useNotifications.ts
│   └── useWebSocket.ts
├── context/
│   └── AuthContext.tsx      # Auth provider + context
├── pages/                  # Route-level page components
│   ├── LoginPage.tsx
│   ├── RegisterPage.tsx
│   ├── KYCPage.tsx
│   ├── WalletPage.tsx
│   ├── BettingPage.tsx
│   ├── BetHistoryPage.tsx
│   ├── NotificationsPage.tsx
│   └── NotFoundPage.tsx
├── types/                  # Shared TypeScript types
│   ├── auth.ts
│   ├── wallet.ts
│   ├── betting.ts
│   └── notifications.ts
├── utils/                  # Pure utility functions
│   ├── formatCurrency.ts
│   ├── formatDate.ts
│   └── validators.ts
├── styles/
│   ├── tokens.css          # Design tokens (CSS custom properties)
│   ├── reset.css           # CSS reset
│   └── global.css          # Global typography, base styles
├── assets/
├── App.tsx                 # Router setup + providers
├── main.tsx                # Entry point
└── router.tsx              # Route definitions
```

### Route Structure
```
/login                → LoginPage (public)
/register             → RegisterPage (public)
/kyc                  → KYCPage (protected)
/wallet               → WalletPage (protected)
/betting              → BettingPage (protected)
/history              → BetHistoryPage (protected)
/notifications        → NotificationsPage (protected)
*                     → NotFoundPage (public)
```

---

## Phase 1 — Project Foundation & Design System

### Goal
Install core dependencies, set up routing, establish project structure, create design token system and base common components.

### Tasks
- Install dependencies: `react-router`, `@tanstack/react-query`, `react-hook-form`, `zod`
- Install dev dependencies: `vitest`, `@testing-library/react`, `@testing-library/jest-dom`, `jsdom`, `eslint-plugin-jsx-a11y`
- Create folder structure: `src/api/`, `src/components/common/`, `src/components/layout/`, `src/context/`, `src/hooks/`, `src/pages/`, `src/types/`, `src/utils/`, `src/styles/`
- Create design tokens CSS (`src/styles/tokens.css`) — colors, spacing, typography, shadows, border-radius, breakpoints
- Create CSS reset (`src/styles/reset.css`)
- Create global styles (`src/styles/global.css`)
- Create common components: `Button`, `Input`, `Card`, `Spinner`, `ErrorMessage`
- Create layout components: `PageLayout`, `Header`, `Footer`
- Set up React Router with lazy-loaded routes and a `NotFoundPage`
- Set up TanStack Query provider in `App.tsx`
- Configure Vitest in `vite.config.ts`
- Add `eslint-plugin-jsx-a11y` to ESLint config
- Add semantic HTML landmarks (`<header>`, `<main>`, `<nav>`, `<footer>`)
- Add skip-to-content link

### Allowed Files
- `package.json`
- `vite.config.ts`
- `eslint.config.js`
- `src/styles/*`
- `src/components/common/*`
- `src/components/layout/*`
- `src/pages/NotFoundPage.tsx`
- `src/router.tsx`
- `src/App.tsx`
- `src/main.tsx`
- `src/index.css` (replace with new global styles)

### Forbidden Changes
- No business logic or API calls
- No auth implementation
- No feature-specific components

### Verify Commands
```bash
npm run build          # TypeScript + Vite build succeeds
npm run lint           # ESLint passes
npx vitest run         # Test runner works (even if no tests yet)
```

### Acceptance Criteria
- [ ] All dependencies installed and `npm run build` succeeds
- [ ] Router renders `NotFoundPage` for unknown routes
- [ ] Design tokens defined as CSS custom properties
- [ ] Common components render without errors
- [ ] Layout wraps content with `<header>`, `<main>`, `<footer>`
- [ ] Skip-to-content link present
- [ ] Vitest configured and runnable

### Context Needed
- architecture/component-design.md
- architecture/patterns.md
- architecture/styling.md
- architecture/accessibility.md
- workflow/implementation.md

---

## Phase 2 — Authentication (Registration & Login)

### Goal
Implement auth context, login page, registration page, and protected route wrapper.

### Tasks
- Define auth types (`src/types/auth.ts`): `User`, `LoginCredentials`, `RegisterCredentials`, `AuthState`
- Create API service stubs (`src/api/client.ts`, `src/api/auth.ts`) — typed functions returning mock data until real API is connected
- Create `AuthContext` with `useReducer` for auth state (user, token, loading, error)
- Create `useAuth` hook exposing `login`, `register`, `logout`, `isAuthenticated`, `user`
- Create `ProtectedRoute` component (redirects to `/login` if unauthenticated)
- Create `LoginPage` with form (email + password), validation (Zod), error display
- Create `RegisterPage` with form (email + password + confirm password), validation, error display
- Wire up routes: `/login`, `/register`, protected routes redirect
- Handle loading and error states in auth flow

### Allowed Files
- `src/types/auth.ts`
- `src/api/client.ts`
- `src/api/auth.ts`
- `src/context/AuthContext.tsx`
- `src/hooks/useAuth.ts`
- `src/components/auth/*`
- `src/pages/LoginPage.tsx`
- `src/pages/RegisterPage.tsx`
- `src/router.tsx` (add auth routes)

### Forbidden Changes
- No changes to common components (unless bug found)
- No wallet, betting, or KYC logic
- No real API endpoint calls — use typed stubs

### Verify Commands
```bash
npm run build
npm run lint
npx vitest run
```

### Acceptance Criteria
- [ ] Login form validates and calls auth stub
- [ ] Registration form validates and calls auth stub
- [ ] Auth state persists in context across navigation
- [ ] Protected routes redirect to `/login` when unauthenticated
- [ ] After login, user is redirected to a default protected page
- [ ] Loading spinners shown during auth requests
- [ ] Form validation errors shown inline
- [ ] Accessible: labels, focus management, error announcements

### Context Needed
- architecture/patterns.md
- architecture/data-flow.md
- architecture/error-handling.md
- infrastructure/security.md
- workflow/implementation.md

---

## Phase 3 — KYC Verification

### Goal
Implement KYC verification page with document upload flow and status display.

### Tasks
- Define KYC types (`src/types/kyc.ts`): `KYCStatus`, `KYCDocument`, `KYCSubmission`
- Create API stubs (`src/api/kyc.ts`): `getKYCStatus`, `submitKYCDocuments`
- Create `useKYC` hook for KYC status and submission
- Create `KYCPage` with multi-step flow: personal info → document upload → confirmation
- Create `DocumentUpload` component (file input with preview, type constraints)
- Create `KYCStatus` component (pending/approved/rejected display)
- Add `/kyc` route (protected)
- Gate wallet/betting features behind KYC completion (display a prompt to complete KYC)

### Allowed Files
- `src/types/kyc.ts`
- `src/api/kyc.ts`
- `src/hooks/useKYC.ts`
- `src/components/kyc/*`
- `src/pages/KYCPage.tsx`
- `src/router.tsx` (add KYC route)

### Forbidden Changes
- No changes to auth logic
- No wallet or betting logic

### Verify Commands
```bash
npm run build
npm run lint
npx vitest run
```

### Acceptance Criteria
- [ ] KYC page shows current verification status
- [ ] Multi-step form collects personal info and documents
- [ ] File upload component accepts images/PDFs with size limits
- [ ] Form validation with Zod
- [ ] Status states: not started, pending review, approved, rejected
- [ ] Accessible: form labels, error messages, step indicators

### Context Needed
- architecture/component-design.md
- architecture/patterns.md
- architecture/error-handling.md
- workflow/implementation.md

---

## Phase 4 — Wallet (Deposit & Withdraw)

### Goal
Implement wallet page with balance display, deposit flow, and withdrawal flow.

### Tasks
- Define wallet types (`src/types/wallet.ts`): `WalletBalance`, `Transaction`, `DepositRequest`, `WithdrawRequest`
- Create API stubs (`src/api/wallet.ts`): `getBalance`, `getTransactions`, `deposit`, `withdraw`
- Create `useWallet` hook (balance, transactions, deposit/withdraw mutations)
- Create `BalanceCard` component (current balance display)
- Create `DepositForm` component (amount + payment method selection)
- Create `WithdrawForm` component (amount + destination)
- Create `TransactionList` component (paginated transaction history)
- Create `WalletPage` composing balance, deposit, withdraw, and recent transactions
- Add `/wallet` route (protected, requires KYC)

### Allowed Files
- `src/types/wallet.ts`
- `src/api/wallet.ts`
- `src/hooks/useWallet.ts`
- `src/components/wallet/*`
- `src/pages/WalletPage.tsx`
- `src/router.tsx` (add wallet route)

### Forbidden Changes
- No changes to auth or KYC logic
- No betting logic

### Verify Commands
```bash
npm run build
npm run lint
npx vitest run
```

### Acceptance Criteria
- [ ] Balance displayed prominently on wallet page
- [ ] Deposit form with amount validation (min/max)
- [ ] Withdraw form with amount validation (cannot exceed balance)
- [ ] Transaction list with type, amount, date, status
- [ ] Loading and error states for all async operations
- [ ] Currency formatting consistent throughout
- [ ] Accessible: forms, data tables, balance announced to screen readers

### Context Needed
- architecture/component-design.md
- architecture/data-flow.md
- architecture/error-handling.md
- workflow/implementation.md

---

## Phase 5 — Betting Core (Odds Display & Bet Placement)

### Goal
Implement real-time odds display and bet placement flow.

### Tasks
- Define betting types (`src/types/betting.ts`): `Event`, `Market`, `Odds`, `BetSlip`, `BetRequest`, `BetConfirmation`
- Create API stubs (`src/api/bets.ts`): `getEvents`, `getMarkets`, `getOdds`, `placeBet`
- Create `useWebSocket` hook (generic WebSocket connection with reconnection logic)
- Create `useBets` hook (events, markets, odds queries + place bet mutation)
- Create `EventCard` component (event name, teams/participants, start time)
- Create `OddsDisplay` component (real-time odds with visual change indicators — flash on update)
- Create `BetSlip` component (selected bets, stake input, potential payout calculation, confirm button)
- Create `BetConfirmation` component (success/failure display after placement)
- Create `BettingPage` composing event list, odds, and bet slip
- Add `/betting` route (protected, requires KYC)
- Connect `OddsDisplay` to WebSocket for live updates

### Allowed Files
- `src/types/betting.ts`
- `src/api/bets.ts`
- `src/hooks/useWebSocket.ts`
- `src/hooks/useBets.ts`
- `src/components/betting/*`
- `src/pages/BettingPage.tsx`
- `src/router.tsx` (add betting route)

### Forbidden Changes
- No changes to auth, KYC, or wallet logic
- No bet history logic (separate phase)

### Verify Commands
```bash
npm run build
npm run lint
npx vitest run
```

### Acceptance Criteria
- [ ] Events listed with markets and odds
- [ ] Odds update in real time via WebSocket (with visual change indicator)
- [ ] User can add selections to bet slip
- [ ] Bet slip calculates potential payout
- [ ] Stake validation (min/max, sufficient balance)
- [ ] Bet confirmation shown after placement
- [ ] Loading, error, and empty states handled
- [ ] Accessible: live regions for odds updates, keyboard-navigable bet slip

### Context Needed
- architecture/component-design.md
- architecture/data-flow.md
- architecture/state-management.md
- architecture/error-handling.md
- workflow/implementation.md

---

## Phase 6 — Bet History

### Goal
Implement bet history page with filtering and detail view.

### Tasks
- Extend betting types if needed: `BetHistoryItem`, `BetStatus`, `BetHistoryFilters`
- Create API stubs: `getBetHistory`, `getBetDetail`
- Create `useBetHistory` hook (paginated history query with filters)
- Create `BetHistoryList` component (table/list of past bets with status, event, stake, payout)
- Create `BetDetail` component (expanded view of a single bet)
- Create `HistoryFilters` component (date range, status, event type)
- Create `BetHistoryPage` composing filters, list, and detail
- Add `/history` route (protected)

### Allowed Files
- `src/types/betting.ts` (extend if needed)
- `src/api/bets.ts` (add history endpoints)
- `src/hooks/useBetHistory.ts`
- `src/components/history/*`
- `src/pages/BetHistoryPage.tsx`
- `src/router.tsx` (add history route)

### Forbidden Changes
- No changes to active betting logic
- No changes to wallet or auth

### Verify Commands
```bash
npm run build
npm run lint
npx vitest run
```

### Acceptance Criteria
- [ ] Bet history list with pagination
- [ ] Filter by status (pending, won, lost, void), date range
- [ ] Bet detail shows full event info, odds at time of placement, outcome
- [ ] Empty state when no bets exist
- [ ] Loading and error states
- [ ] Accessible: data table with proper headers, filter form labels

### Context Needed
- architecture/component-design.md
- architecture/data-flow.md
- workflow/implementation.md

---

## Phase 7 — Notifications

### Goal
Implement notification system with real-time delivery and notification center.

### Tasks
- Define notification types (`src/types/notifications.ts`): `Notification`, `NotificationType`, `NotificationPreferences`
- Create API stubs (`src/api/notifications.ts`): `getNotifications`, `markAsRead`, `markAllAsRead`
- Create `useNotifications` hook (notifications query, unread count, mark as read mutations, WebSocket subscription)
- Create `NotificationBell` component (icon with unread badge in header)
- Create `NotificationItem` component (individual notification with type icon, message, timestamp, read/unread styling)
- Create `NotificationList` component (dropdown or panel from bell, paginated)
- Create `NotificationsPage` for full notification history
- Connect to WebSocket for real-time notification delivery
- Add toast notifications for high-priority alerts (bet won, deposit confirmed)
- Create `Toast` common component if not already built in Phase 1
- Add `/notifications` route (protected)

### Allowed Files
- `src/types/notifications.ts`
- `src/api/notifications.ts`
- `src/hooks/useNotifications.ts`
- `src/components/notifications/*`
- `src/components/common/Toast.tsx` (if not created in Phase 1)
- `src/components/layout/Header.tsx` (add NotificationBell)
- `src/pages/NotificationsPage.tsx`
- `src/router.tsx` (add notifications route)

### Forbidden Changes
- No changes to betting, wallet, or auth logic
- Header change limited to adding NotificationBell

### Verify Commands
```bash
npm run build
npm run lint
npx vitest run
```

### Acceptance Criteria
- [ ] Bell icon in header shows unread count badge
- [ ] Dropdown/panel shows recent notifications
- [ ] Notifications delivered in real time via WebSocket
- [ ] Mark individual or all as read
- [ ] Full notification history page with pagination
- [ ] Toast for high-priority notifications
- [ ] Accessible: `aria-live` for new notifications, badge announced, keyboard-navigable list

### Context Needed
- architecture/component-design.md
- architecture/data-flow.md
- architecture/accessibility.md
- workflow/implementation.md

---

## Phase 8 — Error Handling, Testing & Polish

### Goal
Add error boundaries, comprehensive loading/error/empty states, and tests for all features.

### Tasks
- Create `ErrorBoundary` component (class component, per architecture/error-handling.md pattern)
- Add root-level error boundary wrapping `<App>`
- Add per-route error boundaries
- Audit all pages for consistent loading states (skeletons or spinners)
- Audit all pages for empty states
- Add toast component for transient errors if not done in Phase 7
- Write unit tests for custom hooks (`useAuth`, `useWallet`, `useBets`, `useNotifications`)
- Write component tests for common components (Button, Input, Card, Modal)
- Write integration tests for auth flow (login, register, protected route redirect)
- Write integration tests for bet placement flow
- Run accessibility audit with axe-core
- Fix any a11y violations found

### Allowed Files
- `src/components/common/ErrorBoundary.tsx`
- `src/**/*.test.tsx`
- `src/**/*.test.ts`
- Any file that needs error/loading/empty state additions

### Forbidden Changes
- No new features
- No API endpoint changes

### Verify Commands
```bash
npm run build
npm run lint
npx vitest run
npx vitest run --coverage    # if coverage configured
```

### Acceptance Criteria
- [ ] Error boundary catches render errors and shows fallback UI
- [ ] All async operations have loading, error, and empty states
- [ ] Test suite passes with coverage for all hooks and critical flows
- [ ] No ESLint a11y warnings
- [ ] Build succeeds with no TypeScript errors
- [ ] No console errors or warnings in normal operation

### Context Needed
- architecture/error-handling.md
- architecture/accessibility.md
- workflow/testing.md
- workflow/implementation.md

---

## Next Step
```
execute plan 1 for TEST-1
```
