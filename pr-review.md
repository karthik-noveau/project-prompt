```
────────────────────────
EXTERNAL PR REVIEW CONFIG
────────────────────────
Add this to: `.claude/settings.json`

{
  "alwaysThinkingEnabled": true,
  "mcpServers": {
    "github": {
      "command": "npx",
      "args": ["-y", "@modelcontextprotocol/server-github"],
      "env": {
        "GITHUB_PERSONAL_ACCESS_TOKEN": "<TOKEN>"
      }
    }
  }
}


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
Do **NOT** modify code.

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
REVIEW FOCUS
────────────────────────

• Code correctness and quality
• Readability and maintainability
• Proper reuse of existing utilities and patterns
• Performance and efficiency
• Security and stability
• Follow project architecture and conventions
• Review only changes introduced in this PR

────────────────────────
CHECK FOR
────────────────────────

Structure & Reuse

* Duplicate logic or missed reuse
* Repeated code that should be extracted (utils/hooks)
* Oversized functions/components needing split
* Multiple concerns bundled in one PR

Correctness & Code Quality

* Logic bugs or weak guard conditions
* Hardcoded values or debug leftovers
* Console logs left in production
* Commented-out code
* Incorrect null/undefined handling
* Poor or missing error handling
* Misleading names or inconsistent naming
* Accidental mutation of state/props

Async & State

* Mixed or incorrect async patterns
* Missing loading/error state handling
* Race conditions or unhandled promises
* State updates after unmount
* Missing/incorrect hook dependencies

Performance

* Unnecessary re-renders
* Heavy computations inside render
* Expensive work not memoized
* Inefficient loops or repeated processing

Stability & Safety

* Memory leaks or missing cleanups
* Timers/listeners not cleared
* Input validation gaps
* Unsafe data handling

Reliability

* Breaking changes or compatibility risks
* Edge cases not handled
* Empty/loading/failure states missing

Deleted Code

* Removed safeguards or edge-case handling
* Deleted required error handling or cleanup

Architecture

* Tight coupling or poor abstractions
* Business logic inside UI layer
* Missing or weak test coverage

────────────────────────
OUTPUT FORMAT
────────────────────────

### A) Inline Review Comments

• Professional and constructive tone
• Explain why change is needed
• Suggest fixes where helpful
• Comment only on changed lines

Formatting:

External PR → GitHub inline review comments
Local changes / Self PR → Plain findings list

---

### B) Summary

Include:

• File Path(s)
• Key Issues *(introduced by this change only)*
• Severity: Low / Medium / High

Label unrelated issues as:

`[Pre-existing]`

---

### C) Suggested Commits (if needed)

• One logical change per commit
• Follow Conventional Commit format

────────────────────────
FINAL INTERACTION FLOW
────────────────────────

After generating the review summary, follow this interaction strictly.

STEP 1 — Ask for summary confirmation

Display ONLY the message below:

---

Review ready.

Please confirm the summary:

• Reply with issue numbers to skip (example: `Skip: 1, 5, 6`)
• Reply `0` to keep all issues
• I will then reorder and finalize the summary

---

STOP.

Wait for the user's response.

Do NOT show the next step yet.

---

STEP 2 — After confirmation

When the user replies with `0` or `Skip: ...`, then display:

How should I proceed?

1. Prepare GitHub review comments and suggested commits
2. Apply confirmed fixes directly
3. Share findings report only


```
