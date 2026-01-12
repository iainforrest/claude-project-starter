---
name: domain-frontend
domain: frontend
description: Frontend/UI development patterns for React, Vue, Angular, and web frontends covering component composition, state management, hooks, accessibility, performance, and styling.
triggers: ["*.tsx", "*.jsx", "*.vue", "*.svelte", "*/components/*", "*/hooks/*", "*/pages/*"]
---

## Patterns to Apply

### Component Composition
- **Atomic Design**: Break into atoms (Button, Input), molecules (FormField), organisms (Form)
- **Single Responsibility**: Each component does one thing well
- **Composition over Inheritance**: Use children/slots, not class extension
- **Props Interface**: Clear, documented prop types; use defaults for optional props
- **Render Props/Slots**: Pass UI logic without prop drilling

### State Management
- **Local State**: useState for single-component UI state (form inputs, UI toggles)
- **Context API**: Share state 2-3 levels deep; avoid for high-frequency updates
- **Store Pattern**: Redux/Pinia/Zustand for app-wide state, async data
- **Separation**: Keep UI state separate from business logic state
- **Derived State**: Compute from props/state, don't duplicate state

### Hooks & Lifecycle (React)
- **useEffect Dependencies**: Always specify deps; missing deps = stale closures
- **Cleanup**: Return cleanup functions for subscriptions, timers, event listeners
- **Custom Hooks**: Extract reusable logic (useApi, useForm, useLocalStorage)
- **Rule of Hooks**: Call hooks conditionally with care; extract to custom hooks
- **useCallback/useMemo**: Memoize only expensive computations or callbacks passed to children

### Accessibility (a11y)
- **Semantic HTML**: Use `<button>`, `<nav>`, `<main>`, `<form>` not styled divs
- **ARIA Labels**: Add aria-label to icon buttons, aria-labelledby to sections
- **Keyboard Navigation**: Tab order, :focus-visible, trap focus in modals
- **Color Contrast**: WCAG AA minimum 4.5:1 for text; test with tools
- **Alt Text**: Meaningful descriptions for images; skip decorative images
- **Error Messages**: Link to form fields with aria-describedby, announce dynamically

### Performance
- **Code Splitting**: Lazy load routes with React.lazy/Suspense; split heavy components
- **Memoization**: React.memo for pure components receiving new props frequently
- **Image Optimization**: Lazy load with IntersectionObserver; srcset for responsive; WebP format
- **List Virtualization**: Virtualize long lists (react-window, react-virtual)
- **Bundle Size**: Monitor with webpack-bundle-analyzer; tree-shake unused imports
- **Render Optimization**: Avoid inline objects/functions in JSX; extract to module scope

### Styling Approaches
- **CSS Modules**: Scoped styles, import as objects; best for component-level styles
- **CSS-in-JS**: Emotion/Styled-Components for dynamic theming, media queries
- **Utility-First**: Tailwind for rapid prototyping; pair with CSS modules for complex layouts
- **Design Tokens**: Centralized color, spacing, font scales; reference not hardcoded values
- **Responsive**: Mobile-first; min-width media queries; rem units for scalability
- **Dark Mode**: CSS custom properties or class-based (html.dark-mode); test both themes

## Pitfalls to Avoid

- **Prop Drilling**: Context, composition, or store pattern instead
- **State in useEffect**: Causes infinite loops; move to useState or callbacks
- **Missing Dependencies**: useEffect deps cause stale data; use linter (eslint-plugin-react-hooks)
- **Unoptimized Renders**: Every prop change triggers child re-render; memoize or restructure
- **Inline Styling**: Dynamic styles in JSX; move to CSS modules or CSS-in-JS
- **Overcomplicated Components**: >300 lines = split it; multiple responsibilities = extract
- **Hardcoded Values**: Colors, spacing, breakpoints in components; use design tokens
- **Async in useEffect**: Use promise chains or custom hooks; avoid async function as useEffect callback
- **Focus Loss**: Modal dialogs, tabs, overlays should trap focus; test with keyboard
- **Missing Error Boundaries**: Unhandled errors crash entire app; wrap routes with boundaries
- **Flickering Hydration**: Client-rendered content differs from server; ensure consistency

## Quality Checks

### Before Submitting Code
- [ ] No console errors/warnings (except expected logs)
- [ ] PropTypes or TypeScript types defined for all props
- [ ] Component re-renders checked in DevTools Profiler (no excessive renders)
- [ ] Keyboard navigation works (Tab, Enter, Escape)
- [ ] Screen reader tested (Lighthouse a11y audit, NVDA/JAWS spot check)
- [ ] Mobile responsive (tested at 375px, 768px, 1200px)
- [ ] Loading states visible (spinners, skeletons)
- [ ] Error states handled (error message + recovery action)
- [ ] Empty states have guidance (not blank)
- [ ] Images optimized (no oversized files; formats tested)
- [ ] CSS bundle size reasonable (<100KB gzip for styles)
- [ ] No unused imports/code
- [ ] Linting passes (ESLint, Prettier)
- [ ] Tests pass (unit, integration; a11y checks)
- [ ] Design tokens used, not hardcoded values
