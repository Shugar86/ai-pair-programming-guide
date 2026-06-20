# VibeCraft Rewrite Implementation Plan

**Goal:** Переписать все `.md`-файлы гайда и добавить `docs/17-future.md` так, чтобы гайд звучал как приглашение создавать вместе с AI: продвинуто, понятно, без душнилы, с реальными примерами, ссылками и взглядом на 2+ года.

> **For agentic workers:** REQUIRED SUB-SKILL: Use `superpowers:subagent-driven-development` to implement this plan task-by-task. Steps use checkbox (`- [ ]`) syntax for tracking.

**Architecture:** Сохраняем текущую структуру из 16 файлов, добавляем 17-й. Каждый файл переписывается целиком с единым голосом: прямое «ты», конкретные диалоги, ссылки, короткий вердикт первым. Шаблоны обновляются под тот же голос.

**Tech Stack:** Markdown, git. Проверка — вручную: чтение первых абзацев, поиск запрещённых фраз, карта ссылок.

---

## Общий голос (эталон для всех задач)

Тон: `creative-partner`. Продвинутый друг, который показывает, как не наломать дров.

**Делать:**
- Прямое «ты».
- Короткие предложения.
- Каждая абстракция — с примером или диалогом.
- Вердикт первым, детали потом.
- Ссылки на официальные доки или другие разделы гайда.

**Не делать:**
- Официоз: призывы действовать вместе, безличные модальные глаголы, вводные про «важность понимания».
- Морализаторство.
- Маркетинговый пафос.
- Голые списки без контекста.

**Пример старого vs нового голоса:**

Старый:
```text
AI-редакторы уже умеют писать код. Но код, который они пишут без твоего контроля, быстро превращается в лапшу.
```

Новый:
```text
Агенты пишут код быстро. Но если ты не держишь руль, они быстро наворачивают архитектуру, которую никто не просил. Этот гайд — про то, как использовать AI так, чтобы он усиливал тебя, а не мешал думать.
```

---

## Task 1: Rewrite README.md

**Files:**
- Modify: `README.md`

**Requirements:**
- Сделать README манифестом.
- Три входа для аудиторий: новичок / практик / лид.
- Объяснить, почему гайд про творчество, а не про дисциплину.
- Сохранить список разделов, но добавить пути для разных аудиторий.
- 1–2 диалога «ты — агент».

**Anchor content (начало README):**
```markdown
# AI Pair Programming — создавай вместе с агентом

Этот гайд не учит нажимать кнопку «сделай за меня». Он учит работать с Cursor, Kimi Code, Claude Code и другими агентами как с напарником: ты держишь направление, агент помогает писать, проверять и не тупить.

> **Суть:** AI — усилитель твоего мышления, не замена.

---

## Кому этот гайд

- **Новичок.** Ты только открыл AI-редактор. Начни с установки окружения и первой сессии.
- **Практик.** Уже пишешь код — хочешь работать с агентом быстрее и чище.
- **Лид.** Решаешь, как команда будет использовать AI, и не хочешь получить лапшу в репозитории.

Каждый путь — свой, но принципы одни.
```

- [ ] **Step 1: Read spec sections 1–5 and existing README.md**
- [ ] **Step 2: Write new README.md with the three-audience structure and creative-partner voice**
- [ ] **Step 3: Verify**

Run:
```bash
cd /home/shugar/dev/ai-pair-programming-guide
grep -c "давайте\|необходимо\|следует\|важно понимать" README.md || true
```
Expected: 0 (or only inside code blocks).

- [ ] **Step 4: Commit**

```bash
git add README.md
git commit -m "docs: rewrite README in creative-partner vibe"
```

---

## Task 2: Rewrite docs/01-what-is-pair-programming.md

**Files:**
- Modify: `docs/01-what-is-pair-programming.md`

**Requirements:**
- Переформулировать pair programming как совместное мышление.
- Новая метафора: «два мозга делают одну вещь», а не «ты водитель — агент навигатор».
- Убрать морализаторство.
- Сохранить разделы: классическое, AI как напарник, что это не такое, метафора.
- Добавить диалог, где агент предлагает слишком сложное, а ты возвращаешь к простому.

- [ ] **Step 1: Read existing file and spec section 5 (01 row)**
- [ ] **Step 2: Rewrite with new metaphor and creative-partner voice**
- [ ] **Step 3: Verify no forbidden phrases and at least one dialogue**
- [ ] **Step 4: Commit**

