---
title: "Connect to DeepSeek (Recommended)"
subtitle: "Direct access, affordable, and powerful"
course: "OpenCode Practical Course"
stage: "Stage 1"
lesson: "1.4b"
duration: "10 min"
practice: "5 min"
level: "Beginner"
description: "Get your DeepSeek API Key and complete your first conversation in OpenCode."
tags:
  - Model
  - DeepSeek
  - API Key
prerequisite:
  - "1.2 Installation"
---

# Connect to DeepSeek (Recommended)

> Estimated time: 5-10 minutes

DeepSeek is great for beginners: direct access (no VPN needed in most regions), simple registration, extremely affordable, and strong coding capabilities.

If you haven't read "What is an API Key", we recommend going back to [1.4 Overview](./04-connect) to understand the concepts first.

---

## What You'll Be Able to Do

- Get a DeepSeek API Key
- Connect DeepSeek in OpenCode
- Send your first message and receive a response

---

## 🎒 Before You Start

- [ ] Completed [1.2 Installation](./02-install) and can run `opencode`
- [ ] Can access `https://platform.deepseek.com`

---

## Follow Along

### Step 1: Register a DeepSeek Account

Visit: https://platform.deepseek.com

Click "Login/Register" in the top right corner, and follow the prompts to register with your phone number or email.

---

### Step 2: Get Your API Key

Go to the API Keys page:
- Left menu in console: `API Keys`
- Or visit directly: https://platform.deepseek.com/api_keys

Create a new Key and **copy and save it immediately**.

::: warning Only shown once!
Most platforms only display the Key once. Once you close the window, you won't be able to see the complete Key again.

Please copy it to a safe place (password manager/notes) immediately. Don't share it in group chats, don't screenshot it, don't commit it to GitHub.
:::

---

### Step 3: (Optional but Recommended) Add Credits

DeepSeek usually gives new users a small amount of credits, but they run out quickly. Adding about 10 CNY worth of credits will last you a long time.

---

### Step 4: Connect DeepSeek in OpenCode

Start OpenCode:

```bash
opencode
```

In the input box, enter:

```
/connect
```

Select `DeepSeek` from the provider list, then paste your API Key.

After success, you'll enter the model selection interface showing DeepSeek's available models (such as `deepseek-chat`, `deepseek-reasoner`). Select a model to start chatting.

---

### Step 5: Send Your First Message (Verify Success)

In the input box, enter:

```
Hello, please introduce yourself
```

If you receive a response, the connection is successful.

---

## Checklist ✅

- [ ] Sending messages receives AI responses
- [ ] No errors (such as `API key invalid` / `insufficient balance` / `connection timeout`)

---

## Common Issues

| Issue | Cause | Solution |
|-------|-------|----------|
| `API key invalid` | Key copied incorrectly or has extra spaces | Copy again, make sure there are no extra spaces |
| `insufficient balance` | Insufficient balance | Add credits in the console |
| `connection timeout` | Network fluctuation | Wait a moment and try again |

---

## Next Steps

- Go back to [1.4 Overview](./04-connect) to choose your next path, or proceed to [2.1 Interface & Basic Operations](../2-daily/01-interface)

::: tip Having issues?
Stuck during configuration? [Join the community](/en/community) to connect with 2000+ fellow learners for real-time support.
:::
