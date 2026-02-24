---
title: "Connect Claude (Anthropic): 5-Minute Setup for Claude 3.5/3.7 | OpenCode Tutorial"
subtitle: "Connect Claude (Anthropic)"
course: "OpenCode Practical Course"
stage: "Stage 1"
lesson: "1.4e"
duration: "15 minutes"
practice: "5 minutes"
level: "Beginner"
description: "Learn to configure Anthropic Claude provider, get API Key, understand Claude 3.5/3.7 model features, and complete your first conversation."
tags:
  - Model
  - Claude
  - Anthropic
  - API Key
prerequisite:
  - "1.2 Installation"
  - "1.3 Network Configuration"
---

# Connect Claude (Anthropic)

Claude is Anthropic's large language model, excellent at complex coding tasks with a 200K tokens context window.

In regions with network restrictions, you typically need to complete [1.3 Network Configuration](/en/1-start/03-network) first, otherwise you may experience connection timeouts.

---

## What You'll Be Able to Do

- Get an Anthropic API Key and configure it in OpenCode
- Understand the features of Claude 3.5 Sonnet, Claude 3.7 Sonnet, and other models
- Complete your first conversation using Claude models

## Your Current Situation

You might have already:

- Heard about Claude's strong code generation capabilities
- Have an Anthropic API Key or Claude Max subscription
- Want to use Claude models in OpenCode

But don't know how to configure it, or which model to choose.

## When to Use This

- You have an Anthropic API Key or Claude Max subscription
- You need Claude's long context capabilities (200K tokens)
- You have high requirements for code quality and reasoning ability

---

## 🎒 Before You Start

