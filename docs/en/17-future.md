# 17. What's next: agents as part of the team

🌐 **English** · [Русский](../17-future.md)

In a couple of years the agent will stop being just a window in your editor. It'll be a partner with memory, a role, and skills — but you still make the decisions.

> **Verdict:** the technology will grow, but the distribution of responsibility won't change. You hold the direction, the agent speeds up the routine.

---

## Agents as team members: skills, memory, persona

Right now you explain the stack and the rules every time. Ahead, the agent will arrive with a loaded profile.

**Skills.** The agent knows your conventions: how to name components, where to keep utilities, which linter. You don't repeat "we don't do it that way."

> Example: you ask it to build a form. The agent immediately uses your `Button` from `ui-kit`, because its profile says: "all buttons — from `ui-kit`, don't create new ones."

**Memory.** The agent remembers what you did yesterday. It continues from the same place instead of re-asking for context.

> Example: yesterday you stopped at refactoring `billing.py`. Today you write: "let's continue billing." The agent picks up the plan and warns which tests are still failing.

**Persona.** The same model can work in different roles: a patient explainer for a beginner, a strict reviewer for a diff, an aggressive simplifier for legacy.

> Example: you switch the mode: "right now you're a reviewer — look for extra diff and strange names." The agent doesn't propose code, it checks.

This is a continuation of the idea from [11-advanced-scenarios.md](11-advanced-scenarios.md): each agent holds one role.

---

## Long context and large codebases

Context windows are growing. The agent will be able to hold hundreds of files in its head — but not everything that matters.

> Example: you walk into a 300,000-line monolith and ask: "where is `Order` created, and who modifies it?" The agent builds a map in minutes instead of hours.

The value is in targeted questions. The danger is in the illusion of full understanding. The agent might miss a hidden dependency through a config or a business rule. You verify the output the same way you verify a diff now.

---

## Multi-agent and orchestration

It's hard for one agent to be the architect, the coder, and the reviewer at once. In the future you'll launch several agents and hand them tasks.

> Example: Claude records the ADR, Cursor writes code per the plan, Kimi checks the diff. You don't ask one to do everything — you direct the flow.

Agents don't coordinate with each other on their own. Between them are you and the documents: `AGENTS.md`, ADRs, `workspace-context.md`. Without that, orchestration turns into chaos.

More on roles and context — in [11-advanced-scenarios.md](11-advanced-scenarios.md).

---

## Reasoning models

Reasoning models think out loud: they lay out the steps, weigh the options, find mistakes in their own reasoning. This is useful, but not magic.

> Example: before the code the agent writes: "There are three options for storing sessions. Option A is simpler but doesn't scale. Option B scales but adds a dependency. I choose A, because we have < 1000 users." You read the logic and catch it: "we already have 5000, choose B."

Reasoning isn't a replacement for your judgment. It's a draft you correct.

---

## Managing several projects at once

When agents become the norm, you'll have 2–3 projects in flight at once. You can't keep the context in your head — you move it into files.

> Example: `project-a` changes the API response format. You ask the agent: "which endpoints in `project-b` use this response?" It looks at `workspace-context.md` and answers to the point, instead of guessing.

Each project — its own `AGENTS.md`. Each switch — a clean session. Otherwise the agent will start mixing stacks.

It works on the same principles as now: [03-principles.md](03-principles.md) — minimal diff, plan before code, escalating uncertainty.

---

## For seniors and leads

You'll write less code. Your work shifts toward designing context, setting quality gates, and making architecture decisions.

The agent will handle the implementation if you set the boundaries. You describe the `AGENTS.md`, the acceptance checklists, the ADRs, and the orchestration rules. Without that, agents quickly turn from helpers into a source of technical debt.

Quality is no longer checked by hand, line by line. You design the quality gates: which tests are mandatory, which invariants can't be broken, what diff counts as acceptable. The agent passes through these gates, and you control their height.

A detailed playbook for seniors and leads — in [18-senior-playbook.md](18-senior-playbook.md).

---

## How the lead/senior role will change

The role won't disappear — it'll shift up the abstraction ladder.

- **Context as a product.** The lead designs not only the code architecture, but the context architecture: `AGENTS.md`, checklists, session templates, ADRs. This becomes part of the team's infrastructure.
- **Quality gates instead of line-by-line review.** You don't check every line — you set the rules the agent and the team are accepted by: tests, invariants, acceptable diff.
- **Orchestration instead of execution.** Working with several agents and projects requires the same skill as managing a team: assign roles, synchronize the flow, don't let contexts mix.
- **Retros and metrics.** Adopting AI is a process change. The lead watches the metrics, runs retros, and adjusts the rules — not just permits using an agent.

Concrete patterns — in [18-senior-playbook.md](18-senior-playbook.md). Metrics and the retro format — in [20-metrics-and-retro.md](20-metrics-and-retro.md).

---

## Scenario: a team without AI vs. a team with the guide's practices

Let's look at two teams two years out.

**Team A: without systematic practices**

- Each developer has their own prompt style and their own arrangements with the agent.
- Context lives in chats — when a person leaves, the knowledge is lost.
- Agents generate a lot of code, but regressions grow because there are no clear quality gates.
- The lead drowns in review, trying to manually catch hallucinations and extra diff.
- Technical debt piles up faster than before: agents can write, but can't answer for the consequences.

**Team B: the guide's practices**

- `AGENTS.md`, checklists, and session templates work as the team's operating system.
- A new developer joins a project and immediately understands how to work with the agent.
- AI-usage retros happen regularly, the rules get updated.
- The lead watches the metrics: time to PR, rollbacks, review load.
- Agents speed up the routine, but architecture decisions, invariants, and responsibility stay with people.

**The difference.** Both teams use AI. But for one it became a source of chaos and debt, and for the other — a predictable accelerator. The difference isn't the model, it's the discipline.

---

## What won't change

You still decide: which task to do, which architecture to choose, when to stop, what goes into a commit, and when to call a human.

The agent will suggest. It will write code faster than you. But responsibility for the result stays with you.

> Example: the agent says: "I'm sure it's better to rewrite the module on a new framework." You ask: "And what are the risks? How long will it take? What breaks?" — and you decide yourself.

---

Previous step: learn to talk to the agent — [16-ai-for-beginners.md](16-ai-for-beginners.md).

Let's return to the fundamentals that will always be relevant — [03-principles.md](03-principles.md).

Or back to the start — [README.md](../../README.md).
