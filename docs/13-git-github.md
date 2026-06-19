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
```

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

Следующий шаг: попробуй первую сессию pair programming по [`04-workflow.md`](04-workflow.md).
