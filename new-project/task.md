```text
# Task — Engine-Based Generation

## Project

Name        : <project name>
Description : <one sentence>

## Tech Stack

Framework  : React
Language   : TypeScript
Styling    : CSS Modules
State      : Zustand
Data fetch : <axios / fetch / react-query>
Testing    : Jest + React Testing Library
Build      : Vite

## Generation Rules

1. Split project into discrete Engines
2. Order: foundational → integration → advanced
3. Generate ONE engine at a time
4. After each engine: stop, show output, wait for approval
5. No stubs — every engine fully functional
6. Every engine independently runnable and testable
7. No assumptions about next engine's implementation

## Engine Template

### ENGINE [N] — [NAME]

#### Objective

Problem this engine solves:
What exists after this engine that didn't before:

#### Scope

In
- <feature>
- <feature>

Out
- <deferred feature>
- <deferred feature>

#### Risk

Level  : Low / Medium / High
Reason : <why>

#### Data Contracts

Input  : <props / store shape / API response this engine receives>
Output : <exported types / store updates / rendered UI this engine produces>

#### Folder Structure

src/
  <exact files and folders this engine creates>

#### State Design (Zustand)

store/<slice_name>.ts
  state  : { <field>: <type> }
  actions: { <action>: <signature> }

#### Component Responsibilities

<ComponentName>
  receives : <props>
  renders  : <what UI>
  emits    : <events / callbacks>

#### Functional Flow

1. User action
2. Event handler triggered
3. Zustand action called
4. State updated
5. API call (if needed) → loading / error / success handled
6. UI re-renders

#### API Calls (if any)

common/api/<domain>.ts
  <functionName>(<params>): Promise<<ReturnType>>
  Endpoint : <METHOD> /path
  Error    : <how handled>

#### Test Cases

Unit
  - <function> — <scenario> → <expected>

State
  - <action> called → <store shape after>

Component
  - renders <component> with <props> → <assertion>
  - user does <action> → <expected behavior>

Edge / Error
  - <condition> → <expected fallback>

#### Exit Criteria

[ ] Folder structure matches architecture rules
[ ] All in-scope features implemented — no stubs
[ ] Every async path handles loading / error / empty
[ ] All test cases pass
[ ] No cross-boundary imports
[ ] No console.log, no hardcoded values
[ ] Component files under 200 lines
[ ] No `any`, no type assertions (`as`) without justification
[ ] `npx tsc --noEmit` passes with zero errors

### ENGINE GATE

ENGINE [N] complete.

Approve?
  YES → proceed to ENGINE [N+1]
  NO  → list what needs to change

## Global Constraints

- No architectural shortcuts
- No skipped test cases
- No forward assumptions (engine N cannot know engine N+1's shape)
- No new libraries without explicit approval
- Every engine leaves the codebase in a working, committable state

## Create each page design before the development need to confirm the design

- Generate high-fidelity HTML mockups for every page

```
