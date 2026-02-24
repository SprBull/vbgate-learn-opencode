---
title: "5.21 Thinking Depth Configuration"
subtitle: "Set thinking budget for individual models"
course: "OpenCode Practical Course"
stage: "Stage 5"
lesson: "5.21"
duration: "18 min"
practice: "12 min"
level: "Advanced"
description: "Learn to set thinking budget for individual models via opencode.json, and use Ctrl+T shortcut to switch between different depths."
tags:
  - "Configuration"
  - "Model"
  - "Thinking"
  - "Shortcut"
prerequisite:
  - "5.1 Configuration Complete Guide"
---

# 5.21 Thinking Depth Configuration

> Treat "thinking depth" like gears: shallow for speed, deep for stability.

## What You'll Learn

- Set thinking budget for individual models
- Understand how the "variants" mechanism controls thinking depth
- Use <kbd>Ctrl</kbd>+<kbd>T</kbd> to switch between different thinking depths

---

## Your Current Dilemma

- Same model, sometimes you want fast, sometimes deep, but don't know how to switch
- After writing config in `opencode.json`, unsure if it took effect
- When using relay/proxy models, unsure if you can still control thinking depth

---

## When to Use This

- When you need: make "thinking depth" a switchable gear
- And don't want: change models or modify config every time

---

## 🎒 Before You Start

- [ ] Completed [5.1 Configuration Complete Guide](/en/5-advanced/01a-config-basics)
- [ ] Can start OpenCode normally

---

## Core Concept

1. OpenCode uses **model variants** to save different thinking depths
2. Variants are model-level configurations with higher priority than defaults
3. <kbd>Ctrl</kbd>+<kbd>T</kbd> cycles through variants

::: info ℹ️ What is "Thinking Depth"?
It refers to the model's "available thinking budget", such as Anthropic's `thinking.budgetTokens`.
Higher values mean more tokens available for reasoning, but slower response and higher cost.
:::

---

## Follow Along

### Step 1: Confirm Model Supports Thinking Variants

**Why** Not all models have variants, OpenCode checks `capabilities.reasoning` first.

**How** Choose a model that supports reasoning (e.g., Anthropic / Gemini 3 / OpenAI).

**You Should See** Variants like `high` / `max` appear in the model list.

---

### Step 2: Set Thinking Budget for Individual Models in opencode.json

**Why** Variant config goes under `provider.models.[modelID].variants`, which can override defaults.

**How** Fill in the corresponding fields based on your Provider:

**Anthropic Example** (thinking.budgetTokens)

```jsonc
{
  "$schema": "https://opencode.ai/config.json",
  "provider": {
    "anthropic": {
      "models": {
        "claude-sonnet-4-5": {
          "variants": {
            "high": {
              "thinking": { "type": "enabled", "budgetTokens": 20000 }
            },
            "max": {
              "thinking": { "type": "enabled", "budgetTokens": 32000 }
            }
          }
        }
      }
    }
  }
}
```

**Gemini 3 Example** (thinkingConfig.thinkingBudget)

```jsonc
{
  "$schema": "https://opencode.ai/config.json",
  "provider": {
    "google": {
      "models": {
        "gemini-3-flash": {
          "variants": {
            "high": {
              "thinkingConfig": { "includeThoughts": true, "thinkingBudget": 16000 }
            },
            "max": {
              "thinkingConfig": { "includeThoughts": true, "thinkingBudget": 24576 }
            }
          }
        }
      }
    }
  }
}
```

**You Should See** Variant values take effect after restart.

---

### Step 3: Switch Thinking Depths with Ctrl+T

**Why** After setting up variants, using a shortcut to switch is more convenient.

**How** Press <kbd>Ctrl</kbd>+<kbd>T</kbd> in the chat input box to cycle:

```
(none) → high → max → (none) → high → ...
```

**You Should See** Status bar shows current variant name (e.g., `high`).

---

### Step 4: Customize Variant Names (Optional)

**Why** Variant names aren't fixed, you can change them to things like "Deep Think" / "Fast".

**How** Use custom keys in `variants`:

```jsonc
{
  "provider": {
    "anthropic": {
      "models": {
        "claude-sonnet-4-5": {
          "variants": {
            "fast": { "thinking": { "type": "enabled", "budgetTokens": 8000 } },
            "deep": { "thinking": { "type": "enabled", "budgetTokens": 32000 } }
          }
        }
      }
    }
  }
}
```

**You Should See** <kbd>Ctrl</kbd>+<kbd>T</kbd> switches between "fast/deep".

::: info ℹ️ Custom Variants Are "Added", Not "Replaced"
OpenCode **merges** the variants you write in `opencode.json` with default variants.
If you only want custom variants, explicitly disable the default `high`/`max`:

```jsonc
{
  "provider": {
    "anthropic": {
      "models": {
        "claude-sonnet-4-5": {
          "variants": {
            "high": { "disabled": true },
            "max": { "disabled": true },
            "fast": { "thinking": { "type": "enabled", "budgetTokens": 8000 } },
            "deep": { "thinking": { "type": "enabled", "budgetTokens": 32000 } }
          }
        }
      }
    }
  }
}
```
:::

**How to Configure Third-Party Relays**

If your relay uses `openai-compatible`, it defaults to `reasoningEffort`. Example:

