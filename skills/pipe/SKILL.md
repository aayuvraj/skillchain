---
name: pipe
description: Chain multiple AI agent skills into sequential pipelines. Output of each skill feeds as context into the next.
trigger: /pipe
platforms: claude, codex, claw, opencode, aider, cursor, gemini
---

# /pipe

Chain any skills together into a pipeline. Each skill's output becomes context for the next skill in the chain.

## Usage

```
/pipe review -> security-review -> caveman-commit
/pipe analyze -> refactor -> test
/pipe explain -> document -> summarize
/pipe <skill1> -> <skill2> -> <skill3>
```

## What /pipe Does

Without pipe, skills are isolated — `/review` has no idea `/security-review` exists. You manually copy context between them.

With pipe:
1. Runs `skill1` fully
2. Captures output + context
3. Feeds into `skill2` as prior context
4. Repeats down the chain
5. Final skill output = pipeline result

## Rules

- Skills separated by ` -> ` (with spaces)
- Minimum 2 skills required
- Skills run **sequentially**, never in parallel
- Each step gets: original user request + all prior step outputs as context
- If a step fails or produces empty output, pipeline halts and reports which step failed
- No infinite loops — each skill runs exactly once per pipeline invocation

## What You Must Do When Invoked

Parse the pipeline from the arguments. The format is:

```
/pipe <skill1> -> <skill2> -> ... -> <skillN>
```

**Step 1 — Parse**
Extract skill names by splitting on ` -> `. Trim whitespace. Minimum 2 skills. If fewer, tell user: "pipe needs at least 2 skills: /pipe skill1 -> skill2"

**Step 2 — Announce**
Tell user the pipeline you're about to run:
```
Pipeline: skill1 → skill2 → skill3
Running step 1/3: skill1
```

**Step 3 — Execute step 1**
Look up what skill1 does from your knowledge of available skills or CLAUDE.md/AGENTS.md. Execute it fully as if the user invoked it directly. Capture the complete output.

**Step 4 — Transition**
Announce: `Step 1/3 complete. Running step 2/3: skill2`
Inject prior step's output as context prefix: "Prior step (skill1) produced: [output summary]"

**Step 5 — Execute step 2..N**
Repeat for each skill in chain. Each step receives:
- Original user request/codebase context
- Summary of all prior steps' outputs

**Step 6 — Final summary**
After all steps complete:
```
Pipeline complete: skill1 → skill2 → skill3
[Final output from last skill]
```

## Supported Platforms

/pipe works with any agent that supports skill/slash-command invocation:
- Claude Code (`/pipe`)
- Codex (via AGENTS.md)
- OpenCode (via AGENTS.md)
- Aider (via AGENTS.md)
- Claw (via AGENTS.md)
- Cursor (via .cursor/rules)
- Gemini CLI (via GEMINI.md)

## Examples

**Code review pipeline:**
```
/pipe review -> security-review -> caveman-commit
```
Full review → security audit → compressed commit message, all in one command.

**Understand before change:**
```
/pipe explain -> refactor
```
Explains current code first, then refactors with that understanding as context.

**Document everything:**
```
/pipe review -> document -> summarize
```
Review code, generate docs, then summarize changes for PR description.
