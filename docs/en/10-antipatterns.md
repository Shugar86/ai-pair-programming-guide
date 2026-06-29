# 10. Anti-patterns as creative traps

🌐 **English** · [Русский](../10-antipatterns.md)

When you create fast, it's easy to fall into one of these traps. They don't mean you work badly. They mean speed outran focus.

> **Verdict:** a trap isn't a verdict. Recognize it by the symptom, pull out by the rule.

---

## Map of traps

| Trap | Symptom | Short counter-measure |
| :-- | :-- | :-- |
| ["Make it pretty" without boundaries](#1-make-it-pretty-without-boundaries) | Dozens of files in the diff, half unrelated to the task | One sentence + explicit boundaries + plan before code |
| [Invisible changes](#2-invisible-changes) | The agent quietly changes types, signatures, or contracts | The whole diff, ask about contracts, tests after each step |
| [API and SDK hallucinations](#3-api-and-sdk-hallucinations) | Methods/flags appear that don't exist in the version used | Check the docs, specify the version, agree on dependencies |
| [Swapping the task's goal](#4-swapping-the-tasks-goal) | A simple script turns into a mini-framework | Success criteria, YAGNI, the "is this needed now?" question |
| [Pseudo-refactoring for its own sake](#5-pseudo-refactoring-for-its-own-sake) | Noisy renames with no architecture improvement | Separate features and refactoring, use a linter |
| [Ignoring tests and tooling](#6-ignoring-tests-and-tooling) | Code without running tests, types, the linter | Require green checks before accept |
| [A dialogue without project context](#7-a-dialogue-without-project-context) | A "tutorial-style" solution that doesn't fit the project | `AGENTS.md`, README, examples from the project |
| [Blind trust](#8-blind-trust) | Accept all without reading the diff | Read the diff, don't commit what you don't understand |

---

## 1. "Make it pretty" without boundaries

**Symptom:** the task sounds vague, the agent stages a mass refactoring across the whole repo.

**What breaks:** dozens of files in the diff, half unrelated to the task, tests fail, behavior changes where you didn't ask.

**Where it's caught early:**
- The KISS, minimal-diff, and YAGNI principles — in [03-principles.md](03-principles.md).
- The "Sketch the path" and "Build the minimum" steps — in [04-workflow.md](04-workflow.md).
- The before-session and before-accept checklists — in [09-checklists.md](09-checklists.md).

**How to catch it:**
- State the task in one sentence.
- Add explicit boundaries: "this file only," "don't touch the UI," "don't change the architecture."
- Ask for a plan before code and agree on scope.

**Example prompt:**

```text
Clean up the code only in the file src/orders/service.py.
Don't change public contracts and don't touch other modules.
First show a 3-step plan.
```

---

## 2. Invisible changes

**Symptom:** the agent quietly edits types, function signatures, API contracts, or domain-model invariants.

**What breaks:** the code compiles, but the logic drifts. Errors surface later, when you no longer remember what changed.

**How to catch it:**
- Read the whole diff, not just what the agent highlighted.
- Ask it to explain which contracts changed, before applying.
- Run the tests after each step.

**Dialogue:**

```text
Agent: Done. createUser now takes an additional options object and returns a Result instead of a User.
You:   We didn't agree to a contract change. You changed the signature and return type silently.
Agent: It was needed for the new validation.
You:   Revert the public contract. Do the validation internally, without breaking callers.
```

**Example prompt:**

```text
Before applying the edits, list all public signatures, API contracts, and invariants that changed.
If a contract changed without my explicit request — revert it and agree first.
```

---

## 3. API and SDK hallucinations

**Symptom:** methods, flags, or libraries appear in the code that don't exist in the version being used.

**What breaks:** the build fails, and if it doesn't — the runtime fails in production.

**Where it's caught early:**
- The "Check everything" principle — in [03-principles.md](03-principles.md).
- The "Test by feel" step — in [04-workflow.md](04-workflow.md).
- The extended before-accept checklist — in [09-checklists.md](09-checklists.md).

**How to catch it:**
- Check any unfamiliar method against the official docs.
- Specify the library version in the prompt.
- Don't let the agent add new dependencies without agreement.

**Example prompt:**

```text
Use only methods from Django 4.2 documented in the official docs.
If you need a method that isn't in this version — say so.
```

---

## 4. Swapping the task's goal

**Symptom:** instead of a simple script, a mini-framework with configs, plugins, and abstractions suddenly emerges.

**What breaks:** the solution is overloaded, hard to maintain, and the original task is over-solved.

**How to catch it:**
- Fix the success criteria: "what should work after this commit?"
- Ask: "is this needed for the current task?"
- Use YAGNI as a shield.

**Dialogue:**

```text
Agent: I added a plugin system for error handling.
You:   We need only one 404 handler. Remove the plugins, make a single handler.
```

**Example prompt:**

```text
We need only one 404 handler. Remove the plugin system and make a single handler.
```

---

## 5. Pseudo-refactoring for its own sake

**Symptom:** the agent renames variables, reorders imports, and changes formatting without improving the architecture.

**What breaks:** the diff is noisy, review turns into hell, the commit history loses meaning.

**How to catch it:**
- Separate refactoring and features into different commits.
- Ask the agent not to change style if the task isn't about that.
- Use a linter/formatter so style isn't up for debate.

**Example prompt:**

```text
Don't rename variables and don't change formatting.
Only structural changes for the current task.
```

---

## 6. Ignoring tests and tooling

**Symptom:** the agent writes code but doesn't run the tests, check types, or look at the linter.

**What breaks:** the code "looks OK," but doesn't work or doesn't pass CI.

**How to catch it:**
- Always ask it to run the relevant tests.
- Check the CI/linter output before committing.
- Don't accept changes if you haven't seen green checks.

**Example prompt:**

```text
After the changes, run the tests for the orders module.
If they fail — explain the cause and propose a fix. Don't ask me to check blind.
```

---

## 7. A dialogue without project context

**Symptom:** you paste chunks of code into the chat without explaining the architecture, and get a solution that doesn't fit the project.

**What breaks:** the agent proposes "tutorial-style," not "the way your team does it."

**How to catch it:**
- Give the agent [`AGENTS.md`](../../templates/AGENTS.md), the README, and the project structure.
- Point out existing conventions: "for this we use the service layer."
- Show examples of similar code from the project.

**Dialogue:**

```text
You:   Our validation goes through the service layer, not the serializer.
Agent: Got it. I'll move the logic to services/validation.py.
```

**Example prompt:**

```text
Our validation goes through the service layer, not the serializer.
Move the logic to services/validation.py, without changing the project's approach.
```

---

## 8. Blind trust

**Symptom:** you hit "Accept all" without reading the diff, because "the agent's smart, right?"

**What breaks:** anything at all gets into the code: bugs, vulnerabilities, extra dependencies, changes you didn't ask for.

**Where it's caught early:**
- The "Check everything" principle — in [03-principles.md](03-principles.md).
- The "Test by feel" step — in [04-workflow.md](04-workflow.md).
- The before-accept checklist — in [09-checklists.md](09-checklists.md).

**How to catch it:**
- Read the diff before every accept.
- Set a rule: "I don't commit what I don't understand."
- Use `git diff` and revert if something's off.

**Dialogue:**

```text
You:   [hits Accept all without reading the diff] I accepted everything.
Agent: The diff had 12 files, including removing the validation and a new dependency.
You:   From now on, don't apply changes automatically. Show the diff and wait for my approve.
```

**Example prompt:**

```text
Show a condensed diff of all changes before applying.
Only after my approve — then make the edits to the files.
```

---

## 🚩 Stop signals — a trigger to pause

If you see this — stop. Don't try to "force" the task through in the same direction. Revert, rebuild the plan, and start again.

- The diff suddenly has dozens of files instead of 1–2.
- Calls to functions/methods appeared that don't exist in the project or library.
- The agent changes function contracts without an explicit request.
- There's a lot of "for the future" code with no link to the task.
- Tests weren't run after the changes.
- You can't explain yourself what happened in the commit.

Every stop signal is a reason to return to [04-workflow.md](04-workflow.md) and run one more cycle: idea, plan, minimum, check, reflection.

---

## Self-diagnosis sheet

Answer honestly. If "yes" to 3 or more — re-read [03-principles.md](03-principles.md), [04-workflow.md](04-workflow.md), [09-checklists.md](09-checklists.md), and this file.

- [ ] I hit Accept without reading the whole diff.
- [ ] Files or changes I didn't ask for appeared in the diff.
- [ ] I can't explain how this change works.
- [ ] I agreed to a new dependency, library, or contract without checking.
- [ ] I gave the agent a task with no project context, `AGENTS.md`, or examples from the code.

---

Previous step: check yourself against the checklists — [09-checklists.md](09-checklists.md).

Next step: see how these same principles work in complex projects — [11-advanced-scenarios.md](11-advanced-scenarios.md).
