# 01. What pair programming is

🌐 **English** · [Русский](../01-what-is-pair-programming.md)

Pair programming with AI is shared thinking. Your brain owns meaning and direction; the agent owns speed and routine. Together you build one thing, not two separate products.

← [README](../../README.md) | [02. The agent as a pair-programmer](02-agent-as-pair-programmer.md) →

## Classic pair programming

In the classic form, two developers sit at one computer: one types, the other watches from the side and catches mistakes. The result is sturdier, because two heads check the solution at the same time.

Example: the two of you are adding order filtering. One writes the query; the other notices that an empty value will return `null`, which the UI doesn't expect. The bug is caught before the commit, not in production.

More on the classic approach in the Agile Alliance glossary: [Pair Programming](https://www.agilealliance.org/glossary/pairing/).

## Comparison: classic pair vs. AI-pair

| | Classic pair | AI-pair |
| :-- | :-- | :-- |
| Who's at the keyboard | Two developers swap places | You type, the agent completes |
| How attention is split | One writes, the other catches errors | You hold the meaning, the agent the details |
| What the human partner brings | Business context, taste, accountability | You set the context and priorities |
| What the agent doesn't bring / and vice versa | A human feels risk and carries responsibility | The agent offers options and routine, but isn't accountable for the result |

## AI as a partner

With an AI editor the point is the same: two minds build one thing. But the second mind isn't a human — it's a model. It doesn't feel the business context, doesn't know what's "elegant" and what's a "hack," and bears no responsibility. So you set the direction and the agent helps you move.

```text
You:   We need to show a clear message if the file failed to upload.
Agent: Plan: add error codes, localization, logging, and a fallback UI.
You:   Let's start with the text under the button. Leave localization for now.
Agent: [proposes a patch]
You:   [reads the diff and refines the error text]
```

## What it is not

- **Not "write everything for me."** The agent writes, but you decide what stays.
- **Not Q&A.** You're working on a task, not asking it to explain a concept.
- **Not generate-and-pray.** Every change must solve a concrete task.

A typical trap: a student opens an empty project and writes "build me an online store." That's not pair programming. That's a blind order.

## Metaphor: two minds, one thing

Don't think of yourself as the driver and the agent as the navigator. Think of yourselves assembling one mechanism together. You hold the blueprint; the agent hands you tools and parts. If you get distracted, the mechanism won't be assembled to the blueprint.

```text
You:   We need to show the user the file upload progress.
Agent: We could build a WebSocket channel with a separate service and a task queue.
You:   Overkill. While the file is small, just update the percentage in the same request.
Agent: OK, adding a progress field to the response and a progress bar to the UI.
```

The agent proposes scale. Your job is to choose the scale that fits right now.

## How this connects to the rest of the guide

- [02. The agent as a pair-programmer](02-agent-as-pair-programmer.md) — who leads, who advises.
- [03. Principles](03-principles.md) — the boundaries this pair works within.
- [04. The creative loop](04-workflow.md) — how an idea becomes a commit.

Next: [02. The agent as a pair-programmer](02-agent-as-pair-programmer.md).
