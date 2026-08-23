# AI Backend Development Protocol

## Tech Stack

```text
Runtime     : Node.js
Framework   : Express
ODM         : Dynamoose
Database    : AWS DynamoDB
Storage     : AWS S3
Testing     : Jest
```

## Spec Structure

```text
spec/
├── architecture.md
├── codebase-guide.md
├── development.md
├── data-model.md
├── api-contract.md
└── engines/
```

---
<details>
<summary><strong>🏗️ Architecture (architecture.md)</strong></summary>

```md
# architecture.md

The implementation blueprint, in three ordered sections.

---

## 1 · Requirements

  - Project overview
  - Consumers and roles
  - Resource list
  - Business rules
  - AWS resources required
  - Out of scope

---

## 2 · Complete Flow Chart

One ASCII diagram of the end-to-end business flow.
Cover entry point, every major workflow, decision branches, side effects and failure paths.

Example
  Register → Sign In → Browse Products → Add to Cart
           → Place Order → Payment → Order Confirmed → Sale Recorded

---

## 3 · Technical Flow Chart

One ASCII diagram per major workflow, showing how the code executes it.
Cover module responsibilities, server boot and AWS init, route map, the layer flow of every endpoint, the table and index touched at each step, and the error path.

Example
  Client → Route → Controller → Service → Model → DynamoDB → Response

---

Detailed enough for another developer to implement without asking questions.
```

</details>

---

<details>
<summary><strong>📚 Codebase Guide (codebase-guide.md)</strong></summary>

