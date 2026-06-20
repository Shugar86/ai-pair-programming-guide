# 13. Git и GitHub: страховка для экспериментов

Git — это страховка, которая позволяет тебе и агенту пробовать идеи без страха. Ты решаешь, что попадает в коммит, а не агент.

---

## Что такое git и GitHub

- **Git** — система контроля версий на твоём компьютере. Она помнит, что изменилось и когда.
- **GitHub** — облачный сервис, куда можно отправить репозиторий, чтобы хранить код и работать вместе.

---

## Создание репозитория

### Локально

```bash
mkdir my-project
cd my-project
git init
git branch -M main
```

В папке появится скрытая директория `.git` — это история проекта.

### На GitHub через веб

1. Открой https://github.com/new
2. Введи имя репозитория, выбери `Public` или `Private`.
3. Не добавляй README и `.gitignore`, если создаёшь локально — сделаешь это сам.

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

В pair programming лучше добавлять файлы по одному. Ты контролируешь, что попадёт в коммит, а не агент.

**Диалог: добавляем только нужный файл**

```text
Ты: Агент поменял три файла, а я хочу закоммитить только один. Как это сделать?
Агент: Используй `git add имя_файла`. Например, `git add src/auth.py`.
Ты: А `git add .` не подойдёт?
Агент: Она добавит всё сразу. В pair programming лучше по одному — так ты точно видишь, что попадает в коммит.
```

### 3. Зафиксировать изменения

```bash
git commit -m "feat: add email validation"
```

Сообщение говорит, что изменилось. Не пиши просто «fix» или «update».

### 4. Посмотреть историю

```bash
git log --oneline
```

### 5. Откатить незакоммиченные изменения

```bash
git checkout -- filename.py   # один файл
git reset --hard HEAD         # всё к последнему коммиту (осторожно!)
```

---

## Работа с GitHub

### Привязать локальный репозиторий

```bash
git remote add origin https://github.com/username/repo.git
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

1. Установить зависимости: `npm install`, `pip install -r requirements.txt` и т.д.
2. Запустить тесты.
3. Открыть проект в редакторе.

---

## Ветки

Ветки — это черновики. Пробуй идею в отдельной ветке, не ломая основной код.

```bash
git checkout -b feature-login
```

После работы:

```bash
git add filename.py
git commit -m "feat: add login form"
git push origin feature-login
```

Затем на GitHub создай Pull Request, чтобы влить изменения в `main`.

---

## Pull Requests

Pull Request — запрос на влитие ветки в `main`. Через PR можно обсудить изменения и прогнать проверки.

### Через веб

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
# или кнопка Merge pull request на GitHub
```

---

## Merge и конфликты

Merge — слияние одной ветки с другой.

```bash
git checkout main
git pull origin main
git merge feature-login
```

### Конфликт

Конфликт возникает, когда одна и та же строка изменена в двух ветках.

Git помечает это так:

```text
<<<<<<< HEAD
старая версия
=======
новая версия
>>>>>>> feature-login
```

Что делать:

1. Открой файл в редакторе.
2. Выбери нужный вариант, удали маркеры.
3. Сохрани файл.
4. `git add <файл>`
5. `git commit -m "merge: resolve conflict"`

Если конфликты пугают — делай ветки короткими и чаще забирай актуальный `main`.

---

## CI/CD — автопроверки

CI/CD запускает проверки и деплой при каждом push. В учебных проектах чаще всего используется CI:

- при push в PR запускаются тесты;
- если тесты падают — PR не вливают;
- линтер проверяет стиль кода.

На GitHub CI настраивается через GitHub Actions — файлы `.github/workflows/*.yml`.

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
git diff --staged          # что уже в коммите
```

### git add -p

Добавь не весь файл, а только выбранный кусок:

```bash
git add -p filename.py
```

Git спросит для каждого куска: добавлять или нет.

---

## GitHub CLI

`gh` упрощает работу с GitHub из терминала.

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

- **Не коммить секреты.** Пароли, API-ключи, `.env` — добавь в `.gitignore`.
- **Не делай force push без крайней нужды.** `git push --force` ломает историю у других.
- **Не коммить всё подряд.** Используй `git add <файл>` и проверяй `git status`.

---

## Практика

1. Создай локальный репозиторий.
2. Добавь файл `README.md`, закоммить его.
3. Создай репозиторий на GitHub и запушь код.
4. Сделай изменение, закоммить и запушь снова.

Когда это работает на автомате — можно спокойно экспериментировать с агентом. Ты контролируешь, что попадает в коммит, а не агент.

---

Предыдущий шаг: подготовь рабочее окружение — [12-setup.md](12-setup.md).

Следующий шаг: разберись, как работать в IDE и терминале — [14-ide-cli-workflow.md](14-ide-cli-workflow.md).