```bash
git add docs/01-what-is-pair-programming.md
git commit -m "docs: rewrite 01-what-is-pair-programming in creative-partner vibe"
```

---

## Task 3: Rewrite docs/02-agent-as-pair-programmer.md

**Files:**
- Modify: `docs/02-agent-as-pair-programmer.md`

**Requirements:**
- Фокус на co-creation.
- Обязанности ты/агент — без бюрократического тона.
- Когда ты ведёшь, когда агент.
- Границы: что не делегируешь, что агент не должен делать.
- Намёк на multi-agent в конце.
- 2 диалога.

- [ ] **Step 1: Read existing file and spec section 5 (02 row)**
- [ ] **Step 2: Rewrite with co-creation framing**
- [ ] **Step 3: Verify at least two dialogues and link to 03-principles.md**
- [ ] **Step 4: Commit**

```bash
git add docs/02-agent-as-pair-programmer.md
git commit -m "docs: rewrite 02-agent-as-pair-programmer in creative-partner vibe"
```

---

## Task 4: Rewrite docs/03-principles.md

**Files:**
- Modify: `docs/03-principles.md`

**Requirements:**
- 8 принципов оставить, но подать как творческие ограничения.
- К каждому принципу добавить: «что это даёт творчески».
- Примеры промптов оставить, но сделать их естественнее.
- Добавить диалог или сценарий к каждому принципу.

- [ ] **Step 1: Read existing file and spec section 5 (03 row)**
- [ ] **Step 2: Rewrite all 8 principles with creative framing**
- [ ] **Step 3: Verify each principle has example + "creative payoff"**
- [ ] **Step 4: Commit**

```bash
git add docs/03-principles.md
git commit -m "docs: rewrite 03-principles in creative-partner vibe"
```

---

## Task 5: Rewrite docs/04-workflow.md

**Files:**
- Modify: `docs/04-workflow.md`

**Requirements:**
- Петля как прототипирование: идея → план → минимум → проверка → рефлексия.
- Меньше ритуала, больше создания.
- Сохранить 6 шагов, но переименовать/переформулировать под созидание.
- Реальный пример сессии с тупиком и выходом.

- [ ] **Step 1: Read existing file and spec section 5 (04 row)**
- [ ] **Step 2: Rewrite workflow as creative loop**
- [ ] **Step 3: Verify example includes a stuck-and-recover moment**
- [ ] **Step 4: Commit**

```bash
git add docs/04-workflow.md
git commit -m "docs: rewrite 04-workflow in creative-partner vibe"
```

---

## Task 6: Rewrite docs/05-environments.md

**Files:**
- Modify: `docs/05-environments.md`

**Requirements:**
- Среды как инструменты под разные задачи.
- Cursor — визуальная работа, Kimi/Claude — большие проекты и серверы, Copilot/Cody — моментальная помощь.
- Каждая среда: когда выбирать, как начать, на что обратить внимание.
- Добавить ссылки на официальные сайты.

- [ ] **Step 1: Read existing file and spec section 5 (05 row)**
- [ ] **Step 2: Rewrite environments as tool selection guide**
- [ ] **Step 3: Verify all 5 environments have links and use-case framing**
- [ ] **Step 4: Commit**

```bash
git add docs/05-environments.md
git commit -m "docs: rewrite 05-environments in creative-partner vibe"
```

---

## Task 7: Rewrite docs/06-prompt-patterns.md

**Files:**
- Modify: `docs/06-prompt-patterns.md`

**Requirements:**
- Промпты как креативные брифы.
- 8 шаблонов оставить, но переименовать/переформулировать.
- Каждый шаблон: когда использовать, пример, почему работает.
- Добавить раздел «как комбинировать».

- [ ] **Step 1: Read existing file and spec section 5 (06 row)**
- [ ] **Step 2: Rewrite prompts as creative briefs**
- [ ] **Step 3: Verify all 8 patterns have use-case + example + combination note**
- [ ] **Step 4: Commit**

```bash
git add docs/06-prompt-patterns.md
git commit -m "docs: rewrite 06-prompt-patterns in creative-partner vibe"
```

---

## Task 8: Rewrite docs/07-examples/

**Files:**
- Modify: `docs/07-examples/cursor-feature.md`
- Modify: `docs/07-examples/claude-refactor.md`
- Modify: `docs/07-examples/kimi-bugfix.md`