::: warning Prerequisites
- **Anthropic Account**: Register at [console.anthropic.com](https://console.anthropic.com)
- **API Key or Claude Max subscription**: Choose one
- **Network Environment**: Need access to Anthropic API (may require VPN)
:::

---

## Core Concept

The workflow for configuring Anthropic Claude provider:

```
Get API Key → Configure in OpenCode → Verify Connection
```

---

## Follow Along

### Step 1: Get Anthropic API Key

Visit the Anthropic console to get your API Key:

1. Open [console.anthropic.com](https://console.anthropic.com)
2. Log in or register an account
3. Click **API Keys** → **Create Key**
4. Copy the generated API Key (format: `sk-ant-...`)

::: warning Security Tips
- The API Key is only shown once, save it immediately
- Do not commit the API Key to code repositories
- Rotate API Keys regularly
:::

**You should see**: A string similar to `sk-ant-api03-xxxx-xxxx-xxxx`

### Step 2: Configure in OpenCode

OpenCode provides two configuration methods, choose the one that suits you:

#### Method 1: Use Environment Variable (Recommended)

Set the API Key as an environment variable:

::: code-group

```bash [macOS/Linux (Temporary)]
export ANTHROPIC_API_KEY=sk-ant-api03-your-key-here
opencode
```

```bash [macOS/Linux (Permanent)]
# Add to ~/.bashrc or ~/.zshrc
echo 'export ANTHROPIC_API_KEY=sk-ant-api03-your-key-here' >> ~/.zshrc
source ~/.zshrc
opencode
```

```powershell [Windows (Temporary)]
$env:ANTHROPIC_API_KEY="sk-ant-api03-your-key-here"
opencode
```

```powershell [Windows (Permanent)]
# Add to system environment variables
[System.Environment]::SetEnvironmentVariable("ANTHROPIC_API_KEY", "sk-ant-api03-your-key-here", "User")
```

:::

#### Method 2: Use OpenCode Auth Command

Run the authentication command, OpenCode will save the API Key locally:

```bash
opencode auth login
```

Then:

1. Select `Anthropic`
2. Paste the API Key
3. Press Enter to complete

**You should see**: `Done` or `Login successful`

::: details Auth Storage Location
OpenCode stores authentication information at:
- **All platforms**: `~/.local/share/opencode/auth.json` (follows XDG specification)
:::

### Step 3: Verify Configuration

Verify if the Anthropic provider is configured successfully:

```bash
opencode auth list
```

**You should see**:

```
Credentials ~/.local/share/opencode/auth.json
● Anthropic api

Environment
● Anthropic ANTHROPIC_API_KEY
```

This indicates you have successfully configured the Anthropic provider.

### Step 4: View Available Models

View all models provided by Anthropic:

```bash
opencode models
```

**You should see** something like:

```
anthropic/claude-3-5-haiku-20241022
anthropic/claude-3-5-sonnet-20241022
anthropic/claude-3-7-sonnet-20250219
anthropic/claude-opus-4-20250514
...
```

::: tip View Complete Model Information
Use `opencode models --verbose` to see detailed metadata like model names and costs.
:::

### Step 5: Have Your First Conversation

Start OpenCode and select a Claude model:

```bash
cd /path/to/your/project
opencode
```

In the OpenCode interface, enter your first question:

```
Help me write a simple HTTP server
```

**You should see**:

1. AI starts generating a response (using Claude model)
2. May invoke tools to create files
3. Provides complete code and explanation

---

## Claude Model Selection Guide

Anthropic provides multiple Claude models, choose based on your needs:

| Model | Model ID | Context Window | Features | Best For |
|-------|----------|----------------|----------|----------|
| Claude 3.7 Sonnet | `claude-3-7-sonnet-20250219` | 200K | Latest and most powerful, excellent reasoning | Complex tasks, code generation, refactoring |
| Claude 3.5 Sonnet | `claude-3-5-sonnet-20241022` | 200K | Balanced performance and cost | Daily development, code review |
| Claude Opus 4 | `claude-opus-4-20250514` | 200K | Flagship performance, most expensive | Ultra-complex tasks, research work |
| Claude 3.5 Haiku | `claude-3-5-haiku-20241022` | 200K | Fast response, low cost | Simple tasks, quick Q&A |

::: tip Recommended Choices
- **Default choice**: Claude 3.7 Sonnet (most powerful)
- **Cost-sensitive**: Claude 3.5 Sonnet (best value)
- **Fast response**: Claude 3.5 Haiku (fastest)
:::

---

## Checklist ✅

After completing the above steps, you should be able to:

- [ ] See Anthropic provider in `opencode auth list`
- [ ] See Claude series models in `opencode models`
- [ ] Start OpenCode and have a conversation using Claude model
- [ ] See the model return with Claude identification

---

## Common Issues

### Invalid API Key

**Symptoms**: Shows `Authentication failed` or `Invalid API Key`

**Causes**:
- API Key format error (doesn't start with `sk-ant-`)
- API Key expired or revoked
- API Key doesn't have permission to access the specified model

**Solutions**:
1. Check if API Key format is correct
2. Regenerate API Key in Anthropic console
3. Confirm account has sufficient balance or valid subscription

### Network Connection Failed

**Symptoms**: Shows `Network error` or `Connection timeout`

**Causes**:
- Cannot access Anthropic API (may need VPN)
- Unstable network

**Solutions**:
1. Check network connection
2. Configure proxy (if needed):

```bash
export HTTP_PROXY=http://your-proxy:port
export HTTPS_PROXY=http://your-proxy:port
```

### Model Unavailable

**Symptoms**: Shows `Model not found` or model list is empty

**Causes**:
- API Key doesn't have permission to access this model
- Model has been discontinued or renamed

**Solutions**:
1. Check model access permissions in Anthropic console
2. Use `opencode models` to view available models
3. Upgrade account plan to access more models

---

## Lesson Summary

In this lesson you learned:

1. **Get API Key**: Obtain API Key from Anthropic console
2. **Configure Authentication**: Use environment variable or `opencode auth login`
3. **Verify Connection**: Confirm successful configuration and view available models
4. **Model Selection**: Understand features and use cases of different Claude models

**Key Commands**:

| Command | Purpose |
|---------|---------|
| `opencode auth login` | Configure provider authentication |
| `opencode auth list` | View configured providers |
| `opencode models` | View available models |

**Claude Model Features**:

- ✅ Long context window (200K tokens)
- ✅ Strong code generation capability
- ✅ Excellent reasoning ability (Claude 3.7 Sonnet)

---

## Next Lesson Preview

> Next lesson we'll learn about **[Claude Code Relay](/en/1-start/04f-claudecode-relay)**.
>
> You'll learn:
> - What is Claude Code relay service
> - How to configure relay endpoint
> - Differences between relay and official API

---

## Appendix: Source Code Reference

<details>
<summary><strong>Click to expand source code locations</strong></summary>

> Last updated: 2026-02-14

| Feature | File Path | Line Number |
|---------|-----------|-------------|
| Anthropic provider definition | [`src/provider/provider.ts`](https://github.com/anomalyco/opencode/blob/main/packages/opencode/src/provider/provider.ts) | 93-103 |
| Environment variable detection | [`src/provider/provider.ts`](https://github.com/anomalyco/opencode/blob/main/packages/opencode/src/provider/provider.ts) | 841-850 |
| Model data loading | [`src/provider/models.ts`](https://github.com/anomalyco/opencode/blob/main/packages/opencode/src/provider/models.ts) | 87-104 |
| Authentication management | [`src/auth/index.ts`](https://github.com/anomalyco/opencode/blob/main/packages/opencode/src/auth/index.ts) | 37-70 |

**Key Configuration**:

- **Environment variable name**: `ANTHROPIC_API_KEY`
- **Auth type**: API Key only (OAuth not supported)
- **Auto-load**: `false` (requires manual API Key configuration)

</details>
