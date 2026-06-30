# 1. Code Changes — High Level

**Goal:** Understand how the functionality works first, then identify what changed.

```text
Analyze the code changes and organize the impacted functionality into a hierarchical functional tree.

Start with the highest-level responsibilities, then recursively group related touch points under each responsibility while preserving the execution order within each branch.

Include intermediate touch points required to understand the flow, even if they are unchanged.

For each node briefly explain:
- Responsibility
- Purpose
- What happens next

Under each changed node, summarize the code change in one line.

Use only a hierarchical ASCII tree (top-down branching). Do NOT generate a linear execution flow, flowchart, boxes, or tables.
```

---

# 2. Code Changes — Deep Technical

**Goal:** Understand how the functionality works internally and how the code changes are implemented.

```text
Analyze the code changes and organize the impacted functionality into a detailed hierarchical functional tree.

Start from the top-level functionality, recursively decompose it into responsibilities, execution touch points, and implementation steps while preserving execution order within each branch.

Include intermediate touch points required to understand the flow, even if they are unchanged.

For each node explain:
- Responsibility
- Purpose
- Inputs
- Outputs
- Internal processing
- Technical terms
- Dependencies
- Why it leads to the next touch point

Under each changed node explain:
- What changed
- Why it changed
- Impact

Expand only branches related to the code changes.

Use only a hierarchical ASCII tree (top-down branching). Do NOT use boxes, flowcharts, or tables.
```

---

# 3. Feature — High Level

**Goal:** Understand the complete feature workflow.

```text
Analyze the complete feature and organize it into a hierarchical functional tree.

Start with the highest-level responsibilities, then recursively group related touch points while preserving execution order within each branch.

Include important intermediate touch points required to understand the feature.

For each node briefly explain:
- Responsibility
- Purpose
- What happens next

Use only a hierarchical ASCII tree (top-down branching). Do NOT generate a linear execution flow, flowchart, boxes, or tables.
```

---

# 4. Feature — Deep Technical

**Goal:** Master the complete feature implementation.

```text
Analyze the complete feature and organize it into a detailed hierarchical functional tree.

Start from the top-level functionality, recursively decompose it into responsibilities, execution touch points, and implementation steps while preserving execution order within each branch.

For each node explain:
- Responsibility
- Purpose
- Inputs
- Outputs
- Internal processing
- Technical terms
- Dependencies
- Design decisions
- Edge cases
- Why it connects to the next touch point

Expand every important branch required to understand the feature.

Use only a hierarchical ASCII tree (top-down branching). Do NOT use boxes, flowcharts, or tables.
```
