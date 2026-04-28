# Pipeline: Feature End-to-End

```
/pipe plan -> implement -> test -> document
```

**What it does:**
1. `plan` — spec the feature: acceptance criteria, edge cases, API surface, data model
2. `implement` — write code against the plan from step 1
3. `test` — write tests that verify the implementation from step 2
4. `document` — write docs covering the feature, informed by all prior steps

**When to use:** Greenfield features. Each step builds on real output from the previous — no hallucinated context.

**Works with:** Claude Code, Codex, Cursor, Aider, Claw, OpenCode
