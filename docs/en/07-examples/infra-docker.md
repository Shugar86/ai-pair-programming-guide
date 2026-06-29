# Example: Docker for a Python + Node app

🌐 **English** · [Русский](../../07-examples/infra-docker.md)

**Verdict:** you verify a Docker image not by eye, but with `docker build` and `docker run`.

**Environment:** Kimi Code (CLI)  
**Task:** Build a `Dockerfile` for an app: FastAPI (backend) and Vite/React (frontend) in one repository. The image must be compact, with no `.env` and no secrets.

---

## 1. Define the task

```text
You: We need a Dockerfile for our app. Inside:
     - a FastAPI backend, folder backend/, dependencies in backend/requirements.txt;
     - a Vite + React frontend, folder frontend/, built with npm run build;
     - in production the frontend is served via nginx, the backend is a separate process.
     For now make a single image: nginx serves the static files and proxies /api to uvicorn.
     Multi-stage, no .env inside the image, final layer — slim.
```

## 2. Agree on a plan

```text
Agent: Plan:
1. Study the structure of backend/ and frontend/.
2. Write a Dockerfile with three stages:
   - build-node — build the frontend;
   - build-python — install the backend dependencies;
   - runtime — a slim image with nginx, uvicorn, and the built static files.
3. Add a .dockerignore to exclude .env, node_modules, __pycache__.
4. Verify the build and the container run.

You: OK. Don't put .env in and don't hardcode secrets. External port — 80.
```

## 3. Implementation and the dead end

The agent shows the first diff. You notice `.env` didn't make it into `.dockerignore`, and `backend/.env` ends up in the final image.

```text
You: Remove .env from the image. And add .env to .dockerignore.
Agent: [adds .env to .dockerignore and removes backend/.env from the copy]
```

The agent rewrites the Dockerfile, but now it copies the whole `frontend/node_modules` into the final image — one stage instead of multi-stage.

```text
You: This isn't multi-stage. The final image should get only the frontend's dist/ and the backend code without dev dependencies.
Agent: [reworks it into build-node + build-python + runtime]
```

The agent runs the build. The image builds, but it's 1.4 GB.

```text
You: Why so big?
Agent: The runtime stage uses python:3.11, not slim.
You: Switch runtime to python:3.11-slim and don't forget nginx.
Agent: [uses slim, installs nginx, copies the config]
```

## 4. Verification

```text
Agent: docker build -t myapp:latest .
Agent: docker images myapp:latest
Agent: REPOSITORY   TAG       SIZE
       myapp        latest    287MB

You: Good. Now run it and check /api/health and the home page.
Agent: docker run -d -p 8080:80 --name myapp-test myapp:latest
Agent: curl -s http://localhost:8080/api/health
Agent: {"status":"ok"}
Agent: curl -s -o /dev/null -w "%{http_code}" http://localhost:8080/
Agent: 200

You: Check there's no .env inside the container.
Agent: docker exec myapp-test find / -name ".env" 2>/dev/null
Agent: [empty output]
```

## 5. Commit

```bash
git add Dockerfile .dockerignore nginx.conf
git commit -m "infra: add multi-stage Dockerfile for Python + Node app"
```

## 6. Reflection

- Worked: the explicit "no .env and no secrets" constraint helped catch the leak early.
- First dead end: the agent forgot `.dockerignore` and pulled `.env` into the build context. `.dockerignore` is a mandatory companion to a Dockerfile.
- Second dead end: the first version wasn't multi-stage. You needed to say "three stages" up front, not hope the agent would guess.
- Third dead end: the image ballooned because of a non-slim base. Size is also a check; 1.4 GB is a signal something extra is in there.
- Could be better: show the folder structure and an example `nginx.conf` up front, so the agent doesn't invent routes.

## Takeaway

Docker with an agent isn't "generate a Dockerfile and forget it." The image needs to be built, run, and inspected from the inside. Multi-stage and `.dockerignore` are worth stating up front, because the agent often writes a "working" image that drags half the dev environment along with it.

Which patterns worked here — see [`06-prompt-patterns.md`](../06-prompt-patterns.md).

Next example: adding CI/CD — [`infra-ci.md`](infra-ci.md).
