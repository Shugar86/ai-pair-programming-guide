# Example: GitHub Actions CI

🌐 **English** · [Русский](../../07-examples/infra-ci.md)

**Verdict:** CI works only when you verify it not locally, but with a real push.

**Environment:** Cursor  
**Task:** Add a GitHub Actions workflow that runs the backend and frontend tests, checks the linters, and caches dependencies.

---

## 1. Define the task

```text
You: We need a GitHub Actions workflow. Runs on push to main and on pull_request.
     Two parallel jobs:
     - backend: set up Python, pip, pytest, flake8;
     - frontend: set up Node, npm ci, lint, test.
     Cache dependencies by the lock files. Secrets — via env or secrets, no hardcoding.
```

## 2. Agree on a plan

```text
Agent: Plan:
1. Create .github/workflows/ci.yml.
2. Add push and pull_request triggers.
3. Two jobs: backend and frontend.
4. Cache pip by requirements.txt and npm by package-lock.json.
5. Validate the YAML syntax.

You: OK. pull_request — only to main. Don't hardcode env variables into the file.
```

## 3. Implementation and the dead end

The agent creates the file. You see the npm cache key is set as `package-lock.json`, but the frontend lives in `frontend/package-lock.json`.

```text
You: The npm cache key looks at the root, but the lock file is in frontend/. Fix the path.
Agent: [fixes cache-dependency-path: frontend/package-lock.json]
```

The agent commits and pushes. The workflow fails at the backend-tests step.

```text
Agent: Error: pytest can't connect to PostgreSQL.
You: In CI we should have a separate test DB. Where's DATABASE_URL?
Agent: I took it from .env.example, but didn't pass it into the job's env.
You: Add env DATABASE_URL=postgresql://postgres:postgres@localhost:5432/test and bring up a Postgres service.
Agent: [adds services.postgres and env]
```

The agent adds the service, but now the job fails with an error: the `pull_request` trigger runs the workflow from a fork too, and there's no needed secret for reports there.

```text
You: For a pull_request from a fork, don't use the codecov secret. Gate the step with if: github.event_name != 'pull_request' || github.event.pull_request.head.repo.full_name == github.repository.
Agent: [adds the condition and removes the secret for forks]
```

## 4. Verification

```text
Agent: git push origin feature/ci
Agent: [opens Actions in the GitHub tab]
Agent: backend and frontend passed. Cache hit on both jobs.

You: Check the cache really works: re-run the job and look at the time.
Agent: [re-run job]
Agent: Dependency install time dropped from 2:10 to 0:18.

You: Create a test PR from a fork, if you have access. Make sure the secret isn't requested.
Agent: The PR from the fork passed without the codecov step.
```

## 5. Commit

```bash
git add .github/workflows/ci.yml
git commit -m "ci: add GitHub Actions workflow for backend and frontend"
```

## 6. Reflection

- Worked: splitting into two parallel jobs sped up feedback. Caching by lock files really cut the time.
- First dead end: the wrong path to `package-lock.json`. The cache missed and installed dependencies from scratch every time.
- Second dead end: forgot to pass `DATABASE_URL` and the Postgres service. Locally the tests passed because `.env` was at hand.
- Third dead end: secrets in a `pull_request` from a fork. The `if` condition protected CI from failing on external contributions.
- Could be better: give the agent the `.env.example` up front and say which variables are needed in CI and which aren't.

## Takeaway

CI with an agent goes through several iterations: YAML being syntactically valid doesn't mean the pipeline works. The real check is a push, a real PR, and a job re-run. Cache, secrets, and services are the three places where the agent regularly misses, because it can't see your local environment.

Which patterns worked here — see [`06-prompt-patterns.md`](../06-prompt-patterns.md).

Next step: lock in the skills with practice — [`08-exercises.md`](../08-exercises.md).
