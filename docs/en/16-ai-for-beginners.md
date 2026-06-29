# 16. Your first conversation with an agent

🌐 **English** · [Русский](../16-ai-for-beginners.md)

The agent doesn't read minds. The more specific the task — the closer the result to what you wanted.

---

## What AI doesn't do for you

AI is a powerful partner, but not a wizard. Three things stay on your side:

- **It won't read the whole project itself.** The agent sees what you showed it. Context is your job.
- **It doesn't guarantee the truth.** It confidently gives almost-correct answers and sometimes invents facts. Verify.
- **It doesn't remove responsibility.** The code in production is still yours. You make the decisions.

If you remember these three points, the agent becomes an accelerator, not a source of surprises.

---

## How to explain a task when nothing is clear

A good request has three parts:

1. What needs to be done — in one sentence.
2. Context — stack, file, library, version.
3. What you expect in the answer — a plan, code, an explanation, three options.

**Bad:**

```text
build auth
```

**Good:**

```text
I need to add email auth to a Django 4.2 project.
The login form already exists: app/users/forms.py.
First propose a 3-step plan, then we implement the first one.
```

If you don't know where to start — say so directly:

```text
I'm a beginner. I want to add auth, but I don't understand how the project is built.
Tell me which files are involved and suggest the first step.
```

---

## If the agent didn't get it

Don't repeat the same request louder. Change the phrasing.

- Add an example: "Here's what it should look like..."
- Break it into steps: "First do X, then Y."
- Specify the answer format: "Answer as a list," "Verdict first, then details."
- Give context: "In our project we use the service layer for this."

**Example dialogue:**

```text
You:   Build a registration form.
Agent: [proposes something off]
You:   Not it. Here's an example of the form I need: name, email, password. No email confirmation.
```

---

## How to ask clarifying questions

Going back and forth with the agent is normal.

```text
Explain it more simply — I didn't get why this step is needed.
```

```text
Give an example of the input and output data for this function.
```

```text
Why exactly this way? What other options are there?
```

```text
Rewrite it without complex terms, as if I were 15.
```

---

## How not to drown in the answer

Agents love to write a lot. To get a short answer:

```text
Give the answer in 3 points.
```

```text
A short verdict first, then the details.
```

```text
No intro — straight to the point.
```

```text
If you're not sure — say so directly.
```

---

## How to catch hallucinations

Agents confidently generate almost-correct answers. Sometimes they invent:

- methods that don't exist in the library;
- versions that don't exist;
- reasons for errors unrelated to reality.

**How to catch them:**

- Verify facts against the official docs.
- Run the code, don't take its word.
- If the agent confidently asserts something strange — ask for the source.

**Example:**

```text
You:   Why is this error happening?
Agent: Because Django 5.0 removed method X.
You:   We're on Django 4.2. Show me the docs link where this is stated.
```

---

## What to do if nothing makes sense

1. Stop. Don't keep pushing the agent — you'll get more tangled.
2. Identify what exactly is unclear: the code, a term, the architecture, or the task?
3. Ask it to explain from scratch:
   ```text
   I really didn't get it. Explain from the very beginning what we're trying to do.
   ```
4. Find a tutorial or docs on the topic. The agent is good on specifics but a poor replacement for a basic course.
5. Ask a human. If you're stuck more than 30 minutes — that's not shameful, it's efficient.

---

## Examples of starter requests

```text
I'm a beginner. Explain what this file does, line by line:
[paste the code]
```

```text
How does this code work? Explain it in simple words, no jargon.
```

```text
I want to understand how auth is built in this project.
Tell me which files are involved and what happens in them.
```

```text
I need to add a "Delete" button to the task list page.
Stack: React 18, Tailwind CSS. First propose a 3-step plan.
```

```text
Here's the error: [paste the text]. What does it mean and how do I fix it?
```

---

## The 90-minute route

If you want to try working with an agent without a week of theory — here's the minimal path.

| Stage | Time | What to do | Where to look |
|---|---|---|---|
| Get the idea | 10 min | Read what AI pair programming is and how the agent becomes a partner | [01-what-is-pair-programming.md](01-what-is-pair-programming.md), [02-agent-as-pair-programmer.md](02-agent-as-pair-programmer.md) |
| Get set up | 20 min | Choose a tool, set up the environment and the workflow | [12-setup.md](12-setup.md), [14-ide-cli-workflow.md](14-ide-cli-workflow.md) |
| Do one task | 60 min | Go through the full cycle: idea → plan → code → check → commit | [04-workflow.md](04-workflow.md) |

In an hour and a half you'll get not an abstract "understanding of AI," but one real task done together with an agent. After that — it's easier.

---

## The main rule

> AI doesn't know what you want until you say it. The more specific the phrasing — the better the result.

Don't expect the agent to guess the context. Your job is to make it a second brain, not a magical fortune-teller.

---

Previous step: figure out what to do when things break — [15-troubleshooting.md](15-troubleshooting.md).

Next step: see where all this is heading — [17-future.md](17-future.md).
