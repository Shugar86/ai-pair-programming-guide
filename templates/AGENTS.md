# AGENTS.md — the project contract

🌐 **English** · [Русский](AGENTS.ru.md)

Copy this template into the project root as `AGENTS.md` and fill it in. It tells the agent who leads and who helps.

## General

- **Language:** Russian / English
- **Agent role:** pair-programmer
- **You lead:** priorities, architecture, trade-offs
- **The agent helps:** write code, review, narrow uncertainty
- **Project stack:** e.g., Python 3.11, Next.js 14, PostgreSQL 15

## Role and responsibility

The agent helps you create, but doesn't decide for you. It proposes options, writes code, and catches problems. The choice of direction, risk assessment, and the final decision are always yours.

> Example: if the agent wants to change the architecture or pull in a new dependency — stop, discuss it first.

## Stack

- **Language:**
- **Framework:**
- **Database:**
- **Tests:**
- **Linter/formatter:**

## Rules

- KISS — the simplest solution
- Minimal diff — touch only what's needed
- YAGNI — no code "for the future"
- Plan before code — agree on the approach before implementing
- Check the diff before applying
- In doubt — ask

## Git

- Commit the result of the task.
- Commit message: `<type>: <what changed>`.
- Don't commit `.env`, keys, or local settings.

## Forbidden

- Hardcoding secrets.
- Force push.
- Editing production without agreement.
- Pretending everything's clear when it isn't.
- Changing more than 3 files without agreement.

## Contacts / escalation

- Who to ask when unsure:
- How to deploy:
- Where the logs are:

---

## Examples for common stacks

Copy the matching block into your `AGENTS.md` and delete the rest.

### TypeScript web product

```markdown
## General

- **Language:** English
- **Agent role:** pair-programmer
- **You lead:** UX, architecture, feature priorities
- **The agent helps:** components, tests, types, diff review

## Stack

- **Language:** TypeScript 5.x
- **Framework:** Next.js 14 (App Router)
- **Styles:** Tailwind CSS
- **Database:** PostgreSQL 15
- **ORM:** Prisma
- **Tests:** Vitest, Playwright for e2e
- **Linter/formatter:** ESLint, Prettier

## Rules

- Components are functions, not classes.
- Declare every props interface explicitly.
- Data fetching — in server components or route handlers.
- Don't add client libraries without discussion.
- Minimal diff: one feature — one component / one endpoint.
```

### Python backend

```markdown
## General

- **Language:** English
- **Agent role:** pair-programmer
- **You lead:** API contracts, the DB schema, integrations
- **The agent helps:** endpoints, services, tests, migrations

## Stack

- **Language:** Python 3.11
- **Framework:** FastAPI
- **Database:** PostgreSQL 15
- **ORM / migrations:** SQLAlchemy 2.x, Alembic
- **Tests:** pytest
- **Linter/formatter:** ruff, mypy

## Rules

- The API layer doesn't know DB details — use the service layer.
- Pydantic schemas separate from SQLAlchemy models.
- Migrations by hand, don't auto-generate without review.
- All endpoints covered by tests for 200 and for errors.
- Don't change the public API without agreement.
```

### Infrastructure repository

```markdown
## General

- **Language:** English
- **Agent role:** pair-programmer
- **You lead:** infrastructure architecture, access, budget
- **The agent helps:** Terraform configs, pipelines, automation scripts

## Stack

- **Provider:** Terraform + AWS / Yandex Cloud
- **Configuration:** Ansible for bare-metal
- **CI/CD:** GitHub Actions / GitLab CI
- **Containers:** Docker, Docker Compose
- **Tests:** terraform validate, tflint, molecule

## Rules

- No secrets in the repository — only references to vault / ssm.
- Infrastructure changes — via PR and a plan before apply.
- Describe backups and rollbacks explicitly.
- Don't change production without agreement.
- Every script must be idempotent.
```

More on the role of `AGENTS.md` and working with the environment — in [05-environments.md](../docs/en/05-environments.md) and [18-senior-playbook.md](../docs/en/18-senior-playbook.md).
