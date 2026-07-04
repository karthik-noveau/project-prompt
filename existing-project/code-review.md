````text
# Code Review

## Review Scope

Mode:
1. External PR → `gh pr diff <number|url>`
2. Local → `git diff main...HEAD`
3. Self PR → both

Review **only changed code**.

Ignore unrelated existing issues.
If a touched file contains an old issue, report it as **[Pre-existing]**.

Run before review:

```bash
npm run lint
npm test
npx tsc --noEmit
```

Fix failures before continuing.

Verify every item in the PR description.
Missing required implementation/tests → BLOCKER.

---

# Stop after the first BLOCKER.

## 1. Codebase Consistency [BLOCKER]

Ensure changes follow existing project conventions.

- folder structure
- naming
- imports
- hooks/utilities/components reused
- state management
- API pattern
- styling pattern
- error handling
- no unnecessary abstraction
- no new dependency unless justified

---

## 2. Breaking Changes [BLOCKER]

Trace every changed public API.

Verify:

- callers still work
- props unchanged
- response shape unchanged
- shared exports still valid
- deleted code has no consumers

---

## 3. Correctness [BLOCKER]

Trace:

- happy path
- null/undefined
- empty input
- boundary values
- invalid input
- legacy data

Verify:

- validation
- conditions
- payload correctness
- no accidental mutation
- loading/error/empty states
- no debug/commented code

---

## 4. Async & State [BLOCKER]

Verify:

- async errors handled
- no silent catch
- no mixed async styles
- cleanup on unmount
- hook dependencies complete
- race conditions handled
- optimistic updates rollback

---

## 5. Security [BLOCKER]

Check:

- XSS
- auth
- secrets
- logging
- URL validation

---

## 6. Reliability [REQUIRED]

Check:

- invalid input
- network failure
- empty states
- cleanup
- recursion guard

---

## 7. Performance [REQUIRED]

Check:

- expensive render work
- unnecessary renders
- unstable references
- memoization
- virtualization when applicable

---

## 8. Maintainability [REQUIRED]

Check:

- duplicated logic
- duplicated types
- magic values
- large functions
- deep nesting
- import order

---

## 9. Tests [REQUIRED]

Verify:

- meaningful assertions
- edge cases
- error paths
- existing tests still pass

---

## Output

FILE:
LINE:
SEVERITY: BLOCKER | REQUIRED | SUGGESTED | [Pre-existing]

ISSUE:

FIX:

---

Summary

BLOCKER:
REQUIRED:
Pre-existing:

Review complete.

Skip issues:
0
or
Skip: <numbers>

Wait.

Then:

1. GitHub inline comments + suggested commits
2. Apply fixes
3. Report only
````
