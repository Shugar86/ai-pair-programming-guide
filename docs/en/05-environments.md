# 05. Environments as task-fit tools

🌐 **English** · [Русский](../05-environments.md)

**Verdict:** an environment isn't a religion, it's a tool for the task.

An environment isn't a religion, it's a tool. Cursor is handy when you watch the result. Kimi and Claude are good for large projects and servers. Copilot and Cody help in the moment. Choose by the task, not by the hype.

To avoid getting lost in each tool, the same template is used below:

- **How to show context.** How to give the agent files, the project map, and `AGENTS.md`.
- **Where to see the diff.** Where to check what the agent is about to change.
- **How to limit scope.** How to keep the agent in the right files.

---

## Cursor

**When to choose it.** You work with UI, you want the diff next to the code, and you want to quickly click "accept" or "revert."

**How to start.**

1. Download Cursor from [cursor.com](https://www.cursor.com).
2. Open the project. Press `Cmd/Ctrl + L` — the chat opens.
3. Switch to Agent or Composer mode if the task touches several files.
4. Ask for a plan before code.

**How to show context.**

- Use `@AGENTS.md`, `@README.md`, `@file`, or `@folder` in the chat.
- In Agent mode Cursor sees open files and the project tree. Before a complex task, open the needed files or reference them explicitly with `@`.
- For a general project map use `@Codebase` — but check that it didn't invent the structure.

**Where to see the diff.**

- Composer/Agent shows the diff before applying it, in the right-hand panel.
- The **Changes** tab (Ctrl/Cmd + Shift + G) — a list of all changes.
- Enable inline diff in the editor to see edits line by line.

**How to limit scope.**

- Select specific code before the request — Cursor will apply the edit only to the selection.
- Say it explicitly: "Change only `ProfileCard.tsx`, don't touch neighboring components."
- Disable auto-applying changes in the settings if you want to read the diff first.

---

## Kimi Code

**When to choose it.** You're in the terminal or IDE, the project is large, and you need an agent that remembers the rules from `AGENTS.md`.

**How to start.**

1. Install Kimi Code per the official instructions for your editor or terminal: [kimi.com/code](https://www.kimi.com/code).
2. Go into the project folder.
3. Create `AGENTS.md` in the root (template — in [`templates/AGENTS.md`](../../templates/AGENTS.md)).
4. Start a session and describe the task.

**How to show context.**

- Kimi Code automatically reads `AGENTS.md` in the project root. Make sure the file is current.
- Reference files explicitly: "First read `src/orders/service.py` and `tests/test_orders.py`."
- For a project overview, ask: "Show the structure of the modules related to the task."

**Where to see the diff.**

- The agent prints the diff in the terminal before applying.
- After the edit, use `git diff` for a final check.
- In an IDE the diff shows in the standard changes panel.

**How to limit scope.**

- List the allowed files in the first message: "We work only with `src/orders/`."
- Use a selection: highlight a fragment and ask to change only it.
- Rules in `AGENTS.md` act as a guardrail: "Change no more than 3 files without agreement."

---

## Claude Code

**When to choose it.** You're in the terminal, the task is complex and needs discussion. Works well on a server and with large codebases.

**How to start.**

1. Install Claude Code from [claude.ai/code](https://claude.ai/code).
2. Run `claude` in the project folder.
3. Describe the task in text.
4. Use `/clear` when the context grows, and `/help` for commands.

**How to show context.**

- Add files manually: `/add src/orders/service.py` or `/add docs/architecture.md`.
- Claude sees the working directory, but don't rely on it — point out the key files.
- At the start of a session say: "Start with `AGENTS.md` and `README.md`."

**Where to see the diff.**

- Claude shows the diff in the terminal before each change and asks for confirmation.
- Use `/git diff` or the regular `git diff` to compare against the current state.

**How to limit scope.**

- State the boundaries explicitly: "We work only in `src/billing/`, we don't change the API of other modules."
- Use `/clear` between unrelated tasks so context doesn't mix.
- Ask for a plan before code and fix the scope in that plan.

---

## OpenCode

**When to choose it.** You want an open solution, flexibility in model choice, and integration via MCP.

**How to start.**

1. Install OpenCode from [opencode.ai](https://opencode.ai).
2. Configure the provider in `opencode.json`.
3. Open the project and start a dialogue.

**How to show context.**

- Connect `AGENTS.md` and the README as context sources via MCP or explicit references.
- Use `@file` or similar commands to select specific files.
- Check which provider and model are set — the context size depends on it.

**Where to see the diff.**

- The diff shows in the UI or terminal depending on the provider.
- Always double-check via `git diff` before committing — OpenCode isn't uniform in its output.

**How to limit scope.**

- Limit file selection at the UI/CLI level: open only the needed folder.
- Spell out clear boundaries in the prompt: "Don't change the configuration, only the logic in `src/`."
- Start with a single provider and a simple setup. Add MCP and extra models once the base works.

---

## GitHub Copilot / Cody

**When to choose it.** You're already in the editor and need autocomplete, a quick explanation, or a small in-line edit.

**How to start.**

- Copilot: install the extension in VS Code, JetBrains, or Neovim from [github.com/features/copilot](https://github.com/features/copilot).
- Cody: install the Sourcegraph extension from [sourcegraph.com/cody](https://sourcegraph.com/cody).

**How to show context.**

- Copilot Chat: use `@workspace` or `@file` for context.
- Cody: use `@codebase` to search the project and `@file` for specific files.
- `AGENTS.md` isn't always read automatically — copy the key rules into the prompt or attach the file via `@`.

**Where to see the diff.**

- Copilot: inline suggestions, the Copilot Chat panel with proposals, the diff in the editor.
- Cody: the diff in the chat and in the changes panel.
- For large changes, switch to a tool with explicit diff review.

**How to limit scope.**

- Select specific code before the request — both tools orient on the selection.
- Keep requests short and specific: "Add email validation in this function."
- For tasks bigger than one file, switch to Cursor, Kimi, or Claude. Don't try to rewrite half the project through autocomplete.

---

## Notes on privacy and sending code

Code goes to the vendor in almost every cloud tool. The rule is simple: don't send what you can't show.

| Tool | What goes to the server | What to watch for |
| :-- | :-- | :-- |
| Cursor | Project files, diff, chat history | Cloud mode. Don't put `.env`, keys, passwords, or PII in the project. Check the privacy-mode settings if you work with sensitive code. |
| Kimi Code | Project files, prompts, diff | Cloud service. Avoid sending secrets and personal data. For corporate projects, clear it with policy. |
| Claude Code | Project files, prompts, diff | Anthropic doesn't use ordinary requests to train models by default, but check the current terms. Still, don't send secrets. |
| OpenCode | Depends on the chosen provider | The most flexible scenario: you can set up a local model or a self-hosted provider. Check exactly where the data goes. |
| GitHub Copilot | Editor context, part of the files | Microsoft/GitHub filter secrets, but don't rely on it. Use Copilot carefully with code under NDA. |
| Cody | The code you reference | Sourcegraph can run in the cloud or self-hosted. For private repos, confirm the deployment. |

**Universal rules:**

- Never send passwords, tokens, private keys, or users' personal data.
- For secret code, prefer local models or self-hosted solutions.
- Agree on an internal AI policy in the team: what may be sent to agents and what may not.
- More in [`docs/19-security-and-policy.md`](19-security-and-policy.md).

---

## The universal verdict

Don't hunt for the "best" environment. Take the one already installed and apply the principles from [`03-principles.md`](03-principles.md). A good request in a suitable environment beats a perfect tool with a bad request.

Next step: learn to frame tasks — [`06-prompt-patterns.md`](06-prompt-patterns.md).