**Requirements:**
- Сделать сессии живыми.
- Не только успех, но и тупик, откат, уточнение.
- Каждый пример: среда, задача, диалог, diff, проверка, рефлексия.
- Добавить мини-вывод в конце каждого.

- [ ] **Step 1: Read all three example files and spec section 5 (07 row)**
- [ ] **Step 2: Rewrite each example with failure-recovery arc**
- [ ] **Step 3: Verify each example has reflection and realistic dialogue**
- [ ] **Step 4: Commit**

```bash
git add docs/07-examples/
git commit -m "docs: rewrite 07-examples with realistic failure-recovery arcs"
```

---

## Task 9: Rewrite docs/08-exercises.md

**Files:**
- Modify: `docs/08-exercises.md`

**Requirements:**
- Упражнения как мини-проекты.
- Для каждого: уровень, задача, что делать, критерий успеха.
- Связать с принципами (03) и workflow (04).
- Добавить упражнение про multi-agent или проектирование с агентом.

- [ ] **Step 1: Read existing file and spec section 5 (08 row)**
- [ ] **Step 2: Rewrite exercises as mini-projects with measurable outcomes**
- [ ] **Step 3: Verify each exercise links to principles or workflow**
- [ ] **Step 4: Commit**

```bash
git add docs/08-exercises.md
git commit -m "docs: rewrite 08-exercises as mini-projects"
```

---

## Task 10: Rewrite docs/09-checklists.md

**Files:**
- Modify: `docs/09-checklists.md`

**Requirements:**
- Чеклисты как pre-flight checks.
- Тон: «проверь перед стартом», а не «правила, которые надо соблюдать».
- 4 чеклиста: перед сессией, перед принятием изменений, перед коммитом, перед показом.
- Стоп-сигналы — как повод остановиться и пересобрать.

- [ ] **Step 1: Read existing file and spec section 5 (09 row)**
- [ ] **Step 2: Rewrite checklists as pre-flight checks**
- [ ] **Step 3: Verify tone is helper-like, not bureaucratic**
- [ ] **Step 4: Commit**

```bash
git add docs/09-checklists.md
git commit -m "docs: rewrite 09-checklists as pre-flight checks"
```

---

## Task 11: Rewrite docs/10-antipatterns.md

**Files:**
- Modify: `docs/10-antipatterns.md`

**Requirements:**
- Антипаттерны как ловушки скорости.
- 8 антипаттернов оставить, но подать через призму «когда творишь быстро, легко свалиться».
- Каждый: симптом, что ломается, как ловить, пример промпта.
- Стоп-сигналы — как триггер для паузы.

- [ ] **Step 1: Read existing file and spec section 5 (10 row)**
- [ ] **Step 2: Rewrite antipatterns as creative traps**
- [ ] **Step 3: Verify each antipattern has symptom + fix + prompt example**
- [ ] **Step 4: Commit**

```bash
git add docs/10-antipatterns.md
git commit -m "docs: rewrite 10-antipatterns as creative traps"
```

---

## Task 12: Rewrite docs/11-advanced-scenarios.md

**Files:**
- Modify: `docs/11-advanced-scenarios.md`

**Requirements:**
- Оркестрация агентов, легаси, миграции, проектирование.
- Для лидов: как держать несколько проектов и агентов одновременно.
- Добавить секцию «multi-project context management».
- Сохранить ADR-шаблон ссылку.

- [ ] **Step 1: Read existing file and spec section 5 (11 row)**
- [ ] **Step 2: Rewrite advanced scenarios with orchestration and multi-project focus**
- [ ] **Step 3: Verify multi-agent and multi-project sections exist**
- [ ] **Step 4: Commit**

```bash
git add docs/11-advanced-scenarios.md
git commit -m "docs: rewrite 11-advanced-scenarios with orchestration focus"
```

---

## Task 13: Rewrite docs/12-setup.md

**Files:**
- Modify: `docs/12-setup.md`

**Requirements:**
- Чёткий путь от нуля до первой сессии.
- Для новичков: где скачать, как установить, как проверить.
- Ссылки на официальные сайты.
- Не сюсюкать, но не бросать в болото.

- [ ] **Step 1: Read existing file and spec section 5 (12 row)**
- [ ] **Step 2: Rewrite setup as clear onboarding path**
- [ ] **Step 3: Verify all download links are present and verification commands included**
- [ ] **Step 4: Commit**

```bash
git add docs/12-setup.md
git commit -m "docs: rewrite 12-setup as clear onboarding path"
```

