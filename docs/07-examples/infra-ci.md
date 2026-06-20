# Пример: GitHub Actions CI

**Вердикт:** CI работает только тогда, когда проверяешь его не локально, а настоящим пушем.

**Среда:** Cursor  
**Задача:** Добавить GitHub Actions workflow, который запускает тесты backend и frontend, проверяет линтеры и кэширует зависимости.

---

## 1. Определяем задачу

```text
Ты: Нужен GitHub Actions workflow. Запускается на push в main и на pull_request.
     Две параллельные джобы:
     - backend: установка Python, pip, pytest, flake8;
     - frontend: установка Node, npm ci, lint, test.
     Кэшировать зависимости по lock-файлам. Секреты — через env или secrets, без хардкода.
```

## 2. Согласуем план

```text
Агент: План:
1. Создать .github/workflows/ci.yml.
2. Добавить триггеры push и pull_request.
3. Две джобы: backend и frontend.
4. Кэш pip по requirements.txt и npm по package-lock.json.
5. Проверить синтаксис YAML.

Ты: Ок. pull_request — только на main. Не хардкоди переменные окружения в файл.
```

## 3. Реализация и тупик

Агент создаёт файл. Ты видишь, что ключ кэша npm задан как `package-lock.json`, но фронтенд живёт в `frontend/package-lock.json`.

```text
Ты: Ключ кэша npm смотрит в корень, а lock-файл в frontend/. Поправь путь.
Агент: [исправляет cache-dependency-path: frontend/package-lock.json]
```

Агент коммитит и пушит. Workflow падает на шаге backend-тестов.

```text
Агент: Ошибка: pytest не может подключиться к PostgreSQL.
Ты: У нас в CI должна быть отдельная тестовая БД. Где DATABASE_URL?
Агент: Я взял его из .env.example, но не прокинул в env job.
Ты: Добавь env DATABASE_URL=postgresql://postgres:postgres@localhost:5432/test и подними сервис Postgres.
Агент: [добавляет services.postgres и env]
```

Агент добавляет сервис, но теперь джоба падает с ошибкой: `pull_request` триггер запускает workflow и из форка, а там нет нужного secret для отчётов.

```text
Ты: Для pull_request из форка не используй секрет codecov. Ограничь шаг условием if: github.event_name != 'pull_request' || github.event.pull_request.head.repo.full_name == github.repository.
Агент: [добавляет условие и убирает секрет из форков]
```

## 4. Проверка

```text
Агент: git push origin feature/ci
Агент: [открывает Actions во вкладке GitHub]
Агент: backend и frontend прошли. Кэш hit на обоих джобах.

Ты: Проверь, что кэш действительно работает: перезапусти job и посмотри на время.
Агент: [re-run job]
Агент: Время установки зависимостей упало с 2:10 до 0:18.

Ты: Создай тестовый PR из форка, если есть доступ. Убедись, что секрет не запрашивается.
Агент: PR из форка прошёл без шага codecov.
```

## 5. Коммит

```bash
git add .github/workflows/ci.yml
git commit -m "ci: add GitHub Actions workflow for backend and frontend"
```

## 6. Рефлексия

- Сработало: разделение на две параллельные джобы ускорило feedback. Кэш по lock-файлам реально сократил время.
- Первый тупик: неправильный путь к `package-lock.json`. Кэш промахивался и каждый раз ставил зависимости с нуля.
- Второй тупик: забыл прокинуть `DATABASE_URL` и сервис Postgres. Локально тесты проходили, потому что `.env` был под рукой.
- Третий тупик: секреты в `pull_request` из форка. Условие `if` защитило CI от падений на внешних вкладах.
- Можно лучше: сразу передать агенту пример `.env.example` и сказать, какие переменные нужны в CI, а какие нет.

## Мини-вывод

CI с агентом проходит через несколько итераций: YAML синтаксически верен — это ещё не значит, что pipeline рабочий. Настоящая проверка — push, реальный PR и перезапуск job. Кэш, секреты и сервисы — три места, где агент регулярно промахивается, потому что не видит твоего локального окружения.

Какие паттерны здесь работали — см. [`06-prompt-patterns.md`](../06-prompt-patterns.md).

Следующий шаг: закрепи навыки на практике — [`08-exercises.md`](../08-exercises.md).
