# AI Project Development Protocol

## Tech Stack

```text
Framework   : React
Language    : TypeScript
Build Tool  : Vite
State       : Zustand
Routing     : React Router
Styling     : CSS Modules
Testing     : Jest
```

## Spec Structure

```text
spec/
├── architecture.md
├── codebase-guide.md
├── development.md
├── ui-prototypes/
└── engines/
```

---

<details>
<summary><strong>🏗️ Architecture (architecture.md)</strong></summary>

```md
# architecture.md

The implementation blueprint, in three ordered sections.

---

## 1 · Requirements

  - Project overview
  - Users and roles
  - Feature list
  - Every page and what it does
  - Business rules
  - Out of scope

---

## 2 · Complete Flow Chart

One ASCII diagram of the end-to-end product flow.
Cover entry point, navigation, every major user workflow, decision branches and error paths.

Example
  Entry → Auth → Home → List → Detail → Action → Result

---

## 3 · Technical Flow Chart

One ASCII diagram per major workflow, showing how the code executes it.
Cover module responsibilities, routing, data flow through every layer, state ownership and the error path.

Example
  User → Route → Page → Hook → API → Store → Component → UI

---

Detailed enough for another developer to implement without asking questions.
```

</details>

---

<details>
<summary><strong>📚 Codebase Guide (codebase-guide.md)</strong></summary>

```md
# CODEBASE ARCHITECTURE

This document defines the mandatory architecture, coding standards, folder structure, implementation boundaries and quality rules for the entire project.
The implementation must strictly follow this guide.

---

# Source Structure

src/
  assets/                  // images · logos · icons · fonts
    logos/
    icons/
    home/
  common/                  // reusable across pages, never page-specific
    api/                   // the single data boundary — every read and write, one module per domain
    components/            // reusable UI only — Button · Modal · Table · Card · Badge · Avatar · Spinner
    constants/             // global constants only
    hooks/                 // reusable hooks — useDebounce · usePagination · useModal
    utils/                 // shared helpers
  store/                   // one Zustand store per domain, never combine unrelated domains
    auth.store.ts
    settings.store.ts
  pages/                   // every page self-contained, cross-page imports are not allowed
    home/
      index.tsx            // composition only
      components/
      hooks/               // this page's business logic
      mocks/
      constants.ts
      types.ts
      utils.ts
      styles.module.css
    settings/
  theme/                   // colours.css · fonts.css · overrides.css
    colours.css
    fonts.css
    overrides.css
  App.tsx                  // bootstrap · providers · routing, nothing else

The data source is swappable behind common/api and nothing above it changes.
Never create page-specific components in common/components.
spec/ is the source of truth. Never place application code there.

---

# Import Rules

Order
  1 React
  2 Third-party libraries
  3 Common modules
  4 Store
  5 Page modules
  6 Relative imports
  7 CSS Modules
Use absolute imports whenever possible.
Remove unused imports.

---

# Naming Convention

Folders
  kebab-case
Pages
  kebab-case
Components
  PascalCase.tsx
Hooks
  useCamelCase.ts
Utilities
  camelCase.ts
Stores
  <domain>.store.ts
Types
  types.ts
Constants
  constants.ts
JSON
  kebab-case.json
Icons
  kebab-case.svg
CSS Modules
  styles.module.css

---

# TypeScript Rules

Strict Mode
  Enabled
Never use
  any
Prefer
  type instead of interface.
Exported functions require explicit return types.
Use readonly whenever appropriate.
Use exhaustive switch statements.
Avoid implicit typing where clarity improves maintainability.

---

# React Rules

Functional components only.
Hooks only.
No classes.
No HOCs unless required.
No render props unless justified.
index.tsx performs composition only.
Business logic belongs inside
  - hooks
  - stores
Avoid unnecessary re-renders.
Memoize expensive calculations.
Use React.lazy() for pages.

---

# Component Rules

Maximum
  200 lines/component
Maximum
  60 lines/function
One component/file
One responsibility/component
No prop drilling beyond two levels.
Use Zustand instead.

---

# Routing

React Router only.
Centralised route configuration.
Every page lazy-loaded.
Required
  - 404
  - Redirect handling
  - Nested routes (if applicable)

---

# Data Flow

Component → Hook → common/api → Store → UI
Components never reach the data source directly.
Only common/api knows where data comes from.

---

# Data Loading

All data is loaded through the common/api abstraction.
Every call must support
  - Loading
  - Success
  - Empty
  - Error
Validate loaded data.

---

# Zustand Rules

One domain per file.
Derived values
  Computed
  Never stored.
Mutations only through actions.
No direct mutation.
Reset state on page unmount where necessary.

---

# Styling Rules

CSS Modules only.
Forbidden
  - Tailwind
  - Styled Components
  - Emotion
  - Inline styles
Colours
  Only from
    theme/colours.css
Never hardcode colours.
Class names
  camelCase

---

# Accessibility

Semantic HTML
Keyboard support
ARIA
Visible focus
Colour contrast
Labels
Screen reader friendly
Accessible navigation

---

# Performance

Lazy loading
Memoization
Avoid unnecessary renders
Avoid unnecessary state
Split large components
Code splitting
Optimised assets

---

# Error Handling

Never fail silently.
Every feature supports
  - Loading
  - Empty
  - Error
  - Success
Display meaningful user messages.
Provide validation messages and recovery options where applicable.

---

# Testing

Framework
  Jest
  React Testing Library

---

Unit Tests
  Co-located
Example
  Avatar.tsx
  Avatar.test.tsx

---

Hook Tests
  useDebounce.ts
  useDebounce.test.ts

---

Store Tests
  settings.store.ts
  settings.store.test.ts

---

Integration Tests
  __tests__/

---

Testing Rules
Every feature includes
  - Component tests
  - Hook tests
  - Store tests

---

# Documentation

Prefer self-documenting code.
Comment only complex business logic.
Avoid redundant comments.

---

# Code Quality

Follow
  - DRY
  - KISS
  - SOLID
  - Single Responsibility Principle
Prefer
  - Composition
  - Early returns
Avoid
  - Deep nesting
  - Duplicate logic

---

# Forbidden

console.log
debugger
TODO
FIXME
Magic numbers
Magic strings
Dead code
Circular imports
Unused variables
Barrel exports (unless explicitly requested)
```

