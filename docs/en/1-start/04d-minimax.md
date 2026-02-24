---
title: "Connect MiniMax (M2.5/M2.1)"
subtitle: "9.9 CNY Starter Monthly Plan Available"
course: "OpenCode Chinese Practical Course"
stage: "Phase 1"
lesson: "1.4d"
duration: "15 minutes"
practice: "5 minutes"
level: "Beginner"
description: "Get MiniMax API Key and connect M2.5, M2.1 models in OpenCode."
tags:
  - "Model"
  - "MiniMax"
  - "API Key"
prerequisite:
  - "1.2 Installation"
---

# Connect MiniMax (M2.5/M2.1)

> Estimated time: 10-15 minutes

MiniMax offers models like M2.5 and M2.1, with a **Coding Plan** (e.g., Starter Monthly Plan) for trying out.

If you haven't read "What is an API Key", we recommend going back to [1.4 Overview](./04-connect).

---

## What You'll Be Able to Do

- Get MiniMax API Key
- Connect MiniMax in OpenCode
- Select a model and complete your first conversation

---

## 🎒 Before You Start

- [ ] Completed [1.2 Installation](./02-install) and can run `opencode`
- [ ] Have access to MiniMax console and obtained API Key

---

## Follow Along

### Step 1: Register and Get API Key

Visit MiniMax platform:

- https://platform.minimax.io (International)
- https://platform.minimaxi.com (China)

MiniMax offers two ways to get your Key:

- **Coding Plan (Monthly/Bundle)**: Subscribe via the page, then copy your exclusive Key from the plan management page
- **Pay-as-you-go**: Create and copy your Key from the API Key page

---

### Step 2: Connect MiniMax in OpenCode

Method A (Recommended to try first):

1. Start OpenCode:
   ```bash
   opencode
   ```
2. Enter:
   ```
   /connect
   ```
3. Search and select `MiniMax`, then paste your API Key

If MiniMax is not in your provider list, or you need to customize an Anthropic-compatible endpoint, use Method B.

---

### (Optional) Method B: Manual Custom Endpoint (Anthropic Compatible)

> Applies when: You need to specify `baseURL`, or your version doesn't have a built-in MiniMax entry.

MiniMax has two API endpoints:
- **International**: `https://api.minimax.io/anthropic/v1`
- **China**: `https://api.minimaxi.com/anthropic/v1`

1. Edit `~/.config/opencode/opencode.json` and add provider:

```json
{
  "$schema": "https://opencode.ai/config.json",
  "provider": {
    "minimax": {
      "npm": "@ai-sdk/anthropic",
      "options": {
        "baseURL": "https://api.minimax.io/anthropic/v1"
      },
      "models": {
        "MiniMax-M2.5": {
          "name": "MiniMax-M2.5"
        },
        "MiniMax-M2.1": {
          "name": "MiniMax-M2.1"
        }
      }
    }
  }
}
```

> 💡 China users can change `baseURL` to `https://api.minimaxi.com/anthropic/v1`

2. Run the login command to add your Key:

```bash
opencode auth login
```

In the interactive interface: select `Other` → enter provider ID: `minimax` → paste your API Key.

::: warning Environment Variable Conflict
If you have previously set `ANTHROPIC_AUTH_TOKEN` or `ANTHROPIC_BASE_URL`, it may affect Anthropic-compatible providers (including MiniMax).

You can clear them first:

```bash
unset ANTHROPIC_AUTH_TOKEN
unset ANTHROPIC_BASE_URL
```
:::

---

### Step 3: Select Model and Verify

Enter:

```
/models
```

Select `MiniMax-M2.5` or `MiniMax-M2.1` (or other models in your configuration/list), then send a test message:

```
Hello, please introduce yourself
```

---

## Checklist ✅

- [ ] Can see and select MiniMax models in `/models`
- [ ] Can receive AI responses after sending messages

---

## Common Issues

| Symptom | Cause | Solution |
|---------|-------|----------|
| `Cannot read properties of undefined` | Incomplete configuration or wrong Key | Check baseURL and apiKey configuration |
| No response | Environment variable conflict | Clear `ANTHROPIC_AUTH_TOKEN` and other environment variables |

---

## Next Steps

- Return to [1.4 Overview](./04-connect) to choose another route, or proceed to [2.1 Interface and Basic Operations](../2-daily/01-interface)
