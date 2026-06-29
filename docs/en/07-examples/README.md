# Session examples

🌐 **English** · [Русский](../../07-examples/README.md)

This section isn't a set of perfect success stories — it's real dialogues with an agent. In every session there's a moment where something goes wrong: the agent drifts off, forgets a constraint, or proposes something extra. The point is how to get it back on course.

If you haven't read [`06-prompt-patterns.md`](../06-prompt-patterns.md) yet, start there: the examples show how those patterns work in real life.

---

## Index of examples

| Task | Stack | File | Key moments |
|---|---|---|---|
| Add a "Copy" button to the profile | React / TypeScript / Cursor | [`cursor-feature.md`](cursor-feature.md) | The agent grabbed global styles. Scope before code cut the excess. |
| Extract shared validation from three handlers | Python / Claude Code | [`claude-refactor.md`](claude-refactor.md) | Not all paths are the same: `strict` stayed in place. |
| Fix a 500 when creating an order without an address | Python / Kimi Code | [`kimi-bugfix.md`](kimi-bugfix.md) | A test reproduced the bug first. The "endpoint only" constraint held the architecture. |
| Build a Docker image for a Python + Node app | Docker / Kimi Code | [`infra-docker.md`](infra-docker.md) | The agent forgot multi-stage and almost pulled `.env` into the image. |
| Add GitHub Actions CI | GitHub Actions / Cursor | [`infra-ci.md`](infra-ci.md) | A wrong cache key and an extra `pull_request` target — fixed after it failed. |

---

## How to read them

Each file follows one structure:

1. **Task** — what you wanted to get.
2. **Plan** — what the agent proposed before code.
3. **Implementation and dead end** — where you got stuck and what you said to get out.
4. **Verification** — commands and tests.
5. **Commit** — the final diff.
6. **Reflection** — what worked and what's worth saying up front.

---

## Where to go next

- Lock in the skills with practice — [`08-exercises.md`](../08-exercises.md).
- Learn how not to fall into typical traps — [`10-antipatterns.md`](../10-antipatterns.md).
- See how to run complex scenarios — [`18-senior-playbook.md`](../18-senior-playbook.md).
