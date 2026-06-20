# Product Structure Iteration Implementation Plan

> **For agentic workers:** REQUIRED SUB-SKILL: Use `superpowers:subagent-driven-development` to implement this plan task-by-task.

**Goal:** Добавить в гайд структуру, навигацию по ролям, безопасность, метрики и рецепты под стеки, сохраняя живой голос.

**Architecture:** Итерация поверх существующих файлов. Добавляем блоки, таблицы, индексы, новые файлы. Перекрёстные ссылки связывают всё в единую навигацию.

**Tech Stack:** Markdown, git. SVG — если есть инструменты, иначе обновить текстовую подпись.

---

## Task 1: README.md — стартовая страница

**Files:**
- Modify: `README.md`

**Requirements:**
- Блок «Если ты торопишься» с 3 ссылками (04, 10, 18).
- «Что внутри» сгруппировано по блокам: база, ежедневный цикл, окружение, для новичков, для сеньоров/лидов.
- Секция «Как использовать в команде».

- [ ] **Step 1: Read current README and spec section 2**
- [ ] **Step 2: Add "Если ты торопишься" block**
- [ ] **Step 3: Regroup "Что внутри" by blocks**
- [ ] **Step 4: Add "Как использовать в команде" section**
- [ ] **Step 5: Verify links and commit**

```bash
cd /home/shugar/dev/ai-pair-programming-guide
git add README.md
git commit -m "docs: restructure README as product landing page"
```

---

## Task 2: Core philosophy files (01–04)

**Files:**
- Modify: `docs/01-what-is-pair-programming.md`
- Modify: `docs/02-agent-as-pair-programmer.md`
- Modify: `docs/03-principles.md`
- Modify: `docs/04-workflow.md`

**Requirements:**
- 01: table classic vs AI-pair; links to 02, 03, 04.
- 02: responsibility table (you vs agent); agent limitations block linking to 10.
- 03: 8 principles one-liner at top; principle→loop mapping table; anti-examples for some principles linking to 10.
- 04: caption steps under SVG; technical checklist after step 4; two case formats (smooth and bad→fix).

- [ ] **Step 1: Read current files and spec sections 3–6**
- [ ] **Step 2: Add tables, blocks, and case formats**
- [ ] **Step 3: Verify links and no forbidden phrases**
- [ ] **Step 4: Commit each file separately**

```bash
cd /home/shugar/dev/ai-pair-programming-guide
git add docs/01-what-is-pair-programming.md && git commit -m "docs: add comparison and navigation to 01"
git add docs/02-agent-as-pair-programmer.md && git commit -m "docs: add responsibility table and agent limits to 02"
git add docs/03-principles.md && git commit -m "docs: add principles map and anti-examples to 03"
git add docs/04-workflow.md && git commit -m "docs: add step captions, tech checklist, and dual case formats to 04"
```

---

## Task 3: Tools and prompt patterns (05–06)

**Files:**
- Modify: `docs/05-environments.md`
- Modify: `docs/06-prompt-patterns.md`

**Requirements:**
- 05: per-tool micro-sections (context, diff, scope); privacy/code-sending notes linking to 19.
- 06: pattern classification (plan→code, refactoring, debug, review, docs); links to where patterns are used; 2–3 stack recipes (Next.js, Python backend, infra).

- [ ] **Step 1: Read current files and spec sections 7–8**
- [ ] **Step 2: Add micro-sections, classification, recipes**
- [ ] **Step 3: Verify links and commit**

```bash
cd /home/shugar/dev/ai-pair-programming-guide
git add docs/05-environments.md && git commit -m "docs: add per-tool sections and privacy notes to 05"
git add docs/06-prompt-patterns.md && git commit -m "docs: classify patterns and add stack recipes to 06"
```

---

## Task 4: Examples library (07)

**Files:**
- Create: `docs/07-examples/README.md`
- Create: `docs/07-examples/infra-ci.md` (or similar)

**Requirements:**
- README.md index with table: task → stack → files → key moments.
- 1–2 infra/DevOps examples (Docker, CI/CD, Terraform).

- [ ] **Step 1: Read existing examples and spec section 9**
- [ ] **Step 2: Create index README and 1–2 infra examples**
- [ ] **Step 3: Verify links and commit**

```bash
cd /home/shugar/dev/ai-pair-programming-guide
git add docs/07-examples/
git commit -m "docs: add examples index and infra sessions"
```

---

## Task 5: Exercises, checklists, antipatterns (08–10)

**Files:**
- Modify: `docs/08-exercises.md`
- Modify: `docs/09-checklists.md`
- Modify: `docs/10-antipatterns.md`

**Requirements:**
- 08: split by level; expected outcome per exercise; links to principles; team workshop section.
- 09: checklists by loop stage; minimal and extended sets; links from 04 and 18.
- 10: top map table; links to 03/04/09 for common traps; self-diagnosis list at end.

- [ ] **Step 1: Read current files and spec sections 10–12**
- [ ] **Step 2: Add levels, expected outcomes, map table, self-diagnosis**
- [ ] **Step 3: Verify links and commit**

```bash
cd /home/shugar/dev/ai-pair-programming-guide
git add docs/08-exercises.md && git commit -m "docs: split exercises by level and add workshop section"
git add docs/09-checklists.md && git commit -m "docs: add minimal/extended checklists by loop stage"
git add docs/10-antipatterns.md && git commit -m "docs: add antipatterns map and self-diagnosis list"
```

---

## Task 6: Advanced and infrastructure (11–15)

**Files:**
- Modify: `docs/11-advanced-scenarios.md`
- Modify: `docs/12-setup.md`
- Modify: `docs/13-git-github.md`
- Modify: `docs/14-ide-cli-workflow.md`
- Modify: `docs/15-troubleshooting.md`

