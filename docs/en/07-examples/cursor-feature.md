# Example: adding a feature in Cursor

🌐 **English** · [Русский](../../07-examples/cursor-feature.md)

**Verdict:** even a small feature needs scope control.

**Environment:** Cursor  
**Task:** Add a "Copy" button next to the email on the user profile.

---

## 1. Define the task

```text
You: Add a "Copy" button next to the email on the user profile.
     On click, the email is copied to the clipboard.
     The button text changes to "Copied" for 2 seconds, then reverts.
     Touch only the profile components.
```

## 2. Agree on a plan

```text
Agent: Plan:
1. Find the profile component where the email is shown.
2. Add a Copy button next to the email.
3. Implement the click handler with navigator.clipboard.writeText.
4. Add a data-testid for the button.

You: OK. No toast notifications — just change the button text.
```

## 3. Implementation and the first dead end

The agent proposes a diff. You see it touched 4 files, including global styles.

```text
You: Stop. Keep changes only in ProfileCard.tsx and UserEmail.tsx. Don't touch the rest.
Agent: [reverts the extra files]
```

The agent rewrites, but now the button is added to both components — duplication.

```text
You: Remove the button from ProfileCard. Keep it only in UserEmail.tsx — there's one email there, let the logic live next to it.
Agent: [moves the logic into UserEmail.tsx]
```

## 4. Verification

```text
You: Run the tests for UserEmail.
Agent: npm test UserEmail
Agent: Tests passed, but one snapshot is stale.
You: Update the snapshot only if the change in it is our new button.
Agent: [updates the snapshot and shows the diff]
You: Yes, OK. Add data-testid="copy-email-button".
```

## 5. Commit

```bash
git add src/components/UserEmail.tsx src/components/__tests__/UserEmail.test.tsx
git commit -m "feat: add copy email button in profile"
```

## 6. Reflection

- Worked: the plan before code aligned expectations. The "profile components only" constraint helped quickly cut the excess.
- First dead end: the agent grabbed global styles. The Cursor checkpoint saved a manual revert.
- Could be better: say "UserEmail.tsx only" up front, to avoid removing the duplication in a second round.

## Takeaway

Even a simple button can smear across the project. Specify scope before the first diff and read every change. Cursor fixes direction mistakes fast if you catch them early.

Which patterns worked here — see [`06-prompt-patterns.md`](../06-prompt-patterns.md).

Next example: refactoring in Claude Code — [`claude-refactor.md`](claude-refactor.md).
