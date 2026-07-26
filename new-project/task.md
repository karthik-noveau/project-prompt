```text
# AI ENGINE DEVELOPMENT PROTOCOL

## Project

Name        : <Project Name>
Description : <One sentence>

## Platform

Type        : Frontend Only
Backend     : None
API         : Local Mock Data (JSON)
Persistence : Browser Storage (if required)
Deployment  : Static Hosting

The application must be fully functional without any backend server.

Never generate:
- Express
- Node.js
- NestJS
- Firebase
- Supabase
- MongoDB
- MySQL
- PostgreSQL
- GraphQL Server
- REST Server
- Authentication Server

All data must come from:
- Local JSON
- Static Assets
- Zustand
- Browser Storage

## Tech Stack

Framework      : React
Language       : TypeScript
Build          : Vite
State          : Zustand
Styling        : CSS Modules
Routing        : React Router
Data Fetching  : fetch (Local JSON only)
Testing        : Jest + React Testing Library

## Development Model

Use Specification Driven Development.

Never write implementation before specification approval.

Every phase must be independently reviewable.

Every phase must stop and wait for approval.

## Engine Rules

1. Generate only ONE engine.
2. Never generate future engines.
3. Never assume future implementation.
4. Never modify completed engines unless requested.
5. Every engine must compile independently.
6. Every engine must be testable independently.
7. Every engine must be production ready.
8. No placeholders.
9. No TODO.
10. No stubs.

## Engine Categories

### Engine A — Product Architecture

Responsible for:

- Product structure
- Feature boundaries
- Folder architecture
- Routing strategy
- Module boundaries
- Data ownership
- State ownership
- Dependency rules

Output only documentation.

No React code.

Stop.

Wait for approval.

---

### Engine B — Design System

Responsible for:

- Colour palette
- Typography
- Icons
- Grid
- Spacing
- Elevation
- Border radius
- Shadows
- Animation language
- Component variants
- Accessibility rules

Output only documentation.

No React code.

Stop.

Wait for approval.

---

### Engine C — Page Experience

Responsible for ONE page only.

Generate:

- High Fidelity HTML
- CSS
- Responsive Layout
- Animation Description
- User Interaction
- Loading State
- Empty State
- Error State
- Accessibility Notes

No React.

No TypeScript.

No Zustand.

Only prototype.

Stop.

Wait for approval.

---

### Engine D — React UI

Convert approved HTML into React.

Generate:

- Components
- CSS Modules
- Props
- Types
- Accessibility
- Responsive Layout

No business logic.

No state management.

No API.

Pure presentation.

Stop.

Wait for approval.

---

### Engine E — State Management

Responsible for:

- Zustand Store
- State
- Actions
- Selectors
- Derived State
- Persistence

No UI.

No routing.

No API.

Stop.

Wait for approval.

---

### Engine F — Feature Logic

Responsible for:

- Business logic
- User interactions
- Validation
- Local JSON loading
- Browser Storage
- Error handling

No UI redesign.

Stop.

Wait for approval.

---

### Engine G — Testing

Generate:

- Unit Tests
- Store Tests
- Component Tests
- Integration Tests
- Accessibility Tests

Stop.

Wait for approval.

---

### Engine H — Verification

Verify:

✓ Folder Structure

✓ Architecture Rules

✓ Dependency Rules

✓ Import Rules

✓ Naming Rules

✓ Type Safety

✓ Accessibility

✓ Responsive Behaviour

✓ Testing

✓ Performance

✓ Dead Code

✓ Duplicate Logic

✓ Console Statements

✓ Build Errors

✓ TypeScript Errors

Generate verification report only.

Stop.

## Engine Template

### ENGINE [N]

Name

Purpose

Dependencies

Complexity

Risk

### Objective

Problem solved

Deliverables

Success criteria

### Scope

In

Out

### Folder Changes

Created

Modified

Deleted

### Architecture

Component hierarchy

Module boundaries

Dependency graph

### State

Input

Output

Store

Events

### UI

Components

Props

Events

Accessibility

Responsive

### Data

Source

Transformation

Validation

### Functional Flow

1.
2.
3.
4.
5.

### Tests

Unit

Store

Component

Integration

Accessibility

### Exit Checklist

[ ] No TypeScript errors

[ ] No ESLint errors

[ ] No build warnings

[ ] No placeholders

[ ] No TODO

[ ] No console.log

[ ] No unused imports

[ ] No dead code

[ ] No duplicated code

[ ] Component under 200 lines

[ ] Function under 60 lines

[ ] CSS Module used

[ ] Strict typing

[ ] Loading handled

[ ] Error handled

[ ] Empty handled

[ ] Responsive

[ ] Accessible

### Engine Gate

ENGINE COMPLETE

Stop.

Wait for approval.

YES

Proceed to next engine.

NO

Revise current engine only.

## Global Constraints

Never generate backend code.

Never generate APIs requiring a server.

Never generate authentication.

Never generate databases.

Never generate deployment scripts for backend.

Never assume future engines.

Never skip approval gates.

Never mix responsibilities between engines.

One engine.

One responsibility.

One approval.

One commit.

Every engine must leave the project in a compilable, production-ready state.
```
