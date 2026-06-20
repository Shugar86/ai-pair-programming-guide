# 12. Путь от нуля до первой сессии

Установка — не цель, а подготовка. Шесть шагов, после которых ты откроешь редактор и попробуешь первую сессию pair programming.

---

## Что понадобится

1. Компьютер с Windows, macOS или Linux.
2. Редактор кода с AI-агентом.
3. Git.
4. Аккаунт на GitHub.
5. Интерпретатор или компилятор под твой стек: Node.js, Python, Go, Rust и т.д.

---

## Шаг 1. Редактор с AI-агентом

Выбирай любой. Принципы гайда работают везде.

### Cursor

- **Что это:** IDE на базе VS Code со встроенным агентом.
- **Где скачать:** https://www.cursor.com/
- **Что нужно:** аккаунт Cursor, можно войти через GitHub.
- **После установки:** открой проект, нажми `Cmd/Ctrl + L` — откроется чат.
- **Стоимость:** бесплатный тариф с лимитами; платный — от $20/мес.

Пример первого запроса:

```text
Привет. Это мой проект. Объясни, из чего он состоит, и предложи, что можно улучшить.
```

### Claude Code

- **Что это:** терминальный ассистент от Anthropic.
- **Где скачать:** https://claude.ai/code
- **Что нужно:** аккаунт Anthropic, подписка Pro или API-ключ.
- **После установки:** зайди в папку проекта и запусти `claude`.
- **Когда выбирать:** большие проекты, сервер по SSH, минимум интерфейса.

### Kimi Code

- **Что это:** ассистент от Moonshot AI.
- **Где скачать:** https://kimi.moonshot.cn/
- **Что нужно:** аккаунт Moonshot AI.
- **После установки:** плагин в IDE или отдельный клиент по инструкции.
- **Примечание:** формат клиента меняется — сверяйся с актуальной документацией.

### OpenCode

- **Что это:** открытый ассистент с несколькими провайдерами.
- **Где скачать:** https://opencode.ai/
- **Что нужно:** установить OpenCode и настроить провайдера через `opencode.json`.
- **После установки:** запусти в папке проекта и начни диалог.
- **Плюс:** можно использовать свои API-ключи и локальные модели.

### GitHub Copilot

- **Что это:** ассистент от GitHub, встроенный в редактор.
- **Где скачать:** https://github.com/features/copilot — плагин для VS Code, JetBrains, Neovim.
- **Что нужно:** аккаунт GitHub, подписка Copilot (студентам — бесплатно).
- **После установки:** авторизуй плагин и пиши код.

### Cody

- **Что это:** ассистент от Sourcegraph с поиском по коду.
- **Где скачать:** https://sourcegraph.com/cody
- **Что нужно:** аккаунт Sourcegraph, плагин для редактора.

Не знаешь, с чего начать — бери Cursor или VS Code + Copilot. Там проще увидеть, что происходит.

---

## Шаг 2. Git

Git запоминает, что и когда изменилось, и позволяет откатываться. Без него агент может написать код, а ты потеряешь рабочую версию.

### Установка

- **Windows:** https://git-scm.com/download/win
- **macOS:** `xcode-select --install` или `brew install git`
- **Linux:** `sudo apt install git` (Debian/Ubuntu) или `sudo dnf install git` (Fedora)

### Проверка

```bash
git --version
```

Должно вывести что-то вроде `git version 2.43.0`.

### Базовая настройка

```bash
git config --global user.name "Твоё Имя"
git config --global user.email "you@example.com"
```

### Если git не найден

1. Перезапусти терминал.
2. На Windows используй Git Bash — он идёт в комплекте.
3. Если не помогло — перезагрузи компьютер.

Больше про проблемы — в [`15-troubleshooting.md`](15-troubleshooting.md).

---

## Шаг 3. GitHub

GitHub — облачное хранилище для git-репозиториев.

1. Регистрация: https://github.com/signup
2. GitHub CLI (опционально, но удобно): https://cli.github.com/
3. Проверка: `gh --version`
4. Авторизация: `gh auth login`

---

## Шаг 4. Стек проекта

Установи язык, на котором пишешь:

- **JavaScript / TypeScript:** Node.js с https://nodejs.org/ (бери LTS).
- **Python:** https://www.python.org/downloads/
- **Go:** https://go.dev/dl/
- **Rust:** https://www.rust-lang.org/tools/install
- **Java:** Eclipse Temurin или Amazon Corretto.

Проверь:

```bash
node --version
python3 --version
go version
rustc --version
```

**Диалог: проверяем Node.js**

```text
Ты: Как проверить, установлен ли Node.js?
Агент: Открой терминал и запусти `node --version`. Если видишь номер версии — всё ок.
Ты: А если терминал пишет «command not found»?
Агент: Значит, Node.js ещё не установлен. Скачай LTS-версию с nodejs.org и перезапусти терминал.
```

---

## Шаг 5. Пакеты и зависимости проекта

Почти любой проект использует библиотеки. Вот как их ставить.

### JavaScript / TypeScript

```bash
npm install
# или
yarn install
# или
pnpm install
```

### Python

```bash
pip install -r requirements.txt
# или
poetry install
```

### Rust

```bash
cargo build
```

### Go

```bash
go mod download
```

### Системные пакеты

```bash
sudo apt update && sudo apt install <название-пакета>   # Debian/Ubuntu
sudo dnf install <название-пакета>                      # Fedora
brew install <название-пакета>                          # macOS
```

Если команда падает — сначала проверь, что менеджер пакетов установлен. Подробнее — в [`15-troubleshooting.md`](15-troubleshooting.md).

---

## Шаг 6. Проверка готовности

Перед первой сессией убедись:

- Редактор с агентом запускается.
- `git --version` показывает версию.
- Аккаунт на GitHub создан.
- Стек проекта установлен.
- Пакеты проекта устанавливаются без ошибок.

Когда всё на месте — открывай проект и пробуй первую сессию.

---

Предыдущий шаг: разберись с продвинутыми сценариями — [11-advanced-scenarios.md](11-advanced-scenarios.md).

Следующий шаг: научись фиксировать изменения в git — [13-git-github.md](13-git-github.md).
