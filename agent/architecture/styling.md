# Styling & Design System
> Tags: css, styling, theme, responsive, design-tokens, breakpoints
> Scope: How the application is styled, themed, and made responsive
> Last updated: initialise

## Styling Approach
- Method: Vanilla CSS (global files, no CSS Modules, no CSS-in-JS, no Tailwind)
- Location: `src/index.css` (global reset/typography) and `src/App.css` (component-level)

## Design Tokens
The default Vite scaffold uses hardcoded values, not CSS custom properties for design tokens. The existing CSS variables are limited to the `:root` in `index.css`:

```css
:root {
  font-family: system-ui, Avenir, Helvetica, Arial, sans-serif;
  line-height: 1.5;
  font-weight: 400;
  color-scheme: light dark;
  color: rgba(255, 255, 255, 0.87);
  background-color: #242424;
}
```

No formal design token system is established.

## Responsive Breakpoints
No breakpoints are defined. The only responsive consideration is `min-width: 320px` on `body`.

## Theming
- Strategy: `prefers-color-scheme` media query for automatic light/dark mode
- Dark mode: Supported via CSS `@media (prefers-color-scheme: light)` override
- No manual theme toggle — relies on OS/browser preference

## Component Styling Rules
- Co-locate styles with components (same directory)
- Use semantic class names
- No inline styles exist in the current codebase
- The project does not use CSS custom properties for design tokens yet

## Z-Index Scale
Not defined — no overlapping UI exists yet.

## Changelog
<!-- [PROJ-123] Added dark mode theme variables -->
