---
title: "OpenCode Zen"
description: "Curated model service tested and validated by the OpenCode team"
---

# OpenCode Zen

OpenCode Zen is a curated model service tested and validated by the OpenCode team.

> OpenCode Zen is currently in Beta.

Zen works like any other provider in OpenCode. You log in to OpenCode Zen to get an API key. It's **completely optional** — you can use OpenCode without it.

## Background

There are many models on the market, but only a few work well as coding agents. Additionally, most providers have varying configurations, leading to inconsistent performance and quality.

> We've tested a set of models that work well with OpenCode.

If you use models through services like OpenRouter, you can't be sure you're getting the best version.

To address this, we've done several things:

1. Tested a curated set of models and discussed with the team how to run them optimally
2. Partnered with several providers to ensure they're served correctly
3. Benchmarked model/provider combinations to produce a recommendation list

OpenCode Zen is an AI gateway that gives you access to these models.

## How to Use

<AdInArticle />

OpenCode Zen works like other providers:

1. Log in to the [OpenCode Zen Console](https://console.opencode.ai), add payment information, and copy your API key
2. Run the `/connect` command in the TUI, select OpenCode Zen, and paste your API key
3. Run `/models` in the TUI to see the list of recommended models

Billing is per-request. You can add credits to your account.

## API Endpoints

You can also access models through the following API endpoints:

| Model | Model ID | Endpoint | AI SDK Package |
|-------|----------|----------|----------------|
| GPT 5.2 | gpt-5.2 | `https://opencode.ai/zen/v1/responses` | `@ai-sdk/openai` |
| GPT 5.1 | gpt-5.1 | `https://opencode.ai/zen/v1/responses` | `@ai-sdk/openai` |
| GPT 5.1 Codex | gpt-5.1-codex | `https://opencode.ai/zen/v1/responses` | `@ai-sdk/openai` |
| GPT 5.1 Codex Max | gpt-5.1-codex-max | `https://opencode.ai/zen/v1/responses` | `@ai-sdk/openai` |
| GPT 5.1 Codex Mini | gpt-5.1-codex-mini | `https://opencode.ai/zen/v1/responses` | `@ai-sdk/openai` |
| GPT 5 | gpt-5 | `https://opencode.ai/zen/v1/responses` | `@ai-sdk/openai` |
| GPT 5 Codex | gpt-5-codex | `https://opencode.ai/zen/v1/responses` | `@ai-sdk/openai` |
| GPT 5 Nano | gpt-5-nano | `https://opencode.ai/zen/v1/responses` | `@ai-sdk/openai` |
| Claude Sonnet 4.5 | claude-sonnet-4-5 | `https://opencode.ai/zen/v1/messages` | `@ai-sdk/anthropic` |
| Claude Sonnet 4 | claude-sonnet-4 | `https://opencode.ai/zen/v1/messages` | `@ai-sdk/anthropic` |
| Claude Haiku 4.5 | claude-haiku-4-5 | `https://opencode.ai/zen/v1/messages` | `@ai-sdk/anthropic` |
| Claude Haiku 3.5 | claude-3-5-haiku | `https://opencode.ai/zen/v1/messages` | `@ai-sdk/anthropic` |
| Claude Opus 4.5 | claude-opus-4-5 | `https://opencode.ai/zen/v1/messages` | `@ai-sdk/anthropic` |
| Claude Opus 4.1 | claude-opus-4-1 | `https://opencode.ai/zen/v1/messages` | `@ai-sdk/anthropic` |
| MiniMax M2.1 | minimax-m2.1-free | `https://opencode.ai/zen/v1/messages` | `@ai-sdk/anthropic` |
| Gemini 3 Pro | gemini-3-pro | `https://opencode.ai/zen/v1/models/gemini-3-pro` | `@ai-sdk/google` |
| Gemini 3 Flash | gemini-3-flash | `https://opencode.ai/zen/v1/models/gemini-3-flash` | `@ai-sdk/google` |
| GLM 4.6 | glm-4.6 | `https://opencode.ai/zen/v1/chat/completions` | `@ai-sdk/openai-compatible` |
| GLM 4.7 | glm-4.7-free | `https://opencode.ai/zen/v1/chat/completions` | `@ai-sdk/openai-compatible` |
| Kimi K2 | kimi-k2 | `https://opencode.ai/zen/v1/chat/completions` | `@ai-sdk/openai-compatible` |
| Kimi K2 Thinking | kimi-k2-thinking | `https://opencode.ai/zen/v1/chat/completions` | `@ai-sdk/openai-compatible` |
| Qwen3 Coder 480B | qwen3-coder | `https://opencode.ai/zen/v1/chat/completions` | `@ai-sdk/openai-compatible` |
| Grok Code Fast 1 | grok-code | `https://opencode.ai/zen/v1/chat/completions` | `@ai-sdk/openai-compatible` |
| Big Pickle | big-pickle | `https://opencode.ai/zen/v1/chat/completions` | `@ai-sdk/openai-compatible` |

Model IDs in OpenCode configuration use the format `opencode/<model-id>`. For example, GPT 5.1 Codex uses `opencode/gpt-5.1-codex`.

### Getting the Model List

Get available models and their metadata:

```
https://opencode.ai/zen/v1/models
```

## Pricing

Pay per request. Prices below are **per 1 million tokens**:

| Model | Input | Output | Cache Read | Cache Write |
|-------|-------|--------|------------|-------------|
| Big Pickle | Free | Free | Free | - |
| Grok Code Fast 1 | Free | Free | Free | - |
| MiniMax M2.1 | Free | Free | Free | - |
| GLM 4.7 | Free | Free | Free | - |
| GLM 4.6 | $0.60 | $2.20 | $0.10 | - |
| Kimi K2 | $0.40 | $2.50 | - | - |
| Kimi K2 Thinking | $0.40 | $2.50 | - | - |
| Qwen3 Coder 480B | $0.45 | $1.50 | - | - |
| Claude Sonnet 4.5 (≤ 200K tokens) | $3.00 | $15.00 | $0.30 | $3.75 |
| Claude Sonnet 4.5 (> 200K tokens) | $6.00 | $22.50 | $0.60 | $7.50 |
| Claude Sonnet 4 (≤ 200K tokens) | $3.00 | $15.00 | $0.30 | $3.75 |
| Claude Sonnet 4 (> 200K tokens) | $6.00 | $22.50 | $0.60 | $7.50 |
| Claude Haiku 4.5 | $1.00 | $5.00 | $0.10 | $1.25 |
| Claude Haiku 3.5 | $0.80 | $4.00 | $0.08 | $1.00 |
| Claude Opus 4.5 | $5.00 | $25.00 | $0.50 | $6.25 |
| Claude Opus 4.1 | $15.00 | $75.00 | $1.50 | $18.75 |
| Gemini 3 Pro (≤ 200K tokens) | $2.00 | $12.00 | $0.20 | - |
| Gemini 3 Pro (> 200K tokens) | $4.00 | $18.00 | $0.40 | - |
| Gemini 3 Flash | $0.50 | $3.00 | $0.05 | - |
| GPT 5.2 | $1.75 | $14.00 | $0.175 | - |
| GPT 5.1 | $1.07 | $8.50 | $0.107 | - |
| GPT 5.1 Codex | $1.07 | $8.50 | $0.107 | - |
| GPT 5.1 Codex Max | $1.25 | $10.00 | $0.125 | - |
| GPT 5.1 Codex Mini | $0.25 | $2.00 | $0.025 | - |
| GPT 5 | $1.07 | $8.50 | $0.107 | - |
| GPT 5 Codex | $1.07 | $8.50 | $0.107 | - |
| GPT 5 Nano | Free | Free | Free | - |

You may see _Claude Haiku 3.5_ in your usage history — this is a low-cost model used to generate session titles.

> Credit card charges are passed through at cost (4.4% + $0.30 per transaction), we don't add any extra fees.

Free model notes:

- **Grok Code Fast 1**: Free for a limited time, the xAI team is collecting feedback to improve Grok Code
- **GLM 4.7**: Free for a limited time, the team is collecting feedback to improve the model
- **MiniMax M2.1**: Free for a limited time, the team is collecting feedback to improve the model
- **Big Pickle**: Stealth model, free for a limited time, the team is collecting feedback to improve the model

### Auto-Reload

When your balance falls below $5, Zen will automatically reload $20.

You can change the auto-reload amount or disable auto-reload entirely.

### Monthly Limits

You can set monthly usage limits for your entire workspace and for each team member.

For example, if you set a monthly limit of $20, Zen won't use more than $20 per month. However, if auto-reload is enabled, you may be charged more than $20 when your balance falls below $5.

## Privacy

All models are hosted in the United States. Providers follow a zero-retention policy and don't use your data for model training, with the following exceptions:

- **Grok Code Fast 1**: Data collected during the free period may be used to improve Grok Code
- **GLM 4.7**: Data collected during the free period may be used to improve the model
- **MiniMax M2.1**: Data collected during the free period may be used to improve the model
- **Big Pickle**: Data collected during the free period may be used to improve the model
- **OpenAI API**: Requests are retained for 30 days according to [OpenAI's data policy](https://platform.openai.com/docs/guides/your-data)
- **Anthropic API**: Requests are retained for 30 days according to [Anthropic's data policy](https://docs.anthropic.com/en/docs/claude-code/data-usage)

## Team Features

Zen is great for teams. You can invite teammates, assign roles, manage which models your team uses, and more.

> Workspace management is free during Beta.

### Roles

You can invite teammates and assign roles:

- **Admin**: Manage models, members, API keys, and billing
- **Member**: Can only manage their own API keys

Admins can also set monthly spending limits for each member.

### Model Access Control

Admins can enable or disable specific models for the workspace. Requests sent to disabled models will return an error.

This is useful for blocking models that collect data.

### Bring Your Own Key

You can use your own OpenAI or Anthropic API keys while still accessing other models in Zen.

When using your own keys, tokens are billed directly by the provider, not Zen.

For example, your organization might already have OpenAI or Anthropic keys and want to use them instead of Zen-provided keys.

## Goals

We created OpenCode Zen to:

1. **Benchmark** the best models/providers for coding agents
2. Provide access to the **highest quality** options without downgrading performance or routing to cheaper providers
3. **Pass on price reductions** at cost — the only markup is processing fees
4. Have **no lock-in**, allowing use with any other coding agent and allowing use of any other provider in OpenCode
