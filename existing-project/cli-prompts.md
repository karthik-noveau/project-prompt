Analyze the code changes and explain the impacted functionality as an end-to-end execution tree from a new developer's perspective.

Generate a single connected ASCII tree that follows the actual runtime execution, from the entry point to the final outcome.

Use the following hierarchy:

[route/event/trigger]
└── Major Execution Step
    ├── [purpose]: Explain what this step is responsible for.
    ├── [change]: Explain the code change here (omit if unchanged).
    ├── [external]: Show external systems (API, DB, Queue, Event, Cache, etc.) when applicable.
    ├── [next]: Explain what executes next.
    │
    └── Child Execution Step
        ├── [purpose]: ...
        ├── [change]: ...
        ├── [external]: ...
        └── [next]: ...

Guidelines:
- Organize the tree by runtime execution, NOT by folders or files.
- Start from the real entry point (HTTP route, UI action, cron, queue, event, CLI, etc.).
- Continue through every important touch point until the real end point (response, publish, notification, database update, UI update, etc.).
- Never skip intermediate execution steps that are required to understand the flow, even if they are unchanged.
- Group related operations under meaningful execution phases only when it improves readability.
- Show nested workflows, async jobs, child workflows, events, and background processes as child branches.
- Mention the implementation location inline when helpful using:
  (folder/file → Class/Component → Method/Function)
- Keep each [purpose], [change], [external], and [next] concise (1–2 lines).
- Omit optional sections ([change], [external]) if they are not applicable.
- Focus on business execution flow rather than low-level implementation details.
- Use only ASCII tree characters (├── │ └──).
