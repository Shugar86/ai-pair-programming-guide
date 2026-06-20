# Пример: Docker для Python + Node приложения

**Вердикт:** Docker-образ проверяешь не глазами, а `docker build` и `docker run`.

**Среда:** Kimi Code (CLI)  
**Задача:** Собрать `Dockerfile` для приложения: FastAPI (backend) и Vite/React (frontend) в одном репозитории. Образ должен быть компактным, без `.env` и секретов.

---

## 1. Определяем задачу

```text
Ты: Нужен Dockerfile для нашего приложения. Внутри:
     - backend на FastAPI, папка backend/, зависимости в backend/requirements.txt;
     - frontend на Vite + React, папка frontend/, собирается через npm run build;
     - в проде фронт отдаётся через nginx, бэкенд — отдельный процесс.
     Пока сделай один образ: nginx раздаёт статику и проксирует /api на uvicorn.
     Multi-stage, никаких .env внутри образа, финальный слой — slim.
```

## 2. Согласуем план

```text
Агент: План:
1. Изучить структуру backend/ и frontend/.
2. Написать Dockerfile с тремя стадиями:
   - build-node — собрать фронт;
   - build-python — установить зависимости бэкенда;
   - runtime — slim-образ с nginx, uvicorn и собранной статикой.
3. Добавить .dockerignore, чтобы исключить .env, node_modules, __pycache__.
4. Проверить сборку и запуск контейнера.

Ты: Ок. Не клади .env и не хардкодь секреты. Порт наружу — 80.
```

## 3. Реализация и тупик

Агент показывает первый diff. Ты замечаешь, что `.env` не попал в `.dockerignore`, а в финальном образе лежит `backend/.env`.

```text
Ты: Убери .env из образа. И добавь .env в .dockerignore.
Агент: [добавляет .env в .dockerignore и удаляет backend/.env из копирования]
```

Агент переписывает Dockerfile, но теперь он копирует весь `frontend/node_modules` в финальный образ — одна стадия вместо multi-stage.

```text
Ты: Это не multi-stage. Финальный образ должен получать только dist/ фронта и код бэкенда без dev-зависимостей.
Агент: [переделывает на build-node + build-python + runtime]
```

Агент запускает сборку. Образ собирается, но размер 1.4 ГБ.

```text
Ты: Почему так много?
Агент: В runtime-стадии используется python:3.11, не slim.
Ты: Переведи runtime на python:3.11-slim и не забудь nginx.
Агент: [использует slim, устанавливает nginx, копирует конфиг]
```

## 4. Проверка

```text
Агент: docker build -t myapp:latest .
Агент: docker images myapp:latest
Агент: REPOSITORY   TAG       SIZE
       myapp        latest    287MB

Ты: Хорошо. Теперь запусти и проверь /api/health и главную.
Агент: docker run -d -p 8080:80 --name myapp-test myapp:latest
Агент: curl -s http://localhost:8080/api/health
Агент: {"status":"ok"}
Агент: curl -s -o /dev/null -w "%{http_code}" http://localhost:8080/
Агент: 200

Ты: Проверь, что внутри контейнера нет .env.
Агент: docker exec myapp-test find / -name ".env" 2>/dev/null
Агент: [пустой вывод]
```

## 5. Коммит

```bash
git add Dockerfile .dockerignore nginx.conf
git commit -m "infra: add multi-stage Dockerfile for Python + Node app"
```

## 6. Рефлексия

- Сработало: явное ограничение «без .env и секретов» помогло поймать утечку на раннем этапе.
- Первый тупик: агент забыл про `.dockerignore` и тащил `.env` в контекст сборки. `.dockerignore` — обязательная пара к Dockerfile.
- Второй тупик: первая версия не была multi-stage. Нужно было сразу сказать «три стадии», а не надеяться, что агент сам угадает.
- Третий тупик: образ раздулся из-за не-slim базы. Размер — тоже проверка; 1.4 ГБ это сигнал, что что-то лишнее.
- Можно лучше: сразу показать структуру папок и пример `nginx.conf`, чтобы агент не придумывал маршруты.

## Мини-вывод

Docker с агентом — это не про «сгенерируй Dockerfile и забудь». Образ нужно собрать, запустить и залезть внутрь. Multi-stage и `.dockerignore` стоит озвучивать заранее, потому что агент часто пишет «работающий» образ, который тянет за собой половину окружения разработки.

Какие паттерны здесь работали — см. [`06-prompt-patterns.md`](../06-prompt-patterns.md).

Следующий пример: добавление CI/CD — [`infra-ci.md`](infra-ci.md).