**Requirements:**
- 11: group scenarios by type; multi-session flow with artifacts for each.
- 12: two routes — minimal and team-lead setup.
- 13: "AI and Git" section (no auto-push, read diff, commit/PR messages).
- 14: link CLI steps to loop in 04.
- 15: block "when it's not environment but agent" linking to 03/05/10.

- [ ] **Step 1: Read current files and spec section 13–14**
- [ ] **Step 2: Add grouped scenarios, routes, AI-and-Git section, CLI-loop links, agent troubleshooting**
- [ ] **Step 3: Verify links and commit**

```bash
cd /home/shugar/dev/ai-pair-programming-guide
git add docs/11-advanced-scenarios.md && git commit -m "docs: group advanced scenarios and add multi-session flows"
git add docs/12-setup.md && git commit -m "docs: add minimal and team-lead setup routes"
git add docs/13-git-github.md && git commit -m "docs: add AI and Git section"
git add docs/14-ide-cli-workflow.md && git commit -m "docs: link CLI workflow to loop"
git add docs/15-troubleshooting.md && git commit -m "docs: add agent-side troubleshooting block"
```

---

## Task 7: Beginners, future, senior playbook (16–18)

**Files:**
- Modify: `docs/16-ai-for-beginners.md`
- Modify: `docs/17-future.md`
- Modify: `docs/18-senior-playbook.md`

**Requirements:**
- 16: "What AI doesn't do for you" block; 90-minute route.
- 17: "How lead/senior role changes" block; scenario team-without-AI vs team-with-guide.
- 18: format cases as Case 1/2/3 with steps; links to templates; "Checklist for leads" section linking to 20.

- [ ] **Step 1: Read current files and spec sections 15–17**
- [ ] **Step 2: Add blocks, route, scenarios, lead checklist**
- [ ] **Step 3: Verify links and commit**

```bash
cd /home/shugar/dev/ai-pair-programming-guide
git add docs/16-ai-for-beginners.md && git commit -m "docs: add AI limitations and 90-minute route to 16"
git add docs/17-future.md && git commit -m "docs: add lead role evolution and scenario to 17"
git add docs/18-senior-playbook.md && git commit -m "docs: format cases and add lead checklist to 18"
```

---

## Task 8: New files — security and metrics (19–20)

**Files:**
- Create: `docs/19-security-and-policy.md`
- Create: `docs/20-metrics-and-retro.md`

**Requirements:**
- 19: what not to send agents; local LLMs; internal AI policy; links to 05, 13, 18.
- 20: metrics (time to PR, rollbacks, load); retro format; links to 09, 18.
- Both: previous link to 18; 20 links back to 19 or README.

- [ ] **Step 1: Read spec section 20 and existing 05/13/18**
- [ ] **Step 2: Create both files**
- [ ] **Step 3: Verify links and commit**

```bash
cd /home/shugar/dev/ai-pair-programming-guide
git add docs/19-security-and-policy.md && git commit -m "docs: add 19-security-and-policy.md"
git add docs/20-metrics-and-retro.md && git commit -m "docs: add 20-metrics-and-retro.md"
```

---

## Task 9: Templates and assets

**Files:**
- Create: `templates/README.md`
- Modify: `templates/AGENTS.md`
- Modify: `templates/ADR-template.md`
- Modify: `assets/workflow.svg` (if possible)

**Requirements:**
- `templates/README.md`: describe AGENTS.md, ADR, session card usage.
- `AGENTS.md`: add examples for TS web, Python backend, infra stacks.
- `ADR-template.md`: add AI-impact fields and AGENTS.md/checklist update questions.
- `assets/workflow.svg`: label steps with same wording as 04-workflow.md.

- [ ] **Step 1: Read current templates and spec sections 18–19**
- [ ] **Step 2: Create README and update templates**
- [ ] **Step 3: Update SVG or add text caption if SVG tools unavailable**
- [ ] **Step 4: Verify links and commit**

```bash
cd /home/shugar/dev/ai-pair-programming-guide
git add templates/README.md && git commit -m "docs: add templates README"
git add templates/AGENTS.md && git commit -m "docs: add stack examples to AGENTS.md template"
git add templates/ADR-template.md && git commit -m "docs: add AI fields to ADR template"
git add assets/workflow.svg && git commit -m "docs: update workflow.svg labels"
```

---

## Task 10: Final verification and merge

**Files:**
- All `.md` files, templates, assets.

- [ ] **Step 1: Comprehensive link check**

Run:
```bash
cd /home/shugar/dev/ai-pair-programming-guide
python3 - <<'PY'
import re, pathlib
files = list(pathlib.Path('docs').rglob('*.md')) + [pathlib.Path('README.md'), pathlib.Path('templates/AGENTS.md'), pathlib.Path('templates/session-template.md'), pathlib.Path('templates/ADR-template.md'), pathlib.Path('templates/README.md')]
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

- [ ] **Step 2: Forbidden phrases check**

```bash
cd /home/shugar/dev/ai-pair-programming-guide
grep -Rin "давайте\|необходимо\|следует\|важно понимать" README.md docs/ templates/ || echo "No forbidden phrases in prose"
```

Expected: No matches outside code blocks.

- [ ] **Step 3: Navigation sanity check**

Verify README has quick-start block, role-based grouping, team usage section.
Verify 16 has 90-minute route.
Verify 19 and 20 are linked from relevant files.

- [ ] **Step 4: Commit fixes if any**

```bash
git add -A
git commit -m "docs: final product-structure link and navigation fixes"
```

- [ ] **Step 5: Push to main**

```bash
git push origin main
```
