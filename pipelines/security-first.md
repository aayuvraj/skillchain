# Pipeline: Security-First Fix

```
/pipe security-review -> fix -> review -> commit
```

**What it does:**
1. `security-review` — find all vulnerabilities: injection, auth, secrets, insecure deps
2. `fix` — patch every issue found in step 1
3. `review` — general quality pass on the fixed code
4. `commit` — commit message summarizing what was patched and why

**When to use:** Before shipping anything that touches auth, user data, external APIs, or file I/O.

**Works with:** Claude Code, Codex, Cursor, Aider, Claw, OpenCode
