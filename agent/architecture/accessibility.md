# Accessibility (a11y)
> Tags: accessibility, wcag, aria, keyboard, screen-reader
> Scope: Accessibility requirements and patterns for the application
> Last updated: initialise

## Standard
- Target: **WCAG 2.1 AA** compliance
- Testing: automated (eslint-plugin-jsx-a11y not yet installed) + manual

## Current State
The default Vite scaffold has minimal accessibility:
- `<html lang="en">` is set in `index.html`
- `<meta name="viewport">` is set for responsive behavior
- Logo images have `alt` text (`"Vite logo"`, `"React logo"`)
- External links do NOT have `rel="noopener noreferrer"` (missing from scaffold)
- No semantic landmark elements (`<header>`, `<main>`, `<nav>`, `<footer>`)
- No ARIA attributes
- No skip-to-content link
- No `eslint-plugin-jsx-a11y` installed

## Semantic HTML First
```tsx
// CORRECT — semantic elements
<header>...</header>
<nav aria-label="Main navigation">...</nav>
<main>...</main>
<section aria-labelledby="section-title">...</section>
<footer>...</footer>
<button onClick={handleClick}>Save</button>

// WRONG — divs with roles
<div role="banner">...</div>
<div role="navigation">...</div>
<div role="main">...</div>
<div onClick={handleClick}>Save</div>  // not keyboard accessible
```

## ARIA Rules
- Use native HTML elements FIRST — ARIA is a last resort
- Every interactive element must be keyboard accessible
- Every image must have `alt` text (or `alt=""` for decorative)
- Every form input must have a visible `<label>` or `aria-label`
- Every icon-only button must have `aria-label`
- Live regions for dynamic content: `aria-live="polite"` or `aria-live="assertive"`

## Keyboard Navigation
- The counter button is natively keyboard accessible (standard `<button>`)
- Tab order follows DOM order
- Focus styles use browser defaults

## Color & Contrast
- Dark mode: white text (#fff at 0.87 opacity) on dark background (#242424)
- Light mode: dark text (#213547) on white background (#ffffff)
- Contrast ratios have not been formally audited

## Recommendations (for future tickets)
- Install `eslint-plugin-jsx-a11y` and add to ESLint config
- Add `rel="noopener noreferrer"` to external `target="_blank"` links
- Use semantic HTML landmarks when layout components are created
- Add a skip-to-content link
- Ensure all interactive elements are keyboard accessible
- Add focus management for modals/dialogs when introduced

## Component Checklist
When creating or reviewing any component:
- [ ] Semantic HTML elements used where possible
- [ ] All interactive elements keyboard accessible
- [ ] Focus visible on all focusable elements
- [ ] Images have appropriate `alt` text
- [ ] Form inputs have associated labels
- [ ] Color contrast meets WCAG AA (4.5:1 / 3:1)
- [ ] Dynamic content uses `aria-live` regions
- [ ] Modals trap focus and return focus on close
- [ ] No content conveyed by color alone

## Changelog
<!-- [PROJ-123] Added focus management to modal component -->
