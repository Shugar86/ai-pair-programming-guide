# 18. The senior playbook

🌐 **English** · [Русский](../18-senior-playbook.md)

You already know the basic loop: plan, code, tests, diff. At the senior or lead level the game shifts toward the system. The agent helps you design, orchestrate, remember, and verify. You stay responsible for the architecture and the decisions.

Previous step: complex scenarios and roles — in [11-advanced-scenarios.md](11-advanced-scenarios.md).

---

## 1. Designing with the agent

> **Verdict:** use the agent at the design stage, not just for writing code. Fixing architecture later costs more than an hour of dialogue.

The "architect + skeptic" pattern works like this: one agent or role proposes a solution, the other attacks it — looking for invariant violations, unhandled failure modes, hidden dependencies. These aren't two models, but two modes of thinking. You can switch roles in one session or run separate chats.

An ADR through dialogue is the endpoint of any non-trivial discussion. First the agents generate options and trade-offs, then you choose, then you record the decision in an ADR. Code is written after the ADR.

**Case 1. Designing a notifications service with the agent**

Steps:

1. **Set the task for the architect.** Describe the context, the constraints, and request options.
2. **Launch the skeptic.** Ask it to attack each option: failures, invariants, migrations.
3. **Choose an option.** The decision is yours, not the agent's.
4. **Record the ADR.** Write down the choice and the reasons using the template [templates/ADR-template.md](../../templates/ADR-template.md).

```text
You: We need a notifications service. Channels: email, push. There'll be new channels.
      Propose 3 architecture options with pros, cons, and trade-offs.
      After the discussion we'll record an ADR.

Architect agent:
Option A — a Strategy pattern inside the monolith. Pro: simple. Con: the channels are tied
to a single deploy.
Option B — a separate service with a queue. Pro: scales. Con: infrastructure.
Option C — a DB outbox + worker. Pro: delivery guarantee. Con: complexity.

Skeptic agent:
For option B: what happens when the queue goes down? How do you ensure idempotency?
How do you migrate existing users without double emails?
```

**Trade-offs:**

- Pro: architecture mistakes surface before the code, the decision is documented.
- Con: slower than writing code right away.
- When it applies: new services, cross-module changes, contract changes.

Connection to the basics: planning and simplicity principles — in [03-principles.md](03-principles.md).

---

## 2. Multi-agent setups

> **Verdict:** split the roles between agents. One agent shouldn't design, write, and review at the same time.

Clear roles:

- **Architect** — the map, the boundaries, the ADR, the invariants.
- **Implementer** — code per the plan, minimal diff.
- **Reviewer** — the diff, conformance to the plan, the risks.
- **Tester** — coverage, edge cases, rollbacks.

You can parallelize when the tasks don't overlap by file. We don't parallelize two implementers in one module — you'll get conflicts and lost context. You do the orchestration.

The contracts between agents are `AGENTS.md`, ADRs, and checklists. `AGENTS.md` spells out the stack, conventions, prohibitions, and responsibilities. An ADR — the choice of approach. A checklist — what counts as done.

**Case 2. Refactoring the billing module with three agents**

Steps:

1. **Assign the roles.** Architect, implementer, reviewer — each with its own zone.
2. **Fix the contracts.** `AGENTS.md`, an ADR, and an acceptance checklist — a common language for all agents.
3. **Run them in turn.** One agent's output becomes the next one's input.
4. **Check the diff with the reviewer.** Before accepting — a system check for conformance to the plan.

```text
Architect: Map out legacy_billing.py. Find the seams. Record an ADR:
           how to split the module and in what order.

Implementer: Move the tax calculation into a separate file per the ADR. One step — one
             responsibility. Show the diff before applying.

Reviewer: Review this diff. Find: violations of minimal diff, potential
          bugs, deviations from the ADR.
```

**Trade-offs:**

- Pro: depth of checking, less context "flooding."
- Con: the overhead of switching, you're the synchronization point.
- When it applies: changes of more than three files, cross-module edits, legacy.

More on roles and orchestration — in [11-advanced-scenarios.md](11-advanced-scenarios.md). Checklists — in [09-checklists.md](09-checklists.md).

---

## 3. Managing context between sessions

> **Verdict:** long-term memory lives in files, not in the chat. If the context is only in the message history — it's gone in a week.

`AGENTS.md` is the project's long-term memory: stack, conventions, decisions made, open questions. Session cards are brief notes on each significant session: what was done, where you stopped, what's blocking, what's next.

Handoff between Cursor, Kimi, Claude is done through files, not by copying the chat. You open a new session and give links: "start with `AGENTS.md` and `docs/sessions/2026-06-20.md`."

**Case 3. Returning to a project after a week**

Steps:

