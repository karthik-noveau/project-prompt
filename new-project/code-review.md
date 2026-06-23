# Engine Code Review

## Run First
```bash
npm run lint && npm test && npx tsc --noEmit
```
All must pass. Fix failures before manual review.

## Diff
```bash
git diff HEAD~1
```

## Manual Review — stop at first BLOCKER

### Architecture [BLOCKER]
Does every file live where it belongs? Does this engine introduce dependencies that block future engines?
- Files: shared → `common/`, page-local → `pages/<name>/`, API calls → `common/api/`
- No cross-page imports
- `index.jsx` is JSX composition only — no `useState`, no `useEffect`
- No logic duplicated from a previous engine

### Engine Regression [BLOCKER]
What did every previous engine assume about shared code? Does this change break any of those assumptions?
- Shared component / hook modified → all existing callers still work
- Zustand store shape changed → all consumers updated
- No prop removed or renamed on a component already in use

### Async & State [BLOCKER]
Trace the failure path of every async operation. What state is the user left in when it fails?
- Every `async` has error handling — no silent failures
- `catch` block is not empty and not silent — error is logged or reported to user
- Every `.then()` chain has a `.catch()` — no unhandled rejections in chains
- No mixed async patterns — `async/await` and `.then()` not combined in the same function
- Race condition on rapid re-trigger handled (abort / debounce)
- `useEffect` returns cleanup → no state update after unmount
- Optimistic updates roll back on failure
- Read / selector / getter that also writes to the data it reads — getter must not have write side effects
- Recursive function on external/user data — add a maximum depth guard to prevent stack overflow
- loading / error / empty states all rendered — not just happy path

### Correctness [BLOCKER]
Trace every code path with null, empty, boundary, and adversarial input. Does the right thing happen?
- Output matches functional flow declared in task
- Null / undefined guarded on every API response field access
- New field on existing stored / persisted data shape — guard against absence in legacy records
- Numeric input validated with `min` only — verify `max` is also enforced if large values cause issues
- Two code paths to the same write — verify both apply equivalent validation
- No always-true / always-false conditions
- Boolean condition change (`||` ↔ `&&`) — trace every combination to verify intent
- Multiple fields set to the same value — verify intentional, not a copy-paste error
- Submit gate condition matches API payload guard — data sent only when UI validation passes
- Null / undefined stripped from payload — verify no required field accidentally filtered out
- No direct object mutation (`delete obj.key`) — use destructuring or spread
- No hardcoded values — named constants only
- Two distinct features sharing the same constant or config key — verify intentional
- Lookup table / mapping defined inside a function — move to module or file level

### Security [BLOCKER]
What can a malicious or accidental input do? What does the code expose?
- No user input rendered as raw HTML
- No tokens / PII in state or logs
- Auth-gated routes enforce session check

### Tests [REQUIRED]
Do tests verify the behavior works, or just that it runs? What input would make the test fail if the logic is wrong?
- New logic has tests with specific assertions — not `.toBeTruthy()`
- No duplicate test cases — identical setup + identical assertions = one test
- No test that only checks the component renders without crashing

## Output
```
FILE: <path>  LINE: <n>  SEVERITY: BLOCKER|REQUIRED|SUGGESTED
ISSUE: <what>
FIX: <how>
```
BLOCKERs: <n> | REQUIREDs: <n>

## Decision
```
APPROVE → all clear — proceed to next engine
REVISE  → list fixes → re-review
```
