# AI Project Development Protocol

<details>
<summary><strong>📋 Task Generation (task-generation.md)</strong></summary>

```md
# AI PROJECT SPECIFICATION & DEVELOPMENT PROTOCOL

## Objective

Before generating **any application source code**, the AI must first generate the complete `spec/` directory. The specification serves as the **single source of truth** for architecture, UI, implementation order, development workflow, and coding standards.

No source code may be generated until the specification has been completed and explicitly approved.

---

# Project Rules

- Generate the entire `spec/` directory before writing application source code.
- Never skip specification generation.
- Never partially generate the specification.
- Wait for approval after completing the specification.
- Only begin implementation after approval.
- Follow the specification throughout the project.
- If implementation differs from the specification, update the specification first.

---

# Directory Structure

spec/
├── architecture.md
├── codebase-guide.md
├── ui-prototypes/
│   ├── index.html
│   ├── assets/
│   │   ├── css/
│   │   ├── js/
│   │   ├── images/
│   │   ├── icons/
│   │   └── fonts/
│   ├── pages/
│   └── README.md
└── engines/
    ├── engine-status.md
    ├── engine-01-<work-name>.md
    ├── engine-02-<work-name>.md
    ├── engine-03-<work-name>.md
    └── ...

---

# architecture.md

Generate a complete implementation blueprint.

The document must include:

- Project overview
- Technical architecture
- Folder structure
- Module responsibilities
- Application lifecycle
- Routing architecture
- Component hierarchy
- Business workflows
- State management
- API/data flow
- Dependency graph
- Feature implementation plan
- Design decisions
- Assumptions
- Constraints
- Error handling strategy
- Performance strategy
- Accessibility strategy
- Testing strategy
- Security considerations (frontend)
- Responsive design strategy

Every major workflow must include an ASCII diagram.

Example

User
 │
 ▼
Route
 │
 ▼
Page
 │
 ▼
Hook
 │
 ▼
API
 │
 ▼
Store
 │
 ▼
Component
 │
 ▼
UI

The document should be detailed enough for another developer to implement the project without additional clarification.

---

# codebase-guide.md

Create this file only.

Do not write any content.

Never modify it.

It must remain completely empty.

---

# UI Prototypes

Create a fully navigable static prototype inside

spec/
└── ui-prototypes/

Opening

index.html

must launch the complete UI prototype without requiring:

- React
- Vite
- npm
- Node.js
- Build tools
- Backend

The prototype should behave like a real application.

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
│   ├── dashboard.html
│   ├── products.html
│   ├── orders.html
│   ├── settings.html
│   └── ...
└── README.md

---

# UI Requirements

The prototype represents the FINAL approved UI.

It must include

- Landing page
- Dashboard
- Every application page
- Sidebar
- Header
- Footer
- Navigation
- Responsive layouts
- Cards
- Tables
- Forms
- Buttons
- Dialogs
- Drawers
- Dropdowns
- Tabs
- Notifications
- Empty states
- Loading states
- Error states

---

# Navigation

The prototype must allow users to navigate naturally.

Examples

- Sidebar
- Header
- Breadcrumbs
- Tabs
- Mobile navigation
- Profile menu
- Settings menu

Every page must be reachable from the prototype.

---

# Prototype Rules

The prototype is UI only.

Allowed

- HTML
- CSS
- Vanilla JavaScript

Forbidden

- React
- Frameworks
- Backend
- API
- Business logic

JavaScript may only be used for UI interactions.

Examples

- Sidebar collapse
- Drawer open
- Modal preview
- Dropdown
- Tabs
- Accordion
- Mobile menu
- Theme preview

---

# Responsive Design

Support

- Mobile
- Tablet
- Laptop
- Desktop
- Ultra-wide

---

# Visual Quality

The prototype must closely resemble the final product.

Maintain

- Layout
- Spacing
- Colours
- Typography
- Icons
- Visual hierarchy
- Component sizing
- Responsive behaviour

During implementation, React pages must match the prototype.

No redesign is allowed unless the prototype is updated first.

---

# Demo Data

Use realistic static demo data.

Examples

- Users
- Products
- Orders
- Charts
- Notifications
- Tables
- Statistics

---

# Development Engines

Split implementation into independent engines.

Naming

engine-01-project-setup.md

engine-02-routing.md

engine-03-dashboard.md

...

Rules

- One engine performs exactly one responsibility.
- Never combine responsibilities.
- Later engines depend only on completed engines.
- Complete one engine before beginning another.

---

# Engine Contents

Every engine must contain

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

---

# Engine Workflow

1. Generate specification.
2. Wait for approval.
3. Implement Engine 01.
4. Validate.
5. Execute tests.
6. Update engine status.
7. Stop.
8. Request approval.
9. Begin next engine after approval.

Never implement future engines early.

---

# General Constraints

- Specification first.
- Implementation second.
- Validation third.
- Approval fourth.
- Repeat.

The specification remains the authoritative source throughout the project.
```

</details>

---

<details>
<summary><strong>📚 Codebase Guide (codebase-guide.md)</strong></summary>

