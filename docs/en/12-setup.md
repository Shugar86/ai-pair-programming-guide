# 12. The path from zero to your first session

🌐 **English** · [Русский](../12-setup.md)

Setup isn't the goal — it's the preparation. After it you'll open the editor and try your first pair-programming session.

Choose your route:

- **Minimal setup** — one editor, one project, one stack.
- **A working setup for a team lead** — several repositories, SSH, CI, shared rules for the team.

---

## Route A. Minimal setup for a quick start

Good if you just want to try it. No infrastructure, one project, one editor.

### What you'll need

1. A computer with Windows, macOS, or Linux.
2. A code editor with an AI agent.
3. Git.
4. A GitHub account.
5. An interpreter or compiler for your stack: Node.js, Python, Go, Rust, etc.

### Step 1. An editor with an AI agent

Pick any. The guide's principles work everywhere.

#### Cursor

- **What it is:** an IDE based on VS Code with a built-in agent.
- **Where to download:** https://www.cursor.com/
- **What you need:** a Cursor account, you can sign in via GitHub.
- **After installing:** open the project, press `Cmd/Ctrl + L` — the chat opens.
- **Cost:** a free tier with limits; paid — from $20/mo.

Example of a first request:

```text
Hi. This is my project. Explain what it's made of, and suggest what could be improved.
```

#### Claude Code

- **What it is:** a terminal assistant from Anthropic.
- **Where to download:** https://claude.ai/code
- **What you need:** an Anthropic account, a Pro subscription or an API key.
- **After installing:** go into the project folder and run `claude`.
- **When to choose it:** large projects, a server over SSH, minimal interface.

#### Kimi Code

- **What it is:** an assistant from Moonshot AI.
- **Where to download:** https://www.kimi.com/code
- **What you need:** a Moonshot AI account.
- **After installing:** a plugin in your IDE or a separate client per the instructions.
- **Note:** the client format changes — check against the current docs.

#### OpenCode

- **What it is:** an open assistant with several providers.
- **Where to download:** https://opencode.ai/
- **What you need:** install OpenCode and configure a provider via `opencode.json`.
- **After installing:** run it in the project folder and start a dialogue.
- **Plus:** you can use your own API keys and local models.

#### GitHub Copilot

- **What it is:** an assistant from GitHub, built into the editor.
- **Where to download:** https://github.com/features/copilot — a plugin for VS Code, JetBrains, Neovim.
- **What you need:** a GitHub account, a Copilot subscription (free for students).
- **After installing:** authorize the plugin and write code.

#### Cody

- **What it is:** an assistant from Sourcegraph with code search.
- **Where to download:** https://sourcegraph.com/cody
- **What you need:** a Sourcegraph account, an editor plugin.

Don't know where to start — take Cursor, or VS Code + Copilot. It's easier to see what's happening there.

### Step 2. Git

Git remembers what changed and when, and lets you roll back. Without it the agent can write code and you'll lose your working version.

#### Installation

- **Windows:** https://git-scm.com/download/win
- **macOS:** `xcode-select --install` or `brew install git`
- **Linux:** `sudo apt install git` (Debian/Ubuntu) or `sudo dnf install git` (Fedora)

#### Check

```bash
git --version
```

Should print something like `git version 2.43.0`.

#### Basic configuration

```bash
git config --global user.name "Your Name"
git config --global user.email "you@example.com"
```

#### If git isn't found

1. Restart the terminal.
2. On Windows use Git Bash — it comes bundled.
3. If that didn't help — reboot the computer.

More on problems — in [`15-troubleshooting.md`](15-troubleshooting.md).

### Step 3. GitHub

GitHub is cloud storage for git repositories.

1. Sign up: https://github.com/signup
2. GitHub CLI (optional, but handy): https://cli.github.com/
3. Check: `gh --version`
4. Authorize: `gh auth login`

### Step 4. The project stack

Install the language you write in:

- **JavaScript / TypeScript:** Node.js from https://nodejs.org/ (take the LTS).
- **Python:** https://www.python.org/downloads/
- **Go:** https://go.dev/dl/
- **Rust:** https://www.rust-lang.org/tools/install
- **Java:** Eclipse Temurin or Amazon Corretto.

