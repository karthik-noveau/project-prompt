────────────────────────
PR REVIEW CONFIG
────────────────────────

COMPARE_BRANCH: main

Select review type:

1. External PR
2. Local changes
3. Local changes + Self PR

---

If option **1 (External PR)**

Ask:

Enter PR URL or PR number

Run:

`gh pr diff <number|url>`

Review changes against `${COMPARE_BRANCH}`.

Do NOT modify code.

---

If option **2 (Local changes)**

Run:

`git diff ${COMPARE_BRANCH}...HEAD`

Review local changes only.

---

If option **3 (Local changes + Self PR)**

Ask:

Enter PR URL or PR number

Run:

`gh pr diff <number|url>`
`git diff ${COMPARE_BRANCH}...HEAD`

Review both PR changes and local changes.

────────────────────────
REVIEW PRINCIPLES
────────────────────────

• Review only changes introduced by this PR
• Prioritize correctness over style
• Avoid subjective preferences
• Prefer existing project patterns and conventions
• Suggest changes only when they improve:

* correctness
* readability
* maintainability
* performance
* reliability
* safety

• Avoid unrelated refactors
• Do not assume issues without evidence

────────────────────────
REVIEW FOCUS
────────────────────────

• Code correctness and quality
• Readability and maintainability
• Proper reuse of existing utilities and patterns
• Performance and efficiency
• Security and stability
• Project architecture and conventions
• Testing and compatibility

────────────────────────
CHECK FOR
────────────────────────

Structure & Reuse

* Duplicate logic or missed reuse
* Repeated code that should be extracted
* Oversized functions/components
* Multiple concerns bundled together
* Existing utilities/hooks not reused

Correctness & Code Quality

* Logic bugs
* Weak guard conditions
* Hardcoded values
* Debug leftovers
* Console logs in production
* Commented-out code
* Incorrect null/undefined handling
* Missing error handling
* Misleading names
* Accidental mutation of state/props

Async & State

* Mixed async patterns
* Missing loading states
* Missing error states
* Race conditions
* Unhandled promises
* State updates after unmount
* Incorrect hook dependencies

Performance

* Unnecessary re-renders
* Heavy work inside render
* Missing memoization
* Inefficient loops
* Repeated processing
* Excessive API calls

Stability & Safety

* Memory leaks
* Missing cleanup
* Timers/listeners not removed
* Input validation gaps
* Unsafe data handling

Reliability

* Breaking changes
* Compatibility risks
* Edge cases not handled
* Missing empty/loading/failure states

Deleted Code

* Removed safeguards
* Removed cleanup logic
* Deleted required validations
* Lost error handling

Architecture

* Tight coupling
* Poor abstractions
* Business logic inside UI
* Missing separation of concerns

Testing

* Existing tests broken
* Missing tests for new logic
* Edge cases not covered
* Snapshot updates required

Compatibility

* API contract changes
* Type/interface changes
* Schema changes
* Migration risks
* Backward compatibility issues

Dependencies

* Unnecessary packages
* Duplicate libraries
* Version conflicts
* Bundle size impact
* Unused dependencies

Type Safety

* Unsafe casts
* Missing null checks
* Excessive any usage
* Inconsistent types
* Duplicate interfaces

Accessibility (Frontend)

* Missing labels
* Keyboard navigation issues
* Incorrect ARIA usage
* Color-only indicators

Monitoring

* Sensitive data logged
* Missing logging where required
* Missing metrics/tracing
* Insufficient error context

────────────────────────
FALSE POSITIVE GUARD
────────────────────────

* Verify the issue is introduced by this change

* Mark unrelated findings as:

  `[Pre-existing]`

* Ignore pre-existing problems

* Avoid speculative comments

* Do not request unrelated refactors

* Prefer project conventions over personal preferences

────────────────────────
PRIORITY ORDER
────────────────────────

1. Correctness
2. Security
3. Stability
4. Performance
5. Maintainability
6. Style / Nitpicks

Avoid overwhelming the author with low-value comments.

────────────────────────
OUTPUT FORMAT
────────────────────────

### A) Inline Review Comments

External PR

* GitHub inline review comments
* Professional and constructive tone
* Explain why the change is needed
* Suggest fixes when helpful
* Comment only on changed lines

Local Changes / Self PR

* Plain findings list
* Comment only on changed code

---

### B) Summary

Order findings by severity.

Severity Levels

* Critical
* High
* Medium
* Low
* Nit

Format

| # | File Path | Issue | Severity |
| - | --------- | ----- | -------- |

Example

|1|src/hooks/useApi.ts|Unhandled promise rejection|High|
|2|src/pages/Home.tsx|Duplicate filtering logic|Medium|

For unrelated problems use:

`[Pre-existing]`

---

### C) Suggested Commits

One logical change per commit.

Follow Conventional Commit format.

Example:

`fix(auth): handle null refresh token`

`refactor(products): extract duplicate filtering logic`

────────────────────────
NO FINDINGS CASE
────────────────────────

If no issues are found:

### A) Inline Review Comments

No issues found.

### B) Summary

Reviewed files:
...

No correctness, maintainability, performance,
security, or stability concerns were introduced
by this change.

────────────────────────
FINAL INTERACTION FLOW
────────────────────────

PHASE 1

Generate findings summary.

STOP.

Display ONLY:

---

Review ready.

Please confirm the summary:

• Reply with issue numbers to skip
Example:

`Skip: 2, 5`

• Reply `0` to keep all issues

I will then reorder and finalize the summary.

---

STOP.

Wait for user response.

Do NOT continue.

────────────────────────

PHASE 2

After receiving:

`0`

or

`Skip: ...`

Proceed.

Ask:

How should I proceed?

1. Prepare GitHub review comments and suggested commits
2. Apply confirmed fixes directly
3. Share findings report only

Wait for the user's choice.

────────────────────────

PHASE 3

Based on the user's selection:

1

Generate:

• GitHub review comments
• Suggested commits

2

Apply confirmed fixes.

3

Share findings report only.
