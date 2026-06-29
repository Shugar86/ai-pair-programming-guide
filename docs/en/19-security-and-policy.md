# 19. Security and the AI-usage policy

🌐 **English** · [Русский](../19-security-and-policy.md)

**Verdict:** secrets are not sent to agents. Ever.

The agent is a convenient interlocutor, but it works somewhere else: in the vendor's cloud, on the company's server, or locally. While you write a prompt, the code leaves your machine. Our job is to control what exactly goes out, and where.

---

## What must not be sent to agents

- **Credentials and keys:** passwords, API keys, tokens, private SSH keys, certificates.
- **Secret files:** the contents of `.env`, `secrets.yml`, `kubeconfig`, Terraform state, `.pem` and `*.key`.
- **Personal data:** emails, phone numbers, addresses, users' medical and payment data.
- **Proprietary data:** code under NDA, export-restricted code, internal algorithms that can't be shared without review.

If the agent needs an example — replace real values with `REDACTED` or `example-`.

---

## Cloud tools and local models

| Option | What it means | When to choose it |
| :-- | :-- | :-- |
| Cloud agent (Cursor, Kimi, Claude, Copilot) | Code and prompts go to the vendor's server. | Ordinary development, public repos, no secrets in the code. |
| Corporate / self-hosted | The model or the whole stack is deployed in the company's infrastructure. | Private code, regulatory requirements, corporate policy. |
| Local LLM (Ollama, llama.cpp, etc.) | The model runs on your machine, nothing goes out. | Experiments, secret code, offline mode, a limited budget. |

Local models are slower and weaker, but give full control. Cloud ones are more convenient, but require discipline.

---

## A minimal internal AI policy

You don't need the policy as a thick document. One page that everyone has read and can apply is enough:

1. **What may be sent.** Public repos, internal code without secrets, anonymized data.
2. **What may not.** Secrets, PII, code under NDA, prod configurations.
3. **Which tools are allowed.** A list of approved agents and providers with a note on where the data goes.
4. **Who's responsible for a leak.** The developer who sent the prompt.
5. **How to check.** A periodic audit of chat history and commits for `.env`, keys, and PII.

---

## Practical measures

- Add `.env`, `*.pem`, `*.key`, `secrets.*` to `.gitignore`.
- Don't copy production errors with real data into the chat — anonymize them.
- Use separate sessions for code with and without secrets.
- Check the privacy-mode settings in each tool.
- If in doubt — don't send it. Better ask the lead or a security engineer.

---

Where security and responsibility are discussed:

- How to choose an environment and what goes to the server — in [05-environments.md](05-environments.md).
- How not to commit secrets and to control the diff — in [13-git-github.md](13-git-github.md).
- The senior view on risks and escalation — in [18-senior-playbook.md](18-senior-playbook.md).

---

Previous step: the senior playbook — [18-senior-playbook.md](18-senior-playbook.md).

Next step: metrics and retro — [20-metrics-and-retro.md](20-metrics-and-retro.md).
