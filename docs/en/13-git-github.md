# 13. Git and GitHub: a safety net for experiments

🌐 **English** · [Русский](../13-git-github.md)

Git is the safety net that lets you and the agent try ideas without fear. You decide what goes into a commit, not the agent.

---

## AI and Git

The agent writes code well and carries responsibility for history poorly. Git is your zone.

### Don't let the agent push

Push is publication. Only you decide when changes are ready to go to the shared repository. The agent can prepare a diff, write the commit message, assemble a PR — but it doesn't press `git push`.

**Why:** the agent doesn't feel the team's context, doesn't know what's in `main` right now, and doesn't understand whether changes should be merged this very moment.

**How to do it:**
- In the CLI, don't give commands like "push" or "send to GitHub."
- In the IDE, apply the diff yourself, commit yourself, push yourself.
- If the agent suggests a push — stop and double-check.

### Always read the diff before a commit

The diff is the answer to "what actually changed?" Read it before every commit.

```bash
git diff                    # what changed but isn't staged yet
git diff --staged          # what's already in the index
```

What to look for:
- extra files — `console.log`, temp files, `.env`;
- changes unrelated to the task;
- strange edits in neighboring files;
- hardcoded values or commented-out code.

The diff-acceptance checklist is in [`09-checklists.md`](09-checklists.md).

### Use the agent for commit messages and PR descriptions

The agent is great at phrasing what changed, if you give it the diff.

**Commit message:**

```text
Here's the diff. Write a commit message in the format <type>: <what changed>.
No more than one line.
```

**PR description:**

```text
Here's the list of commits and the diff. Write a PR description:
- what changed,
- why,
- what was tested,
- what the reviewer should pay attention to.
```

Check the result. The agent sometimes exaggerates or forgets an important detail. The commit message is your face in the history.

---

## What git and GitHub are

- **Git** is a version-control system on your computer. It remembers what changed and when.
- **GitHub** is a cloud service you can push a repository to, in order to store code and work together.

---

## Creating a repository

### Locally

```bash
mkdir my-project
cd my-project
git init
git branch -M main
```

A hidden `.git` directory will appear in the folder — that's the project's history.

### On GitHub via the web

1. Open https://github.com/new
2. Enter a repo name, choose `Public` or `Private`.
3. Don't add a README and `.gitignore` if you're creating locally — you'll do that yourself.

---

## The basic working cycle

### 1. See what changed

```bash
git status
```

### 2. Add files to the upcoming commit

```bash
git add filename.py          # one file
git add src/                 # a folder
git add .                    # everything current (careful!)
```

In pair programming it's better to add files one at a time. You control what goes into the commit, not the agent.

**Dialogue: adding only the needed file**

```text
You:   The agent changed three files, but I want to commit only one. How?
Agent: Use `git add filename`. For example, `git add src/auth.py`.
You:   Won't `git add .` do?
Agent: It adds everything at once. In pair programming it's better one at a time — that way you see exactly what goes into the commit.
```

### 3. Record the changes

```bash
git commit -m "feat: add email validation"
```

The message says what changed. Don't write just "fix" or "update."

### 4. Look at the history

```bash
git log --oneline
```

### 5. Discard uncommitted changes

```bash
git checkout -- filename.py   # one file
git reset --hard HEAD         # everything back to the last commit (careful!)
```

---

## Working with GitHub

### Link a local repository

```bash
git remote add origin https://github.com/username/repo.git
git push -u origin main
```

### Send changes

```bash
git push origin main
```

### Pull changes

```bash
git pull origin main
```

### Clone someone else's repository

```bash
git clone https://github.com/username/repo.git
cd repo
```

After cloning you usually need to:

1. Install dependencies: `npm install`, `pip install -r requirements.txt`, etc.
2. Run the tests.
3. Open the project in the editor.

---

## Branches

Branches are drafts. Try an idea in a separate branch without breaking the main code.

```bash
git checkout -b feature-login
```

After the work:

```bash
git add filename.py
git commit -m "feat: add login form"
git push origin feature-login
```

Then on GitHub create a Pull Request to merge the changes into `main`.

---

## Pull Requests

A Pull Request is a request to merge a branch into `main`. Through a PR you can discuss the changes and run the checks.

### Via the web

1. Push the branch: `git push origin feature-login`.
2. Open the repository on GitHub.
3. Click **Compare & pull request**.
4. Write a title and description: what changed and why.
5. Click **Create pull request**.

### Via the GitHub CLI

```bash
gh pr create --title "feat: add login" --body "What changed and why"
```

### After approval

```bash
gh pr merge
# or the Merge pull request button on GitHub
```

---

## Merge and conflicts

Merge is combining one branch with another.

```bash
git checkout main
git pull origin main
git merge feature-login
```

### A conflict

A conflict arises when the same line is changed in two branches.

Git marks it like this:

```text
<<<<<<< HEAD
the old version
=======
the new version
>>>>>>> feature-login
```

What to do:

1. Open the file in the editor.
2. Choose the right variant, remove the markers.
3. Save the file.
4. `git add <file>`
5. `git commit -m "merge: resolve conflict"`

If conflicts scare you — keep branches short and pull the current `main` more often.

---

## CI/CD — automated checks

CI/CD runs checks and deploys on every push. In learning projects, CI is the most common:

- on push to a PR the tests run;
- if the tests fail — the PR isn't merged;
- the linter checks code style.

On GitHub, CI is configured via GitHub Actions — `.github/workflows/*.yml` files.

```yaml
# Example .github/workflows/ci.yml
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

If CI is red — look at the logs, fix the errors, push again.

---

## Viewing changes before a commit

### git diff

```bash
git diff                    # what changed but isn't staged yet
git diff --staged          # what's already in the commit
```

### git add -p

Add not the whole file, but only a selected chunk:

```bash
git add -p filename.py
```

Git asks for each chunk: add it or not.

---

## GitHub CLI

`gh` simplifies working with GitHub from the terminal.

### Create a repository and push

```bash
cd my-project
gh repo create my-project --public --source=. --remote=origin --push
```

### View information about a repository

```bash
gh repo view username/repo
```

### Create a Pull Request

```bash
gh pr create --title "feat: add login" --body "What changed and why"
```

---

## What not to do

- **Don't commit secrets.** Passwords, API keys, `.env` — add them to `.gitignore`.
- **Don't force-push without dire need.** `git push --force` breaks history for others.
- **Don't commit everything indiscriminately.** Use `git add <file>` and check `git status`.
- **Don't let the agent push.** Push is your decision, not its.

---

## Practice

1. Create a local repository.
2. Add a `README.md` file, commit it.
3. Create a repository on GitHub and push the code.
4. Make a change, commit, and push again.

When this works on autopilot — you can experiment with the agent calmly. You control what goes into the commit, not the agent.

---

Previous step: prepare your working environment — [12-setup.md](12-setup.md).

Next step: figure out how to work in the IDE and the terminal — [14-ide-cli-workflow.md](14-ide-cli-workflow.md).
