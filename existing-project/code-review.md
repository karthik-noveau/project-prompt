````markdown
# PR Review

## Scope

Mode:
1. External → `gh pr diff <number|url>`
2. Local → `git diff main...HEAD`
3. Self PR → both

Review **changed code only**.

- Ignore unrelated issues.
- Existing issues in touched files → ⚪ Pre-existing.
- Verify every PR description requirement.

Run first:

```bash
npm run lint
npm test
npx tsc --noEmit
```

Fix failures before reviewing.

> Stop after the **first 🔴 BLOCKER**.

---

## Checks

### 1. Codebase Consistency 🔴
Verify project conventions:
- Structure
- Naming
- Imports
- Reuse existing hooks/components/utils
- State/API/style patterns
- Error handling
- No unnecessary abstraction/dependencies

### 2. Breaking Changes 🔴
Verify:
- Public APIs
- Existing callers
- Props
- Request/response shape
- Shared exports
- Deleted code has no consumers

### 3. Correctness 🔴
Verify:
- Happy path
- Null/undefined
- Empty/boundary/invalid input
- Legacy data
- Validation
- Payload correctness
- Loading/error/empty states
- No accidental mutation
- No debug/commented code

### 4. Async & State 🔴
Verify:
- Async error handling
- Cleanup
- Hook dependencies
- Race conditions
- Consistent async pattern
- Optimistic rollback

### 5. Security 🔴
Verify:
- XSS
- Auth/AuthZ
- Secrets
- Sensitive logging
- URL/input validation

### 6. Reliability 🟠
Check invalid input, network failures, retries, cleanup, recursion guards.

### 7. Performance 🟠
Check unnecessary renders, unstable references, memoization, duplicate requests, virtualization.

### 8. Maintainability 🟠
Check duplication, magic values, large functions, nesting, imports, dead code.

### 9. Tests 🟠
Verify new logic, edge cases, error paths, and existing tests.

---

# Output

## Review Summary

| Metric | Count |
|--------|------:|
| Files Reviewed | <count> |
| 🔴 BLOCKER | <count> |
| 🟠 REQUIRED | <count> |
| 🟡 SUGGESTED | <count> |
| ⚪ Pre-existing | <count> |

---

## Findings

| # | Severity | File:Line | Category | Issue | Recommended Fix |
|---|----------|-----------|----------|-------|-----------------|
| 1 | 🔴 BLOCKER | `path/file.ts:120` | Breaking Changes | Describe the issue clearly. | Describe the exact fix. |
| 2 | 🟠 REQUIRED | `path/file.ts:86` | Reliability | Describe the issue. | Recommended fix. |
| 3 | 🟡 SUGGESTED | `path/file.ts:45` | Maintainability | Optional improvement. | Suggested improvement. |
| 4 | ⚪ Pre-existing | `path/file.ts:20` | Maintainability | Existing issue unrelated to this PR. | Ignore for this PR. |

---

## Result

### If a 🔴 BLOCKER exists

Stop immediately after reporting the first BLOCKER.

```text
Review stopped after the first BLOCKER.

Wait.
```

### Otherwise

```text
Review complete.

Skip issues:
0
```

or

```text
Review complete.

Skip:
#2, #5
```

Wait.

---

## After User Continues

1. Generate GitHub inline review comments.
2. Generate suggested commits.
3. Apply fixes (if requested).
4. Report only the applied changes.
````
