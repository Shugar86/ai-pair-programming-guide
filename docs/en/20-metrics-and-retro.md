# 20. Metrics and retro

🌐 **English** · [Русский](../20-metrics-and-retro.md)

AI in a team is a process change. To make it go in the right direction, watch the numbers and regularly discuss what works and what doesn't.

---

## Metrics

| Metric | What it shows | How to use it |
| :-- | :-- | :-- |
| **Time from task to PR** | Whether the agent speeds up the cycle or adds edits. | Compare periods before and after adopting the agent. A rise — a signal to look into it. |
| **Rollbacks and bugs after agent edits** | The quality of the code coming out of sessions. | Regressions shouldn't grow. If they do — check the checklists and prompts. |
| **Subjective load** | How tired the team is from context switching and checking the agent. | Run a survey every two weeks: "how much did the agent ease or complicate the work?" |
| **Review cycles** | How many iterations a PR needs to get approved. | If agent code goes through more rounds — look at prompt and checklist quality. |

Don't gather metrics for the sake of metrics. Four or five indicators the team is willing to discuss are enough.

---

## The retro format

Run a retro every 2–4 weeks for the first six months, then — on signals.

### How the retro goes

1. **Facts.** Gather the metrics for the period.
2. **Patterns.** What repeated? What helped, what got in the way?
3. **Rules.** What to add or change in `AGENTS.md` and the checklists?
4. **Actions.** Who makes the changes, and when?

### Questions for the team

- Where did the agent really speed up a task, and where did it slow it down?
- Which bugs or rollbacks happened most often?
- What moment of working with the agent was the most annoying?
- What did we recently send the agent that we'd better not have?
- Which rule is worth adding to `AGENTS.md` after these two weeks?

The answers turn into concrete rules, instead of staying up in the air.

---

Related sections:

- Checklists for accepting code and for the retro — in [09-checklists.md](09-checklists.md).
- The senior playbook: roles, context, and system review — in [18-senior-playbook.md](18-senior-playbook.md).

---

Previous step: security and policy — [19-security-and-policy.md](19-security-and-policy.md).

Back to the start — [README.md](../../README.md) or [03-principles.md](03-principles.md).
