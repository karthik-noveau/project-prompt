````text
# Project Task Generation

Generate the complete project specification inside the `spec/` directory before writing any application source code.

## Directory Structure

```text
spec/
├── architecture.md
├── codebase-guide.md
├── ui-prototypes/
└── engines/
```

## Tech Stack

```text
Framework : React
Language  : TypeScript
Build     : Vite
State     : Zustand
Styling   : CSS Modules
Routing   : React Router
Testing   : Jest + React Testing Library
```

## architecture.md

Create comprehensive technical documentation covering:

- Overall application architecture
- Module and folder structure
- End-to-end application flow
- Libraries, frameworks, and major dependencies
- Business logic and feature workflows
- Component hierarchy and interactions
- State management flow
- Routing structure
- Data flow between modules
- Folder responsibilities
- Design decisions
- Assumptions and constraints
- ASCII flow diagrams for every major workflow

This document must serve as the complete implementation blueprint.

## codebase-guide.md

- Create this file as an empty file only.
- Never write, modify, or populate its contents.

## ui-prototypes/

Create one minimized HTML prototype for every application page.

Requirements:

- One HTML file per page.
- UI only (no application logic).
- Responsive layout.
- Proper spacing and alignment.
- Typography.
- Colour palette.
- Component positioning.
- Visual hierarchy.
- Overall UX structure.

Prototype Rules:

- These are not wireframes or mock-ups.
- They represent the final approved UI.
- During development, every React page must match its corresponding prototype as closely as possible.
- Layout, spacing, colours, typography, sizing, alignment, responsiveness, and visual hierarchy must remain consistent.
- Treat these prototypes as the single source of truth for the application's UI.

## engines/

Split the implementation into multiple independent development engines.

Naming Convention:

```text
engine-01-<work_name>.md
engine-02-<work_name>.md
engine-03-<work_name>.md
...
```

Each engine must contain:

- Objective
- Scope
- Dependencies
- Files to create or modify
- Implementation steps
- Acceptance criteria
- Edge cases
- Validation checklist
- Test cases
- Completion checklist

Rules:

- One engine must perform exactly one responsibility.
- Never combine unrelated work into a single engine.
- Every engine must be fully implemented before the next begins.
- Include implementation, validation, and complete test coverage.
- All tests must pass before an engine is considered complete.
- Later engines may depend only on previously completed engines.
- Never skip, partially implement, or merge engines.
- Stop after completing each engine and request confirmation before starting the next.
- Do not generate source code for future engines until the current engine is completed and approved.

Generate the entire `spec/` directory first. Only after it has been completed and approved may application source code be generated.
````
