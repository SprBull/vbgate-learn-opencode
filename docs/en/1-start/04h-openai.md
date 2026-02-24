---
title: "Connect to OpenAI (GPT-5.2 / Codex)"
subtitle: "The world's most well-known AI model provider"
course: "OpenCode Practical Guide"
stage: "Phase 1"
lesson: "1.4h"
duration: "10 minutes"
practice: "5 minutes"
level: "Beginner"
description: "Connect to OpenAI using ChatGPT subscription or API Key to access the latest models like GPT-5.2 and Codex."
tags:
  - "Model"
  - "OpenAI"
  - "GPT-5.2"
  - "Codex"
  - "ChatGPT"
prerequisite:
  - "1.2 Installation"
  - "1.3 Network Configuration"
---

# Connect to OpenAI (GPT-5.2 / Codex)

> Estimated time: 10 minutes

OpenAI is the company behind ChatGPT, providing some of the most powerful AI models available. **GPT-5.2**, released in December 2025, is the current flagship model, while **GPT-5.2-Codex** is a version specifically optimized for coding tasks.

::: warning Note for users in China
OpenAI requires a proxy to access. Please complete [1.3 Network Configuration](./03-network) first.

If you can't set up the network, consider using domestic alternatives like [Zhipu](./04c-zhipu) or [DeepSeek](./04b-deepseek).
:::

---

## What You'll Be Able to Do

- Log in to OpenCode directly with a ChatGPT subscription
- Or connect to OpenAI with an API Key
- Use the latest models like GPT-5.2 and GPT-5.2-Codex

---

## Two Login Methods

| Method | Best for | Advantages |
|--------|----------|------------|
| **ChatGPT Subscription** (Recommended) | Existing Plus/Pro members | Use directly, no extra cost |
| **API Key** | Users without subscription | Pay-as-you-go, pay only for what you use |

---

## Method 1: ChatGPT Subscription Login (Recommended)

If you're already a **ChatGPT Plus** ($20/month) or **ChatGPT Pro** ($200/month) subscriber, you can log in directly with your subscription without needing to purchase API separately.

### 🎒 Before You Start

- [ ] Completed [1.2 Installation](./02-install), able to run `opencode`
- [ ] Completed [1.3 Network Configuration](./03-network) (required for users in China)
- [ ] Have a ChatGPT Plus or Pro subscription

### Follow Along

#### Step 1: Start OpenCode

```bash
opencode
```

#### Step 2: Connect to OpenAI

Enter:

```
/connect
```

Use arrow keys to find **OpenAI**, press Enter.

#### Step 3: Select Login Method

You'll see the login method selection:

```
┌ Select auth method
│
│ ChatGPT Plus/Pro (Recommended)
│ Create an API Key
│ Manually enter API Key
└
```

Select **ChatGPT Plus/Pro**, press Enter.

#### Step 4: Browser Authorization

OpenCode will automatically open your browser and redirect to the OpenAI login page.

1. Log in with your ChatGPT account
2. Click **Authorize**
3. After seeing "Authorization successful", return to the terminal

#### Step 5: Verify Success

Back in OpenCode, you'll see:

```
✓ Login successful
```

Now enter `/models`, and you should see all OpenAI models! If you've just enabled a new model but the list hasn't updated, run `opencode models --refresh` in your system terminal to refresh the cache, then return to `/models`.

---

## Method 2: API Key Login

If you don't have a ChatGPT subscription, you can use the API Key method with pay-as-you-go pricing.

### 🎒 Before You Start

- [ ] Completed [1.2 Installation](./02-install)
- [ ] Completed [1.3 Network Configuration](./03-network) (required for users in China)
- [ ] Have an international payment method (Visa / Mastercard)

### Follow Along

#### Step 1: Register an OpenAI Account

Visit: https://platform.openai.com

Click **Sign up** and follow the prompts to register and log in.

#### Step 2: Get Your API Key

1. After logging in, click **API keys** in the left menu
2. Or visit directly: https://platform.openai.com/api-keys
3. Click **Create new secret key**
4. Give your key a name (like `opencode`)
5. **Copy and save immediately**

::: warning Shown only once!
The API Key will only be displayed once. You won't be able to see it after closing the window. Please copy it to a safe place immediately.
:::

#### Step 3: Add Credits

1. Visit: https://platform.openai.com/settings/organization/billing
2. Click **Add payment method**
3. Add a credit card and add credits (we recommend starting with $5 to try it out)

#### Step 4: Connect in OpenCode

Start OpenCode and enter:

```
/connect
```

Select **OpenAI**, then choose **Manually enter API Key**.

Paste your API Key:

```
┌ API key
│ sk-xxxxxxxxxxxxxxxxxxxxxxxx
└ Press Enter to confirm
```

---

## Selecting a Model

After successfully connecting, enter:

```
/models
```

You'll see OpenAI's model list. Here are the latest model recommendations as of January 2026:

### GPT-5.2 Series (Latest Flagship)

