# Example: refactoring in Claude Code

🌐 **English** · [Русский](../../07-examples/claude-refactor.md)

**Verdict:** refactoring without tests is roulette.

**Environment:** Claude Code (terminal)  
**Task:** Extract repeated validation logic from three handlers into a separate function.

---

## 1. Define the task

```text
You: Three handlers duplicate the input check. Extract it into a separate function.
     Don't change the validation logic — just move it.
     Use the name validate_payload, because it's not only users being validated.
```

## 2. Agree on a plan

```text
Agent: Plan:
1. Find the three handlers with duplicated validation.
2. Create a validate_payload function in validators.py.
3. Replace the duplicated code with a call to validate_payload.
4. Run the tests.

You: OK. If there are no tests for this validation — add one minimal test.
```

## 3. Implementation and the dead end

The agent shows the diff. You notice the function is named validate_user_input, even though orders and payments are validated too.

```text
You: Rename it to validate_payload, as we agreed.
Agent: [renames it]
```

The agent runs the tests. One fails.

```text
Agent: pytest tests/
Agent: FAILED tests/handlers/test_payment.py::test_missing_field
Agent: Error: validate_payload doesn't accept the optional strict parameter that was in one of the handlers.
You: Restore the old call in the payment handler and keep strict in place. Move only the common part.
Agent: [restores the strict logic in the payment handler]
```

## 4. Verification

```text
Agent: pytest tests/
Agent: All tests passed.
You: [reviews the diff] Good. Make sure the behavior in all three handlers is unchanged.
Agent: [runs the tests again and shows the output]
```

## 5. Commit

```bash
git add app/validators.py app/handlers/
git commit -m "refactor: extract validate_payload helper"
```

## 6. Reflection

- Worked: the "just move it" constraint held the scope. Naming the function up front saved one edit cycle.
- Dead end: the optional strict parameter turned out to be in only one handler. The agent tried to unify what can't be unified.
- Could be better: show the agent example calls from all three handlers up front, so it sees the differences.

## Takeaway

Refactoring isn't about perfect symmetry — it's about preserving behavior. If different paths have the right to differ — say so explicitly. Claude fixes direction well after concrete feedback.

Which patterns worked here — see [`06-prompt-patterns.md`](../06-prompt-patterns.md).

Next example: fixing a bug in Kimi Code — [`kimi-bugfix.md`](kimi-bugfix.md).
