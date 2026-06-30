# 1. Code Changes — High Level

**Goal:** Understand the functionality first, then the code changes.

```text
Analyze the code changes and explain the impacted functionality as a working flow.

Generate a collapsed hierarchical ASCII tree (similar to the Linux `tree` command). Do NOT use boxes, tables, or flowcharts.

First, show the complete functionality flow from trigger to completion using only the major touch points.

For each node, briefly explain:
- What happens?
- Why is it needed?
- Key technical terms (if any)

Then, under the relevant node, summarize the code changes in a single line.

Skip implementation details and unrelated branches.
```

---

# 2. Code Changes — Deep Technical

**Goal:** Understand the functionality, then the implementation behind the changes.

```text
Analyze the code changes and explain the impacted functionality as a detailed working flow.

Generate a hierarchical ASCII tree (Linux `tree` style). Do NOT use boxes, tables, or flowcharts.

First, show the complete functionality flow from trigger to completion.

Then, recursively expand only the impacted branches to the lowest meaningful level.

For each node, explain:
- Purpose
- Inputs
- Outputs
- Internal processing
- Data/control flow
- Technical terms
- Dependencies
- Edge cases

Under each affected node, explain the related code change in one line.

Skip unrelated branches.
```

---

# 3. Feature — High Level

**Goal:** Understand how the complete feature works.

```text
Analyze the complete feature and explain it as a working flow.

Generate a collapsed hierarchical ASCII tree (Linux `tree` style). Do NOT use boxes, tables, or flowcharts.

Trace the functionality from trigger to completion, showing only the major touch points.

For each node, briefly explain:
- What happens?
- Why is it needed?
- Key technical terms (if any)

Skip implementation details and unrelated branches.
```

---

# 4. Feature — Deep Technical

**Goal:** Understand the complete implementation of the feature.

```text
Analyze the complete feature and explain it as a detailed working flow.

Generate a hierarchical ASCII tree (Linux `tree` style). Do NOT use boxes, tables, or flowcharts.

Recursively expand the execution path to the lowest meaningful level.

For each node, explain:
- Purpose
- Inputs
- Outputs
- Internal processing
- Data/control flow
- Technical terms
- Dependencies
- Design decisions
- Edge cases
- Interactions with related modules

Skip unrelated functionality.
```