```jsonc
{
  "provider": {
    "relay": {
      "options": {
        "baseURL": "https://your-relay.example.com/v1",
        "apiKey": "{env:RELAY_API_KEY}"
      },
      "models": {
        "gpt-5": {
          "variants": {
            "low": { "reasoningEffort": "low" },
            "high": { "reasoningEffort": "high" }
          }
        }
      }
    }
  }
}
```

If your relay actually forwards to Anthropic (still using `openai-compatible` SDK), you can directly override with Anthropic fields:

```jsonc
{
  "provider": {
    "relay": {
      "options": {
        "baseURL": "https://your-relay.example.com/v1",
        "apiKey": "{env:RELAY_API_KEY}"
      },
      "models": {
        "claude-sonnet-4-5": {
          "variants": {
            "high": {
              "thinking": { "type": "enabled", "budgetTokens": 20000 }
            },
            "max": {
              "thinking": { "type": "enabled", "budgetTokens": 32000 }
            }
          }
        }
      }
    }
  }
}
```

Prerequisite: your relay server forwards the `thinking` field to Anthropic as-is.

---

## Checklist ✅

- [ ] `opencode.json` contains `provider.models.[modelID].variants`
- [ ] Variant name appears in status bar after startup
- [ ] <kbd>Ctrl</kbd>+<kbd>T</kbd> can cycle through variants

---

## Common Issues

| Symptom | Cause | Solution |
|-----|------|------|
| <kbd>Ctrl</kbd>+<kbd>T</kbd> does nothing | Current model has no variants | Switch to a reasoning-capable model or add variants |
| Variants exist but don't show | Haven't switched to a variant yet | Press <kbd>Ctrl</kbd>+<kbd>T</kbd> once |
| Config doesn't take effect | Wrong model ID | Copy complete ID from model list |
| Relay shows no change | Using `openai-compatible`, only supports reasoningEffort | Manually override parameters in variants |

---

## Lesson Summary

You learned:

1. Variants are "thinking depth gears", configured in `provider.models.[modelID].variants`
2. Default variants are auto-generated by ProviderTransform, can be overridden by config
3. <kbd>Ctrl</kbd>+<kbd>T</kbd> cycles through variants

---

## Next Lesson Preview

> Next we'll learn **[Debugging & Diagnostic Tools](/en/5-advanced/22-debugging)**.
>
> You'll learn:
> - How to use `opencode debug` commands
> - Diagnose LSP, config, and search issues
> - Analyze OpenCode like a developer

---

## Appendix: Source Code Reference

<details>
<summary><strong>Click to expand source code locations</strong></summary>

> Updated: 2026-01-16

| Feature | File Path | Lines |
|-----|---------|------|
| Variant generation entry | [`src/provider/transform.ts`](https://github.com/anomalyco/opencode/blob/dev/packages/opencode/src/provider/transform.ts#L297-L477) | 297-477 |
| Reasoning filter & exclusion | [`src/provider/transform.ts`](https://github.com/anomalyco/opencode/blob/dev/packages/opencode/src/provider/transform.ts#L298-L301) | 298-301 |
| Anthropic thinking budget defaults | [`src/provider/transform.ts`](https://github.com/anomalyco/opencode/blob/dev/packages/opencode/src/provider/transform.ts#L371-L385) | 371-385 |
| Gemini 3 thinking budget defaults | [`src/provider/transform.ts`](https://github.com/anomalyco/opencode/blob/dev/packages/opencode/src/provider/transform.ts#L421-L439) | 421-439 |
| Variant config Schema | [`src/config/config.ts`](https://github.com/anomalyco/opencode/blob/dev/packages/opencode/src/config/config.ts#L818-L833) | 818-833 |
| Variant config merge | [`src/provider/provider.ts`](https://github.com/anomalyco/opencode/blob/dev/packages/opencode/src/provider/provider.ts#L929-L936) | 929-936 |
| Ctrl+T default shortcut | [`src/config/config.ts`](https://github.com/anomalyco/opencode/blob/dev/packages/opencode/src/config/config.ts#L632-L688) | 632-688 |
| Ctrl+T command binding | [`src/cli/cmd/tui/app.tsx`](https://github.com/anomalyco/opencode/blob/dev/packages/opencode/src/cli/cmd/tui/app.tsx#L393-L399) | 393-399 |
| Variant cycling logic | [`src/cli/cmd/tui/context/local.tsx`](https://github.com/anomalyco/opencode/blob/dev/packages/opencode/src/cli/cmd/tui/context/local.tsx#L310-L346) | 310-346 |
| Variant display logic | [`src/cli/cmd/tui/component/prompt/index.tsx`](https://github.com/anomalyco/opencode/blob/dev/packages/opencode/src/cli/cmd/tui/component/prompt/index.tsx#L696-L700) | 696-700 |
| Variant name rendering | [`src/cli/cmd/tui/component/prompt/index.tsx`](https://github.com/anomalyco/opencode/blob/dev/packages/opencode/src/cli/cmd/tui/component/prompt/index.tsx#L946-L950) | 946-950 |
| Variant applied to LLM params | [`src/session/llm.ts`](https://github.com/anomalyco/opencode/blob/dev/packages/opencode/src/session/llm.ts#L96-L109) | 96-109 |
| Variant keybind config | [`src/config/config.ts`](https://github.com/anomalyco/opencode/blob/dev/packages/opencode/src/config/config.ts#L632-L688) | 632-688 |

**Key Constants**:
- `WIDELY_SUPPORTED_EFFORTS = ["low", "medium", "high"]`
- `OPENAI_EFFORTS = ["none", "minimal", "low", "medium", "high", "xhigh"]`

</details>
