# Pipeline: Onboard a New Codebase

```
/pipe graphify -> explain -> document
```

**What it does:**
1. `graphify` — build knowledge graph of entire codebase: nodes, edges, communities, architecture map
2. `explain` — plain-language walkthrough of what the codebase does, informed by the full graph from step 1
3. `document` — generate `ARCHITECTURE.md` covering modules, data flow, entry points, key decisions

**When to use:** First day on a new project. Generates a full architecture doc from zero in one command.

**Requires:** [graphify](https://github.com/graphify/graphify) installed.

**Works with:** Claude Code, Codex, Cursor, Aider, Claw, OpenCode
