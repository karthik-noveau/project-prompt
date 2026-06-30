Analyze the code changes by reverse engineering the complete runtime execution workflow from a new developer's perspective.



Generate a single connected ASCII execution tree that reconstructs the actual runtime execution, NOT the source-code structure or folder hierarchy.



The tree must represent the real business execution flow from the first public entry point to the final outcome.



Use the following structure:



[route] <HTTP Method> <URL Path>

[event] <Event Name>

[queue] <Queue Name>

[worker] <Worker Name>

[cron] <Cron Job Name>

[cli] <Command>

[ui] <UI Action>

[webhook] <Webhook Name>



└── Business Execution Step

    ├── [purpose]: Explain what this execution step accomplishes.

    ├── [change]: Explain only the code changes here. Omit if unchanged.

    ├── [external]: Mention external systems only when applicable (API, DB, Queue, Cache, Storage, Event, etc.).

    ├── [next]: Explain the next business execution step.

    │

    └── Child Business Execution Step

        ├── [purpose]: ...

        ├── [change]: ...

        ├── [external]: ...

        ├── [next]: ...

        │

        └── Nested Business Execution Step

            ...



Execution Rules:

- Start from every public entry point (HTTP route, UI action, queue consumer, worker, cron, webhook, CLI, event, etc.).

- If multiple entry points exist, generate a separate execution tree for each.

- Reconstruct the runtime call graph, not the file/class hierarchy.

- Continue recursively until the true execution end (response, publish, notification, database update, cache update, UI update, etc.).

- Never skip important runtime touch points, even if they are unchanged.

- Preserve branching (if/else, sync/async, remote/local, retries, parallel execution, nested workflows).

- Show nested workflows as child branches.

- Group helper/private/pass-through methods into the business execution step that owns them.

- Collapse implementation details that do not change the business flow.

- Name tree nodes using meaningful business responsibilities (e.g. "Resolve Flow Service Type", "Create Pages", "Publish Page") instead of raw method names.

- Mention the implementation location inline only when helpful:

  (folder/file → Class/Component → Method/Function).

- Keep [purpose], [change], [external], and [next] concise (1–2 lines).

- Omit [change] and [external] when not applicable.

- Use only ASCII tree characters (├── │ └──).

- Produce one continuous execution tree per entry point without separate architecture summaries or file-based sections.
