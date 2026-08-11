# Frontend Rules

Constraints on building user-facing UI.

## Component Boundaries

- Give each component a single, clear responsibility.
- Keep component props explicit, typed, and minimal.
- Do not reach outside a component's boundary to touch shared state directly.

## State Management

- Prefer local state and lift it only when data must be shared.
- Keep state changes explicit and traceable; avoid hidden mutation.
- Derive computed values instead of storing redundant state.

## Forms

- Manage form state explicitly and keep it aligned with what the user sees.
- Preserve user input across validation failures instead of clearing it.
- Make submit explicit about success and failure.

## Validation

- Validate input on the client for usability, but never rely on it for safety.
- Mirror server validation with a matching client rule set to show errors early.
- Show validation feedback close to the field it applies to.

## Accessibility

- Use semantic HTML and native controls before custom widgets.
- Provide labels, focus management, and keyboard-accessible flows.
- Maintain sufficient contrast and expose state changes to assistive technology.
- Do not break navigation with custom scroll, focus, or interaction handling.

## Responsive Behavior

- Design for the full range of supported viewports from the start, not as an afterthought.
- Let content scale rather than hiding critical functionality.
- Test at the smallest supported size.

## Loading and Error States

- Represent loading, empty, and error states explicitly in the UI.
- Never leave the user blocked on an unhandled failure.
- Show retry affordances where recovery is possible.

## API Integration

- Centralize API calls rather than scattering fetch logic in components.
- Normalize API data at the integration boundary, not inside rendering.
- Propagate API errors to the relevant UI state.

## Security

- Never embed secrets, tokens, or credentials in client code.
- Treat all user content as untrusted; escape before rendering.
- Do not disable or weaken built-in browser protections for convenience.

## Performance

- Avoid unnecessary re-renders and large bundle payloads.
- Use frameworks and tooling already present; do not add performance libraries speculatively.
- Measure before optimizing; keep lists, large images, and animations efficient.