# 13. Git и GitHub: минимум для pair programming

AI-агент может писать код, но сохранять историю, ветки и публикацию контролируешь ты. Этот раздел даёт минимальный набор команд, без которых pair programming превращается в хаос.

---

## Что такое git и GitHub

- **Git** — система контроля версий на твоём компьютере. Она запоминает, что и когда изменилось, и позволяет откатиться.
- **GitHub** — облачный сервис, куда можно отправить git-репозиторий, чтобы хранить код, делиться им и работать в команде.

---

## Создание репозитория

### Локально

```bash
mkdir my-project
cd my-project
git init
git branch -M main
```

Теперь в папке появилась скрытая директория `.git` — это история проекта.

### На GitHub через веб

1. Зайди на https://github.com/new
2. Введи имя репозитория, выбери `Public` или `Private`.
3. Не добавляй README или .gitignore, если создаёшь локально — сделаешь это сам.

---

## Базовый рабочий цикл

### 1. Посмотреть, что изменилось

```bash
git status
```

### 2. Добавить файлы в будущий коммит

```bash
git add filename.py          # один файл
git add src/                 # папка
git add .                    # всё текущее (осторожно!)
```

> **Совет:** в pair programming используй `git add <конкретный файл>`, чтобы не закоммитить случайные изменения агента.

### 3. Зафиксировать изменения

```bash
git commit -m "feat: add email validation"
```

Сообщение должно говорить, что изменилось, а не просто «fix» или «update».

### 4. Посмотреть историю

```bash
git log --oneline
```

### 5. Откатить незакоммиченные изменения

```bash
git checkout -- filename.py   # откатить один файл
git reset --hard HEAD         # откатить всё (осторожно!)
```

---

## Работа с GitHub

### Привязать локальный репозиторий к GitHub

```bash
git remote add origin https://github.com/username/repo.git
git branch -M main
git push -u origin main
```

### Отправить изменения

```bash
git push origin main
```

### Забрать изменения

```bash
git pull origin main
```

### Склонировать чужой репозиторий

```bash
git clone https://github.com/username/repo.git
cd repo
```

После клонирования обычно нужно:

1. Установить зависимости (`npm install`, `pip install -r requirements.txt` и т.д.).
2. Запустить тесты, чтобы убедиться, что всё работает.
3. Открыть проект в редакторе и начать работу.

---

## Ветки

Ветки позволяют экспериментировать, не ломая основной код.

```bash
git branch feature-login       # создать ветку
git checkout feature-login     # переключиться на неё
# или одной командой:
git checkout -b feature-login
```

После работы:

```bash
git add .
git commit -m "feat: add login form"
git push origin feature-login
```

Затем на GitHub можно создать Pull Request, чтобы влить изменения в `main`.

---

## Pull Requests

Pull Request (PR) — это запрос на влитие твоей ветки в `main`. Через PR можно обсудить изменения и прогнать проверки до того, как они попадут в основную ветку.

### Через веб-интерфейс

1. Запушь ветку: `git push origin feature-login`.
2. Открой репозиторий на GitHub.
3. Нажми **Compare & pull request**.
4. Напиши заголовок и описание: что изменилось и зачем.
5. Нажми **Create pull request**.

### Через GitHub CLI

```bash
gh pr create --title "feat: add login" --body "What changed and why"
```

### После approve

```bash
gh pr merge
# или нажми Merge pull request на GitHub
```

---

## Merge и конфликты

**Merge** — слияние одной ветки с другой. Обычно вливаешь свою feature-ветку в `main`.

```bash
git checkout main
git pull origin main
git merge feature-login
```

### Конфликт

Конфликт возникает, когда одна и та же строка изменена в обеих ветках. Git не может сам решить, какой вариант правильный.

**Признаки:**

```text
<<<<<<< HEAD
старая версия
=======
новая версия
>>>>>>> feature-login
```

**Что делать:**

1. Открой файл в редакторе.
2. Выбери нужный вариант, удали маркеры `<<<<<<<`, `=======`, `>>>>>>>`.
3. Сохрани файл.
4. `git add <файл>`
5. `git commit -m "merge: resolve conflict"`

Если боишься конфликтов — делай ветки короткими и чаще забирай актуальный `main`.

---

## CI/CD — что это

CI/CD (Continuous Integration / Continuous Deployment) — автоматические проверки и деплой при каждом push.

В учебных проектах чаще всего используется **CI**:

- при push в PR запускаются тесты;
- если тесты падают — PR не вливают, пока не починят;
- линтер проверяет стиль кода.

На GitHub CI настраивается через **GitHub Actions** — файлы `.github/workflows/*.yml` в репозитории.

```yaml
# Пример .github/workflows/ci.yml
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

Если CI красный — смотри логи, исправляй ошибки, push снова.

---

## Просмотр изменений перед коммитом

### git diff

```bash
git diff                    # что изменилось, но ещё не добавлено
git diff --staged          # что уже добавлено в коммит
```

### git add -p

Позволяет добавить не весь файл, а только выбранные куски:

```bash
git add -p filename.py
```

Git будет спрашивать для каждого куска: добавлять или нет.

---

## GitHub CLI

GitHub CLI (`gh`) упрощает работу с GitHub из терминала.

### Создать репозиторий и запушить

```bash
cd my-project
gh repo create my-project --public --source=. --remote=origin --push
```

### Посмотреть информацию о репозитории

```bash
gh repo view username/repo
```

### Создать Pull Request

```bash
gh pr create --title "feat: add login" --body "What changed and why"
```

---

## Что не делать

- **Не коммить секреты:** пароли, API-ключи, `.env` — добавь их в `.gitignore`.
- **Не делай force push** без крайней необходимости: `git push --force` ломает историю у других.
- **Не коммить всё подряд:** используй `git add <файл>` и проверяй `git status`.

---

## Практика

1. Создай локальный репозиторий.
2. Добавь файл `README.md`, закоммить его.
3. Создай репозиторий на GitHub и запушь код.
4. Сделай изменение в файле, закоммить и снова запушь.

Когда это работает на автомате — можно спокойно работать с агентом: ты контролируешь, что попадает в коммит, а не агент.

---

Следующие шаги:
- Попробуй первую сессию pair programming — [`04-workflow.md`](04-workflow.md).
- Разберись, как работать в IDE и терминале — [`14-ide-cli-workflow.md`](14-ide-cli-workflow.md).
- Если что-то пошло не так — [`15-troubleshooting.md`](15-troubleshooting.md).