1. **Keep an `AGENTS.md`.** The project's long-term memory: stack, conventions, open questions. Template — [templates/AGENTS.md](../../templates/AGENTS.md).
2. **Write session cards.** Briefly record what was done, where you stopped, what's blocking. Template — [templates/session-template.md](../../templates/session-template.md).
3. **Start a new session from files.** Don't copy the chat history — give links to `AGENTS.md` and the latest card.
4. **Check the status before continuing.** Ask the agent to first describe the state, and only then propose the next step.

```text
You: We're continuing the task of extracting the price calculation.
     First read AGENTS.md and docs/sessions/2026-06-13.md.
     After that, tell me the state of the code and the next step.

Agent: Status: a PricingAdapter is created, 4 of 7 calls migrated.
        Blocker: the test legacy_pricing_test.py fails on discounts > 100%.
        Next step: migrate the remaining 3 calls and delete the old module.
```

**Trade-offs:**

- Pro: continuity between sessions and tools.
- Con: requires the discipline to keep the cards.
- When it applies: the project lives longer than one session or you work in several editors.

The `AGENTS.md` template — in [templates/AGENTS.md](../../templates/AGENTS.md). The session-card template — in [templates/session-template.md](../../templates/session-template.md).

---

## 4. Managing several projects

> **Verdict:** don't mix contexts in one session. Each project — its own `AGENTS.md`, each switch — a clean start.

`workspace/` or `docs/` becomes a single source of truth. One level above the projects, keep a `workspace-context.md`: how the projects relate, what contracts exist between them, where to commit, who's responsible.

Hot switching: you close the first project's session, open the second, feed it its `AGENTS.md`. Don't try to hold the stacks of two repos in one chat — the agent will start mixing up conventions.

**Example:** you fix a bug in project-a while the agent remembers project-b's contract.

```text
You: Before editing, read workspace-context.md.
     We're changing the API response format of /invoice in project-a.
     Which endpoints in project-b use this response?
     Don't write code, only a list of places and risks.

Agent: project-b calls /invoice in two places:
       - reports/sync.py: expects the field amount_cents.
       - billing/ui.ts: expects the string amount_formatted.
       Risk: both places break if the old field is removed without an adapter.
```

**Trade-offs:**

- Pro: you eliminate the mixing of stacks and conventions.
- Con: the cost of switching between sessions.
- When it applies: 2 or more projects active at once.

Basic separation and minimal-diff principles — in [03-principles.md](03-principles.md). On workspace — in [11-advanced-scenarios.md](11-advanced-scenarios.md).

---

## 5. Review at the system level

> **Verdict:** ask the agent to review the architecture, not just the code. Many bugs are born at module boundaries, not in lines.

A system review checks:

- Module boundaries: who's responsible for what, whether responsibilities leak.
- Contracts: data formats, APIs, invariants.
- Invariants: what must stay true under any changes.
- Rollbacks: what breaks if the feature is disabled or reverted.

A prompt for a system review:

```text
Don't write code. Read the ADR and the affected modules.
Find invariant violations, blurred module boundaries, and rollback risks.
For each problem, give the file, the line, and why it's dangerous.
```

**Example:** a new "flexible discounts" feature adds a discount that can exceed the order amount.

```text
Agent: In orders/total.py it isn't checked that the total ≥ 0.
       If discount > amount, we get a negative sum.
       This violates the "order.total >= 0" invariant recorded in docs/invariants.md.
       Fix: either cap the discount, or reset total to 0.
```

**Trade-offs:**

- Pro: catches whole classes of errors invisible at the line level.
- Con: takes more time than a code review.
- When it applies: cross-module features, contract changes, new invariants.

The lead/reviewer checklist — in [09-checklists.md](09-checklists.md).

---

## 6. Refactoring legacy under control

> **Verdict:** don't rewrite legacy in one commit. Map, seams, adapters, gradual migration — that's the path of minimal risk.

The four-step strategy:

1. **Map.** The agent describes what the module does, who calls it, where the hidden dependencies are.
2. **Seams.** You find places where the code can be split with minimal risk — clear inputs and outputs.
3. **Adapters.** You introduce adapters that let the old and new code coexist.
4. **Gradual migration.** You switch calls one at a time, with tests after each step.

The agent is good at mechanical operations: moving functions, renaming, replacing types. Architecture decisions are yours: where the boundary is, in what order to migrate, when to delete the old code.

**Example:** extracting the price calculation from the monolith.

```text
You: Map out pricing_legacy.py. Find all calls to calculate_price.
     Propose an order for extracting it into a separate service via an adapter.

Agent: calculate_price is called from 7 places. 4 — in orders, 2 — in reports, 1 — in admin.
        Seam: the function depends only on product_id, qty, and discount.
        Plan:
        1. Create a PricingAdapter with the same interface.
        2. Migrate orders/*, check the tests.
        3. Migrate reports/*, admin/*.
        4. Delete the legacy function.
```

