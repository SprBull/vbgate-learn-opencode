---
title: "Free Models"
subtitle: "No login required, ready to use"
course: "OpenCode Practical Course"
stage: "Stage 1"
lesson: "1.4a"
duration: "5 minutes"
practice: "2 minutes"
level: "Beginner"
description: "Use OpenCode's built-in free models without registration, start your first conversation right away."
tags:
  - "Model"
  - "Free"
  - "OpenCode Zen"
prerequisite:
  - "1.2 Installation"
---

# Free Models

> Best for: You want to complete your **first OpenCode conversation with 0 cost and 0 configuration**.

OpenCode includes a set of **completely free** models that require **no registration or API Key** - they work immediately after installation.

---

## Current Free Models

| Model ID | Name | Features |
|----------|------|----------|
| `glm-4.7-free` | GLM-4.7 | By Zhipu, supports reasoning, excellent Chinese performance |
| `minimax-m2.1-free` | MiniMax M2.1 | By MiniMax, supports reasoning, 200K context |
| `gpt-5-nano` | GPT-5 Nano | By OpenAI, lightweight and fast |
| `kimi-k2.5-free` | Kimi K2.5 | By Moonshot, supports reasoning, 256K context |
| `big-pickle` | Big Pickle | Hidden model, limited-time free trial |

::: tip Note
The free model list may change over time. The list shown in `/models` command is always accurate.

Free models have IP-level usage limits, suitable for trial and light use. For higher quotas, you can log in to OpenCode Zen to get an API Key.
:::

---

## Follow Along

### Step 1: Start OpenCode

```bash
opencode
```

On first launch, OpenCode automatically loads free models with no configuration needed.

---

### Step 2: Select a Free Model

Enter:

```
/models
```

Choose any free model from the list, for example:
- `opencode/glm-4.7-free`
- `opencode/minimax-m2.1-free`

::: tip How to identify free models?
Free models usually have a `-free` suffix, or show `$0` price in the `/models` list.
:::

---

### Step 3: Send Your First Message

```
Hello, please introduce yourself
```

If you receive a response, you've successfully completed the "Install → Select Model → Chat" workflow.

---

## Checklist

- [ ] Running `/models` shows `opencode/*-free` or models with `$0` price
- [ ] Sending a message receives an AI response

---

## Common Issues

| Issue | Cause | Solution |
|-------|-------|----------|
| No free models in `/models` | Network issue or outdated version | Check network, run `opencode upgrade` to update |
| Request rejected / rate limited | Free models have IP-level quotas | Try a different free model or wait a while |
| Slow response | Free model servers under high load | Normal behavior, be patient or try another model |

---

## Want More?

Free models are great for trial and light use. If you need:
- Higher request quotas
- More model choices (Claude, GPT-5, etc.)
- More stable service

You can log in to [OpenCode Zen](https://opencode.ai/zen) to get an API Key. See [1.4 Connect Models](/en/1-start/04-connect) for more details.

---

## Next Steps

- Return to [1.4 Overview](/en/1-start/04-connect) to choose your next path
- Or proceed to [2.1 Interface & Basics](/en/2-daily/01-interface) to learn daily usage
