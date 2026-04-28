# Pipeline: Understand Before Changing

```
/pipe explain -> refactor
```

**What it does:**
1. `explain` — maps the code: what it does, why it exists, hidden dependencies, edge cases
2. `refactor` — improves the code with full understanding from step 1 as context

**When to use:** Touching unfamiliar code. Prevents refactors that break things explain would have caught.

**Works with:** Claude Code, Codex, Cursor, Aider, Claw, OpenCode
