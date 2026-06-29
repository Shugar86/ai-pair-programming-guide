# Example: fixing a bug in Kimi Code

🌐 **English** · [Русский](../../07-examples/kimi-bugfix.md)

**Verdict:** a bugfix starts with reproduction, not with guesses.

**Environment:** Kimi Code (CLI)  
**Task:** The API returns a 500 when creating an order without an address.

---

## 1. Define the task

```text
You: When creating an order without an address, the API crashes with a 500. We need to return 400 with a clear error.
     The validation should live in the endpoint, not the service.
     Start with a test that reproduces the bug.
```

## 2. Agree on a plan

```text
Agent: Plan:
1. Find the order-creation endpoint.
2. Write a test that sends a request without an address and expects 400.
3. Add the address check in the endpoint.
4. Run the test and confirm it passes.

You: OK. Endpoint only — don't go into OrderService.
```

## 3. Implementation and the dead end

The agent creates the test. The test fails with a 500 — the bug is reproduced.

```text
You: Good, now fix the validation in the endpoint.
Agent: [adds the check in app/orders/routes.py]
```

You review the diff and see the agent changed OrderService, adding the validation there.

```text
You: Remove the changes from OrderService. The validation should be in the endpoint, as we agreed.
Agent: [moves the check into the endpoint]
```

The agent moves it, but now the endpoint returns a generic "Invalid input" instead of a clear "address is required."

```text
You: The error message must be specific: "address is required".
Agent: [fixes the message]
```

## 4. Verification

```text
Agent: pytest tests/orders/test_create.py -v
Agent: tests/orders/test_create.py::test_create_order_without_address PASSED
Agent: tests/orders/test_create.py::test_create_order_with_address PASSED
You: [sees the new test passes and the old ones didn't break]
```

## 5. Commit

```bash
git add tests/orders/test_create.py app/orders/routes.py
git commit -m "fix: return 400 when order address is missing"
```

## 6. Reflection

- Worked: the test fixed the bug before the fix. The "endpoint only" constraint helped hold the architecture.
- First dead end: the agent moved the validation into the service because it was "cleaner." You returned it to the agreement.
- Second dead end: a generic error message. Specificity in the error is part of the task, and it's worth stating up front.
- Could be better: give an example of the expected error JSON up front.

## Takeaway

A bugfix isn't only a fix — it's protection against recurrence. The test-first approach gives you leverage: you see the bug before you fix it. Kimi in the CLI quickly reverts extra changes if you hold the boundary clearly.

Which patterns worked here — see [`06-prompt-patterns.md`](../06-prompt-patterns.md).

Next step: lock in the skills with practice — [`08-exercises.md`](../08-exercises.md).
