---
name: frontend-development
description: Use when building or modifying user-facing UI. Use for UI architecture, component design, state management, forms, validation, accessibility, performance, responsive design, and API integration.
---

# Frontend Development

## When to use

Use when implementing or changing any UI: new components, screens, forms, interactions, or wiring the client to backend APIs. Also use when auditing frontend code for structure, accessibility, or performance.

## Process

1. **Follow the existing UI architecture**: Match the project's framework, component conventions, styling approach, and file organization. Inspect neighboring components before writing new ones.
2. **Design components around responsibility**: One component, one concern. Compose small components; keep presentational components separate from containers/state. Share logic through established patterns (hooks, composables, utilities) rather than duplicating it.
3. **Manage state where it matters**: Keep global/remote state in the project's state solution (store, context, query cache) and local UI state in components. Derive data; avoid duplicating the same data in multiple stores.
4. **Build forms with explicit validation**: Validate inputs client-side with the project's form library or patterns. Validate on submit (and after interaction for better UX). Never rely on client-side validation alone — the backend remains the security boundary.
5. **Integrate APIs deliberately**: Centralize API calls in a service layer. Handle loading, empty, error, and stale states for every request. Avoid writing fetch logic inside components.
6. **Make it accessible**: Use semantic HTML (`button`, `label`, `nav`), keyboard navigation, visible focus, ARIA only where needed, and adequate color contrast. Never make interactive behavior mouse-only.
7. **Build responsively**: Design for the smallest to largest intended viewports using the project's breakpoints. Test at representative sizes; do not rely on device emulation alone.
8. **Watch performance**: Avoid large synchronous work on the main thread, unnecessary re-renders, layout thrashing, and unbounded renders of large lists. Lazy-load what is not needed on first paint.

## Important checks

- Does the change match existing component and styling conventions?
- Are all request states (loading, error, empty, success) handled in the UI?
- Is validation user-friendly but never the only line of defense?
- Is the UI keyboard-usable and are interactive elements correctly labeled?
- Does the layout hold at target viewport sizes?
- Are re-renders and bundle size justified?

## Common mistakes

- Importing a new library when the project already has a sanctioned one.
- Giant components mixing DOM, logic, and API calls.
- Resetting/fetching all global state on every navigation or keystroke.
- Silently swallowing errors and leaving the user with a frozen screen.
- Using divs where semantic elements are required, or a button that is actually a div.
- Optimizing prematurely with aggressive memoization before measuring.

## Completion

The feature is implemented within the existing UI architecture, components are cohesive and composable, state is managed at the right level, forms validate clearly, API integration handles all states, and the result is accessible, responsive, and free of obvious performance problems. Behavior was verified in the running app.