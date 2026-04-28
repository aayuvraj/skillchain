<div align="center">

# skillchain

**Chain AI coding agent skills into pipelines.**

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
[![Works with Claude](https://img.shields.io/badge/Claude%20Code-✓-blue)](https://claude.ai/code)
[![Works with Codex](https://img.shields.io/badge/Codex-✓-green)](https://openai.com/codex)
[![Works with Cursor](https://img.shields.io/badge/Cursor-✓-purple)](https://cursor.sh)

```
/pipe review -> security-review -> commit
```

*Three skills. One command. Each step knows what the last one found.*

</div>

---

## The Problem

AI coding agents are powerful. Their skills are not.

Every skill is an island. You run `/review`, read the output, manually copy context, run `/security-review`, copy again, paste into your commit message. Three tools. Zero connection between them. Context lost at every handoff.

This is the current state of AI-assisted development:

```
You:  /review
AI:   [finds 4 issues]

You:  [manually copies issues]
You:  /security-review
AI:   [finds 3 vulns, unaware of the 4 issues above]

You:  [manually copies everything]
You:  write me a commit message
AI:   [writes generic message, misses half the context]
```

**skillchain fixes this.**

---

## The Solution

```
/pipe review -> security-review -> commit
```

That's it. Each step's output becomes context for the next. Your security review knows what the code review found. Your commit message knows what both found. No manual work. No lost context.

```
You:  /pipe review -> security-review -> commit

AI:   Pipeline: review → security-review → commit
      Running step 1/3: review...
      [finds 4 issues]

      Step 1 complete. Running step 2/3: security-review...
      [finds 3 vulns, aware of the 4 issues from step 1]

      Step 2 complete. Running step 3/3: commit...
      [writes precise commit citing all 7 findings]

      Pipeline complete.
```

---

## Install

**One file. No servers. No APIs. No configuration.**

### Claude Code

```bash
mkdir -p ~/.claude/skills/pipe
curl -o ~/.claude/skills/pipe/SKILL.md \
  https://raw.githubusercontent.com/aayuvraj/skillchain/main/skills/pipe/SKILL.md
```

Then in any Claude Code session:

```
/pipe review -> security-review -> commit
```

### Other Agents

| Agent | Install |
|-------|---------|
| **Codex** | Append `skills/pipe/SKILL.md` contents to `AGENTS.md` |
| **Cursor** | Copy to `.cursor/rules/pipe.mdc` |
| **Aider** | Append to `AGENTS.md` |
| **OpenCode** | Append to `AGENTS.md` |
| **Claw** | Append to `AGENTS.md` |
| **Gemini CLI** | Append to `GEMINI.md` |

---

## Pipelines

### Code Review Gate
```
/pipe review -> security-review -> commit
```
Full quality + security pass before every commit. Catches issues at two layers, writes a commit that references both.

### Understand Before Changing
```
/pipe explain -> refactor
```
Maps exactly what the code does before touching it. Prevents blind refactors that break hidden dependencies.

### Feature End-to-End
```
/pipe plan -> implement -> test -> document
```
Spec → code → tests → docs. Each step builds on real output from the previous one, not hallucinated context.

### Security-First Fix
```
/pipe security-review -> fix -> review -> commit
```
Find vulnerabilities, patch them, verify the fix, commit — all in one command.

### Onboard a New Codebase
```
/pipe graphify -> explain -> document
```
Build a knowledge graph of the entire codebase, explain the architecture, generate `ARCHITECTURE.md`. First-day-on-the-job, done in one command. Requires [graphify](https://github.com/safishamsi/graphify).

### PR-Ready
```
/pipe review -> document -> summarize
```
Review code, update inline docs, write the PR description. Open a PR that reviewers actually want to merge.

> See the full [pipeline cookbook](./pipelines/) for more examples.

---

## How It Works

`/pipe` is a meta-skill — a single markdown file that teaches any AI agent how to chain skills.

When invoked:

1. **Parses** the pipeline — splits on ` -> `, extracts skill names
2. **Announces** the plan — `Pipeline: review → security-review → commit`
3. **Executes step 1** fully, captures complete output
4. **Transitions** — injects prior step's output as context prefix for step 2
5. **Repeats** down the chain — each step is context-aware of all prior steps
6. **Summarizes** the full pipeline result

The key insight: skills don't need to call each other programmatically. They just need context. `/pipe` handles the context threading so every skill in the chain knows exactly what happened before it.

---

## Why This Matters

| Without skillchain | With skillchain |
|-------------------|-----------------|
| 3 manual skill invocations | 1 command |
| Context lost between steps | Full context carried forward |
| Generic outputs per step | Each step aware of prior findings |
| You copy-paste between tools | Pipeline handles handoffs |
| Works with one agent | Works with 7+ agents |

---

## Philosophy

Unix gave us `|`. One of the most powerful ideas in computing: small, focused tools chained into workflows greater than the sum of their parts.

```bash
cat file.txt | grep error | sort | uniq -c
```

AI coding agents have powerful tools. They just don't have `|` yet.

skillchain is `|` for AI agents.

---

## Roadmap

- [ ] Conditional branching — `if review:fail -> fix -> review`
- [ ] Parallel steps — `skill1 + skill2 -> merge -> skill3`  
- [ ] Named pipelines — save and reuse as shortcuts
- [ ] Community pipeline library
- [ ] Cross-agent pipelines — step 1 in Claude, step 2 in Codex

---

## Contributing

Built a pipeline that saved you time? Add it to the [cookbook](./pipelines/).

1. Fork
2. Add your pipeline to `pipelines/your-pipeline.md`
3. Open a PR

---

## License

MIT

---

<div align="center">

**If this saved you time, a ⭐ helps others find it.**

[github.com/aayuvraj/skillchain](https://github.com/aayuvraj/skillchain)

</div>

<!-- SEO: claude code skills, codex agents.md, cursor rules, aider, ai coding agent pipeline, skill chaining, slash command pipeline, agent workflow composer, claude pipe, skillchain -->
