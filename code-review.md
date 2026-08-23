````text
# PR Review

## Scope

Mode
1. External → `gh pr diff <number|url>`
2. Local → `git diff $(git merge-base HEAD origin/HEAD)...HEAD`
3. Self PR → both

Read the PR description first, then verify every requirement in it.
  gh pr view <number|url>

Read the full changed files for context — a hunk hides what decides whether the change is correct.
Context is for understanding only. It is never what gets reviewed.

## Boundary

Review the PR's changes and nothing else.
- Every finding must sit on a line this PR added or modified.
- A file the PR did not touch is out of scope, even if it is wrong.
- An issue in a touched file but not on a changed line → ⚪ Pre-existing,
  and report it only when the change depends on it. Otherwise leave it out.
- Never propose refactors, renames or improvements beyond the change.
- Verify the PR description's requirements — nothing more.

---

## Checks

Run whatever the project defines, before reviewing.
  lint
  tests
  type check    (if the project uses TypeScript)
  server start  (if the project must boot)

Read package.json scripts. Never assume a script exists.
Report failures as findings. Do not fix anything during review.
A failure that also happens on the base branch is ⚪ Pre-existing.

---

# Review Checklist

## 1. Codebase Consistency
- Structure
- Naming
- Imports
- Reuse of existing hooks, components, utils
- State, data and style patterns
- Error handling
- No unnecessary abstraction or dependency

## 2. Breaking Changes
- Public APIs
- Existing callers
- Props
- Request and response shape
- Shared exports
- Deleted code has no consumers

## 3. Correctness
- Happy path
- Null and undefined
- Empty, boundary and invalid input
- Legacy data
- Validation
- Payload correctness
- Loading, error and empty states
- No accidental mutation
- No debug or commented-out code

## 4. Async & State
- Async error handling
- Cleanup
- Hook dependencies
- Race conditions
- Consistent async patterns
- Optimistic rollback

## 5. Security
- XSS
- Authentication and authorization
- Secrets
- Sensitive logging
- URL and input validation

## 6. Reliability
- Invalid input
- Network failures
- Retry logic
- Cleanup
- Infinite recursion and loop guards

## 7. Performance
- Unnecessary renders
- Unstable references
- Memoization
- Duplicate requests
- Virtualization where applicable

## 8. Maintainability
- Duplicate logic and types
- Magic values
- Large functions
- Deep nesting
- Import order
- Dead code
- Readability

## 9. Tests
- New logic covered
- Edge cases
- Error paths
- Existing tests still pass

---

# Severity

🔴 BLOCKER       breaks correctness or security, or breaks an existing consumer
🟠 REQUIRED      fails in a real scenario — bad input, network failure, race, missing cleanup
🟡 SUGGESTED     safe to ship, worth improving
⚪ Pre-existing  not caused by this PR

Severity is judged per finding, never by category.

---

# Reporting Rules

Report a finding only when
- It sits on a line this PR added or modified.
- The current code around it has been read, not just the diff.
- The input or scenario that breaks it can be named.
- The line number is the line in the changed file.

Never report style the linter already enforces.
Never report a guess. If it cannot be verified, leave it out.

---

# Result

Table only, sorted by severity.

| # | Severity | File | Line | Category | Issue | Recommended Fix |
|---|----------|------|-----:|----------|-------|-----------------|
| 1 | 🔴 BLOCKER | `src/example.ts` | 120 | Breaking Changes | Short issue description. | Short actionable fix. |
| 2 | 🟠 REQUIRED | `src/example.ts` | 86 | Reliability | Short issue description. | Short actionable fix. |
| 3 | 🟡 SUGGESTED | `src/example.ts` | 45 | Maintainability | Short improvement. | Suggested improvement. |
| 4 | ⚪ Pre-existing | `src/example.ts` | 20 | Maintainability | Existing issue unrelated to this PR. | Ignore for this PR. |

If nothing is found, say so in one line. Never pad the table.

---

## After Review
1. Ask which findings to skip.
2. Ask for confirmation before applying any fix.

````
