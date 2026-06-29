# 15. What to do when things break

🌐 **English** · [Русский](../15-troubleshooting.md)

Something will always break. Work the checklist — calmly, step by step.

---

## Before you panic

1. Re-read the error. Often the first two lines say what's wrong.
2. Google the first 1–2 lines of the error. Most likely someone has already solved it.
3. Copy the error and ask the agent: "Here's the error. What does it mean and how do I fix it?"
4. If you've spent more than 30 minutes with no progress — call a human.

**Dialogue: decoding an error**

```text
You:   Here's the error: `ModuleNotFoundError: No module named 'flask'`. What does it mean?
Agent: Python can't find the Flask library. Most likely it isn't installed in the current environment.
You:   How do I fix it?
Agent: Run `pip install flask` or `pip install -r requirements.txt` if a dependency list already exists.
```

---

## When the problem isn't the environment but the agent

You have internet, the dependencies are installed, git works — but the agent still behaves strangely. Most often the cause is context, not code.

### The agent doesn't understand the project

**Symptom:** the agent proposes a solution that doesn't look like your project. It ignores conventions. It changes files you didn't ask about.

**What to do:**

1. Add or update `AGENTS.md` in the project root. Spell out the stack, conventions, prohibitions, owners. Template — in [`templates/AGENTS.md`](../../templates/AGENTS.md).
2. Give the agent the repo structure: "First read `README.md`, `AGENTS.md`, and show which modules relate to the task."
3. Restart the session so the old dialogue doesn't interfere.
4. If the agent is still confused — start with one specific file, not the general task.

**Where to look:**
- context principles — [`03-principles.md`](03-principles.md);
- configuring environments — [`05-environments.md`](05-environments.md);
- typical traps — [`10-antipatterns.md`](10-antipatterns.md).

### The agent doesn't hold the boundaries

**Symptom:** it writes a lot of code, adds abstractions, changes neighboring files.

**What to do:**

1. Remind it about minimal diff and YAGNI — see [`03-principles.md`](03-principles.md).
2. Ask for a plan before code and explicitly limit scope: "Only `src/auth/validation.py`, don't touch the UI."
3. Use the checklists from [`09-checklists.md`](09-checklists.md) before accepting changes.

### The agent lies confidently

**Symptom:** it says the tests passed when they fail. It claims a file exists when it doesn't.

**What to do:**

1. Don't take its word. Check yourself: `git status`, `git diff`, run the tests.
2. Ask the agent to show the command and the output — not just "all good."
3. If the agent isn't sure — make it say so. See the "Escalate uncertainty" principle in [`03-principles.md`](03-principles.md).

---

## Git isn't installed or isn't found

**Error:**

```text
'git' is not recognized as an internal or external command
```

**What to do:**

1. Download git: https://git-scm.com/downloads
2. On Windows, during installation keep the **"Git from the command line and also from 3rd-party software"** checkbox.
3. Restart the terminal.
4. Check: `git --version`.

If it still doesn't work — reboot the computer.

---

## The agent doesn't see the project

**Symptom:** the agent says it can't find the files, or proposes a solution that doesn't look like your project.

**What to do:**

1. Make sure you opened the project folder, not a single file.
2. In the CLI check: `pwd` (macOS/Linux) or `cd` (Windows) — it should be the project folder.
3. Ask the agent to read `README.md` and `AGENTS.md`.
4. Reopen the project or restart the session.

---

## Command not found

**Error:**

```text
command not found: node
```

**What to do:**

1. Make sure the program is installed: `node --version`, `python3 --version`.
2. Restart the terminal after installing.
3. Check PATH. Sometimes the program is installed but the terminal doesn't see it.
4. Reinstall via the official installer.

---

## Errors when installing packages

**Symptom:** `npm install` or `pip install` fails with red text.

**What to do:**

1. Check the language version: `node --version`, `python3 --version`.
2. Remove the cache and try again:
   ```bash
   rm -rf node_modules package-lock.json
   npm install
   ```
3. Check your internet connection and proxy (if you're on a corporate network).
4. Copy the full error text and show it to the agent.

---

## WSL — Linux on Windows

WSL lets you run Linux right inside Windows. Handy if the project is built for Linux/macOS.

### Installation

```powershell
wsl --install
```

After a reboot you'll have Ubuntu. Open it via Start menu → Ubuntu.

### Basic commands

```bash
pwd              # where am I now
ls               # list files
cd /mnt/c        # get to the C: drive
```

### Why it's useful

- Many tools work better in Linux than in Windows.
- The WSL terminal is closer to what's used on servers.

---

## SSH — connecting to a remote server

SSH is needed to log into a server (VDS/VPS) from the terminal.

### Connecting by password

```bash
ssh username@server-ip
```

### Connecting by key

```bash
ssh -i ~/.ssh/my_key username@server-ip
```

### If it won't connect

1. Check the IP address and port.
2. Check the key permissions: `chmod 600 ~/.ssh/my_key`.
3. Make sure SSH access is allowed on the server.
4. Try connecting with the `-v` flag for verbose output: `ssh -v username@server-ip`.

---

## VDS / VPS — a remote server

A VDS/VPS is a computer on the internet that you connect to remotely. Needed for deployment, bots, server apps.

### What you'll need

- An account with a provider (Hetzner, Timeweb, Selectel, etc.).
- An SSH key or password.
- A basic understanding of Linux.

### After connecting

```bash
ls -la           # look at the files
sudo apt update  # update the package list
systemctl status <service>  # check a service's status
```

Don't experiment on production without a backup. If you're not sure — ask before editing.

---

## The agent broke the code

**Symptom:** after the agent's changes, the code stopped working.

**What to do:**

1. Don't panic — you have git.
2. Look at the diff: `git diff`.
3. Revert a specific file: `git checkout -- filename.py`.
4. Or revert the whole commit: `git reset --hard HEAD~1`.
5. If the changes are already pushed — revert via a new commit, not a force push.

---

## Nothing works: the nuclear option

If the project completely fell apart:

```bash
# Save the current changes separately
git stash

# Return to the last working commit
git reset --hard HEAD

# Or re-clone from GitHub
git clone https://github.com/username/repo.git repo-fresh
```

`git reset --hard` deletes unsaved changes. Use it only if the code can be lost.

---

## When to call a human

- You've spent more than 30 minutes and don't understand what's going on.
- The agent proposes changing the architecture or infrastructure.
- You're touching production, the database, secrets, CI/CD.
- You see security errors or suspicious activity.

---

Previous step: figure out how to work in the IDE and the terminal — [14-ide-cli-workflow.md](14-ide-cli-workflow.md).

Next step: learn to explain tasks to the agent — [16-ai-for-beginners.md](16-ai-for-beginners.md).
