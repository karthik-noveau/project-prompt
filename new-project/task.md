# AI Project Development Protocol

<details>
<summary><strong>📋 Task Generation (task-generation.md)</strong></summary>

````md
# AI PROJECT SPECIFICATION & DEVELOPMENT PROTOCOL

The application MUST NOT generate any application source code until the complete `spec/` directory has been generated and approved.

The `spec/` directory is the single source of truth for architecture, UI, workflows, implementation order and development rules.

## Directory Structure

spec/
├── architecture.md
├── codebase-guide.md
├── ui-prototypes/
│   ├── <page-1>.html
│   ├── <page-2>.html
│   └── ...
└── engines/
    ├── engine-01-<work-name>.md
    ├── engine-02-<work-name>.md
    └── ...

## Rules

- Generate the complete `spec/` directory before writing any application source code.
- `architecture.md` must contain the complete implementation blueprint.
- `codebase-guide.md` must remain completely empty.
- Create one HTML UI prototype per page.
- Split implementation into independent engines.
- Each engine must have:
  - Objective
  - Scope
  - Dependencies
  - Files to modify
  - Implementation steps
  - Acceptance criteria
  - Edge cases
  - Validation checklist
  - Test cases
  - Completion checklist
- Complete one engine at a time.
- Stop after every engine and request approval.
- Never generate future engine source code before approval.

`````

</details>

---

<details>
<summary><strong>📚 Codebase Guide (codebase-guide.md)</strong></summary>

```md
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
| spec/ | Source of truth |
| common/ | Shared modules only |
| common/api/ | Data loading |
| common/components/ | Reusable components |
| store/ | Zustand stores |
| pages/<page>/ | Self-contained feature |
| theme/ | Global styles |
| App.tsx | Bootstrap and routing |

## Naming

- Folders → kebab-case
- Components → PascalCase.tsx
- Hooks → useCamelCase.ts
- Utilities → camelCase.ts
- Types → types.ts
- Constants → constants.ts
- Stores → <domain>.store.ts
- CSS Modules → styles.module.css

## TypeScript

- Strict mode
- Never use any
- Explicit return types
- Prefer type over interface

## React

- Functional components
- Hooks only
- Composition in index.tsx
- Business logic in hooks/stores

## Routing

- React Router
- Lazy-loaded pages
- Central route config
- 404 page

## State

- Zustand
- One store per domain
- Derived values computed
- No direct mutation

## Styling

- CSS Modules only
- No inline styles
- No Tailwind
- No Styled Components
- Colours from theme/colours.css

## Testing

- Jest
- React Testing Library
- Co-located unit tests
- Integration tests in __tests__

## Forbidden

- any
- console.log
- debugger
- TODO
- FIXME
- Hardcoded colours
- Dead code
- Cross-page imports

```

</details>

---

<details>
<summary><strong>🚀 Development (development.md)</strong></summary>

```md
# Development Workflow

## Phase 1

Generate the complete `spec/` directory.

Required files:

- architecture.md
- codebase-guide.md
- ui-prototypes/
- engines/

Wait for approval.

---

## Phase 2

Implement Engine 01.

Requirements:

- Complete implementation
- Validation
- Unit tests
- Integration tests
- TypeScript passes
- ESLint passes

Stop.

Wait for approval.

---

## Phase 3

Implement Engine 02.

Repeat the same process.

Continue until all engines are complete.

---

## General Rules

- Never implement multiple engines together.
- Never skip engines.
- Never partially implement an engine.
- Never generate future engine code.
- Every engine must pass:
  - Build
  - TypeScript
  - ESLint
  - Jest

---

## Quality Checklist

- DRY
- KISS
- SOLID
- Composition over inheritance
- Early returns
- No duplicate logic
- No deep nesting
- No dead code
- No unused imports
- No unused variables

---

## Performance

- Lazy loading
- Memoization
- Split large components
- Avoid unnecessary renders

---

## Accessibility

- Semantic HTML
- Keyboard support
- ARIA attributes
- Labels
- Focus states
- Colour contrast

---

## Error Handling

Every feature must support:

- Loading
- Success
- Empty
- Error

Never fail silently.

```

</details>
````
