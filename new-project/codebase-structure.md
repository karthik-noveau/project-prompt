```text
# Codebase Architecture

## Structure

src/
  assets/
    ├── logo/
    ├── icons/
    └── <page_name>/

  common/
    ├── components/
    ├── hooks/
    ├── utils/
    ├── constants/
    └── api/

  store/
    └── <slice_name>.ts

  pages/
    <page_name>/
      ├── index.tsx
      ├── components/
      ├── hooks/
      ├── utils.ts
      ├── constants.ts
      └── style.module.css

  theme/
    ├── colors.css
    ├── override.css
    └── font.css

  App.tsx

## Boundaries

| Location | Rule |
|----------|------|
| `common/` | Shared only — zero page-specific knowledge |
| `common/api/` | All API calls — nowhere else |
| `store/` | Zustand slices only — one file per domain |
| `pages/<name>/` | Self-contained — cannot export to `common/` or other pages |
| `pages/<name>/index.tsx` | Layout + composition only — zero logic |
| `theme/` | Global styles only — never inside pages or common |
| `App.tsx` | Routing only — no logic, no state |

## Naming

| What | Format |
|------|--------|
| Folders | `snake_case` |
| Components | `snake_case.tsx` |
| Hooks | `useCamelCase.ts` |
| Utils | `lowercase.ts` |
| Constants | `SCREAMING_SNAKE_CASE` |
| Store slices | `<slice_name>.ts` |
| CSS Modules | `style.module.css` |
| Icons | `kebab-case.svg` |

No uppercase in any folder name.

## Component Rules

- Max 200 lines — split beyond this, no exceptions
- One component per file
- `index.tsx` — declarative JSX only, no `useState`, no `useEffect`
- State and effects live in `hooks/`
- No prop drilling beyond 2 levels — use Zustand
- No imports across page boundaries

## Data Fetching

- All API calls in `common/api/` — never inline in components or hooks
- Hooks call API functions — components call hooks
- Every fetch handles: loading / error / empty

## State (Zustand)

- One store slice per domain
- Derived values computed, not stored
- Actions defined in the store — no direct mutation outside actions
- Reset page-scoped store on unmount

## Styling

- CSS Modules only
- Class names `camelCase` inside module files
- No inline `style` props
- No Tailwind, styled-components, emotion
- Colors only via CSS variables from `theme/colors.css` — no hardcoded hex

## Testing

common/components/avatar_card/
  avatar_card.tsx
  avatar_card.test.tsx

pages/<name>/hooks/
  useFormState.ts
  useFormState.test.ts

- Unit tests co-located with source file
- Integration tests in `__tests__/` at project root
```
