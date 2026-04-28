# Pipeline: PR-Ready

```
/pipe review -> document -> summarize
```

**What it does:**
1. `review` — full code quality pass, flags issues
2. `document` — generates inline docs and updates any relevant README sections
3. `summarize` — writes PR title, description, and bullet-point summary of changes

**When to use:** Any time you're about to open a pull request. Produces review-ready code + a complete PR description in one shot.

**Works with:** Claude Code, Codex, Cursor, Aider, Claw, OpenCode
