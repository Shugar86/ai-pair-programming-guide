# 11. Advanced scenarios for working with AI

🌐 **English** · [Русский](../11-advanced-scenarios.md)

The basic principles work everywhere. But in complex tasks — legacy, migrations, design, several projects — they need orchestration. You hold the map; the agents move the pieces.

> **Verdict:** the harder the task, the more planning and the less code at once.

---

## Scenarios by type

| Type | When it applies | The main difficulty |
| :-- | :-- | :-- |
| Legacy refactoring | Old code works, but no one understands how | The fear of breaking what "works anyway" |
| Cross-module changes | The change touches several modules | Hidden dependencies and contracts |
| Several repositories / workspace | 2–3 projects in flight at once | Context dissolves between stacks |
| A distributed team | People in different time zones, the agent is the common language | Continuity of context between sessions |

---

## 1. Refactoring a legacy module

The old code works, but no one understands how exactly. It's scary to touch.

### Multi-session flow

#### Day 1 — understanding and a map

**Goal:** learn what the module does, where the seams are, where the risks are.

**Prompt:**

```text
Analyze the file legacy_billing.py.
Don't change the code. Make a list:
1) what this module does,
2) which functions could be extracted separately,
3) where the hidden dependencies are.
```

**Artifacts:**
- `docs/adr/ADR-011-legacy-billing-boundaries.md` — the module boundaries and the first seams.
- `docs/notes/legacy-billing-map.md` — a map of inputs, outputs, side effects.
- A session card: what we learned, what the risks are.

#### Day 2 — the first seam

**Goal:** extract one clean function without changing behavior.

**Prompt:**

```text
Extract the tax calculation from legacy_billing.py into a separate helper.
Don't change the logic. Just duplicate the behavior in a new file and replace the call.
After the edit, run the tests.
```

**Artifacts:**
- A new `src/billing/tax_helper.py`.
- An updated `legacy_billing.py` with the import.
- A session card: diff, tests, remarks.

#### Day 3 — the next seam and locking in

**Goal:** extract the second function, record the intermediate state.

**Prompt:**

```text
Now extract the discount calculation the same way.
After that, update the ADR: which functions are already isolated, what stays inside the module.
```

**Artifacts:**
- An updated ADR.
- The project's `AGENTS.md` extended: the rule "legacy refactoring — one seam per session."
- Commit: `refactor: isolate tax and discount helpers from legacy billing`.

**Rule:** understanding first, then separation, then change. Never all at once.

---

## 2. Cross-module changes

An API change in one place breaks contracts in others. You need to see the chain.

### Multi-session flow

#### Day 1 — a dependency map

**Goal:** find all consumers of the contract being changed.

**Prompt:**

```text
We plan to change the response format of /api/v1/orders.
Find all the places in the project that use this field.
For each place: file, function, how it's used. Don't change the code.
```

**Artifacts:**
- `docs/adr/ADR-012-orders-response-format.md` — why we're changing it, which modules are affected.
- A list of consumers with risk assessment.

#### Day 2 — adapters and tests

**Goal:** introduce the new format so the old consumers don't break.

**Prompt:**

```text
Add an adapter that accepts the new /api/v1/orders format
and exposes the old interface for modules X and Y.
Write tests for both formats.
```

**Artifacts:**
- `src/orders/adapter.py`.
- Compatibility tests.
- A session card: what we checked.

#### Day 3 — migrating the consumers

**Goal:** move one module to the new format.

**Prompt:**

```text
Migrate the module src/reports/ to the new orders response format.
Remove the adapter for this module if it's no longer needed.
Run the reports and orders tests.
```

**Artifacts:**
- An updated `src/reports/`.
- The ADR extended: migration status, what's left.
- Commit: `feat: migrate reports to new orders response format`.

**Rule:** a cross-module change isn't one PR. It's a chain of adapters and tests.

---

## 3. Several repositories / workspace

When 2–3 repos are in flight, context dissolves. The agent starts mixing up stacks, conventions, and boundaries.

### Multi-session flow

#### Day 1 — workspace context

**Goal:** record how the projects relate and what contracts exist between them.

**Prompt:**

```text
We have three repositories: project-a (API), project-b (frontend), project-c (worker).
Make a list of the contracts between them: endpoints, queues, shared schemas.
For each contract — where the source of truth is.
```

**Artifacts:**
- `workspace-context.md` one level above the repositories.
- An `AGENTS.md` in each project.

#### Day 2 — a change in project-a

**Goal:** make a change so that project-b and project-c learn about the risks.

**Prompt:**

