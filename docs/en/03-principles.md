# 03. Principles as creative constraints

🌐 **English** · [Русский](../03-principles.md)

Principles aren't a report card. They're the boundaries that make it easier to move. Every constraint frees you from unnecessary decisions and keeps the agent in focus.

These constraints follow from the agent's role as a partner — see [02-agent-as-pair-programmer.md](02-agent-as-pair-programmer.md).

> **Verdict:** the clearer the boundaries, the bolder the creativity.

They work in Cursor, Kimi Code, Claude Code, OpenCode, Copilot, Cody — anywhere you hold a dialogue with an agent. Below are the eight constraints that turn chaos into a session.

All eight in one line: **KISS**, **minimal diff**, **YAGNI**, **plan first — then code**, **why first — then how**, **verdict first — then details**, **check everything**, **escalate uncertainty**.

---

## 1. KISS — look for simplicity first

**Constraint:** the first solution must be the simple one.

Agents love to build. Sometimes too much. You set the boundary: first a version without factories, interfaces, and configs.

**What it gives you creatively:** you quickly see whether the idea works or not. You add complexity deliberately, once simplicity has proven itself.

**Scenario:**

```text
You:   Add sorting of orders by date.
Agent: I'll create an abstract OrderSorterStrategy with two implementations...
You:   Stop. First a single helper that sorts the list by the date field. No strategies.
Agent: OK, one helper.
```

**Prompt:**

```text
Make the simplest solution that works.
No abstractions that aren't needed right now.
```

This simplicity protects the "minimum" step in [04-workflow.md](04-workflow.md).

---

## 2. Minimal diff — touch only what's needed

**Constraint:** one task — one change. No more.

If neighboring files end up in the diff, review turns into an investigation. The boundary helps the agent stay in its lane.

**What it gives you creatively:** you can experiment without fear. A small diff is easy to revert and rewrite.

**Scenario:**

```text
You: [looks at the diff] You changed 8 files, though I only asked you to fix email validation.
     Remove everything not related to email.
Agent: Removed. Two files left.
```

**Prompt:**

```text
Change only what relates to the task.
Show the diff before applying.
```

Check yourself against the checklist in [09-checklists.md](09-checklists.md) before you hit Accept.

---

## 3. YAGNI — don't cook "for later"

**Constraint:** code appears only for the current task.

"It might come in handy" is the main source of dead code. The boundary stops you from laying a foundation for a house no one ordered.

**What it gives you creatively:** you don't drag along a load of unneeded entities. The space for the next idea stays clean.

**Scenario:**

```text
Agent: I added configuration via YAML so that later we could...
You:   We're not doing configuration now. Remove the YAML and hardcode the value.
       When it's needed — as a separate task.
```

**Prompt:**

```text
Is this needed right now?
If not — remove it, don't leave it for the future.
```

---

## 4. Plan first — then code

**Constraint:** no code is written until there's an agreed plan.

A plan is cheaper than code. Reworking a plan — 30 seconds. Reworking code — 30 minutes.

**What it gives you creatively:** you can discuss several directions without paying for each one with an implementation.

**Scenario:**

```text
You:   I want token-based auth.
Agent: Starting to write middleware...
You:   Stop. First a plan: where we store the token, how we refresh it, where we check it. Three steps.
       Code after we agree.
```

**Prompt:**

```text
Before code, propose a 3-step plan.
Don't write code until we agree on the approach.
```

How this fits into a session — see [04-workflow.md](04-workflow.md).

---

## 5. Why first — then how

**Constraint:** the problem and value first, the technical options after.

Beautiful code with no task is just beautiful code. The boundary forces you to talk about the stake before the brackets.

**What it gives you creatively:** you don't get lost in formatting arguments before it's clear what should even come out.

**Scenario:**

```text
Agent: Redux looks like a fit.
You:   And what problem are we solving? Maybe plain component state is enough?
Agent: We need to sync filters between two pages.
You:   OK, then Redux is fine.
```

**Prompt:**

```text
First explain what problem we're solving and why it matters to the user.
Then propose implementation options.
```

---

## 6. Verdict first — then details

**Constraint:** the gist in the first sentence, details after.

Agents can write a lot. You specify: the answer first, the justification after.

**What it gives you creatively:** you quickly understand whether it's worth digging deeper. If the verdict isn't right — you change course immediately.

**Scenario:**

```text
You:   Should we use a cache here?
Agent: [3 paragraphs about Redis, TTL, invalidation]
You:   First one clear answer: yes or no, and why. Then the details.
```

**Prompt:**

```text
First a short verdict in one sentence.
Then the explanation and alternatives.
If you're not sure, say so.
```

---

## 7. Check everything

**Constraint:** the diff and the tests are part of the creative act, not bureaucracy.

The agent confidently generates almost-correct code. "Almost" is not "correct."

**What it gives you creatively:** you can take risks with ideas because you have fast feedback. Every check is a chance to improve the result.

**Scenario:**

```text
You:   Accepted the changes, ran the tests. 3 of 12 fail.
Agent: Strange, it all worked for me.
You:   Show which tests you ran. And check the diff again — I see an extra argument in the function.
```

**Prompt:**

```text
First show the diff.
Then run the tests and report the result.
If something fails — explain why and propose a fix.
```

**Anti-example:**

```text
You:   Accept.
Agent: Great.
You:   [didn't read the diff and didn't run the tests]
```

See [10-antipatterns.md](10-antipatterns.md).

A verification checklist is in [09-checklists.md](09-checklists.md).

---

## 8. Escalate uncertainty

**Constraint:** if you're not sure — ask. No guessing.

A 10-second question saves 2 hours of rework. The agent rarely says "I don't know" on its own. The initiative is on you.

**What it gives you creatively:** you don't hit a dead end over a misunderstood direction. Doubts become decision points, not mistakes.

**Scenario:**

```text
Agent: I handled errors via middleware.
You:   I'm not sure middleware fits here. Explain why not in the controller,
       and propose a simpler option.
```

**Prompt:**

```text
If anything is ambiguous — ask again.
Don't make assumptions about the task.
```

**Anti-example:**

```text
You:   Just do it somehow.
Agent: [makes an assumption and drags in the wrong architecture]
```

See [10-antipatterns.md](10-antipatterns.md).

---

## Principle → where it shows up in the loop

| Principle | Loop steps |
| :-- | :-- |
| KISS | 3. Build the minimum |
| Minimal diff | 3. Build the minimum, 4. Test by feel |
| YAGNI | 3. Build the minimum |
| Plan first — then code | 2. Sketch the path |
| Why first — then how | 1. Capture the idea, 2. Sketch the path |
| Verdict first — then details | 1. Capture the idea, 2. Sketch the path, 6. Look at what came out |
| Check everything | 4. Test by feel |
| Escalate uncertainty | At every step, especially 1–3 |

Next step: see how these constraints become a working loop — [04-workflow.md](04-workflow.md).