**Trade-offs:**

- Pro: each stage is deployable and reversible, no big bang.
- Con: longer than rewriting "from scratch."
- When it applies: a working system, you can't pause development, you don't fully understand all edge cases.

On legacy refactoring — in [11-advanced-scenarios.md](11-advanced-scenarios.md). The minimal-diff and plan-before-code principles — in [03-principles.md](03-principles.md).

---

## 7. Assessing the quality of the agent's output

> **Verdict:** "looks OK" isn't a criterion. Assess the output by metrics and conformance to the plan.

Criteria:

- **Tests.** Do they all pass? Do they cover the changed paths? Did coverage drop?
- **Diff complexity.** How many files are touched compared to the plan? Are there changes outside the task?
- **Conformance to the plan.** Was what was agreed done, or did the agent drift?
- **Hallucinations.** Did non-existent APIs, imports, dependencies, or settings appear?

You accept an edit only if the metrics are fine. If not — you send it back with a concrete note on what's wrong.

**Example:** the agent proposed 5 files to fix email validation.

```text
You check:
- Tests: 12/12 pass, 3 edge-case tests added.
- Diff: 2 of 5 files changed. The rest — formatting and renames.
- Plan: email validation in the registration form, all on point.
- Hallucinations: the import utils/email.py exists, no new dependencies.

Verdict: you return the agent to the two needed files and ask it to remove the cosmetic changes.
```

**Trade-offs:**

- Pro: an objective acceptance criterion, fewer regressions.
- Con: slows down accepting changes.
- When it applies: any non-trivial edit, especially in shared code.

Acceptance checklists — in [09-checklists.md](09-checklists.md). The "check everything" principle — in [03-principles.md](03-principles.md).

---

## 8. When not to use agents

> **Verdict:** the agent isn't a replacement for your judgment. In an unknown domain, without data, and where responsibility can't be transferred, you make the decision yourself.

Three stop signals:

1. **Researching an unknown domain.** The agent can generate a confident but wrong plan. You won't tell it from the truth until you understand it yourself.
2. **Critical architecture decisions without data.** Without metrics, load, budget, and team expertise, any architecture is a guess.
3. **Responsibility can't be transferred.** If the result affects security, legal obligations, or the fate of the product — the decision stays with a human.

**Example:** the agent proposes switching the database from PostgreSQL to MongoDB.

```text
Agent: PostgreSQL scales poorly, better to move to MongoDB.

You: Stop. We have no load data, no team expertise, no migration plan,
     and no risk assessment. This is an architecture decision, not a task for an agent.
     First we'll gather metrics and make an ADR.
```

**Trade-offs:**

- Pro: you avoid expensive mistakes and the illusion of control.
- Con: slower than delegating everything to the agent.
- When it applies: high stakes, lack of data, a decision that can't be easily rolled back.

On traps and anti-patterns — in [10-antipatterns.md](10-antipatterns.md). On escalating uncertainty — in [03-principles.md](03-principles.md).

---

## A checklist for the lead

When you introduce AI into the team's work, check yourself against this list.

### When to introduce AI rules

- [ ] The team already uses agents chaotically: everyone has their own style and arrangements.
- [ ] Typical mistakes appear: extra diff, tests not run, lost context.
- [ ] A new person spends more than a week onboarding because of implicit conventions.
- [ ] The lead drowns in manual review of agent code.

If you checked at least two — it's time to fix the rules in [`AGENTS.md`](../../templates/AGENTS.md) and checklists.

### How to run an AI-usage retro

1. **Gather facts.** Time from task to PR, number of rollbacks, review complaints, hallucination cases.
2. **Discuss patterns.** What repeats? Where did the agent help, and where did it harm?
3. **Update the rules.** Add prohibitions, refine prompt templates, fix `AGENTS.md`.
4. **Record the decisions.** New rules should be written down, not just spoken.

Run the retro at least once a month for the first six months, then — on signals.

### Which metrics to watch

- **Time from task to PR.** Is it rising or falling after introducing the agent?
- **Share of rollbacks and bugs after agent edits.** Regressions shouldn't grow.
- **Review load.** How much time does the lead spend checking the agent's diff?
- **Test coverage of changed paths.** The agent writes code, but tests are part of acceptance.
- **Number of hallucinations.** Do non-existent APIs, dependencies, or settings appear?

More on metrics and the retro format — in [20-metrics-and-retro.md](20-metrics-and-retro.md).

---

Next step: how the senior and lead role will change going forward — in [17-future.md](17-future.md).