```md
# CODEBASE ARCHITECTURE

The mandatory architecture, boundaries and coding rules for the backend.

---

# Module System

ESM only. package.json sets "type": "module".
Every relative import includes the .js extension.
Named exports only. No require(). No default exports.

---

# Source Structure

index.js                 // imports the server, nothing else
src/
  server.js              // env · middlewares · route mounting · error middleware · listen
  aws/
    config.js            // the only place AWS is initialised — env, region, credentials, dynamoose.aws.sdk
    constant.js          // the only place table and bucket names are defined
    bucket.js            // S3 helpers
  common/                // shared helpers only, never resource-specific
    utils.js             // generateId · hasData · formatUTC
    service.base.js      // outbound request helper
  routes/                // paths and middleware wiring only, one named router per resource
    user.routes.js
    product.routes.js
  controllers/           // HTTP boundary — read, validate, call, respond, delegate errors to errorContext
    user.controller.js
    product.controller.js
    common/
      index.js           // runPaginatedQuery · errorContext · SORT, never duplicated in a controller
  models/                // one Dynamoose schema per resource, the only place keys and indexes live
    userModel.js
    productModel.js
  services/              // logic spanning models or steps, never touches req or res
    orderService.js
  migration/             // one-time table and bucket scripts, disabled by default
    routes.js
    table.js
    bucket.js

server.js and routes never hold business logic or database calls.
Controllers stay thin — multi-step or cross-resource logic belongs in services/.
spec/ is the source of truth. Never place application code there.

---

# Naming Convention

Folders           kebab-case
Routes            <resource>.routes.js
Controllers       <resource>.controller.js
Models            <resource>Model.js
Services          <name>Service.js
Constants         UPPER_SNAKE_CASE
Variables         camelCase
Functions         camelCase
Tables            <project>-<module>-<resource>
Indexes           <partitionKey>-<sortKey>-index
Buckets           kebab-case

---

# DynamoDB Rules

Tables
  One table per resource, created with throughput ON_DEMAND, create true, timestamps true.
  _id is the partition key. Tables queried by owner use the owner id as partition key and sortKey as range key.

Indexes
  A GSI exists for sorting and filtered listing only.
  Name it <partitionKey>-<sortKey>-index, project ALL, and list it in data-model.md.

Queries
  Always Query, never Scan. Scan belongs only in migration scripts.
  Select the index explicitly with .using().
  Whitelist sortable fields through SORT. Never trust req.query.sortBy.

Search
  Maintain a lowercase searchKey concatenating every searchable field.
  Rebuild it on every write. Search with contains.

Pagination
  Cursor based through runPaginatedQuery, using lastKey — the stringified LastEvaluatedKey.
  Never offset pagination. Never load a table into memory to slice it.

Writes
  batchGet caps at 100 keys. Chunk larger lists and tolerate a failed chunk.
  Conditional writes for uniqueness, transactions for multi-item atomicity.

Items
  Under 400KB. Large payloads go to S3 with the key stored on the item.
  Timestamps are ISO 8601 strings.

---

# ID Generation

Every id comes from generateId in common/utils.js.
  ORIGINAL  slug only
  SHORT     slug + 13 char uuid
  LONG      slug + full uuid
Never use a raw uuid where a readable id helps. Never let the client supply an id.

---

# API Rules

REST. Resource routers mounted under a module prefix.
  app.use("/ecommerce/products", productRoutes);

Status codes
  200 ok · 400 validation · 401 auth · 403 forbidden · 404 not found · 500 server

Response shapes
  List    { data, count, pageSize, currentPage, lastKey }
  Single  the object
  Delete  { id }
  Error   { message, error }
Shapes are defined in api-contract.md and must not drift.

---

# Validation

Validate at the controller boundary before any database call — required fields,
types, enums, formats, ranges and id ownership. Return 400 with a clear message.
Never pass unvalidated req.body into a write.
Never let a client set _id, workspaceId, appId, createdAt or updatedAt through a spread.

---

# Error Handling

Every controller wraps its body in try/catch and delegates to errorContext.
  return errorContext("Failed to create the product", { error, req, res });
errorContext attaches the message and request payload, logs the error and returns the right status.
The server registers a final error middleware after all routes.
Never fail silently. Never leak internals in production.
When a secondary update may fail without invalidating the primary operation, log it with context and continue.

---

# Logging

morgan for requests, console.info for lifecycle, console.error for failures with context.
Never console.log. Never log secrets, credentials or tokens.

---

# Configuration

Every secret and environment value comes from process.env through dotenv, documented in the README.
Never hardcode credentials, region or table names. Never commit .env or credential files.

---

# Security

CORS configured explicitly. Body size limits enabled.
Passwords hashed with bcrypt, never stored or returned in plain text.
Auth enforced with middleware, never inside a controller body.
Validate every id against its owning workspace or app before returning data.

---

# Code Quality

DRY · KISS · one responsibility per function.
Prefer early returns, async/await and small pure helpers.
Avoid deep nesting, duplicate query logic and silent catch blocks.
Always await. Never mix .then() with await. Parallelise independent calls with Promise.all.
Limits
  60 lines per function
  300 lines per file

---

# Documentation

Prefer self-documenting code. Comment only complex business logic.
Update data-model.md when a schema, key or index changes.
Update api-contract.md when an endpoint or response changes.

---

# Testing

Jest + Supertest.
  product.controller.test.js · orderService.test.js · utils.test.js · __tests__/
Every endpoint has a success and a failure test. Every service has a unit test.
Model access is mocked in controller tests.

---

# Forbidden

debugger
TODO
FIXME
Magic numbers
Magic strings
Dead code
Circular imports
Unused imports
Unused variables
```

</details>

---

<details>
<summary><strong>🗃️ Data Model (data-model.md)</strong></summary>

```md
# data-model.md

DynamoDB is designed from access patterns, never from entities.
List every access pattern BEFORE designing any table.

Format
  Access Pattern → Table → Key Condition → Index → Sort

Example
  List products of an app, newest first
    Table  studio-ecommerce-products
    Query  appId = :appId
    Index  appId-createdAt-index
    Sort   descending

The document must include
  - Access pattern list
  - Every table with its keys and attributes
  - Every GSI with name, keys and projection
  - Denormalised fields and why they exist
  - Search and pagination strategy

An access pattern that requires a Scan must be redesigned.
Query, index and pagination rules live in codebase-guide.md.
```

</details>

---

<details>
<summary><strong>🔌 API Contract (api-contract.md)</strong></summary>

