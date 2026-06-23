## 🧩 **CODE GENERATION PROMPT TEMPLATE (PLACEHOLDER VERSION)**

---

### **Project Overview**

```
<ONE–TWO LINE DESCRIPTION OF THE PROJECT GOAL>
```

---

### **Tech Stack**

```
Framework   : React
Language    : Typescript
Styling     : CSS module
State       : Zustand
Testing     : Jest
```

---

## **ENGINE-BASED GENERATION STRATEGY**

### **Global Rules**

```
1. Split the entire project into multiple Engines
2. Engine order must be from <POC> → <ADVANCED>
3. Only ONE Engine is generated at a time
4. After each Engine:
   - STOP execution
   - ASK for user approval
5. No Engine may skip or compromise functionality
6. Each Engine must be independently testable
```

---

## **ENGINE TEMPLATE (REPEAT FOR EVERY ENGINE)**

### **ENGINE <ENGINE_NUMBER> : <ENGINE_NAME>**

---

### 1️⃣ Engine Objective

```
<WHY THIS ENGINE EXISTS>
<WHAT PROBLEM IT SOLVES>
```

---

### 2️⃣ Scope

**Inclusions**

```
- <FEATURE_1>
- <FEATURE_2>
```

**Exclusions**

```
- <EXCLUDED_FEATURE_1>
- <EXCLUDED_FEATURE_2>
```

---

### 3️⃣ Architecture (Micro-Level)

**Folder Structure**

```
<ROOT_FOLDER>/
  <FOLDER_1>/
  <FOLDER_2>/
```

**State Design (Zustand)**

```
<STATE_SLICE_NAME>:
  - <STATE_FIELD>
  - <STATE_ACTION>
```

**Component Responsibilities**

```
<COMPONENT_NAME>:
  - <RESPONSIBILITY>
```

**Data Flow**

```
<INPUT> → <STATE> → <RENDER>
```

---

### 4️⃣ Functional Flow (Step-by-Step)

```
1. <USER_ACTION>
2. <EVENT_HANDLER_TRIGGER>
3. <STATE_UPDATE>
4. <DATA_OR_MODEL_UPDATE>   // schema / model / local state / derived data
5. <UI_RE_RENDER>
```

---

### 5️⃣ Flow Diagram (Textual)

```
<USER_ACTION>
  ↓
<EVENT_HANDLER>
  ↓
<STATE_UPDATE>
  ↓
<RENDER_TRIGGER>
```

---

### 6️⃣ Test Cases (Jest)

**Unit Tests**

```
- <UNIT_TEST_CASE_1>
- <UNIT_TEST_CASE_2>
```

**State Tests**

```
- <STATE_BEHAVIOR_TEST>
```

**Rendering Tests**

```
- <RENDER_ASSERTION>
```

**Edge / Failure Cases**

```
- <EDGE_CASE>
```

---

### 7️⃣ Exit Criteria

```
- <CONDITION_1>
- <CONDITION_2>
```

---

### **ENGINE EXECUTION CONTROL**

```
ENGINE <ENGINE_NUMBER> COMPLETE.
Do you approve proceeding to ENGINE <NEXT_ENGINE_NUMBER>?
```

---

## **GLOBAL CONSTRAINTS**

```
- No architectural shortcuts
- No skipped tests
- No assumptions about future Engines
```

---

### **START CONDITION**

```
Begin with ENGINE <1>.
Wait for explicit user approval after each Engine.
```
