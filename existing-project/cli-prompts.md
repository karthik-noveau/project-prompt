# 1. Code Changes — High Level

**Goal:** Understand the functionality first, then the code changes.

```text
Analyze the code changes and generate a collapsed ASCII execution map of the impacted functionality.

First, explain the complete functionality flow from trigger to completion, showing only the major touch points and briefly describing each node's purpose and key technical terms.

Then, summarize the code changes by mapping them to the execution flow, explaining each change in a single line and where it impacts the functionality.

Skip implementation details and unrelated branches.
```

---

# 2. Code Changes — Deep Technical

**Goal:** Understand the functionality, then how the changes are implemented.

```text
Analyze the code changes and generate a detailed ASCII execution map of the impacted functionality.

First, explain the complete functionality flow from trigger to completion.

Then, recursively expand only the impacted execution path to the lowest meaningful level. For each node, explain its purpose, inputs, outputs, data/control flow, technical terms, dependencies, edge cases, and conclude with a single-line explanation of the code change at that node.

Skip unrelated branches.
```

---

# 3. Feature — High Level

**Goal:** Understand the complete feature workflow.

```text
Analyze the complete feature and generate a collapsed ASCII execution map.

Trace the complete lifecycle from trigger to completion, showing the major touch points and how they connect. Briefly explain each node's purpose and key technical terms. Skip implementation details and unrelated branches.
```

---

# 4. Feature — Deep Technical

**Goal:** Master the feature implementation.

```text
Analyze the complete feature and generate a detailed ASCII execution map.

Recursively expand the execution path to the lowest meaningful level. For each node, explain its purpose, inputs, outputs, data/control flow, technical terms, dependencies, design decisions, edge cases, and interactions with related modules. Skip unrelated functionality.
```
