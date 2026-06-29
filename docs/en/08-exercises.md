# 08. Exercises as mini-projects

🌐 **English** · [Русский](../08-exercises.md)

Each exercise is a small project with a measurable result. You don't just read the rules — you test them on your own code.

> **Verdict:** theory only sticks through your hands.

---

## Level: Beginner

### Exercise 1. Minimal diff

**Level:** beginner.  
**Connection:** the "Minimal diff" principle from [03-principles.md](03-principles.md), the "Build the minimum" step from [04-workflow.md](04-workflow.md), the ["Make it pretty"](10-antipatterns.md) trap from [10-antipatterns.md](10-antipatterns.md).

**Task:** add a "Phone" field to the registration form and save it to the database.

**What to do:**
1. Ask the agent to make the change.
2. Read the diff before hitting Accept.
3. If the agent grabbed extra files — revert and ask it to do only what's needed.

**Expected outcome:** the agent makes exactly one change in one file; you read the diff before accepting and revert everything that went beyond the task. The result — a habit of keeping a session inside one logical edit.

**Success criterion:** exactly one file and one logical edit in the diff. Everything else is a separate task.

**Dialogue:**

```text
You: Add a phone field to the registration form.
Agent: [changes the form, the model, the migration, the tests]
You: Stop. The form and the model only first. The migration and tests — as a separate step.
```

---

### Exercise 2. Plan before code

**Level:** beginner.  
**Connection:** the "Plan first — then code" principle from [03-principles.md](03-principles.md), the "Sketch the path" step from [04-workflow.md](04-workflow.md), the ["Swapping the task's goal"](10-antipatterns.md) trap from [10-antipatterns.md](10-antipatterns.md).

**Task:** add a feedback form to the contacts page.

**What to do:**
1. Forbid the agent from writing code until you agree on a plan.
2. Agree on a plan of 4–5 steps.
3. Implement only the first step.

**Expected outcome:** before the first line of code you have an agreed 3–5 step plan, and in the repo — one working commit for the first step only. The result — the reflex "don't code blind."

**Success criterion:** a written plan and one working commit. The plan lives in the session or in `docs/session-notes.md`.

**Dialogue:**

```text
You: I want a feedback form. First a 5-step plan. I don't allow writing code.
Agent: 1) add an endpoint, 2) add validation, 3) send email, 4) UI, 5) tests.
You: Start with the endpoint and validation. The rest — later commits.
```

---

## Level: Practitioner

### Exercise 3. Review your own diff

**Level:** practitioner.  
**Connection:** the "Check everything" principle from [03-principles.md](03-principles.md), the "Test by feel" step from [04-workflow.md](04-workflow.md), the ["Blind trust"](10-antipatterns.md) trap from [10-antipatterns.md](10-antipatterns.md).

**Task:** find the last commit in your project made with an agent.

**What to do:**
1. Open the commit's diff.
2. Find 3 things that could be done better: extra code, a strange name, missing tests.
3. Create a follow-up commit with the fixes.

**Expected outcome:** after the agent's commit you find 3 concrete improvements and make a follow-up commit yourself. The result — your own review as a natural step of the loop, not a formality.

**Success criterion:** three concrete remarks and one follow-up commit.

**Example remarks:**

```text
- The variable name data says nothing.
- The function does two things: validation and saving.
- There's no test for an empty email.
```

---

### Exercise 4. Write AGENTS.md

**Level:** practitioner.  
**Connection:** the "Escalate uncertainty" principle from [03-principles.md](03-principles.md), the "Look at what came out" step from [04-workflow.md](04-workflow.md), the ["A dialogue without project context"](10-antipatterns.md) trap from [10-antipatterns.md](10-antipatterns.md).

**Task:** create an `AGENTS.md` for your project.

**What to do:**
1. Take the template from [`templates/AGENTS.md`](../../templates/AGENTS.md).
2. Fill in: language, stack, commit rules, prohibitions.
3. Run one session with the agent following this contract.
4. After the session, add one remark: what was missing in `AGENTS.md`.

**Expected outcome:** the repo gets a living contract that one real session runs against; afterward one clarification is added. The result — the ability to grow the project's long-term memory instead of copying context into the chat.

**Success criterion:** an `AGENTS.md` file in the repo, one commit following its rules, and one edit to `AGENTS.md` based on the outcome.

---

## Level: Senior / Lead

### Exercise 5. Design a module with multi-agent

**Level:** senior/lead.  
**Connection:** the "Why first — then how" principle from [03-principles.md](03-principles.md), the "Capture the idea" step from [04-workflow.md](04-workflow.md), the ["Swapping the task's goal"](10-antipatterns.md) trap from [10-antipatterns.md](10-antipatterns.md).

**Task:** design a small module — say, a notifications service or a payment handler — using two agents. One agent plays the architect, the other the skeptic.

**What to do:**
1. Ask the first agent to propose 2–3 architecture options with pros and cons.
2. Pass those options to the second agent and ask it to find the weak spots.
3. Choose an approach and record it in an ADR using the template [`templates/ADR-template.md`](../../templates/ADR-template.md).
4. Only then allow writing code.

**Expected outcome:** before code, an ADR is recorded with the chosen approach, the risks, and the trade-offs; the first implementation is limited to a minimal skeleton. The result — architectural discipline instead of impulsive code.

**Success criterion:** an ADR with the chosen approach and reasoning, and one commit with a minimal implementation.

**Dialogue:**

```text
You (to the architect): Propose 3 options for a notifications service: email, push, future channels.
Agent 1: Option A — separate handlers. Option B — a queue. Option C — a pipeline.
You (to the skeptic): Here are 3 options. Where's the catch in each?
Agent 2: A scales poorly. B adds infrastructure. C is over-engineered for the start.
You: I choose A. Recording it in an ADR. Code — only the basic handler in the next commit.
```

---

## How to use it in a team

The exercises work not only solo. They're handy to run in a workshop to align the team's style of working with an agent.

**Format:** 1–2 hours, 2–3 exercises, a retro at the end.

**Roles:**
- Facilitator — usually the lead or the most experienced person on the team. Sets the pace, shows the diff on screen, ties things back to the checklists.
- Participants — work in "human + agent" pairs in their own editor.

**Order:**
1. **Warm-up — 15 min.** Everyone goes through [Exercise 1](#exercise-1-minimal-diff) on a shared test project. The goal — show how to read a diff before accepting.
2. **Main block — 40–60 min.** Each person picks an exercise at their level: beginners — [Exercise 2](#exercise-2-plan-before-code), practitioners — [Exercise 3](#exercise-3-review-your-own-diff) or [4](#exercise-4-write-agentsmd), seniors — [Exercise 5](#exercise-5-design-a-module-with-multi-agent).
3. **Retro — 15–20 min.** Discuss three questions:
   - What worked right away?
   - Where did the diff or plan drift off?
   - What do we add to `AGENTS.md` or the team checklists?

**Materials:** keep [09-checklists.md](09-checklists.md) and [10-antipatterns.md](10-antipatterns.md) on screen — when someone's session gets stuck, tie them to a specific item or trap.

**Workshop outcome:** everyone leaves with one concrete change to their workflow: one starts reading diffs, another starts writing a plan before code, another starts keeping an `AGENTS.md`.

---

## What's next

After doing the exercises, return to [03-principles.md](03-principles.md). Note which principles already come automatically and which still need work.

If you want to check yourself before each session — use the checklists in [09-checklists.md](09-checklists.md).
