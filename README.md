# AI Pair Programming — build together with your agent

🌐 **English** · [Русский](./README.ru.md)

[![License: MIT](https://img.shields.io/badge/license-MIT-yellow.svg)](#license)
[![Lang: EN · RU](https://img.shields.io/badge/lang-EN%20·%20RU-0a7cff.svg)](./README.ru.md)
[![Type: practical guide](https://img.shields.io/badge/type-practical%20guide-8b5cf6.svg)](#whats-inside)
[![Cursor · Claude Code · Kimi](https://img.shields.io/badge/agents-Cursor%20·%20Claude%20Code%20·%20Kimi-1C3C3C.svg)](docs/en/05-environments.md)

This guide doesn't teach you to press a "do it for me" button. It teaches you to work with Cursor, Kimi Code, Claude Code, and other agents as a partner: you hold the direction, the agent helps you write, review, and not go off the rails.

> **The point:** AI is an amplifier of your thinking, not a replacement for it.

---

## Who this guide is for

- **Beginner.** You just opened an AI editor. Start with setting up your environment and your first session.  
  Path: [`docs/en/12-setup.md`](docs/en/12-setup.md) → [`docs/en/16-ai-for-beginners.md`](docs/en/16-ai-for-beginners.md) → [`docs/en/04-workflow.md`](docs/en/04-workflow.md).
- **Practitioner.** You already write code — you want to work with an agent faster and cleaner.  
  Path: [`docs/en/01-what-is-pair-programming.md`](docs/en/01-what-is-pair-programming.md) → [`docs/en/03-principles.md`](docs/en/03-principles.md) → [`docs/en/06-prompt-patterns.md`](docs/en/06-prompt-patterns.md) → [`docs/en/07-examples/`](docs/en/07-examples/).
- **Lead.** You decide how your team will use AI, and you don't want spaghetti in the repo.  
  Path: [`docs/en/11-advanced-scenarios.md`](docs/en/11-advanced-scenarios.md) → [`docs/en/18-senior-playbook.md`](docs/en/18-senior-playbook.md) → [`docs/en/17-future.md`](docs/en/17-future.md).

Each path is its own, but the principles are the same.

## If you're in a hurry

- [Quick start: one session from task to commit](docs/en/04-workflow.md)
- [Anti-patterns and traps](docs/en/10-antipatterns.md)
- [For a lead / senior](docs/en/18-senior-playbook.md)

## Why this is about creating, not discipline

The rules here aren't a report card. They contain chaos to make room for creativity.  
When you know who's leading, what to check, and where to go, the agent stops being an obstacle and becomes a working hand.

Example: you want to add a dark theme to your app. Without boundaries, the agent might rewrite half your CSS, pull in a new library, and break your forms. With boundaries you say: "CSS variables only, no new dependencies, verify both themes on three screens." You get a result, not an archaeology dig.

## What it sounds like

**Dialogue 1. Too complex.**

```text
You:   Add search by name to the projects list.
Agent: We could use full-text search, index the tags, and set up autocomplete.
You:   Stop. For now we search the already-loaded list with includes(). No new services.
Agent: OK, adding a client-side filter.
```

**Dialogue 2. You're leading.**

```text
You:   Fix a bug: validation crashes when the email is empty.
Agent: Plan: validate the input, throw a custom exception, wrap the form in try/catch.
You:   No. Just return null and show a message under the field. Less code — fewer bugs.
Agent: Got it. Changing only the empty-value handling.
```

## What's inside

### Foundation & philosophy

- [`docs/en/01-what-is-pair-programming.md`](docs/en/01-what-is-pair-programming.md) — what pair programming with AI is.
- [`docs/en/02-agent-as-pair-programmer.md`](docs/en/02-agent-as-pair-programmer.md) — who owns what: you vs. the agent.
- [`docs/en/03-principles.md`](docs/en/03-principles.md) — 8 principles that work in any environment.

### The daily loop

- [`docs/en/04-workflow.md`](docs/en/04-workflow.md) — the working loop from task to commit.
- [`docs/en/08-exercises.md`](docs/en/08-exercises.md) — hands-on exercises.
- [`docs/en/09-checklists.md`](docs/en/09-checklists.md) — checklists for every stage.
- [`docs/en/10-antipatterns.md`](docs/en/10-antipatterns.md) — anti-patterns of working with AI.

### Environment & tools

- [`docs/en/05-environments.md`](docs/en/05-environments.md) — Cursor, Kimi, Claude, OpenCode, Copilot, Cody. Official sites: [Cursor](https://www.cursor.com/), [Claude Code](https://docs.anthropic.com/en/docs/agents-and-tools/claude-code/overview), [Kimi Code](https://www.kimi.com/code).
- [`docs/en/06-prompt-patterns.md`](docs/en/06-prompt-patterns.md) — request templates that save time.
- [`docs/en/07-examples/`](docs/en/07-examples/) — real text sessions.
- [`docs/en/12-setup.md`](docs/en/12-setup.md) — what to download, how to install agents, git, packages, and the stack.
- [`docs/en/13-git-github.md`](docs/en/13-git-github.md) — git and GitHub basics: clone, commit, PR, merge, CI/CD.
- [`docs/en/14-ide-cli-workflow.md`](docs/en/14-ide-cli-workflow.md) — how to work in the IDE and in the terminal.
- [`docs/en/15-troubleshooting.md`](docs/en/15-troubleshooting.md) — what to do when nothing works: WSL, SSH, VDS, rollbacks.
- [`templates/`](templates/) — `AGENTS.md`, ADR, and session-card templates for your projects.

### For beginners

- [`docs/en/16-ai-for-beginners.md`](docs/en/16-ai-for-beginners.md) — how to show a task to a neural net and what to do when nothing makes sense.

### For seniors & leads

- [`docs/en/11-advanced-scenarios.md`](docs/en/11-advanced-scenarios.md) — advanced scenarios and real cases.
- [`docs/en/18-senior-playbook.md`](docs/en/18-senior-playbook.md) — the senior/lead playbook: design, multi-agent setups, context, legacy.
- [`docs/en/19-security-and-policy.md`](docs/en/19-security-and-policy.md) — what you must never send to agents, secrets, and the AI-usage policy for a team.
- [`docs/en/20-metrics-and-retro.md`](docs/en/20-metrics-and-retro.md) — AI-adoption metrics and a team retro format.
- [`docs/en/17-future.md`](docs/en/17-future.md) — agents as part of the team: what's coming in 2+ years.

## Quick start

1. Open the project in an AI-enabled editor.
2. Describe the task in one verifiable sentence.
3. Tell the agent: "Plan first, then code. Don't touch the whole project."
4. Pick the smallest step.
5. Implement: the agent writes, you read the diff.
6. Check the tests, the diff, and common sense.
7. Commit with a message that explains what changed.

Details — in [`docs/en/04-workflow.md`](docs/en/04-workflow.md).

## If nothing makes sense

Start with [`docs/en/16-ai-for-beginners.md`](docs/en/16-ai-for-beginners.md). It covers how to show a task to a neural net, what to do when the agent didn't get it, and how not to drown in the answer.  
If your technical environment breaks — go to [`docs/en/15-troubleshooting.md`](docs/en/15-troubleshooting.md).

## How to use it in a team

- Show juniors [`docs/en/16-ai-for-beginners.md`](docs/en/16-ai-for-beginners.md), then [`docs/en/04-workflow.md`](docs/en/04-workflow.md).
- Set up [`AGENTS.md`](templates/AGENTS.md) from [`templates/`](templates/).
- Use [`docs/en/09-checklists.md`](docs/en/09-checklists.md) and [`docs/en/10-antipatterns.md`](docs/en/10-antipatterns.md) as retro checklists.
- Run a workshop on [`docs/en/08-exercises.md`](docs/en/08-exercises.md) if you want to align practice.

## License

MIT — copy, adapt, and use it freely, in study and at work.