```md id="3wqkzn"
# CODEBASE ARCHITECTURE

This document defines the mandatory architecture, coding standards, folder structure, implementation boundaries and quality rules for the entire project.

The implementation must strictly follow this guide.

---

# Technology Stack

Framework : React

Language : TypeScript

Build Tool : Vite

State Management : Zustand

Routing : React Router

Styling : CSS Modules

Testing : Jest + React Testing Library

Persistence : Browser Storage (if required)

Backend : None

Data Source

- Local JSON
- Static Assets
- Zustand
- Browser Storage

---

# Source Structure

src/

  assets/
    logos/
    icons/
    <page-name>/

  common/
    api/
    components/
    constants/
    hooks/
    utils/

  store/
    <domain>.store.ts

  pages/

    <page-name>/
      index.tsx
      components/
      hooks/
      mocks/
      constants.ts
      types.ts
      utils.ts
      styles.module.css

  theme/
    colours.css
    fonts.css
    overrides.css

  App.tsx

---

# Folder Responsibilities

spec/

Source of truth.

Contains

- Architecture
- Engines
- UI Prototype
- Development rules

Never place application code here.

---

assets/

Contains

- Images
- Logos
- Icons
- Fonts
- Static media

---

common/

Contains reusable modules shared across multiple pages.

Must never contain page-specific logic.

---

common/api/

Responsibilities

- Read Local JSON
- Browser Storage
- Mock API abstraction

Components must never access JSON directly.

---

common/components/

Reusable UI only.

Examples

- Button
- Modal
- Table
- Card
- Badge
- Avatar
- Spinner

Never create page-specific components here.

---

common/hooks/

Reusable hooks only.

Examples

- useDebounce
- usePagination
- useModal

---

common/constants/

Global constants only.

---

common/utils/

Shared helper functions.

---

store/

One Zustand store per domain.

Examples

user.store.ts

dashboard.store.ts

settings.store.ts

cart.store.ts

Never combine unrelated domains.

---

pages/

Every page is completely self-contained.

Allowed

pages/products/components/

pages/products/hooks/

pages/products/utils.ts

Forbidden

pages/products importing

pages/orders/components/

Cross-page imports are not allowed.

---

theme/

Contains only global theme.

Examples

colours.css

fonts.css

overrides.css

---

App.tsx

Responsibilities

- Bootstrap
- Providers
- Routing

Nothing else.

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

type

instead of interface.

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

Component

↓

Hook

↓

API

↓

Local JSON

↓

Store

↓

UI

Components never access JSON directly.

---

# Data Fetching

Frontend only.

No backend.

No REST.

No GraphQL.

No Axios unless specifically required.

Use common/api abstraction.

Support

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

---

# Performance

Lazy loading

Memoization

Avoid unnecessary renders

Avoid unnecessary state

Split large components

Code splitting

---

# Error Handling

Never fail silently.

Every feature supports

- Loading
- Empty
- Error
- Success

Display meaningful user messages.

---

# Testing

Framework

Jest

React Testing Library

---

Unit Tests

Co-located

Example

UserAvatar.tsx

UserAvatar.test.tsx

---

Hook Tests

useProducts.ts

useProducts.test.ts

---

Store Tests

dashboard.store.ts

dashboard.store.test.ts

---

Integration Tests

__tests__/

---

Testing Rules

Every feature includes

- Component tests
- Hook tests
- Store tests

Tests must pass before engine completion.

---

# Documentation

Prefer self-documenting code.

Comment only complex business logic.

Avoid redundant comments.

---

# Build Requirements

The project must

Pass

- Build
- TypeScript
- ESLint
- Jest

Contain

- Zero warnings
- Zero dead code
- Zero unused files
- Zero unused imports

---

# Code Quality

Follow

- DRY
- KISS
- SOLID

Prefer

- Composition
- Early returns

Avoid

- Deep nesting
- Duplicate logic

---

# Forbidden

any

console.log

debugger

TODO

FIXME

Hardcoded colours

Magic numbers

Magic strings

Dead code

Circular imports

Cross-page imports

Duplicate logic

Unused imports

Unused variables

Barrel exports (unless explicitly requested)

Framework-specific styling libraries

---

# Completion Criteria

The codebase is considered compliant only when

- Folder structure matches this guide.
- All naming rules are followed.
- All boundaries are respected.
- All tests pass.
- Build passes.
- TypeScript passes.
- ESLint passes.
- No forbidden practices remain.
```

</details>

---

<details>
<summary><strong>🚀 Development (development.md)</strong></summary>

