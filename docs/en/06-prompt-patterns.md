# 06. Prompts as creative briefs

🌐 **English** · [Русский](../06-prompt-patterns.md)

**Verdict:** a good prompt is a short brief, not an incantation.

A good prompt isn't a magic word, it's a short brief. You tell the agent: what I want, in what form, what the constraints are. The more precise the brief, the less rework.

---

## A classification of patterns

Each pattern below belongs to one of five classes. This helps you quickly pick what to use for the task at hand.

| Class | When to use | Patterns | Where it's used |
| :-- | :-- | :-- | :-- |
| **Plan → Code** | The task touches several files or there are several solution paths. | 1. Plan first, 4. Three options, 5. Break into steps | [03-principles.md](03-principles.md), [04-workflow.md](04-workflow.md) |
| **Refactoring** | You need to change the code's structure without changing behavior, or make a pinpoint edit. | 2. Pinpoint edit | [10-antipatterns.md](10-antipatterns.md), [11-advanced-scenarios.md](11-advanced-scenarios.md), [18-senior-playbook.md](18-senior-playbook.md) |
| **Diagnostics / Debug** | Something broke; you need to find the cause and test hypotheses. | 6. Stop and hypothesize | [04-workflow.md](04-workflow.md), [10-antipatterns.md](10-antipatterns.md), [15-troubleshooting.md](15-troubleshooting.md) |
| **Review** | You want to check a diff, find bugs, or assess quality. | 3. Show the diff before applying, 7. Review as a request | [04-workflow.md](04-workflow.md), [09-checklists.md](09-checklists.md), [18-senior-playbook.md](18-senior-playbook.md) |
| **Documentation / ADR** | You need to record a decision, explain an approach, or hand off knowledge. | 8. Verdict first | [11-advanced-scenarios.md](11-advanced-scenarios.md), [18-senior-playbook.md](18-senior-playbook.md) |

---

## 1. Plan first

**Class:** Plan → Code  
**Where it's used:** the "plan first — then code" principle in [03-principles.md](03-principles.md), the "Sketch the path" step in [04-workflow.md](04-workflow.md).

**When to use.** The task touches more than two files or there are several solution paths.

**Example.**

```text
I want to add pagination to the orders list.
First propose a plan in 3–5 steps. Don't write code until we agree on the plan.
```

**Why it works.** The agent fixes the structure before going into details. You catch extra scope before the first diff.

---

## 2. Pinpoint edit

**Class:** Refactoring  
**Where it's used:** the "make it pretty without boundaries" anti-pattern in [10-antipatterns.md](10-antipatterns.md), legacy refactoring in [11-advanced-scenarios.md](11-advanced-scenarios.md) and [18-senior-playbook.md](18-senior-playbook.md).

**When to use.** You need to fix a specific thing without touching neighboring code.

**Example.**

```text
Make the minimal change that fixes the email validation.
Don't touch neighboring code and don't add anything "for the future."
```

**Why it works.** The "only this edit" constraint keeps the agent from refactoring that no one asked for.

---

## 3. Show the diff before applying

**Class:** Review  
**Where it's used:** the "Test by feel" step in [04-workflow.md](04-workflow.md), the checklists in [09-checklists.md](09-checklists.md), system review in [18-senior-playbook.md](18-senior-playbook.md).

**When to use.** You're not sure the agent will get the task on the first try and you want to check the direction.

**Example.**

```text
Apply the change, but first briefly explain what exactly will change and why.
```

You can specify the level:

```text
Explain at the level of "what the user will see" and "what changes in the data."
```

**Why it works.** The agent has to think the edit through out loud. You catch strange decisions before the commit.

---

## 4. Three options

**Class:** Plan → Code  
**Where it's used:** the "why first — then how" principle in [03-principles.md](03-principles.md), service design in [04-workflow.md](04-workflow.md).

**When to use.** There are several equal paths and you want to choose deliberately.

**Example.**

```text
We have a problem: orders are slow with a large list.
Propose 3 solution options with pros and cons.
I'll choose, and then we'll write code.
```

**Why it works.** The agent stops pushing a single solution. You keep control of the choice.

---

## 5. Break into steps

**Class:** Plan → Code  
**Where it's used:** breaking up large tasks in [04-workflow.md](04-workflow.md), the KISS principle and minimal diff in [03-principles.md](03-principles.md).

**When to use.** A vague task like "build the project," or one too big for a single session.

**Example.**

```text
The task is too big: rewrite the billing module.
Break it into 3–5 small subtasks. Let's start with the first one.
```

**Why it works.** An abstraction turns into a queue of concrete actions. Each step can be checked separately.