Check:

```bash
node --version
python3 --version
go version
rustc --version
```

**Dialogue: checking Node.js**

```text
You:   How do I check whether Node.js is installed?
Agent: Open a terminal and run `node --version`. If you see a version number — it's fine.
You:   And if the terminal says "command not found"?
Agent: Then Node.js isn't installed yet. Download the LTS version from nodejs.org and restart the terminal.
```

### Step 5. The project's packages and dependencies

Almost every project uses libraries. Here's how to install them.

#### JavaScript / TypeScript

```bash
npm install
# or
yarn install
# or
pnpm install
```

#### Python

```bash
pip install -r requirements.txt
# or
poetry install
```

#### Rust

```bash
cargo build
```

#### Go

```bash
go mod download
```

#### System packages

```bash
sudo apt update && sudo apt install <package-name>   # Debian/Ubuntu
sudo dnf install <package-name>                       # Fedora
brew install <package-name>                           # macOS
```

If the command fails — first check that the package manager is installed. More in [`15-troubleshooting.md`](15-troubleshooting.md).

### Step 6. Readiness check

Before your first session, make sure:

- The editor with the agent launches.
- `git --version` shows a version.
- A GitHub account is created.
- The project stack is installed.
- The project's packages install without errors.

When everything's in place — open the project and try your first session.

---

## Route B. A working setup for a team lead

When you work with several repositories and a team, minimal setup isn't enough. You need rules, infrastructure, and a shared context.

### Additionally you'll need

1. SSH keys for servers and GitHub.
2. CI/CD: GitHub Actions, GitLab CI, or an equivalent.
3. A shared `AGENTS.md` or template for the team.
4. Workspace context, if there are several projects.

### SSH

SSH is needed to log into a server (VDS/VPS) and to work with GitHub by key.

#### Generate a key

```bash
ssh-keygen -t ed25519 -C "you@example.com"
```

#### Add the key to the ssh-agent

```bash
eval "$(ssh-agent -s)"
ssh-add ~/.ssh/id_ed25519
```

#### Add the public key to GitHub

```bash
cat ~/.ssh/id_ed25519.pub
```

Copy the output and add it under **Settings → SSH and GPG keys**.

### Working with several repositories

```text
~/workspace/
  workspace-context.md
  project-a/
    AGENTS.md
  project-b/
    AGENTS.md
```

`workspace-context.md` is a map of the connections: what contracts exist between the projects, where the source of truth is, where to commit changes for cross-repo tasks.

Example contents:

```markdown
# Workspace context

## Projects
- project-a: Python FastAPI, the source of API contracts.
- project-b: Next.js frontend, the API consumer.

## Contracts
- /api/v1/orders: project-a → project-b.
- order.created events: project-a → RabbitMQ → project-b.

## Rules
- We change API contracts only through an ADR.
- Before editing project-a, we check the consumers in project-b.
```

### CI/CD

Set up automated checks for each repository. Example GitHub Actions:

```yaml
name: CI
on: [push, pull_request]
jobs:
  test:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      - uses: actions/setup-node@v4
        with:
          node-version: '20'
      - run: npm install
      - run: npm test
```

The agent should know which checks run in CI. State it in `AGENTS.md`:

```markdown
## CI
- `npm run lint`
- `npm run typecheck`
- `npm test`
```

### An AGENTS.md template for the team

Create a single template and put it in `templates/AGENTS.md`. When starting a new project, copy it into the root and adapt it. An example template — in [`templates/AGENTS.md`](../../templates/AGENTS.md).

### The team lead's working checklist

- [ ] SSH keys are set up and working.
- [ ] Repositories are organized into a workspace.
- [ ] Every project has an `AGENTS.md`.
- [ ] CI runs the tests and the linter.
- [ ] There's a session-card template — [`templates/session-template.md`](../../templates/session-template.md).
- [ ] The team knows: the agent doesn't push, a human reads the diff.

---

Previous step: work through the advanced scenarios — [11-advanced-scenarios.md](11-advanced-scenarios.md).

Next step: learn to record changes in git — [13-git-github.md](13-git-github.md).
