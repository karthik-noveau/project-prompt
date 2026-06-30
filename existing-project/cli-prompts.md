# 1. Code Changes — High Level

**Goal:** Understand the complete working flow first, then the code changes.

```text
Analyze the code changes and explain the impacted functionality as a continuous working flow.

Generate a simple hierarchical ASCII flow (Linux `tree` style). Follow the actual execution from trigger to completion without skipping intermediate touch points required to understand the flow, even if they are unchanged.

For each touch point, briefly explain:
- What happens?
- Why is this step required?
- What happens next?

When a code change is encountered, explain it in one line directly under that step.

Skip implementation details and unrelated branches.
```

---

# 2. Code Changes — Deep Technical

**Goal:** Understand the complete runtime flow and how the changes are implemented.

```text
Analyze the code changes and explain the impacted functionality as a continuous technical working flow.

Generate a hierarchical ASCII flow (Linux `tree` style). Follow the runtime execution from trigger to completion, including every intermediate touch point required to understand the impacted path.

For each touch point explain:
- Purpose
- Inputs
- Outputs
- Internal processing
- Data/control flow
- Technical terms
- Why it leads to the next touch point

When a modified touch point is reached, explain the code change, why it was required, and its impact.

Expand only the impacted path. Skip unrelated branches.
```

---

# 3. Feature — High Level

**Goal:** Understand how the complete feature works.

```text
Analyze the complete feature and explain it as a continuous working flow.

Generate a simple hierarchical ASCII flow (Linux `tree` style). Follow the functionality from trigger to completion without skipping important intermediate touch points.

For each touch point briefly explain:
- What happens?
- Why is it required?
- What happens next?

Skip implementation details and unrelated branches.
```

---

# 4. Feature — Deep Technical

**Goal:** Understand the complete implementation of the feature.

```text
Analyze the complete feature and explain it as a continuous technical working flow.

Generate a hierarchical ASCII flow (Linux `tree` style). Follow the runtime execution from trigger to completion, expanding every important touch point to the lowest meaningful level.

For each touch point explain:
- Purpose
- Inputs
- Outputs
- Internal processing
- Data/control flow
- Technical terms
- Design decisions
- Dependencies
- Edge cases
- Why it connects to the next touch point

Skip unrelated functionality.
```
