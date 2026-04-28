# Pipeline: Full Code Review Gate

```
/pipe review -> security-review -> caveman-commit
```

**What it does:**
1. `review` — general code quality, logic, style issues
2. `security-review` — OWASP top 10, injection, auth flaws, secrets in code
3. `caveman-commit` — compressed commit message from all findings

**When to use:** Before every non-trivial commit. Catches issues at three layers in one command.

**Works with:** Claude Code, Codex, Cursor, Aider, Claw, OpenCode
