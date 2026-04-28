# skillchain

**Chain AI coding agent skills into pipelines.**

```
/pipe review -> security-review -> commit
```

One command. Three skills. Each step feeds context into the next.

---

## The Problem

AI coding agents (Claude Code, Codex, Cursor, Aider, Claw) have powerful skills — but skills can't talk to each other.

You run `/review`, read the output, manually copy context, then run `/security-review`, read that output, manually copy again, then write your commit message.

Every skill is an island.

## The Solution

`skillchain` adds a `/pipe` skill to any agent. Chain skills with `->`. Output of each step becomes context for the next.

```
/pipe explain -> refactor -> test -> commit
```

That's: understand the code → refactor it → write tests → commit — all in one command, each step aware of what the previous step found.

---

## Quick Start

### Claude Code

```bash
pip install graphifyy
graphify claude install     # installs /graphify to Claude Code
```

Then copy `skills/pipe/SKILL.md` to `~/.claude/skills/pipe/SKILL.md`:

```bash
mkdir -p ~/.claude/skills/pipe
cp skills/pipe/SKILL.md ~/.claude/skills/pipe/SKILL.md
```

Now use it:

```
/pipe review -> security-review -> caveman-commit
```

### Other Agents

| Agent | Install |
|-------|---------|
| Codex | Copy `SKILL.md` content into `AGENTS.md` |
| Cursor | Copy `SKILL.md` content into `.cursor/rules/pipe.mdc` |
| Aider | Copy `SKILL.md` content into `AGENTS.md` |
| OpenCode | Copy `SKILL.md` content into `AGENTS.md` |
| Claw | Copy `SKILL.md` content into `AGENTS.md` |
| Gemini CLI | Copy `SKILL.md` content into `GEMINI.md` |

---

## How It Works

`/pipe` is a meta-skill. When invoked:

1. **Parses** the pipeline: splits on ` -> `, extracts skill names
2. **Announces** the plan: `Pipeline: review → security-review → commit`
3. **Executes step 1** fully, captures complete output
4. **Transitions**: injects prior output as context for step 2
5. **Repeats** down the chain — each step is context-aware of all prior steps
6. **Summarizes** the full pipeline result at the end

No configuration files. No servers. No APIs. Pure prompt composition.

---

## Example Pipelines

```bash
# Full code review pipeline
/pipe review -> security-review -> commit

# Understand before changing
/pipe explain -> refactor

# New feature end-to-end  
/pipe plan -> implement -> test -> document

# Security-first workflow
/pipe security-review -> fix -> review -> commit

# Onboarding a new codebase
/pipe graphify -> explain -> document
```

---

## Why This Matters

Current state of AI coding agents:

- ✅ Individual skills are powerful
- ❌ Skills are isolated — no composition
- ❌ Context is lost between skill invocations
- ❌ Workflows require manual copy-paste between steps

`skillchain` fixes this with a single 100-line skill file that works across every major agent.

---

## Skills That Work Well Together

| Pipeline | What it does |
|----------|--------------|
| `review -> security-review -> commit` | Full quality gate before committing |
| `explain -> refactor` | Understand first, then safely change |
| `graphify -> query` | Build knowledge graph, then query it |
| `plan -> implement -> test` | Spec → code → verify |
| `review -> document -> summarize` | Review + auto-docs + PR summary |

---

## Roadmap

- [ ] **Conditional branching** — `if review fails -> fix -> review` retry loops
- [ ] **Parallel steps** — `skill1 + skill2 -> merge -> skill3`
- [ ] **Named pipelines** — save pipelines as reusable shortcuts
- [ ] **Pipeline library** — community-contributed pipelines for common workflows
- [ ] **Cross-agent pipelines** — run step 1 in Claude, step 2 in Codex
- [ ] **skillchain CLI** — `skillchain run review -> security-review -> commit` from terminal

---

## Contributing

Add a new pipeline to the [Pipeline Library](#) or improve the `/pipe` skill for a specific agent.

1. Fork the repo
2. Add your pipeline example to `pipelines/` or improve `skills/pipe/SKILL.md`
3. Open a PR

---

## Philosophy

Skills should compose. The best AI workflows are pipelines, not one-shots. `skillchain` brings Unix pipe philosophy to AI coding agents — small, focused skills chained into powerful workflows.

```
skill1 | skill2 | skill3
```

Just with context instead of stdout.

---

## License

MIT

---

**If this saved you time, star it.** It helps others find it.

<!-- Keywords: claude code skills, codex agents, cursor rules, aider, ai coding agent, skill chaining, skill pipeline, claude pipe, agent workflow, slash command chaining -->
