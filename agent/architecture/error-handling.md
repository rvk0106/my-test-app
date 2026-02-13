# Error Handling
> Tags: errors, boundaries, api-errors, user-feedback, fallback
> Scope: How errors are caught, displayed, and recovered from
> Last updated: initialise

## Current State
No error handling infrastructure exists. No error boundaries, no API error handling, no form validation, no error UI components.

## Error Categories

| Category | Source | Handling |
|----------|--------|----------|
| **Render errors** | Component throws during render | Not handled — no Error Boundary exists |
| **API errors** | Network, 4xx, 5xx | Not applicable — no API calls |
| **Form validation** | Invalid user input | Not applicable — no forms |
| **Auth errors** | 401, expired token | Not applicable — no auth |
| **Not found** | 404, missing resource | Not applicable — no routing |
| **Unexpected** | Uncaught exceptions | Not handled — no global error boundary |

## Error Boundaries
Not implemented. When needed, follow this pattern:

```tsx
// src/components/common/ErrorBoundary.tsx
import { Component, ErrorInfo, ReactNode } from 'react';

interface Props {
  fallback: ReactNode;
  children: ReactNode;
  onError?: (error: Error, errorInfo: ErrorInfo) => void;
}

class ErrorBoundary extends Component<Props, { hasError: boolean }> {
  state = { hasError: false };

  static getDerivedStateFromError() {
    return { hasError: true };
  }

  componentDidCatch(error: Error, errorInfo: ErrorInfo) {
    this.props.onError?.(error, errorInfo);
  }

  render() {
    if (this.state.hasError) return this.props.fallback;
    return this.props.children;
  }
}
```

### Placement (when implemented)
- **Root**: Global boundary wrapping `<App>` → generic fallback
- **Route**: Per-route boundary → "Something went wrong on this page"
- **Feature**: Around risky components → feature-specific fallback

## API Error Handling
Not applicable — no API integration exists.

## User-Facing Error UI Rules
- ALWAYS show a meaningful message — never a blank screen or raw error
- Include a retry action where appropriate (button or link)
- For form validation: show errors inline next to the field
- For transient errors: use a toast/notification that auto-dismisses
- For fatal errors: show a full-page fallback with a "Go Home" action
- NEVER expose stack traces, error codes, or technical details to users

## Loading States
- Always pair error handling with loading states
- Show skeleton / spinner while loading
- Show error UI if request fails
- Show empty state if data is empty

## Changelog
<!-- [PROJ-123] Added per-route error boundaries -->
