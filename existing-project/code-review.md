# PR Review — Existing Codebase

COMPARE_BRANCH: main

## Mode
```
1 — External PR   → gh pr diff <number|url>
2 — Local changes → git diff main...HEAD
3 — Self PR       → both
```
Scope: diff only. Pre-existing issues → label `[Pre-existing]`, do not action.

## Run Tools
```bash
npm run lint && npm test && npx tsc --noEmit
```
Fix failures before manual review.

## PR Checklist
All items in the PR description must be checked. Unchecked tests item without justification → flag as BLOCKER.

## Manual Review — stop at first BLOCKER

### Fit with Existing Codebase [BLOCKER]
Does this look like it was written by someone who read the codebase first?
- Files placed per existing folder conventions
- No reinvention — existing utils / hooks / components reused
- Naming matches codebase exactly (casing, prefixes, suffixes)
- Same patterns for same problems (state, API, error handling)
- No new library or abstraction the team hasn't adopted
- Same import aliases as rest of codebase
- Styling approach matches — no mixing

### Breaking Changes [BLOCKER]
What does every caller of every changed export expect? Does this break any of those expectations?
- No behavior removed without replacement
- Shared component / hook modified → all callers updated
- API response shape unchanged for existing consumers
- No prop renamed / removed without updating all usages
- Deleted code → verified no other file depended on it
- Deleted export from shared / common file → verified no other file imports it

### Correctness [BLOCKER]
Trace every code path with null, empty, boundary, and adversarial input. Does the right thing happen?
- Logic matches intended behavior
- Null / undefined guarded at every access
- New field on existing stored data — guard against absence in legacy records (`.get()` / optional chaining)
- Numeric input validated with `min` only — verify `max` is also enforced if large values cause issues
- Two code paths to the same write — both apply equivalent validation, not just the primary path
- No inverted conditions, off-by-one errors
- Boolean condition change (`||` ↔ `&&`) — trace every combination to verify intent
- Multiple fields set to the same value — verify intentional, not a copy-paste error
- Submit gate condition matches API payload guard — data sent only when UI validation passes
- Null / undefined stripped from payload — verify no required field accidentally filtered out
- No direct object mutation (`delete obj.key`) — use destructuring or spread
- No hardcoded values, no debug code, no commented-out code
- loading / error / empty / data states all handled

### Async & State [BLOCKER]
Trace the failure path of every async operation. What state is the user left in when it fails?
- Every async has error handling — no silent failures
- `catch` block is not empty and not silent — error is logged or reported to user
- Every `.then()` chain has a `.catch()` — no unhandled promise rejections in chains
- No mixed async patterns — `async/await` and `.then()` not combined in the same function
- Race condition handled (abort / debounce)
- No state update after unmount — effect cleanup present
- All hook dependencies correct and complete
- No derived data stored in state
- Optimistic updates roll back on failure
- Read / selector that also writes to the data it reads — getter must not have write side effects

### Security [BLOCKER]
What can a malicious or accidental input do to this code? What does it expose?
- No user input rendered as raw HTML
- No sensitive data in state / logs / error messages
- Auth checks present where required
- No secrets in frontend code
- External URLs validated before use

### Reliability [REQUIRED]
What happens on bad input, slow network, or degraded state? Does it crash or recover?
- Network errors visible to user — not silently swallowed
- Empty states handled — no blank screen
- Unexpected input doesn't crash component
- Effect cleanup: listeners / timers / subscriptions removed on unmount
- Recursive function traversing user-supplied data — add a maximum depth guard

### Performance [REQUIRED]
What runs on every render? What creates new references? What is proportional to data size?
- No expensive computation in render → `useMemo`
- Callbacks as props → `useCallback`
- `useEffect` not doing event-handler work
- No unstable object / array refs as props
- Large lists virtualized if applicable

### Code Quality [REQUIRED]
Could a new team member read and maintain this without asking questions?
- No duplicated logic — reuse existing utils
- Shared type / PropType shapes not duplicated across components — extracted to one place
- Named constant not recreated if it already exists in the codebase
- Sentinel / magic values (`-1`, `0`, `999`) replaced with named constants
- Two distinct features using the same constant or config key — verify intentional
- Lookup table / mapping defined inside a function — move to module or class level
- Functions do one thing — no mixed responsibilities
- No conditionals nested beyond 2 levels
- No magic numbers — named constants only
- Import order matches codebase convention

### Tests [REQUIRED]
Do tests verify the behavior works, or just that it runs? What input would make the test fail if the logic is wrong?
- New logic has tests with specific assertions — not `.toBeTruthy()`
- No duplicate test cases — identical setup + identical assertions = one test
- Existing tests not broken by this change
- Edge cases covered: null input, empty list, API error

## Output
```
FILE: <path>  LINE: <n>  SEVERITY: BLOCKER|REQUIRED|SUGGESTED|[Pre-existing]
ISSUE: <what>
FIX: <how — reference existing pattern where applicable>
```
Summary: BLOCKERs: <n> | REQUIREDs: <n> | Pre-existing: <n>

## Confirmation
```
Review complete.
Skip issues: "Skip: 1, 3"  or  "0" to keep all.
```
Wait for reply, then:
```
1 — GitHub inline comments + suggested commits
2 — Apply fixes directly
3 — Report only
```