---

## Task 14: Rewrite docs/13-git-github.md

**Files:**
- Modify: `docs/13-git-github.md`

**Requirements:**
- Git как страховка творческих экспериментов.
- Минимум команд, максимум пользы.
- Сохранить основные команды, но убрать учительский тон.
- Акцент: ты контролируешь, что попадает в коммит, а не агент.

- [ ] **Step 1: Read existing file and spec section 5 (13 row)**
- [ ] **Step 2: Rewrite git guide as safety net for experiments**
- [ ] **Step 3: Verify essential commands remain and tone is partner-like**
- [ ] **Step 4: Commit**

```bash
git add docs/13-git-github.md
git commit -m "docs: rewrite 13-git-github as creative safety net"
```

---

## Task 15: Rewrite docs/14-ide-cli-workflow.md

**Files:**
- Modify: `docs/14-ide-cli-workflow.md`

**Requirements:**
- Реалистичный рабочий день без идеализации.
- IDE vs CLI: когда что.
- Как показывать код агенту в каждой среде.
- Горячие клавиши и layout.

- [ ] **Step 1: Read existing file and spec section 5 (14 row)**
- [ ] **Step 2: Rewrite IDE/CLI workflow realistically**
- [ ] **Step 3: Verify comparison table and hotkeys remain useful**
- [ ] **Step 4: Commit**

```bash
git add docs/14-ide-cli-workflow.md
git commit -m "docs: rewrite 14-ide-cli-workflow realistically"
```

---

## Task 16: Rewrite docs/15-troubleshooting.md

**Files:**
- Modify: `docs/15-troubleshooting.md`

**Requirements:**
- Чеклист действий, когда всё сломалось.
- Спокойный, не панический тон.
- Разделы: git, агент не видит проект, command not found, пакеты, WSL, SSH, VDS, агент навредил, nuclear option.
- Когда звать человека.

- [ ] **Step 1: Read existing file and spec section 5 (15 row)**
- [ ] **Step 2: Rewrite troubleshooting as calm action checklist**
- [ ] **Step 3: Verify all original problem sections are covered and tone is calm**
- [ ] **Step 4: Commit**

```bash
git add docs/15-troubleshooting.md
git commit -m "docs: rewrite 15-troubleshooting as calm action checklist"
```

---

## Task 17: Rewrite docs/16-ai-for-beginners.md

**Files:**
- Modify: `docs/16-ai-for-beginners.md`

**Requirements:**
- Первая беседа с агентом.
- Как объяснить задачу, если ничего непонятно.
- Как не утонуть в ответе.
- Как перефразировать, когда агент не понял.
- Как ловить галлюцинации.
- Примеры стартовых запросов.

- [ ] **Step 1: Read existing file and spec section 5 (16 row)**
- [ ] **Step 2: Rewrite beginner guide as first conversation**
- [ ] **Step 3: Verify examples include rephrase, simplification, and hallucination checks**
- [ ] **Step 4: Commit**

```bash
git add docs/16-ai-for-beginners.md
git commit -m "docs: rewrite 16-ai-for-beginners as first conversation"
```

---

## Task 18: Create docs/17-future.md

**Files:**
- Create: `docs/17-future.md`

**Requirements:**
- Новый файл.
- Куда движется область через 2+ года.
- Темы:
  - Агенты как члены команды (skills, memory, persona).
  - Длинный контекст и большие codebase.
  - Multi-agent и оркестрация.
  - Модели с рассуждением (reasoning).
  - Управление несколькими проектами одновременно.
  - Что не изменится: ты всё ещё принимаешь решения.
- Ссылки на существующие разделы (11-advanced, 03-principles).
- Тон: продвинуто, но без фантастики.

- [ ] **Step 1: Read spec section 5 (17 row) and 11-advanced-scenarios.md**
- [ ] **Step 2: Write docs/17-future.md with forward-looking but grounded perspective**
- [ ] **Step 3: Verify all 6 topic areas are covered and links to existing docs exist**
- [ ] **Step 4: Commit**

```bash
git add docs/17-future.md
git commit -m "docs: add 17-future.md with 2+ year perspective"
```

---

## Task 19: Update templates/AGENTS.md

**Files:**
- Modify: `templates/AGENTS.md`

**Requirements:**
- Обновить под creative-partner voice.
- Добавить блок про creativity/scope: «агент помогает создавать, но не решает за тебя».
- Сохранить практичность: стек, правила, git, запрещено, контакты.
- Сделать шаблон заполняемым без сюсюканья.

