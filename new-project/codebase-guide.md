```text
# Codebase Architecture

## Structure

spec/

├── README.md
├── architecture.md
├── codebase-guide.md
├── prototypes/
└── engines/

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
| `common/` | Shared only — zero page-specific knowledge |
| `common/api/` | All data loading functions — nowhere else |
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

## Component Rules

- Maximum 200 lines per component
- Maximum 60 lines per function
- One component per file
- `index.tsx` contains composition only
- Business logic belongs in hooks or stores
- State and effects belong in hooks
- No prop drilling beyond 2 levels — use Zustand
- No imports across page boundaries
- No barrel exports unless explicitly requested

## Data Fetching

- Frontend only
- Local JSON only
- No backend server
- All data loading functions belong in `common/api/`
- Components never fetch directly
- Hooks call API functions
- Every fetch handles loading, success, error and empty states

## State (Zustand)

- One store per domain
- Derived values are computed, never stored
- All state mutations go through store actions
- No direct state mutation
- Reset page-scoped state on unmount when required

## Styling

- CSS Modules only
- Class names use `camelCase`
- No inline styles
- No Tailwind CSS
- No styled-components
- No Emotion
- Colours only through CSS variables from `theme/colours.css`
- No hardcoded colour values

## Testing

common/components/avatar-card/
  UserAvatar.tsx
  UserAvatar.test.tsx

pages/<page-name>/hooks/
  useFormState.ts
  useFormState.test.ts

- Unit tests are co-located with source files
- Integration tests live in `__tests__/` at the project root
- Every feature must include component, hook and store tests where applicable

## Forbidden

- `any`
- `console.log`
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
```
