# AI Project Development Protocol

<details>
<summary><strong>📋 Task Generation (task-generation.md)</strong></summary>

````text
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
    ├── engine-status.md
    ├── engine-01-<work-name>.md
    ├── engine-02-<work-name>.md
    └── ...

## Rules

- Generate the complete `spec/` directory before writing any application source code.
- `architecture.md` must contain the complete implementation blueprint.
- `codebase-guide.md` must remain completely empty.
- Create one HTML UI prototype per page.
- Split implementation into independent engines.
- One engine performs exactly one responsibility.
- Every engine must be completed, validated and approved before the next engine begins.
- Later engines may depend only on previously completed engines.
- Never merge multiple responsibilities into a single engine.
- Never generate future engine source code before approval.

Each engine must contain:

- Objective
- Scope
- Dependencies
- Files to create
- Files to modify
- Implementation steps
- Acceptance criteria
- Edge cases
- Validation checklist
- Test cases
- Completion checklist

Implementation Order

1. Generate complete `spec/`
2. Wait for approval.
3. Implement Engine 01.
4. Validate.
5. Run tests.
6. Stop.
7. Request approval.
8. Continue with the next engine.

`````

</details>

---

<details>
<summary><strong>📚 Codebase Guide (codebase-guide.md)</strong></summary>

```text
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
| spec/ | Source of truth for specifications |
| common/ | Shared modules only |
| common/api/ | Data loading only |
| common/components/ | Reusable UI only |
| store/ | Zustand stores only |
| pages/<page>/ | Self-contained feature |
| pages/<page>/index.tsx | Composition only |
| theme/ | Global styling |
| App.tsx | Bootstrap and routing only |

## Naming

- Folders → kebab-case
- Page folders → kebab-case
- Components → PascalCase.tsx
- Hooks → useCamelCase.ts
- Utilities → camelCase.ts
- Types → types.ts
- Constants → constants.ts
- Stores → <domain>.store.ts
- CSS Modules → styles.module.css
- JSON → kebab-case.json
- Icons → kebab-case.svg

## Imports

1. React
2. Third-party libraries
3. Common modules
4. Store
5. Page modules
6. Relative imports
7. CSS Modules

Use absolute imports whenever possible.

Remove unused imports.

## TypeScript

- Strict mode
- Never use any
- Prefer type over interface
- Explicit return types
- Exhaustive switch statements
- Readonly where appropriate

## React

- Functional components only
- React Hooks only
- Composition inside index.tsx
- Business logic belongs inside hooks/stores
- Avoid unnecessary re-renders

## Routing

- React Router
- Lazy-loaded pages
- Centralized route configuration
- 404 page

## Data Fetching

- Frontend only
- Local JSON only
- No backend
- Components never fetch data
- Hooks call common/api
- Support Loading / Success / Empty / Error

## State

- Zustand
- One store per domain
- Derived values computed
- No direct mutation
- Reset page state when required

## Styling

- CSS Modules only
- No inline styles
- No Tailwind
- No Styled Components
- No Emotion
- Colours only from theme/colours.css

## Performance

- Lazy loading
- Memoization
- Split large components
- Avoid unnecessary renders

## Accessibility

- Semantic HTML
- Keyboard accessible
- Proper ARIA
- Labels
- Focus states
- Colour contrast

## Testing

- Jest
- React Testing Library

Co-located Tests

common/components/
UserAvatar.tsx
UserAvatar.test.tsx

pages/<page>/hooks/
useFormState.ts
useFormState.test.ts

Integration Tests

__tests__/

## File Rules

- One responsibility per file
- One primary export
- Maximum 300 lines/file

## Code Quality

- DRY
- KISS
- SOLID
- Composition over inheritance
- Early returns
- No duplicate logic

## Forbidden

- any
- console.log
- debugger
- TODO
- FIXME
- Hardcoded colours
- Magic numbers
- Magic strings
- Dead code
- Circular imports
- Cross-page imports
- Duplicate logic
- Unused imports
- Unused variables

```

</details>

---

<details>
<summary><strong>🚀 Development (development.md)</strong></summary>

```text
# Development Workflow

## Phase 1

Generate the complete `spec/` directory.

Required files

- architecture.md
- codebase-guide.md
- ui-prototypes/
- engines/

Wait for approval before generating any application source code.

---

## Phase 2

Implement Engine 01.

Requirements

- Complete implementation
- Validation
- Unit tests
- Integration tests
- TypeScript passes
- ESLint passes
- Build passes

Stop.

Wait for approval.

---

## Phase 3

Implement Engine 02.

Repeat the same workflow until every engine has been completed and approved.

---

# Engine Progress Tracking

Maintain one shared status file for the entire project.

Directory

spec/
└── engines/
    ├── engine-status.md
    ├── engine-01-<work-name>.md
    ├── engine-02-<work-name>.md
    └── ...

## Purpose

The `engine-status.md` file represents the real-time progress of the currently active engine.

There must only be **one** status file for the entire project.

---

## Update Frequency

Update the status file whenever the current engine reaches:

- 20%
- 40%
- 60%
- 80%
- 100%

---

## Status File Rules

- Always track only the currently active engine.
- Replace the current engine section when a new engine starts.
- Keep completed engines in a "Completed Engines" section.
- Progress updates must be concise.
- Mention only completed functionality.
- Do not include implementation details.
- Do not include future work beyond the current engine.
- Update immediately after each milestone.

---

## engine-status.md Structure

# Engine Status

## Current Engine

- Engine Name
- Engine Number
- Progress Percentage
- Current Phase

## Completed Functionality

Provide a minimized summary, for example:

- Routing completed
- Dashboard layout completed
- Sidebar completed
- Authentication store completed
- API abstraction completed

## Remaining Work

Short bullet list of remaining functionality.

## Files Modified

Only list modified files.

Example

- pages/dashboard/index.tsx
- store/dashboard.store.ts
- common/api/dashboard.ts

## Validation

- Build
- TypeScript
- ESLint
- Unit Tests
- Integration Tests

Display

✔ Passed

✖ Failed

⏳ Pending

## Last Updated

Timestamp of latest milestone.

---

## Completed Engines

Maintain a growing list.

Example

- ✔ Engine 01 — Project Setup
- ✔ Engine 02 — Routing
- ✔ Engine 03 — Authentication

---

## Engine Completion Rules

An engine is considered complete only when all of the following are satisfied:

- Implementation completed
- Acceptance criteria passed
- Validation checklist completed
- Build passed
- TypeScript passed
- ESLint passed
- Unit tests passed
- Integration tests passed
- engine-status.md updated to 100%
- User approval received

Only after approval may the next engine begin.

---

## General Rules

- Never implement multiple engines together.
- Never skip engines.
- Never partially implement an engine.
- Never generate future engine code.
- One engine equals one responsibility.
- Stop after every completed engine.
- Wait for user approval before continuing.
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
- Proper ARIA attributes
- Labels for inputs
- Visible focus states
- Sufficient colour contrast

---

## Error Handling

Every feature must support:

- Loading
- Success
- Empty
- Error

Never fail silently.

Provide meaningful error messages.

```

</details>