</details>

---

<details>
<summary><strong>🎨 UI Prototypes (ui-prototypes/)</strong></summary>

```md
# UI Prototypes

A fully navigable static prototype in spec/ui-prototypes/.
Opening index.html must launch the whole UI with no React, npm, Node or build tools.
HTML, CSS and vanilla JavaScript only.
JavaScript is for UI interaction only — sidebar, drawer, modal, dropdown, tabs, mobile menu.
No frameworks. No business logic.

---

# UI Prototype Structure

ui-prototypes/
├── index.html
├── assets/
│   ├── css/
│   ├── js/
│   ├── icons/
│   ├── fonts/
│   └── images/
├── pages/
│   ├── home.html
│   ├── settings.html
│   └── ...
└── README.md

---

# UI Requirements

The prototype represents the FINAL approved UI.
It must include
  - Every application page
  - Header, sidebar and footer
  - The components those pages use
  - Loading, empty and error states
Every page must be reachable by navigation.
Use realistic demo data.

---

# Responsive Design

Mobile · Tablet · Laptop · Desktop

---

# Visual Quality

The prototype must closely resemble the final product in layout, spacing, colours, typography and component sizing.
During implementation, React pages must match the prototype.
No redesign is allowed unless the prototype is updated first.
```

</details>

---

<details>
<summary><strong>⚙️ Engines (engines/)</strong></summary>

```md
# Development Engines

Split implementation into independent engines.
Naming
  engine-01-project-setup.md
  engine-02-routing.md
  engine-03-layout.md
  engine-04-auth.md
  ...
Examples
  ✔ Routing
  ✔ One page's listing
  ✘ Two features in one engine
  ✘ A page plus its routing
Rules
  - One engine, one responsibility.
  - Later engines depend only on completed engines.
  - Complete one engine before starting the next.

---

# Engine Contents

Every engine must contain
  - Objective
  - Scope
  - Dependencies
  - Files to create or modify
  - Implementation steps
  - Acceptance criteria

---

# engine-status.md

One status file for the whole project, in spec/engines/.
Never create a second one.

Format
  # Engine Status

  Current    Engine 04 · Auth · In Progress
  Done       Route · Layout · Table · Store
  Next       Sorting · Empty state · Tests
  Checks     Build ✔  TypeScript ✔  ESLint ✔  Tests ⏳
  Updated    YYYY-MM-DD HH:mm

  Completed
    ✔ Engine 01
    ✔ Engine 02

Update it when an engine starts and when it completes.
Never guess completion percentages.
```

</details>

---

<details>
<summary><strong>🚀 Development (development.md)</strong></summary>

```md
# DEVELOPMENT WORKFLOW

How engines start, run and complete.
Coding standards live in codebase-guide.md — that document is authoritative.

---

# Specification Rules

- Never skip or partially generate the specification.
- codebase-guide.md and development.md are supplied. Copy them into spec/ unchanged.
- If implementation differs from the specification, update the specification first.

---

# Development Lifecycle

Generate Specification → User Approval → Engine 01 → Verify → Engine 02 → ... → Done
Approval is required once, for the specification.
After that execution is continuous — engines never wait.

---

# Implementation Order

## Phase 1

Generate every document in the Spec Structure.
Do not generate any application source code.
Wait for approval.

---

## Phase 2

Implement Engine 01, verify it, update engine-status.md.
Continue straight into the next engine and repeat until every engine is complete.

---

# Engine Completion Flow

Read Engine → Implement → Verify → Update Status → Next Engine

---

# Verification

Before moving to the next engine
Run
  npm run build : Pass
  npm run test  : Pass
  npm run lint  : Pass
  TypeScript    : Pass
Check
  - Acceptance criteria met
  - Structure, naming and boundaries follow codebase-guide.md
  - Pages match the prototype
  - No build or lint warnings

---

# Engine Completion Criteria

An engine is complete only if
  ✔ Acceptance criteria satisfied
  ✔ Verification passed
  ✔ engine-status.md marked Complete
Only then may the next engine begin.

---

# Continuous Execution

Never stop between engines.
Never wait for approval once the specification has been approved.
Update engine-status.md, then begin the next engine immediately.

---

# Documentation Rules

Update the specification whenever architecture, structure, scope or shared modules change.
Documentation must remain synchronised with implementation.

---

# Forbidden (Workflow)

Never
  - Skip, merge or partially implement engines
  - Generate future engine code
  - Ignore failing tests, type errors or lint errors
  - Leave incomplete documentation

---

# Project Completion

The project is complete only when
  ✔ Every engine is complete
  ✔ Every specification is satisfied
  ✔ engine-status.md shows all engines completed
  ✔ No remaining work exists
```

</details>