```text
Before editing, check workspace-context.md.
We're changing the API response format in project-a. Which endpoints in project-b and project-c use it?
Don't write code, only a list of places and risks.
```

**Artifacts:**
- An updated `workspace-context.md` with a note about the change.
- A session card: who needs to be warned.

#### Day 3 — synchronization and PRs

**Goal:** prepare coordinated changes in project-b or project-c.

**Prompt:**

```text
In project-b we need to adapt the /orders call to the new format.
Use workspace-context.md and the ADR from project-a.
Don't change anything unrelated to this contract.
```

**Artifacts:**
- A PR in project-a with the ADR.
- A PR in project-b with the adaptation.
- A session card: the dependencies between PRs.

**Rule:** the projects shouldn't have to guess about each other inside the agent's head. Context lives in files.

**Example structure:**

```text
~/workspace/
  workspace-context.md
  project-a/
    AGENTS.md
  project-b/
    AGENTS.md
  project-c/
    AGENTS.md
```

---

## 4. A distributed team

People in different time zones. Sessions get interrupted. You need continuity.

### Multi-session flow

#### Day 1 — task and plan

**Goal:** record the task and plan so the next person continues without re-asking.

**Prompt:**

```text
We're starting a task: add rate limiting to the API.
First propose a plan in 3 stages. Each stage — a working state.
Write it into docs/tasks/rate-limiting-plan.md.
```

**Artifacts:**
- `docs/tasks/rate-limiting-plan.md`.
- `docs/adr/ADR-013-rate-limiting.md` — if the architecture is non-trivial.
- A session card: what's decided, who continues.

#### Day 2 — implementing the first stage

**Goal:** introduce a basic rate limiter without breaking the rest.

**Prompt:**

```text
Implement stage 1 from docs/tasks/rate-limiting-plan.md.
Use the project's AGENTS.md.
After the edit: tests, diff, update the plan — mark what's done.
```

**Artifacts:**
- Working code for the first stage.
- An updated plan.
- A session card: what works, what's blocking.

#### Day 3 — integration and a retro

**Goal:** close the task and leave a note for the team.

**Prompt:**

```text
Finish stage 3. Run the full test suite.
After that, write a short retro note in docs/retro/rate-limiting.md:
what worked, what could have been faster, what to hand off to the next shift.
```

**Artifacts:**
- The commit(s) for the task.
- A retro note.
- An updated `AGENTS.md`, if new rules appeared.

**Rule:** a shift ends not with code, but with a record. The next person starts from a file, not from questions.

---

## Multi-agent and orchestration

It's hard for one agent to hold the code, the architecture, and the review in its head at once. Split the roles between several agents or sessions.

**Roles:**
- **Architect** — discusses the approach and records the ADR.
- **Implementer** — writes code per the plan.
- **Reviewer** — checks the diff, catches problems.

`AGENTS.md` becomes the contract: it spells out who's responsible for what and which tools to use.

**A concrete stack example:**
- **Claude Code** as the architect — designs the approach, records the ADR.
- **Cursor** as the implementer — writes code per the plan.
- **Kimi Code** as the reviewer — checks the diff and catches problems.

**Example prompt for the reviewer:**

```text
Right now you are a strict reviewer.
Don't write code. Read this diff and find:
1) violations of minimal diff,
2) potential bugs,
3) deviations from the plan.
```

**Rule:** each agent holds one role. Don't ask the architect to fix typos, or the reviewer to design.

---

## An ADR template for recording decisions

When the architecture is non-trivial, record the decision. Use the template [`templates/ADR-template.md`](../../templates/ADR-template.md).

AI speeds up the mechanical work, but it doesn't cancel your responsibility for the architecture and the consequences.

---

## The senior view

> **Verdict:** on complex tasks you stop being a buyer of code and become the architect of a system.

Design with the agent, not through the agent. Ask it to generate options, find trade-offs, record an ADR — and only then move to code. Split the roles: one agent holds the architecture, another writes, a third reviews. These aren't extra mouths — they're different modes of attention that rarely fit in one session.

Context lives in files, not in the chat. `AGENTS.md`, `workspace-context.md`, and session cards are your long-term memory between projects and sessions. When switching between repositories, don't drag context along: close one session, open another, give links to the needed files.

More in [18-senior-playbook.md](18-senior-playbook.md).

---

Previous step: figure out how to avoid the creative traps — [10-antipatterns.md](10-antipatterns.md).

Next step: come back to the section you need right now — [03-principles.md](03-principles.md) or [06-prompt-patterns.md](06-prompt-patterns.md).
