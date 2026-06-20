# Senior VibeCraft Layer Implementation Plan

> **For agentic workers:** REQUIRED SUB-SKILL: Use `superpowers:subagent-driven-development` to implement this plan task-by-task.

**Goal:** Добавить в гайд продвинутый слой для сеньоров и лидов: новый `docs/18-senior-playbook.md`, дополнить `11-advanced-scenarios.md`, `17-future.md`, обновить `README.md`.

**Architecture:** Создаём отдельный файл с senior-паттернами, не переписываем базу. Связываем с существующими разделами ссылками. Обновляем навигацию в README.

**Tech Stack:** Markdown, git.

---

## Общий голос для senior-слоя

Тон: `systems-thinker`. Продвинутый напарник, который думает на уровне системы.

**Делать:**
- Ссылаться на базовые разделы (01–10), не повторять их.
- Системные примеры: сервисы, модули, контракты, инварианты.
- Trade-offs: плюсы, минусы, когда применимо.
- Прямое «ты», короткие предложения, вердикт первым.

**Не делать:**
- Повторять KISS/minimal diff/YAGNI.
- Объяснять, как установить Cursor.
- Сюсюкать или душнить.

---

## Task 1: Create docs/18-senior-playbook.md

**Files:**
- Create: `docs/18-senior-playbook.md`

**Requirements:**
- 8 sections as defined in spec.
- Each section: verdict first, concrete example/scenario, trade-offs, links to related guide sections.
- Previous link to `11-advanced-scenarios.md`.
- Forward link to `17-future.md`.
- Voice: `systems-thinker`.

- [ ] **Step 1: Read spec section 4 and existing `docs/11-advanced-scenarios.md`**
- [ ] **Step 2: Write `docs/18-senior-playbook.md` with all 8 sections**
- [ ] **Step 3: Verify no forbidden phrases**

Run:
```bash
cd /home/shugar/dev/ai-pair-programming-guide
grep -n "давайте\|необходимо\|следует\|важно понимать" docs/18-senior-playbook.md || echo "OK"
```

- [ ] **Step 4: Commit**

```bash
git add docs/18-senior-playbook.md
git commit -m "docs: add 18-senior-playbook.md"
```

---

## Task 2: Enhance docs/11-advanced-scenarios.md

**Files:**
- Modify: `docs/11-advanced-scenarios.md`

**Requirements:**
- Add a "Сеньорский взгляд" section near the end.
- Briefly recap 2–3 key senior patterns.
- Link to `18-senior-playbook.md`.

- [ ] **Step 1: Read existing file and spec section 5**
- [ ] **Step 2: Add senior lens section**
- [ ] **Step 3: Verify link to 18-senior-playbook.md resolves**
- [ ] **Step 4: Commit**

```bash
git add docs/11-advanced-scenarios.md
git commit -m "docs: add senior lens to advanced scenarios"
```

---

## Task 3: Enhance docs/17-future.md

**Files:**
- Modify: `docs/17-future.md`

**Requirements:**
- Add a section "Для сеньоров и лидов" about the shift from coding to managing context, quality, and architecture.
- Link to `18-senior-playbook.md`.

- [ ] **Step 1: Read existing file and spec section 6**
- [ ] **Step 2: Add senior/lead future perspective section**
- [ ] **Step 3: Verify link resolves**
- [ ] **Step 4: Commit**

```bash
git add docs/17-future.md
git commit -m "docs: add senior perspective to future"
```

---

## Task 4: Update README.md senior path

**Files:**
- Modify: `README.md`

**Requirements:**
- Add `18-senior-playbook.md` to the senior/lead path.
- Update the section list or path description.
- Ensure link resolves.

- [ ] **Step 1: Read README audience paths and spec section 7**
- [ ] **Step 2: Add 18-senior-playbook.md to senior/lead path**
- [ ] **Step 3: Verify link resolves**
- [ ] **Step 4: Commit**

```bash
git add README.md
git commit -m "docs: add 18-senior-playbook to README senior path"
```

---

## Task 5: Final link and vibe check

**Files:**
- All `.md` files

- [ ] **Step 1: Run comprehensive link check**

Run:
```bash
cd /home/shugar/dev/ai-pair-programming-guide
python3 - <<'PY'
import re, pathlib
files = list(pathlib.Path('docs').rglob('*.md')) + [pathlib.Path('README.md'), pathlib.Path('templates/AGENTS.md'), pathlib.Path('templates/session-template.md')]
broken = []
for f in files:
    text = f.read_text()
    for m in re.finditer(r'\[([^\]]+)\]\(([^)]+)\)', text):
        link = m.group(2)
        if not link.startswith(('http', '#', 'mailto:')):
            target = (f.parent / link).resolve()
            if not target.exists():
                broken.append((f, link))
if broken:
    print('BROKEN:')
    for f, link in broken:
        print(f'  {f} -> {link}')
else:
    print('All internal links OK')
PY
```

Expected: All internal links OK.

- [ ] **Step 2: Run forbidden phrases check**

Run:
```bash
cd /home/shugar/dev/ai-pair-programming-guide
grep -Rin "давайте\|необходимо\|следует\|важно понимать" README.md docs/ templates/ || echo "No forbidden phrases in prose"
```

Expected: No matches outside code blocks.

- [ ] **Step 3: Vibe check for senior files**

Read first two paragraphs of `docs/18-senior-playbook.md`, updated `docs/11-advanced-scenarios.md` section, updated `docs/17-future.md` section. Confirm they sound like senior system thinking, not basic advice.

- [ ] **Step 4: Commit fixes if any**

```bash
git add -A
git commit -m "docs: final senior layer link and vibe fixes"
```

---

## Task 6: Git push

- [ ] **Step 1: Review commit log**

Run:
```bash
cd /home/shugar/dev/ai-pair-programming-guide
git log --oneline main..vibecraft-rewrite | head -20
```

- [ ] **Step 2: Push branch**

```bash
git push origin vibecraft-rewrite
```

Expected: Branch pushed successfully.
