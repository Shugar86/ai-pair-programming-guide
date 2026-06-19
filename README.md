# AI Pair Programming — создавай вместе с агентом

Этот гайд не учит нажимать кнопку «сделай за меня». Он учит работать с Cursor, Kimi Code, Claude Code и другими агентами как с напарником: ты держишь направление, агент помогает писать, проверять и не тупить.

> **Суть:** AI — усилитель твоего мышления, не замена.

---

## Кому этот гайд

- **Новичок.** Ты только открыл AI-редактор. Начни с установки окружения и первой сессии.  
  Путь: [`docs/12-setup.md`](docs/12-setup.md) → [`docs/16-ai-for-beginners.md`](docs/16-ai-for-beginners.md) → [`docs/04-workflow.md`](docs/04-workflow.md).
- **Практик.** Уже пишешь код — хочешь работать с агентом быстрее и чище.  
  Путь: [`docs/01-what-is-pair-programming.md`](docs/01-what-is-pair-programming.md) → [`docs/03-principles.md`](docs/03-principles.md) → [`docs/06-prompt-patterns.md`](docs/06-prompt-patterns.md) → [`docs/07-examples/`](docs/07-examples/).
- **Лид.** Решаешь, как команда будет использовать AI, и не хочешь получить лапшу в репозитории.  
  Путь: [`docs/11-advanced-scenarios.md`](docs/11-advanced-scenarios.md) → [`docs/09-checklists.md`](docs/09-checklists.md) → [`docs/13-git-github.md`](docs/13-git-github.md).

Каждый путь — свой, но принципы одни.

## Почему это про создание, а не про дисциплину

Правила здесь — не табель. Они ограничивают хаос, чтобы освободить место для творчества.  
Когда ты знаешь, кто ведёт, что проверять и куда идти, агент перестаёт быть помехой и становится рабочей рукой.

Пример: ты хочешь добавить тёмную тему в приложение. Без рамок агент может переписать половину CSS, втащить новую библиотеку и сломать формы. С рамками ты говоришь: «Только CSS-переменные, никаких новых зависимостей, проверь обе темы на трёх экранах». Получаешь результат, а не археологию.

## Как это звучит

**Диалог 1. Слишком сложно.**

```text
Ты: Добавь сортировку заказов по дате в личном кабинете.
Агент: Можно взять Elasticsearch, настроить индексы и добавить фильтры в реальном времени.
Ты: Стоп. Пока просто сортируем по убыванию даты в уже загруженном списке. Без новых сервисов.
Агент: Ок, добавляю sort() в запрос и UI-таблицу.
```

**Диалог 2. Ты ведёшь.**

```text
Ты: Нужно исправить баг: при пустом email падает валидация.
Агент: План: проверить input, выбросить кастомное исключение, обернуть форму в try/catch.
Ты: Нет. Просто верни null и покажи сообщение под полем. Меньше кода — меньше ошибок.
Агент: Понял. Меняю только обработку пустого значения.
```

## Что внутри

- [`docs/01-what-is-pair-programming.md`](docs/01-what-is-pair-programming.md) — что такое pair programming с AI: два мозга делают одну вещь.
- [`docs/02-agent-as-pair-programmer.md`](docs/02-agent-as-pair-programmer.md) — кто за что отвечает: ты vs агент.
- [`docs/03-principles.md`](docs/03-principles.md) — 8 принципов, которые работают в любой среде.
- [`docs/04-workflow.md`](docs/04-workflow.md) — рабочая петля от задачи до коммита.
- [`docs/05-environments.md`](docs/05-environments.md) — особенности Cursor, Kimi, Claude, OpenCode, Copilot. Официальные сайты: [Cursor](https://www.cursor.com/), [Claude Code](https://docs.anthropic.com/en/docs/agents-and-tools/claude-code/overview), [Kimi Code](https://www.moonshot.cn/).
- [`docs/06-prompt-patterns.md`](docs/06-prompt-patterns.md) — шаблоны запросов, которые экономят время.
- [`docs/07-examples/`](docs/07-examples/) — реальные текстовые сессии.
- [`docs/08-exercises.md`](docs/08-exercises.md) — практические задания.
- [`docs/09-checklists.md`](docs/09-checklists.md) — чеклисты на каждом этапе.
- [`docs/10-antipatterns.md`](docs/10-antipatterns.md) — антипаттерны работы с AI.
- [`docs/11-advanced-scenarios.md`](docs/11-advanced-scenarios.md) — продвинутые сценарии и рабочие кейсы.
- [`docs/12-setup.md`](docs/12-setup.md) — что скачать, как установить агентов, git, пакеты и стек.
- [`docs/13-git-github.md`](docs/13-git-github.md) — основы git и GitHub: clone, commit, PR, merge, CI/CD.
- [`docs/14-ide-cli-workflow.md`](docs/14-ide-cli-workflow.md) — как работать в IDE и в терминале.
- [`docs/15-troubleshooting.md`](docs/15-troubleshooting.md) — что делать, если ничего не получается: WSL, SSH, VDS, откаты.
- [`docs/16-ai-for-beginners.md`](docs/16-ai-for-beginners.md) — как показать задачу нейросети и что делать, если ничего непонятно.
- [`templates/`](templates/) — шаблоны `AGENTS.md`, ADR и карточки сессии для твоих проектов.

## Быстрый старт

1. Открой проект в редакторе с AI.
2. Опиши задачу одним предложением, которое можно проверить.
3. Скажи агенту: «Сначала план, потом код. Не трогай весь проект.»
4. Выбери минимальный шаг.
5. Реализуй: агент пишет, ты читаешь diff.
6. Проверь тесты, diff, здравый смысл.
7. Коммить с сообщением, которое объясняет, что изменилось.

Подробности — в [`docs/04-workflow.md`](docs/04-workflow.md).

## Если ничего непонятно

Начни с [`docs/16-ai-for-beginners.md`](docs/16-ai-for-beginners.md). Там разобрано, как показать задачу нейросети, что делать, когда агент не понял, и как не утонуть в ответе.  
Если техническое окружение ломается — иди в [`docs/15-troubleshooting.md`](docs/15-troubleshooting.md).

## Лицензия

MIT — свободно копируй, переделывай, используй в учебе и работе.