- [ ] **Step 1: Read existing template and spec section 6**
- [ ] **Step 2: Rewrite AGENTS.md template with creative-partner tone**
- [ ] **Step 3: Verify all original fields remain and creativity/scope block added**
- [ ] **Step 4: Commit**

```bash
git add templates/AGENTS.md
git commit -m "docs: update AGENTS.md template for creative-partner vibe"
```

---

## Task 20: Update templates/session-template.md

**Files:**
- Modify: `templates/session-template.md`

**Requirements:**
- Добавить поле «что мы создали / что решили».
- Сохранить задачу, план, ход работы, проверку, коммит, рефлексию.
- Под лёгким creative-partner голосом.

- [ ] **Step 1: Read existing template and spec section 6**
- [ ] **Step 2: Update session template with outcome/decision field**
- [ ] **Step 3: Verify template is still practical and easy to copy**
- [ ] **Step 4: Commit**

```bash
git add templates/session-template.md
git commit -m "docs: update session template with outcome field"
```

---

## Task 21: Structure and link consistency check

**Files:**
- Modify: all docs and README as needed

**Requirements:**
- Каждый файл ссылается на предыдущий и следующий.
- README обновлён с учётом 17-future.md.
- Все внутренние ссылки работают.
- Три пути для аудиторий в README корректно ведут на нужные разделы.

- [ ] **Step 1: Build link map and check every internal link**

Run:
```bash
cd /home/shugar/dev/ai-pair-programming-guide
python3 - <<'PY'
import re, pathlib
files = list(pathlib.Path('docs').rglob('*.md')) + [pathlib.Path('README.md')]
all_links = []
for f in files:
    text = f.read_text()
    for m in re.finditer(r'\[([^\]]+)\]\(([^)]+)\)', text):
        link = m.group(2)
        if not link.startswith(('http', '#')):
            all_links.append((f, link))
for f, link in all_links:
    target = (f.parent / link).resolve()
    if not target.exists():
        print(f'BROKEN: {f} -> {link}')
print('Check complete.')
PY
```

Expected: No broken links (or list them and fix).

- [ ] **Step 2: Fix any broken links**
- [ ] **Step 3: Commit**

```bash
git add -A
git commit -m "docs: fix internal links and navigation"
```

---

## Task 22: VibeCases check

**Files:**
- All `.md` files

**Requirements:**
- Для каждого файла проверить:
  - [ ] Первые 2 абзаца дают ощущение создания вещей.
  - [ ] Примеры звучат как реальные диалоги.
  - [ ] Нет душнилы (учительского тона, лишних правил, бюрократии).
  - [ ] Есть ощущение: «да, это то, что я хотел передать».

- [ ] **Step 1: Read first two paragraphs of every file and check for forbidden phrases**

Run:
```bash
cd /home/shugar/dev/ai-pair-programming-guide
for f in README.md docs/*.md docs/07-examples/*.md templates/*.md; do
  echo "=== $f ==="
  head -n 20 "$f" | grep -E "давайте|необходимо|следует|важно понимать|следует отметить|необходимо помнить" || echo "OK"
done
```

Expected: No matches outside code blocks.

- [ ] **Step 2: Fix any issues found**
- [ ] **Step 3: Commit**

```bash
git add -A
git commit -m "docs: final vibe polish after VibeCases check"
```

---

## Task 23: Git push

**Files:**
- Branch `vibecraft-rewrite`

- [ ] **Step 1: Review commit log**

Run:
```bash
cd /home/shugar/dev/ai-pair-programming-guide
git log --oneline main..vibecraft-rewrite
```

Expected: ~23 commits covering all files and checks.

- [ ] **Step 2: Push branch**

```bash
git push origin vibecraft-rewrite
```

Expected: Branch pushed successfully.

---

## Self-Review

**Spec coverage:**
- VibeSpark и вайб-токен → Task 1 anchor + voice reference at top of plan.
- Структура 16+1 файлов → Tasks 1–18.
- Шаблоны → Tasks 19–20.
- Структура и связность → Task 21.
- VibeCases → Task 22.
- Git → Task 23.

**Placeholder scan:**
- Нет TBD/TODO.
- Нет «add appropriate error handling».
- Каждый таск содержит конкретные команды.

**Type consistency:**
- Пути файлов согласованы.
- Сообщения коммитов в едином формате.
