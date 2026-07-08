````text
# PR Review

## Scope

Mode:
1. External → `gh pr diff <number|url>`
2. Local → `git diff main...HEAD`
3. Self PR → both

Review **changed code only**.

- Ignore unrelated issues.
- Existing issues in touched files → ⚪ Pre-existing.
- Verify every requirement in the PR description.

Run before review:

```bash
npm run lint
npm test
npx tsc --noEmit
```

Fix any failures before continuing.

---

# Review Checklist

## 1. Codebase Consistency 🔴
Verify:
- Structure
- Naming
- Imports
- Reuse existing hooks/components/utils
- State/API/style patterns
- Error handling
- No unnecessary abstraction or dependencies

## 2. Breaking Changes 🔴
Verify:
- Public APIs
- Existing callers
- Props
- Request/response shape
- Shared exports
- Deleted code has no consumers

## 3. Correctness 🔴
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

## 4. Async & State 🔴
Verify:
- Async error handling
- Cleanup
- Hook dependencies
- Race conditions
- Consistent async patterns
- Optimistic rollback

## 5. Security 🔴
Verify:
- XSS
- Authentication / Authorization
- Secrets
- Sensitive logging
- URL & input validation

## 6. Reliability 🟠
Verify:
- Invalid input
- Network failures
- Retry logic
- Cleanup
- Infinite recursion/loop guards

## 7. Performance 🟠
Verify:
- Unnecessary renders
- Unstable references
- Memoization
- Duplicate requests
- Virtualization (where applicable)

## 8. Maintainability 🟠
Verify:
- Duplicate logic/types
- Magic values
- Large functions
- Deep nesting
- Import order
- Dead code
- Readability

## 9. Tests 🟠
Verify:
- New logic covered
- Edge cases
- Error paths
- Existing tests still pass

---

# Result

## Review summery should be table only 

| # | Severity | File | Line | Category | Issue | Recommended Fix |
|---|----------|------|-----:|----------|-------|-----------------|
| 1 | 🔴 BLOCKER | `src/example.ts` | 120 | Breaking Changes | Short issue description. | Short actionable fix. |
| 2 | 🟠 REQUIRED | `src/example.ts` | 86 | Reliability | Short issue description. | Short actionable fix. |
| 3 | 🟡 SUGGESTED | `src/example.ts` | 45 | Maintainability | Short improvement. | Suggested improvement. |
| 4 | ⚪ Pre-existing | `src/example.ts` | 20 | Maintainability | Existing issue unrelated to this PR. | Ignore for this PR. |


---

## After Review
1. ask what need to skip
2. ask confirmation to apply the fixes

````
