# 14. The working day: IDE or terminal

🌐 **English** · [Русский](../14-ide-cli-workflow.md)

The IDE and the CLI are two desks. The IDE is better when you want to see. The CLI — when you want to move fast or work on a server.

---

## IDE vs CLI: when to use which

| Situation | IDE (Cursor, VS Code + Copilot) | CLI (Claude Code, OpenCode) |
|---|---|---|
| Visual diff, buttons, navigation | ✅ | ❌ |
| A quick edit to one file | ✅ | ✅ |
| A large project, many files | ✅ | ✅ |
| Working on a remote server (SSH/VDS) | ❌ | ✅ |
| Want minimal interface | ❌ | ✅ |
| First experience with an agent | ✅ | ❌ |

Don't know where to start — take the IDE. It's easier to see what the agent changes.

**Dialogue: what to choose today**

```text
You:   I need to quickly fix one config on a server. IDE or CLI?
Agent: CLI. Open a terminal, connect over SSH, and run the agent right there. An IDE is awkward for a server.
You:   And if I'm a beginner and scared of the terminal?
Agent: Then start with the IDE. The main thing — open the project folder and look at the diff before any changes.
```

---

## A typical working day in the IDE

### 1. Open the project

`File → Open Folder...` and pick the project folder. You should open the folder, not a single file.

### 2. Open the chat with the agent

- **Cursor:** `Cmd/Ctrl + L` — the chat side panel.
- **VS Code + Copilot:** the Copilot icon in the side panel.
- **Kimi Code / other plugins:** their own icon in the sidebar.

### 3. Set the task

Write one sentence and ask for a plan:

```text
I need to add email validation at registration.
First propose a plan, then we write code.
```

### 4. Look at the diff

The agent will propose changes. Don't immediately hit "Accept all":

- open the diff (the **Diff** tab or the changes icon);
- read what changed;
- if the agent grabbed extra files — say so.

### 5. Run the checks

The built-in terminal: `Cmd/Ctrl + `` ` (backtick).

```bash
npm test
# or
pytest
```

### 6. Commit

```bash
git add src/auth/validation.py
git commit -m "feat: add email validation in signup"
```

---

## A typical working day in the CLI

The CLI steps are the same loop from [`04-workflow.md`](04-workflow.md), just in the terminal.

### 1. Go into the project folder

```bash
cd ~/projects/my-app
```

### 2. Start the agent

```bash
claude
# or
kimi
# or
opencode
```

### 3. Describe the task

```text
I need to add email validation at registration.
First propose a plan, then we write code.
```

This is step 1 "Capture the idea" and step 2 "Sketch the path" from loop 04.

### 4. Control the changes

The agent will propose edits. Before agreeing:

```bash
git diff
```

This is step 4 "Test by feel": the diff before the tests.

### 5. Run the checks

```bash
npm test
```

This is still step 4: tests, linter, types. The project's command list — in [`05-environments.md`](05-environments.md).

### 6. Commit

```bash
git add src/auth/validation.py
git commit -m "feat: add email validation in signup"
```

This is step 5 "Lock it in." Push stays with you — see "AI and Git" in [`13-git-github.md`](13-git-github.md).

### 7. Reflection

After the commit — two or three lines: what worked, what could have been faster, what to do next time. This is step 6 "Look at what came out."

---

## Mapping the CLI steps to the loop

| CLI step | Loop 04 step | What you check |
| :-- | :-- | :-- |
| Described the task and asked for a plan | 1–2. Capture the idea, Sketch the path | The idea is clear, the plan is short |
| The agent writes code | 3. Build the minimum | Only the needed files |
| `git diff` | 4. Test by feel | Nothing extra, nothing strange |
| `npm test` / `pytest` | 4. Test by feel | The code works |
| `git commit` | 5. Lock it in | The history is clear |
| A short retro note | 6. Look at what came out | What to improve next time |

---

## How to show the agent your code

The agent needs context. Show specific files or fragments.

### In the IDE

- **`@file` or `#file`** — mention a file in the chat: `@src/auth/validation.py`.
- **Select code with the mouse** — many agents see the selected fragment.
- **Copy into the chat** — for short chunks.

### In the CLI

- Name the file in text: "Look at `src/auth/validation.py`."
- For complex cases, use `AGENTS.md` in the project root — the agent will read it itself.

---

## Keyboard shortcuts

| Action | Windows/Linux | macOS |
|---|---|---|
| Command palette | `Ctrl + Shift + P` | `Cmd + Shift + P` |
| Terminal | `` Ctrl + ` `` | `` Cmd + ` `` |
| Find a file | `Ctrl + P` | `Cmd + P` |
| Search the project | `Ctrl + Shift + F` | `Cmd + Shift + F` |
| Undo the last action | `Ctrl + Z` | `Cmd + Z` |

---

## How to arrange the window

A handy minimalist layout:

- **Left** — the project files.
- **Center** — the code.
- **Right** — the chat with the agent.
- **Bottom** — the terminal.

You should see both the code and what the agent writes, without constant switching.

---

## When to switch from IDE to CLI

- You work on a server over SSH.
- The project is large and the IDE lags.
- You want to quickly check something without opening the editor.
- You already know the terminal well.

---

Previous step: learn to record changes in git — [13-git-github.md](13-git-github.md).

Next step: figure out what to do when things break — [15-troubleshooting.md](15-troubleshooting.md).
