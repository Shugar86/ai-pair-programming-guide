# 09. Checklists as pre-flight checks

🌐 **English** · [Русский](../09-checklists.md)

These checklists aren't rules you must obey. They're quick pre-flight checks. Run through the items — and take off.

> **Verdict:** a checklist saves you effort, it doesn't add work.

---

<a id="before-session"></a>

## Before a session

Check that you're ready for the dialogue. If even one item in the minimal set fails — narrow the task.

### Minimal set

- [ ] The task is stated in one sentence.
- [ ] It's clear why it's needed and what changes afterward.
- [ ] I know how to verify the result: tests, a manual scenario, or both.
- [ ] In this session I'm solving no more than one task.
- [ ] The git branch is clean, or I know where to commit.

### Extended set

- [ ] `AGENTS.md` and the README are up to date.
- [ ] There's context from the previous session: a session card or notes.
- [ ] The done criterion is defined: what exactly counts as the end of the task.
- [ ] It's clear who will accept or review the result.
- [ ] Risks and sensitive data are accounted for — see [19-security-and-policy.md](19-security-and-policy.md).
- [ ] There's a plan B if the agent drifts: revert, narrow scope, a new prompt.

**If it fails:** go back to [03-principles.md](03-principles.md), the "Why first — then how" section.

---

<a id="before-accept"></a>

## Before accepting a diff

Don't hit Accept until you've looked at the diff. This is your safety net.

### Minimal set

- [ ] I read the whole diff, not just the first files.
- [ ] Every change relates to the current task.
- [ ] There's no code "for the future."
- [ ] Variable and function names speak for themselves.
- [ ] No hardcoded secrets, passwords, or tokens.

### Extended set

- [ ] I understand why the agent did it this way.
- [ ] Public contracts, APIs, and invariants weren't changed without an explicit request.
- [ ] The relevant tests, linter, and type check were run.
- [ ] New dependencies are agreed and needed right now.
- [ ] Obvious edge cases and rollback paths are considered.
- [ ] I can explain every change out loud.

**If it fails:** ask the agent to explain a line, or revert the changes.

---

<a id="before-commit"></a>

## Before a commit / PR

A commit is a save point. Make sure only what's needed got into it.

### Minimal set

- [ ] Tests pass, or there's a note on why there are none.
- [ ] The linter and formatter don't complain.
- [ ] The commit message describes the gist, not just "edits."
- [ ] `.env`, keys, and local IDE settings didn't get into the commit.
- [ ] The diff matches the commit message.

### Extended set

- [ ] The manual scenario is checked: the feature works not only in theory.
- [ ] Docs and comments are updated if a contract changed.
- [ ] The commit is small: 1–3 logically related files.
- [ ] CI is green, or it's explained why that's fine.
- [ ] A reviewer is assigned, or a self-review was done.
- [ ] Reverting the commit is safe: no destructive migrations or one-way contracts.

**A good message:** `feat: add phone field to registration form`.  
**A bad message:** `fix`.

---

<a id="lead-review"></a>

## For a lead / reviewer

At the team level it matters to look not only at the lines, but at how the solution fits the system.

### Minimal set

- [ ] The task fits the current architecture and ADRs.
- [ ] Contracts, APIs, and invariants aren't violated.
- [ ] The solution isn't overloaded: no extra abstractions or code "for later."
- [ ] There's a testing and rollout plan.
- [ ] Rollback risks and side effects are considered.

### Extended set

- [ ] A system review was done: module boundaries, invariants, rollbacks.
- [ ] Cross-team dependencies and inter-service contracts are checked.
- [ ] Metrics, monitoring, and logging are accounted for.
- [ ] The solution complies with the internal AI policy and security requirements.
- [ ] `AGENTS.md` or an ADR is updated if new conventions appeared.
- [ ] A retro note is added: what worked, what to improve.

---

<a id="stop-signals"></a>

## 🚩 Stop signals — a reason to pause and reassemble

If you notice any of these — don't continue at the same pace. Stop, revert, or rephrase the task.

- [ ] The diff suddenly has dozens of files instead of 1–2.
- [ ] Calls to functions or methods appeared that don't exist in the project or library.
- [ ] The agent changes function contracts without an explicit request.
- [ ] There's a lot of "for the future" code with no link to the task.
- [ ] Tests weren't run after the changes.
- [ ] I can't explain myself what happened in the commit.

What to do: revert to a clean branch, narrow the task, and start with a new plan. More on traps — in [10-antipatterns.md](10-antipatterns.md).

---

Previous step: lock in the theory with practice — [08-exercises.md](08-exercises.md).

Next step: figure out which creative traps most often lead to these stop signals — [10-antipatterns.md](10-antipatterns.md).