| Model | Features | Best for |
|-------|----------|----------|
| `gpt-5.2-chat-latest` (Instant) | Fast response, daily use | Q&A, documentation, translation |
| `gpt-5.2` (Thinking) | Deep thinking, complex tasks | Analysis, planning, difficult problems |
| `gpt-5.2-pro` | Most powerful and precise | Professional work, research |
| `gpt-5.2-codex` | **Code specialized** | Writing code, refactoring, debugging |

### Which to Choose?

- **Daily use**: `gpt-5.2-chat-latest` (fast)
- **Complex tasks**: `gpt-5.2` (powerful)
- **Coding**: `gpt-5.2-codex` (specialized)

Use arrow keys to select, press Enter to confirm.

---

## GPT-5.2-Codex Deep Dive

### What is GPT-5.2-Codex?

GPT-5.2-Codex is a **specialized coding model** released by OpenAI on December 18, 2025. It's built on GPT-5.2 with further optimization specifically for software engineering tasks.

Its features include:

- **Long-running tasks**: Supports context compression, can handle large codebases
- **Large-scale refactoring**: Excellent at code migration, refactoring, and other complex tasks
- **Enhanced visual understanding**: Can understand designs, screenshots, and technical diagrams
- **Cybersecurity capabilities**: Outstanding performance in vulnerability discovery and code auditing

### When to Use Codex?

| Scenario | Recommended Model | Reason |
|----------|------------------|--------|
| Writing complex features | ✅ GPT-5.2-Codex | Good long-running task support |
| Large-scale refactoring | ✅ GPT-5.2-Codex | Specifically optimized |
| Code migration | ✅ GPT-5.2-Codex | Can handle large codebases |
| Debugging | ✅ GPT-5.2-Codex | Deeper understanding of code logic |
| Daily Q&A | GPT-5.2 Instant | Faster |
| Writing documentation | GPT-5.2 Instant | General capabilities sufficient |

**Simply put**: Use Codex for coding, use GPT-5.2 Instant for everything else.

### Switch to Codex

Enter:

```
/models
```

Use arrow keys to find `openai / gpt-5.2-codex`, press Enter to confirm.

### Try Codex Hands-on

After switching to Codex, try this prompt:

```
Help me write a Node.js function that:
1. Reads all .md files in a specified directory
2. Extracts the title from each file (the first line starting with #)
3. Generates a table of contents index file called index.md
```

You'll find that Codex is particularly clear when understanding multi-step tasks, and the generated code structure is excellent.

### Codex Usage Tips

**1. Provide enough context**

The more Codex understands your project, the more accurate its output. Use `@` to reference relevant files:

```
@src/routes/user.ts @src/middleware/auth.ts

Help me add permission checking to the user routes
```

**2. Describe your goals clearly**

Don't just say "optimize this function", be clear about what to optimize:

```
This function has performance issues and is slow with large data.
Please optimize it with these goals:
1. Reduce database query count
2. Add caching
3. Keep the existing interface unchanged
```

**3. Let it analyze before acting**

For complex tasks, you can ask Codex to analyze first:

```
First analyze the code structure of this module, then tell me how you plan to refactor it
```

After it finishes analyzing and you confirm the direction is right, then let it take action.

**4. Leverage visual capabilities**

Codex can understand screenshots and design files. You can:

```
@design.png

Implement the page based on this design
```

---

## Checklist ✅

- [ ] Can see OpenAI models in `/models`
- [ ] Can send messages and receive AI responses
- [ ] Can switch to the GPT-5.2-Codex model

---

## Troubleshooting

| Issue | Cause | Solution |
|-------|-------|----------|
| No response after browser authorization | Network issue | Check proxy, refresh and retry |
| `connection timeout` | Network issue | Check proxy configuration, see [1.3 Network Configuration](./03-network) |
| `API key invalid` | Key copied incorrectly | Copy again, make sure there are no extra spaces |
| `insufficient_quota` | Insufficient balance | Add credits in OpenAI console |
| Page won't load | Proxy not on or unstable | Try a different proxy node |

---

## Pricing

### ChatGPT Subscription Users

- **Plus**: $20/month, includes all GPT-5.2 series models
- **Pro**: $200/month, higher usage limits, access to GPT-5.2 Pro

### API Users

Pay per token (1 token ≈ 0.75 English words ≈ 0.5 Chinese characters):

| Model | Input Price | Output Price |
|-------|-------------|--------------|
| gpt-5.2 / gpt-5.2-chat-latest | $1.75/million | $14/million |
| gpt-5.2-pro | $21/million | $168/million |

Typical daily usage is around $0.1-0.5.

---

## Next Steps

- Return to [1.4 Overview](./04-connect) to choose other models
- Or proceed to [2.1 Interface & Basic Operations](../2-daily/01-interface) to learn more

::: tip Having trouble?
Stuck during configuration? [Join the community](/en/community) to connect with 2000+ fellow learners and get real-time help.
:::
