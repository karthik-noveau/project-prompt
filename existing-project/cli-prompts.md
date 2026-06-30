# 1. Code Changes — High Level

**Goal:** Understand the functionality first, then identify the code changes.

```text
Analyze the code changes and organize the impacted functionality into a top-down hierarchical architecture diagram.

Use an organization-chart style ASCII visualization (not a Linux tree). Group related responsibilities into major branches, then recursively group their touch points beneath them while preserving execution order within each branch.

After the diagram, explain each branch in execution order:
- Responsibility
- Purpose
- How it connects to the next branch

Include intermediate touch points required to understand the flow, even if unchanged.

Finally, under each affected touch point, summarize the related code change in one line.

Do NOT use flowcharts, boxes, or tables.
```

---

# 2. Code Changes — Deep Technical

**Goal:** Understand the functionality and implementation of the changed code.

```text
Analyze the code changes and organize the impacted functionality into a detailed top-down hierarchical architecture diagram.

Use an organization-chart style ASCII visualization. Start from the highest-level functionality and recursively decompose it into responsibilities, execution touch points, and implementation steps while preserving execution order within each branch.

After the diagram, explain each branch from top to bottom:
- Responsibility
- Purpose
- Inputs
- Outputs
- Internal processing
- Technical terms
- Dependencies
- Why it connects to the next touch point

Include intermediate touch points required to understand the flow, even if unchanged.

Under every changed touch point explain:
- What changed
- Why it changed
- Impact

Expand only branches related to the code changes.

Do NOT use flowcharts, boxes, or tables.
```

---

# 3. Feature — High Level

**Goal:** Understand the complete feature workflow.

```text
Analyze the complete feature and organize it into a top-down hierarchical architecture diagram.

Use an organization-chart style ASCII visualization. Group the feature into major responsibilities, then recursively organize related touch points while preserving execution order within each branch.

After the diagram, explain each branch in execution order:
- Responsibility
- Purpose
- How it connects to the next branch

Include important intermediate touch points required to understand the feature.

Do NOT use flowcharts, boxes, or tables.
```

---

# 4. Feature — Deep Technical

**Goal:** Master the complete feature implementation.

```text
Analyze the complete feature and organize it into a detailed top-down hierarchical architecture diagram.

Use an organization-chart style ASCII visualization. Start from the highest-level functionality and recursively decompose it into responsibilities, execution touch points, and implementation steps while preserving execution order within each branch.

After the diagram, explain each branch from top to bottom:
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

Do NOT use flowcharts, boxes, or tables.
```
