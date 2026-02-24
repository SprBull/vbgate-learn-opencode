---
title: "Connect to Qwen (Alibaba Cloud)"
subtitle: "Alibaba Ecosystem, All-Purpose General Model"
course: "OpenCode Practical Course"
stage: "Stage 1"
lesson: "1.4i"
duration: "10 minutes"
practice: "5 minutes"
level: "Beginner"
description: "Get Alibaba Cloud Bailian API Key and use Qwen models in OpenCode."
tags:
  - "Model"
  - "Qwen"
  - "Alibaba Cloud"
  - "DashScope"
  - "API Key"
prerequisite:
  - "1.2 Installation"
---

# Connect to Qwen (Alibaba Cloud)

> Estimated time: 5-10 minutes

Qwen is Alibaba Cloud's large language model, providing API services through the Bailian platform (DashScope). It features comprehensive capabilities, a complete ecosystem, and a rich variety of models.

If you haven't read "What is an API Key", we recommend going back to [1.4 Overview](/en/1-start/04-connect) to understand the concepts first.

---

## What You'll Learn

- Get an Alibaba Cloud Bailian API Key
- Connect Qwen to OpenCode
- Choose the right model for your scenario
- Send your first message and receive a response

---

## 🎒 Prerequisites

- [ ] Completed [1.2 Installation](/en/1-start/02-install), able to run `opencode`
- [ ] Have an Alibaba Cloud account (or can register)

---

## Follow Along

### Step 1: Register for Alibaba Cloud Account

Visit: https://bailian.console.alibabacloud.com

If you don't have an Alibaba Cloud account, follow the prompts to register and complete identity verification.

---

### Step 2: Enable Bailian Service

1. Enter the Bailian console
2. Follow the prompts to enable DashScope service
3. Accept the service agreement

---

### Step 3: Get Your API Key

1. Go to the API-KEY management page
   - Or visit directly: https://bailian.console.alibabacloud.com/#/api-key
2. Create a new API Key
3. **Copy and save it immediately**

::: warning Only shown once!
The API Key will only be displayed once. You won't see the complete Key after closing the window.

Please copy it to a secure location immediately. Don't share it in chats, don't screenshot it, and don't commit it to GitHub.
:::

---

### Step 4: Connect Qwen to OpenCode

Start OpenCode:

```bash
opencode
```

Enter:

```
/connect
```

In the provider list, search for and select:

- **International users**: Select `Alibaba` or search for `alibaba`

Then paste your API Key.

On success, you'll see:

```
✓ Provider added successfully!
```

::: tip International vs China Version
The two versions use different API endpoints:
- China version (`alibaba-cn`): `dashscope.aliyuncs.com`
- International version (`alibaba`): `dashscope-intl.aliyuncs.com`

If you're outside mainland China, using the wrong version may cause connection timeouts or failures.
:::

---

### Step 5: Select Model and Verify

Enter:

```
/models
```

Choose the appropriate model based on your use case:

| Scenario | Recommended Model | Description |
|----------|-------------------|-------------|
| Coding & Development | `qwen3-coder-flash` | 1M context, 65K output, code-specialized |
| General Chat | `qwen-plus`, `qwen-turbo` | Cost-effective, supports reasoning |
| Deep Reasoning | `qwq-plus` | Supports reasoning, ideal for complex problems |
| Visual Understanding | `qwen-vl-max` | Supports image input |

After selecting a model, send a test message:

```
Hello, please introduce yourself
```

If you receive a response, the connection is successful.

---

## Using Environment Variables (Optional)

Besides configuring via the `/connect` command, you can also use environment variables:

```bash
# Method 1: Set at startup
DASHSCOPE_API_KEY=sk-xxx opencode

# Method 2: Add to shell config file
echo 'export DASHSCOPE_API_KEY=sk-xxx' >> ~/.bashrc
source ~/.bashrc
```

---

## Custom Configuration File (Advanced)

If you need to customize the baseURL or add additional models, you can configure them in `opencode.json`:

```jsonc
{
  "$schema": "https://opencode.ai/config.json",
  "provider": {
    "alibaba": {
      "options": {
        "baseURL": "https://dashscope-intl.aliyuncs.com/compatible-mode/v1"
      }
    }
  }
}
```

---

## Checklist ✅

- [ ] Can see Qwen models in `/models`
- [ ] Can receive AI responses when sending messages
- [ ] No errors (like `API key invalid` / `connection error`)

---

## Common Issues

| Issue | Cause | Solution |
|-------|-------|----------|
| `API key invalid` | Key copied incorrectly or service not enabled | Confirm Bailian service is enabled, get a new Key |
| Can't find Alibaba option | OpenCode version too old | Upgrade OpenCode: `opencode upgrade` |
| Insufficient balance | Free quota exhausted | Top up in console |
| Identity verification required | Alibaba Cloud requires verification | Complete identity verification and retry |
| Connection timeout | Wrong version selected | International users should select `alibaba` |
| Some models don't support tool_call | Not all models support tool calls | Use `qwen-plus` or `qwen3-coder-flash` |

---

## Next Steps

- Return to [1.4 Overview](/en/1-start/04-connect) to choose another route, or proceed to [2.1 Interface & Basic Operations](/en/2-daily/01-interface)
