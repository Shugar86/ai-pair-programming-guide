# Templates

🌐 **English** · [Русский](README.ru.md)

This folder contains starter files for working with an agent. Copy them into your project, fill them in for yourself, and update them as you go. A good template saves time on explanations and lowers the risk of the agent going the wrong way.

What's here:

- [`AGENTS.md`](AGENTS.md) — the project contract: stack, roles, rules, prohibitions.
- [`ADR-template.md`](ADR-template.md) — a form for recording architecture decisions.
- [`session-template.md`](session-template.md) — a card for one pair-programming session.

---

## When and why to keep an `AGENTS.md`

`AGENTS.md` is the project's long-term memory for the agent. It states which language to speak, the stack, who makes decisions, which tests to run, and what can't be done without agreement.

Create an `AGENTS.md` if:

- the project lives longer than one session;
- there's more than one developer or several agents on the project;
- there are implicit conventions: naming, folder structure, the migration approach;
- you want to avoid repeated explanations and typical mistakes.

More in [05-environments.md](../docs/en/05-environments.md) and [18-senior-playbook.md](../docs/en/18-senior-playbook.md).

---

## When to use an ADR

An ADR (Architecture Decision Record) captures a non-trivial decision and the reason it was made. Don't write an ADR for every little thing — only when the choice affects module boundaries, contracts, the stack, or rollback.

Examples of reasons for an ADR:

- a new service or module;
- a change to an API or data format;
- replacing a library / database;
- introducing an adapter during legacy refactoring.

How to keep it:

1. Take [`ADR-template.md`](ADR-template.md).
2. Name the file `docs/adr/ADR-NNN-short-title.md`.
3. Fill in the context, the decision, the alternatives, and the consequences.
4. If the decision affects working with the agent, fill in the AI block.

On designing with the agent and recording decisions — in [11-advanced-scenarios.md](../docs/en/11-advanced-scenarios.md) and [18-senior-playbook.md](../docs/en/18-senior-playbook.md).

---

## The session card

[`session-template.md`](session-template.md) helps you not lose the thread in a long dialogue. Fill it in for tasks that don't fit in one iteration, or when you hand off context to another person / agent.

What's recorded:

- the task in one sentence;
- the step plan;
- what's done, what's blocked;
- verification: tests, diff, commit message;
- a short reflection.

Session cards are especially useful in distributed teams and when working across several repositories. More in [04-workflow.md](../docs/en/04-workflow.md) and [11-advanced-scenarios.md](../docs/en/11-advanced-scenarios.md).

---

## How to choose what to use

| Situation | What to use |
| :-- | :-- |
| A new project | `AGENTS.md` + the project's `README.md` |
| A non-trivial architecture decision | `ADR-template.md` |
| A task spanning several sessions | `session-template.md` |
| Several projects | An `AGENTS.md` in each + a shared `workspace-context.md` |

The basic principles of pair programming with an agent — in [03-principles.md](../docs/en/03-principles.md). The step-by-step workflow — in [04-workflow.md](../docs/en/04-workflow.md).
