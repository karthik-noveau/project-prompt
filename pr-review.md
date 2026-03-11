```
────────────────────────
EXTERNAL PR REVIEW CONFIG 
────────────────────────

add in .claude/settings.json

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
PR REVIEW TYPE
────────────────────────

External PR
  → Run: gh pr diff <number|url>
  → Review changed files for context
  → Do NOT modify code

Self PR / Local Changes
  → Run: git diff main...HEAD
  → Apply confirmed fixes after approval

────────────────────────
REVIEW FOCUS
────────────────────────
• Code correctness and quality
• Readability and maintainability
• Proper reuse of existing utilities/patterns
• Performance and efficiency
• Security and stability
• Follow project architecture and conventions
• Review only changes introduced in this PR

────────────────────────
CHECK FOR
────────────────────────

Structure & Reuse
  • Duplicate logic or missed reuse
  • Repeated code that should be extracted (utils/hooks)
  • Oversized functions/components needing split
  • Multiple concerns bundled in one PR

Correctness & Code Quality
  • Logic bugs or weak guard conditions
  • Hardcoded values or debug leftovers
  • Console logs left in production
  • Commented-out code
  • Incorrect null/undefined handling
  • Poor or missing error handling
  • Misleading names or inconsistent naming
  • Accidental mutation of state/props

Async & State
  • Mixed or incorrect async patterns
  • Missing loading/error state handling
  • Race conditions or unhandled promises
  • State updates after unmount
  • Missing/incorrect hook dependencies

Performance
  • Unnecessary re-renders
  • Heavy computations inside render
  • Expensive work not memoized
  • Inefficient loops or repeated processing

Stability & Safety
  • Memory leaks or missing cleanups
  • Timers/listeners not cleared
  • Input validation gaps
  • Unsafe data handling

Reliability
  • Breaking changes or compatibility risks
  • Edge cases not handled
  • Empty/loading/failure states missing

Deleted Code
  • Removed safeguards or edge-case handling
  • Deleted required error handling or cleanup

Architecture
  • Tight coupling or poor abstractions
  • Business logic inside UI layer
  • Missing or weak test coverage

────────────────────────
OUTPUT FORMAT
────────────────────────

A) Inline Review Comments
  • Professional and constructive tone
  • Explain why change is needed
  • Suggest fixes where helpful
  • Comment only on changed lines

  Formatting:
    • External PR → GitHub inline comments
    • Self PR     → Plain findings list

B) Summary
  • File Path(s)
  • Key Issues (introduced by this change only)
  • Severity: Low / Medium / High
  • Label unrelated issues as: [Pre-existing]

C) Suggested Commits (if needed)
  • One logical change per commit
  • Conventional Commit format

────────────────────────
CONFIRMATION (REQUIRED)
────────────────────────
Do not apply fixes, post comments, or create commits yet.

End with:

"Review ready. How should I proceed?

1) Prepare GitHub review comments and suggested commits
2) Apply confirmed fixes directly
3) Share findings report only"
```