---

## 6. Stop and hypothesize

**Class:** Diagnostics / Debug  
**Where it's used:** diagnostics in [04-workflow.md](04-workflow.md), ignoring tests in [10-antipatterns.md](10-antipatterns.md), error analysis in [15-troubleshooting.md](15-troubleshooting.md).

**When to use.** You're both circling the problem and nothing works.

**Example.**

```text
We're stuck on the service crashing under large data volumes.
What do we know for sure, and where is the uncertainty? Which 3 hypotheses are worth testing?
```

**Why it works.** The trial-and-error stops. You move to checking facts instead of guessing.

---

## 7. Review as a request

**Class:** Review  
**Where it's used:** acceptance checklists in [09-checklists.md](09-checklists.md), system review in [18-senior-playbook.md](18-senior-playbook.md), the "check everything" principle in [03-principles.md](03-principles.md).

**When to use.** Code is already written — by you or the agent — and you want to find blind spots.

**Example.**

```text
Review this code. Find:
1. Bugs and edge cases.
2. Unnecessary complexity.
3. Violations of minimal diff.
4. Security: hardcoding, leaks, open dependencies.
```

You can add context:

```text
Imagine this is production code in a banking app. Be strict.
```

**Why it works.** The agent looks at the code with fresh eyes and catches what you missed from being too close to the task.

---

## 8. Verdict first

**Class:** Documentation / ADR  
**Where it's used:** recording decisions in [11-advanced-scenarios.md](11-advanced-scenarios.md), designing with the agent in [18-senior-playbook.md](18-senior-playbook.md).

**When to use.** The agent writes a long intro and you need a short answer.

**Example.**

```text
Give a short answer in the first sentence, then explain the details.
```

**Why it works.** The format forces the agent to state the gist first and unfold it after. It saves time during quick checks and helps record decisions in an ADR.

---

## How to combine them

The patterns stack with each other. Don't pick one — assemble a brief from two or three.

Example for a small feature:

```text
I want to add sorting of orders by date.
First propose a plan in 3 steps.
Then implement only the first step.
Before applying, explain what will change.
```

Example for a complex bug hunt:

```text
We're stuck on the service crashing under large data volumes.
Break the diagnostics task into subtasks.
Then propose 3 hypotheses and a plan to test each.
Give the verdict in the first sentence.
```

Order matters: first the task framing, then the constraints, then the answer format.

---

## Recipes by stack

If you don't want to assemble a prompt from scratch — take a ready-made brief for your stack. Each recipe has: a role, a reference to `AGENTS.md`, and a first prompt.

### Next.js / frontend

**Role:** frontend implementer. Writes UI and client logic per the plan, doesn't go into the backend.

**AGENTS.md:** template — [`templates/AGENTS.md`](../../templates/AGENTS.md), fill in the stack sections (Next.js, React, Tailwind, tests) and rules.

**First prompt:**

```text
We have a Next.js 14 project with TypeScript and Tailwind.
We need to add sorting of orders by date in the table on the /orders page.
First read AGENTS.md.
Propose a 3-step plan: API endpoint, table component, UI button.
Don't touch other pages and don't add new dependencies without agreement.
```

### Python backend

**Role:** backend implementer. Builds endpoints, services, and tests; doesn't touch the frontend.

**AGENTS.md:** template — [`templates/AGENTS.md`](../../templates/AGENTS.md), fill in the stack (FastAPI/Django, PostgreSQL, pytest, ruff/mypy).

**First prompt:**

```text
We have FastAPI + PostgreSQL, tests on pytest.
We need to add an endpoint to export orders to CSV.
First read AGENTS.md.
Propose a 3-step plan: repository, endpoint with a streaming response, tests.
No pandas and no writing files to disk. Don't change the contracts of other endpoints.
```

### Infra / DevOps

**Role:** infrastructure engineer. Edits Docker, CI/CD, configuration — plan first, then the minimal change.

**AGENTS.md:** template — [`templates/AGENTS.md`](../../templates/AGENTS.md), fill in the stack (Docker, GitHub Actions, Terraform/Compose, prod environment).

**First prompt:**

```text
We have Docker Compose for local dev and GitHub Actions for CI.
We need to add a healthcheck for the API service.
First read AGENTS.md and docker-compose.yml.
Propose a 3-step plan: Dockerfile healthcheck, compose depends_on condition, a CI check step.
Don't change the prod configuration and don't touch secrets.
```

---

Previous step: how to choose an environment — [`05-environments.md`](05-environments.md).

Next step: see how the templates work in real sessions — [`07-examples/`](07-examples/).
