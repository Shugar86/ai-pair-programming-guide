# 04. The creative loop

🌐 **English** · [Русский](../04-workflow.md)

Working with an agent isn't a ritual. It's prototyping: idea, plan, minimum, check, reflection. Six steps that repeat until the thing is done.

> **Verdict:** every cycle should produce something tangible.

---

## The diagram

![The creative loop diagram](../../assets/workflow.svg)

*Steps: 1. Capture the idea → 2. Sketch the path → 3. Build the minimum → 4. Test by feel → 5. Lock it in → 6. Look at what came out.*

## Step 1. Capture the idea

State the task in one sentence. If you can't — the idea is too big, break it up.

- ✅ "Add sorting of orders by date in the user dashboard"
- ❌ "Make the dashboard nicer"

A good idea sounds like a result you can touch.

---

## Step 2. Sketch the path

Don't write code until you've agreed on a plan. The plan is your sketch.

Example prompt:

```text
I want to add sorting of orders by date in the user dashboard.
First propose a plan in 3-5 steps. No code.
```

If the plan balloons — narrow it:

```text
The plan looks overloaded.
Propose a simpler option in 3 steps, with no new architecture.
```

Planning leans directly on the principles in [03-principles.md](03-principles.md).

---

## Step 3. Build the minimum

The agent writes. You watch: few files, a simple solution, no code for later.

If the agent brings a big chunk — break it up:

```text
This is too big a step.
Backend first: repository + controller. Don't touch the UI.
```

---

## Step 4. Test by feel

Three checks:

1. **Tests.** Run the relevant ones. If there are none — check by hand.
2. **Diff.** Read what changed.
3. **Common sense.** Does this solve the task? Are there side effects?

After the tests, ask the agent to walk through a checklist itself:

```text
Review the change:
1) are all code branches covered,
2) what are the obvious edge cases,
3) are any extra files touched.
```

**Technical checklist:**

```bash
# Tests
npm test          # or pytest, cargo test, go test

# Linter
npm run lint      # or ruff, eslint, golangci-lint

# Types
npm run typecheck # or mypy, tsc, cargo check
```

Use the project's commands. If there are none — add them before the agent does.

A diff-acceptance checklist is in [09-checklists.md#before-accepting-a-diff](09-checklists.md#before-accepting-a-diff).

---

## Step 5. Lock it in

A commit isn't a formality. It's a save point for a creative experiment.

```bash
git add src/orders/service.py
git commit -m "feat: sort orders by date in profile"
```

The message answers the question "what changed?"

---

## Step 6. Look at what came out

Reflection isn't an essay. Two or three lines that will help the next session.

Ask yourself:

1. What worked?
2. What could have been done faster?
3. What to fix next time?

Example:

```text
+ The 4-step plan was clear.
- Spotted an extra logger in the diff too late.
→ Next time: diff first, then tests.
```

---

## A smooth, successful session

```text
You:   Add sorting of orders by date in the user dashboard.
Agent: Plan: 1) a sort param in the query, 2) a sort helper, 3) a UI button.
You:   Start with the backend. UI later.
Agent: [writes the helper and endpoint]
You:   [looks at the diff] OK, running the tests.
You:   Tests passed. Add the button to the UI.
Agent: [writes the button]
You:   [checks by hand] Works. Commit.
```

Everything's smooth: a clear idea, a short plan, a minimum scoped to the backend, a check with no surprises.

## A bad session → restart by the rules

```text
You:   I need to export orders to CSV from the dashboard.
Agent: Plan: 1) add an endpoint /orders/export, 2) use pandas to generate the CSV,
        3) a UI button.
You:   pandas is an unnecessary dependency for one CSV. Propose an option without pandas.
Agent: OK, I'll use the standard csv module. 1) endpoint, 2) generation via csv.writer,
        3) button.
You:   Start with the backend. UI later.
Agent: [writes the endpoint and service]
You:   [looks at the diff] Here you added writing the file to disk. We need a streaming response,
      not a file.
Agent: [reworks it into a StreamingResponse]
You:   [runs the tests] 1 test fails: the Content-Disposition header is missing.
Agent: [adds the header]
You:   [checks by hand] Works.
You:   git commit -m "feat: export orders to CSV"
```

What happened here: the idea was clear, the plan was trimmed, the minimum was scoped to the backend, and the dead end with the file was resolved by clarifying the response format.

---

Next step: learn how this loop works in a specific editor — [05-environments.md](05-environments.md).

If something went wrong — go back to the principles in [03-principles.md](03-principles.md).