```md
# api-contract.md

The complete REST surface, written before any controller.
Every endpoint must document
  - Method and path
  - Params and request body
  - Success response with status code
  - Error responses with status codes
  - Access pattern used
  - Auth requirement

Example
  GET /ecommerce/products
  Query   appId, pageSize, currentPage, sortBy, sortOrder, search, lastKey
  200     { data, count, pageSize, currentPage, lastKey }
  400     { message }
  500     { message, error }
  Pattern appId-createdAt-index

The contract is frozen once approved.
Changing a response shape requires updating api-contract.md first.
```

</details>

---

<details>
<summary><strong>⚙️ Engines (engines/)</strong></summary>

```md
# Development Engines

Split implementation into independent engines.
Naming
  engine-01-project-setup.md
  engine-02-aws-config.md
  engine-03-product-model.md
  engine-04-product-api.md
  ...
Examples
  ✔ Product Model
  ✔ Product API
  ✘ Model + controller + service in one engine
  ✘ Products + Orders
Rules
  - One engine, one responsibility.
  - Later engines depend only on completed engines.
  - Complete one engine before starting the next.

---

# Engine Contents

Every engine must contain
  - Objective
  - Scope
  - Dependencies
  - Files to create or modify
  - Implementation steps
  - Acceptance criteria

---

# engine-status.md

One status file for the whole project, in spec/engines/.
Never create a second one.

Format
  # Engine Status

  Current    Engine 04 · Products · In Progress
  Done       Routes · Layout · Table · Store
  Next       Sorting · Empty state · Tests
  Checks     Server ✔  ESLint ✔  Tests ⏳
  Updated    YYYY-MM-DD HH:mm

  Completed
    ✔ Engine 01
    ✔ Engine 02

Update it when an engine starts and when it completes.
Never guess completion percentages.
```

</details>

---

<details>
<summary><strong>🚀 Development (development.md)</strong></summary>

```md
# DEVELOPMENT WORKFLOW

How engines start, run and complete.
Coding standards live in codebase-guide.md — that document is authoritative.

---

# Specification Rules

- Never skip or partially generate the specification.
- codebase-guide.md and development.md are supplied. Copy them into spec/ unchanged.
- If implementation differs from the specification, update the specification first.

---

# Development Lifecycle

Generate Specification → User Approval → Engine 01 → Verify → Engine 02 → ... → Done
Approval is required once, for the specification.
After that execution is continuous — engines never wait.

---

# Implementation Order

## Phase 1

Generate every document in the Spec Structure.
Do not generate any application source code.
Wait for approval.

---

## Phase 2

Implement Engine 01, verify it, update engine-status.md.
Continue straight into the next engine and repeat until every engine is complete.

---

# Engine Completion Flow

Read Engine → Implement → Verify → Update Status → Next Engine

---

# Verification

Before moving to the next engine
Run
  npm run server : Starts without error
  npm run test   : Pass
  npm run lint   : Pass
Check
  - Acceptance criteria met
  - Structure, naming and boundaries follow codebase-guide.md
  - Every endpoint matches api-contract.md
  - Tables and indexes match data-model.md
  - No build or lint warnings

---

# Engine Completion Criteria

An engine is complete only if
  ✔ Acceptance criteria satisfied
  ✔ Verification passed
  ✔ engine-status.md marked Complete
Only then may the next engine begin.

---

# Continuous Execution

Never stop between engines.
Never wait for approval once the specification has been approved.
Update engine-status.md, then begin the next engine immediately.

---

# Documentation Rules

Update the specification whenever architecture, structure, scope or shared modules change.
Documentation must remain synchronised with implementation.

---

# Forbidden (Workflow)

Never
  - Skip, merge or partially implement engines
  - Generate future engine code
  - Ignore failing tests, type errors or lint errors
  - Leave incomplete documentation

---

# Project Completion

The project is complete only when
  ✔ Every engine is complete
  ✔ Every specification is satisfied
  ✔ engine-status.md shows all engines completed
  ✔ No remaining work exists
```

</details>
