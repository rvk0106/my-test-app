# Component Design
> Tags: components, props, composition, reusability, ui
> Scope: How components are structured, composed, and reused
> Last updated: initialise

## Current State
The project has a single component (`App.tsx`) — the default Vite scaffold. No component library, no shared components, no feature components exist yet.

## Component Types

### Page Components
- Not used — no router or pages directory exists

### Feature Components
- Not used — no `src/components/` directory exists

### Common / Shared Components
- Not used — no reusable components exist

### Layout Components
- Not used — no layout wrapper, header, sidebar, or footer

## Component Rules

### Functional Components Only
```tsx
// CORRECT
const UserCard: React.FC<UserCardProps> = ({ name, avatar }) => {
  return (
    <div className={styles.card}>
      <img src={avatar} alt={`${name}'s avatar`} />
      <h3>{name}</h3>
    </div>
  );
};

// WRONG — no class components
class UserCard extends React.Component { ... }
```

### Props Interface
- ALWAYS define a TypeScript interface for props
- Use descriptive names, not abbreviations
- Default props via destructuring defaults

### Composition Over Configuration
- Prefer children and composition patterns over prop overload

### Single Responsibility
- Each component does ONE thing
- If a component file exceeds ~200 lines, consider splitting
- Extract hooks for complex logic

## Component File Structure
When components are added, follow this convention:
```
src/components/[feature]/
├── FeatureComponent.tsx           → main component
├── FeatureComponent.test.tsx      → tests
├── FeatureComponent.module.css    → styles (if CSS Modules adopted)
├── useFeatureLogic.ts             → custom hook (if complex logic)
└── index.ts                       → re-export
```

## Changelog
<!-- [PROJ-123] Added compound component pattern for Card -->
