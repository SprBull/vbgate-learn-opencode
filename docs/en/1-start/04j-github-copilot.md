---
title: "Connect GitHub Copilot"
subtitle: "Reuse existing subscription"
course: "OpenCode Practical Course"
stage: "Stage 1"
lesson: "1.4j"
duration: "10 min"
practice: "5 min"
level: "Beginner"
description: "If you already have a GitHub Copilot subscription, you can reuse it in OpenCode without purchasing additional API."
tags:
  - Model
  - GitHub
  - Copilot
  - OAuth
prerequisite:
  - "1.2 Installation"
---

# Connect GitHub Copilot

> Estimated time: 5-10 minutes

If you **already have a GitHub Copilot subscription** (Individual $10/month or Enterprise), you can reuse this subscription in OpenCode to access models like GPT-4o, Claude, etc., without purchasing additional API.

::: tip Who is this for?
- Users with existing GitHub Copilot subscription
- Users who don't want to purchase OpenAI/Anthropic API separately
- Users who want to reuse Copilot models in terminal
:::

If you don't have a Copilot subscription, skip this guide and check other connection tutorials.

---

## What you'll be able to do

- Connect GitHub Copilot in OpenCode
- Use models provided by Copilot (GPT-4o, Claude, etc.)
- Send your first message and receive a response

---

## 🎒 Before you start

- [ ] Completed [1.2 Installation](./02-install), able to run `opencode`
- [ ] **Have a GitHub Copilot subscription** (Individual or Enterprise)
- [ ] Able to access `github.com`

---

## Follow along

### Step 1: Verify your Copilot subscription

Visit GitHub settings page to confirm:

https://github.com/settings/copilot

You should see a status like this:

```
GitHub Copilot
Status: Active
```

If it shows not subscribed, you need to subscribe to GitHub Copilot first.

---

### Step 2: Start connection in OpenCode

Launch OpenCode:

```bash
opencode
```

In the input box, type:

```
/connect
```

Search for `GitHub Copilot` in the provider list and select it.

---

### Step 3: Complete OAuth authorization

After selecting GitHub Copilot, OpenCode will display an authorization link:

```
Please visit: https://github.com/login/device
And enter code: XXXX-XXXX
```

**Steps**:

1. Open browser and visit `https://github.com/login/device`
2. Enter the device code shown on screen (e.g., `XXXX-XXXX`)
3. Click "Authorize" to authorize OpenCode

::: info Auto-open browser
If your terminal supports it, OpenCode will automatically open the browser. If not, manually copy the link.
:::

After successful authorization, OpenCode will display:

```
✓ Provider added successfully!
```

---

### Step 4: Select model

After successful connection, type:

```
/models
```

You'll see models provided by GitHub Copilot:

| Model | Description |
|-------|-------------|
| `gpt-4o` | Recommended, flagship multimodal model |
| `gpt-4o-mini` | Fast, low cost |
| `claude-sonnet-4-5` | Claude latest balanced version |
| `claude-3-5-haiku` | Claude fast version |
| `o1` | Enhanced reasoning model |
| `o1-mini` | Fast reasoning |

Select a model to start the conversation.

::: warning Some models require Pro+ subscription
Advanced models like `o1`, `claude-sonnet-4-5` may require GitHub Copilot Pro+ subscription. With a regular subscription, you may only have access to some models.
:::

---

### Step 5: Send first message (verify success)

In the input box, type:

```
Hello, please introduce yourself
```

If you receive a response, the connection is successful.

---

## Checklist ✅

- [ ] Can see Copilot models in `/models`
- [ ] Can receive AI response when sending message
- [ ] No errors (like `unauthorized` / `subscription required`)

---

## Common issues

| Issue | Cause | Solution |
|-------|-------|----------|
| `unauthorized` | OAuth authorization failed or expired | Re-run `/connect` and select GitHub Copilot |
| `subscription required` | No Copilot subscription | Subscribe to GitHub Copilot first |
| Can't find a model | Subscription tier too low | Upgrade to Pro+ or use other models |
| Authorization page shows error | Device code expired | Re-run `/connect`, complete authorization within 5 minutes |
| Shows `reauthenticate` | Token expired | Re-authorize |

---

## Re-authorization

If Token expires or authorization has issues, you can re-authenticate using:

**Method 1: Reconnect in TUI**

```
/connect
```

Select GitHub Copilot and follow prompts to re-authorize.

**Method 2: Terminal command**

```bash
opencode auth login
# Select GitHub Copilot
```

---

## Next steps

- Go back to [1.4 Overview](./04-connect) to choose next route, or proceed to [2.1 Interface & Basics](../2-daily/01-interface)

::: tip Need help?
Stuck during configuration? [Join the community](/en/community) and connect with 2000+ fellow learners for real-time Q&A.
:::
