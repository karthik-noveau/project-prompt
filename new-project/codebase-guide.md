````text
# Codebase Architecture

## Structure

src/
  assets/
    ├── logos/
    ├── icons/
    └── <page-name>/

  common/
    ├── api/
    ├── components/
    ├── constants/
    ├── hooks/
    └── utils/

  store/
    └── <domain>.store.ts

  pages/
    <page-name>/
      ├── index.tsx
      ├── components/
      ├── hooks/
      ├── constants.ts
      ├── types.ts
      ├── utils.ts
      ├── mocks/
      └── styles.module.css

  theme/
    ├── colours.css
    ├── fonts.css
    └── overrides.css

  App.tsx

## Boundaries

| Location | Rule |
|----------|------|
| `spec/` | Source of truth for architecture, specifications and implementation rules |
| `common/` | Shared modules only — zero page-specific knowledge |
| `common/api/` | All data loading functions belong here |
| `common/components/` | Reusable UI components only |
| `store/` | Zustand stores only — one file per domain |
| `pages/<page-name>/` | Self-contained feature — cannot import from another page |
| `pages/<page-name>/index.tsx` | Composition only — no business logic |
| `theme/` | Global styles only |
| `App.tsx` | Application bootstrap and routing only |

## Naming

| Item | Format |
|------|--------|
| Folders | `kebab-case` |
| Page folders | `kebab-case` |
| Components | `PascalCase.tsx` |
| Hooks | `useCamelCase.ts` |
| Utilities | `camelCase.ts` |
| Types | `types.ts` |
| Constants file | `constants.ts` |
| Constant values | `SCREAMING_SNAKE_CASE` |
| Zustand stores | `<domain>.store.ts` |
| CSS Modules | `styles.module.css` |
| JSON | `kebab-case.json` |
| Icons | `kebab-case.svg` |

## Imports

- Prefer absolute imports using project aliases.
- Import order:
  1. React
  2. Third-party libraries
  3. Common modules
  4. Store
  5. Page modules
  6. Relative imports
  7. CSS Modules
- Remove unused imports.

## TypeScript

- Strict mode enabled.
- Never use `any`.
- Prefer `type` unless interface extension is required.
- Use readonly where appropriate.
- Exported functions must have explicit return types.
- Use exhaustive switch statements.

## React

- Functional components only.
- React Hooks only.
- No class components.
- `index.tsx` performs composition only.
- Business logic belongs in hooks or stores.
- State and side effects belong in hooks.
- Memoize expensive computations when required.
- Prevent unnecessary re-renders.

## Component Rules

- Maximum 200 lines per component.
- Maximum 60 lines per function.
- One component per file.
- No prop drilling beyond two levels — use Zustand.
- No imports across page boundaries.
- No barrel exports unless explicitly requested.

## Routing

- React Router only.
- Lazy-load every page.
- Centralised route configuration.
- Include a 404 page.

## Data Fetching

- Frontend only.
- Local JSON only.
- No backend server.
- All data loading belongs in `common/api/`.
- Components never fetch data directly.
- Hooks call API functions.
- Handle loading, success, error and empty states for every request.

## State (Zustand)

- One store per domain.
- Derived values are computed, never stored.
- All state mutations go through store actions.
- No direct state mutation.
- Reset page-scoped state on unmount when required.

## Styling

- CSS Modules only.
- Class names use `camelCase`.
- No inline styles.
- No Tailwind CSS.
- No styled-components.
- No Emotion.
- Colours must come from CSS variables defined in `theme/colours.css`.
- No hardcoded colour values.

## Performance

- Lazy-load pages.
- Memoize derived values.
- Avoid unnecessary state.
- Split large components.
- Avoid unnecessary re-renders.

## Accessibility

- Use semantic HTML.
- Keyboard accessible.
- Proper ARIA attributes where required.
- Labels for all form fields.
- Visible focus states.
- Maintain sufficient colour contrast.

## Error Handling

- Never fail silently.
- Show user-friendly error messages.
- Validate external data.
- Handle loading, empty and error states consistently.

## Testing

common/components/avatar-card/
  UserAvatar.tsx
  UserAvatar.test.tsx

pages/<page-name>/hooks/
  useFormState.ts
  useFormState.test.ts

- Unit tests are co-located with source files.
- Integration tests live in the project root `__tests__/`.
- Every feature must include component, hook and store tests where applicable.
- All tests must pass before completion.

## File Rules

- One responsibility per file.
- One primary export per file.
- No file should exceed 300 lines.
- Split large files into smaller modules.

## Documentation

- Prefer self-documenting code.
- Add comments only for complex business logic.
- Avoid redundant comments.

## Code Quality

- Follow DRY, KISS and SOLID principles where applicable.
- Prefer composition over inheritance.
- Prefer early returns.
- Avoid deep nesting.
- Remove duplicate logic.

## Build Requirements

The project must:

- Build successfully without warnings.
- Pass TypeScript compilation.
- Pass ESLint.
- Pass all Jest tests.
- Contain zero dead code.
- Contain zero unused files.

## Forbidden

- `any`
- `console.log`
- `debugger`
- `TODO`
- `FIXME`
- Inline styles
- Hardcoded colours
- Magic numbers
- Magic strings
- Circular imports
- Cross-page imports
- Dead code
- Duplicate logic
- Unused imports
- Unused variables
````