```md
# DEVELOPMENT WORKFLOW

This document defines the complete implementation workflow after the project specification has been approved.

Every implementation must strictly follow this workflow.

---

# Development Lifecycle

Project

↓

Generate Specification

↓

User Approval

↓

Engine 01

↓

Validation

↓

Testing

↓

User Approval

↓

Next Engine

↓

Repeat

No engine may begin until the previous engine has been fully completed and approved.

---

# Implementation Order

## Phase 1

Generate the complete `spec/` directory.

Required

- architecture.md
- codebase-guide.md
- ui-prototypes/
- engines/

Do not generate any application source code.

Wait for approval.

---

## Phase 2

Implement Engine 01.

Requirements

- Complete implementation
- Validation
- Build verification
- Unit tests
- Integration tests
- Documentation updates
- Status update

Stop.

Wait for approval.

---

## Phase 3

Implement Engine 02.

Repeat the same workflow.

Continue until every engine has been completed.

---

# Engine Development Rules

Each engine represents exactly one responsibility.

Examples

✔ Project Setup

✔ Routing

✔ Dashboard Layout

✔ Authentication Store

✔ Product Listing

✔ Product Details

✘ Dashboard + Routing

✘ Authentication + Users

✘ Products + Orders

Never merge responsibilities.

---

# Engine Completion Flow

Read Engine Specification

↓

Implement

↓

Validate

↓

Run Tests

↓

Update Status

↓

Verify Acceptance Criteria

↓

Stop

↓

Request Approval

---

# Engine Status Tracking

Maintain a single shared status file.

Directory

spec/

└── engines/

    ├── engine-status.md

    ├── engine-01-...

    ├── engine-02-...

    └── ...

Never create multiple status files.

---

# Status Update Frequency

Update

engine-status.md

at

20%

40%

60%

80%

100%

Progress updates are mandatory.

---

# Status File Responsibilities

The file always represents

the CURRENT engine.

When a new engine begins

replace

Current Engine

Current Progress

Current Phase

Remaining Work

Files Modified

Validation

while preserving

Completed Engines.

---

# engine-status.md Format

# Engine Status

---

## Current Engine

Engine

Engine Number

Progress

Current Phase

Example

Engine 04

Products

40%

Building Product Table

---

## Completed Functionality

Keep concise.

Example

- Product routes
- Product layout
- Filters
- Table
- Pagination
- Zustand store

---

## Remaining Work

Example

- Sorting
- Empty state
- Tests
- Documentation

---

## Files Modified

Example

pages/products/index.tsx

pages/products/components/ProductTable.tsx

store/products.store.ts

common/api/products.ts

---

## Validation

Build

✔

TypeScript

✔

ESLint

✔

Unit Tests

⏳

Integration Tests

⏳

---

## Last Updated

YYYY-MM-DD HH:mm

---

## Completed Engines

✔ Engine 01

✔ Engine 02

✔ Engine 03

---

# Engine Completion Criteria

An engine is complete only if

✔ Implementation completed

✔ Acceptance criteria satisfied

✔ Validation completed

✔ Build passed

✔ TypeScript passed

✔ ESLint passed

✔ Unit tests passed

✔ Integration tests passed

✔ engine-status.md updated to 100%

✔ User approval received

Only then may the next engine begin.

---

# Validation Checklist

Every engine must verify

- Folder structure
- File naming
- Imports
- Routing
- Zustand
- API layer
- Component boundaries
- Styling
- Accessibility
- Error handling
- Performance
- Documentation
- Tests

---

# Testing Requirements

Each engine must include

Component Tests

Hook Tests

Store Tests

Utility Tests (where applicable)

Integration Tests

Every test must pass.

---

# Build Verification

Before requesting approval

Verify

npm run build

Pass

npm run test

Pass

npm run lint

Pass

TypeScript

Pass

No warnings.

No unused files.

No dead code.

---

# Quality Rules

Every engine must follow

DRY

KISS

SOLID

Composition over inheritance

Early returns

Single Responsibility Principle

No duplicate logic

No deep nesting

---

# Performance Rules

Lazy loading

Memoization

Avoid unnecessary renders

Avoid unnecessary state

Split large components

Code splitting

Optimised assets

---

# Accessibility Rules

Semantic HTML

Keyboard support

Visible focus states

ARIA

Labels

Colour contrast

Accessible navigation

---

# Error Handling

Every feature must provide

Loading State

Success State

Empty State

Error State

Validation Messages

Recovery Options (where applicable)

Never fail silently.

---

# Documentation Rules

Update documentation whenever

- Architecture changes
- Folder structure changes
- Engine scope changes
- Shared modules change

Documentation must remain synchronised with implementation.

---

# Approval Rules

After every engine

STOP.

Do not continue automatically.

Present

- Completed functionality
- Validation results
- Test results
- Current engine-status.md

Wait for explicit user approval.

Only after approval

begin the next engine.

---

# Forbidden

Never

- Skip engines
- Merge engines
- Partially implement engines
- Generate future engine code
- Ignore failing tests
- Ignore TypeScript errors
- Ignore ESLint errors
- Leave TODOs
- Leave FIXMEs
- Leave unused code
- Leave dead files
- Leave incomplete documentation

---

# Project Completion

The project is complete only when

✔ Every engine is approved

✔ Every specification is satisfied

✔ All tests pass

✔ Build passes

✔ TypeScript passes

✔ ESLint passes

✔ Documentation is complete

✔ engine-status.md shows all engines completed

✔ No remaining work exists

Only then is the project considered finished.
```

</details>
