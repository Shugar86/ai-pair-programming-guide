# 02. The agent as a pair-programmer

🌐 **English** · [Русский](../02-agent-as-pair-programmer.md)

The core idea is to work together. You don't toss a task at the agent and walk away. You stay in the dialogue, choose the direction, and carry the responsibility. The agent isn't an executor — it's a partner that takes the routine and offers options.

← [01. What pair programming is](01-what-is-pair-programming.md) | [03. Principles](03-principles.md) →

## You're not a client, you're a partner

Bad form:

```text
You:   Build me authentication.
Agent: [writes a pile of code, pulls in libraries, changes routing]
You:   [hit Accept all without reading]
```

Normal form:

```text
You:   I need simple auth for the admin panel only. One user, login/password set in .env.
Agent: A three-step plan first, then code?
You:   Yes. Don't touch the public routes and don't add registration.
Agent: [gives a plan]
You:   [adjust the plan, then allow the code]
```

The only difference: in the second case you stay in the process.

## Zones of responsibility

| You | The agent |
| :-- | :-- |
| Frame the task | Generates options |
| Choose the architecture | Does the mechanical work: refactoring, tests |
| Do the final review | Hints where it might break |
| Accept the risks | Doesn't make decisions for you |

## How we split the work

| What you do | Why |
| :-- | :-- |
| Frame the task | The agent can't guess what you want |
| Set priorities | Time and resources are limited |
| Resolve trade-offs | Only you know what matters more right now |
| Review the diff | The agent can do harm without noticing |
| Run the tests | Automated tests are your safety net |
| Set the direction | The agent suggests, you decide |
| Update the docs | Only you know what the next people will need |

| What the agent does | Why |
| :-- | :-- |
| Writes code | Takes the routine |
| Proposes a plan | Shows the structure before the code |
| Looks for bugs | A fresh pair of eyes |
| Runs commands | Speeds up verification |
| Asks clarifying questions | Narrows the uncertainty |
| Generates tests and fixtures | Locks in behavior |
| Says when it's unsure | Narrows the risk zone |

## When you lead, and when the agent does

You lead when you decide what to do and why. The agent leads when it searches for implementation options and writes code. The switch happens every couple of minutes.

```text
You:   Add a "Copy link" button to the order card.
Agent: Plan: add a button component, a copy handler, a success message.
You:   OK, start with the handler. Leave the message for now.
Agent: [writes code]
You:   [reviews the diff]
You:   Use navigator.clipboard here, not execCommand.
Agent: [fixes it]
You:   [runs the tests]
```

Here you set the boundaries, the agent executes, you correct.

## Boundaries

**You don't delegate:**

- understanding the task;
- the architecture decision;
- the choice between equal options;
- responsibility for the result.

**The agent must not:**

- make large changes without agreement;
- apply edits without your review;
- pretend it understood when it didn't.

If you feel the agent is dragging you along, stop. Close the chat, look at the diff, state in your own words what's happening, and return to the task.

## Beyond a single agent

Soon you'll work with not one agent but several: one writes code, another reviews, a third hunts bugs, a fourth keeps the docs. For now you can imitate this by changing the agent's role in the prompt.

```text
Right now you are a strict reviewer. Don't write code. Find problems in the diff and suggest how to simplify.
```

When multi-agent becomes routine, the rules won't change: you still hold the direction and check the result. More in [`11-advanced-scenarios.md`](11-advanced-scenarios.md).

## The agent's limits

The agent is powerful but not omnipotent. Know where it's blind:

- **Hallucinations.** It can invent an API, a library, or a flag that doesn't exist.
- **No domain context.** It doesn't know your product, your users, or your team's agreements.
- **A pull toward over-engineering.** It loves factories, abstractions, and "flexibility for the future."

More in [10-antipatterns.md](10-antipatterns.md).

Next: lock in the basic rules in [03. Principles](03-principles.md).
