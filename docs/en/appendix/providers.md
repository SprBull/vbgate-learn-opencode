---
title: "Model Provider List"
description: "Complete list of 75+ model providers supported by OpenCode"
---

# Model Provider List

> OpenCode supports 75+ model providers via AI SDK and Models.dev

---

## 📝 Course Notes

Key takeaways from this lesson:

<img src="/images/appendix/providers-notes.mini.jpeg"
     alt="Model Provider Notes"
     data-zoom-src="/images/appendix/providers-notes.jpeg" />

---

## Configuration

Adding a provider requires two steps:

1. Use `/connect` command to add API Key (stored in `~/.local/share/opencode/auth.json`)
2. Configure provider in `opencode.json` (optional, for custom options)

---

## OpenCode Zen (Recommended for Beginners)

Official OpenCode verified model list, ready to use.

```bash
# 1. Run in TUI
/connect

# 2. Select opencode, visit opencode.ai/auth to get API Key

# 3. View available models
/models
```

**Get API Key**: [opencode.ai/auth](https://opencode.ai/auth)

---

## International Models

### Anthropic Claude

| Model | Description |
|-------|-------------|
| `claude-sonnet-4-20250514` | Latest balanced (recommended) |
| `claude-opus-4-20250514` | Most powerful |
| `claude-3-5-haiku-20241022` | Fast model |

**Configuration**:
```bash
/connect  # Select Anthropic

# Options:
# - Claude Pro/Max (browser auth)
# - Create an API Key (create new key)
# - Manually enter API Key
```

**Get API Key**: [console.anthropic.com](https://console.anthropic.com)

---

### OpenAI

| Model | Description |
|-------|-------------|
| `gpt-4o` | Flagship multimodal |
| `gpt-4o-mini` | Budget option |
| `o1` | Reasoning model |
| `o3-mini` | Latest reasoning |

**Configuration**:
```bash
/connect  # Search OpenAI
```

**Get API Key**: [platform.openai.com](https://platform.openai.com)

---

### Google Gemini

Via Vertex AI.

| Model | Description |
|-------|-------------|
| `gemini-2.0-flash` | Latest fast version |
| `gemini-2.0-pro` | Professional |
| `gemini-1.5-pro` | Long context |

**Configuration**:
```bash
# Set Google Cloud project ID (required)
export GOOGLE_CLOUD_PROJECT=your-project-id
# Or use GCP_PROJECT / GCLOUD_PROJECT

# Set region (optional, default us-east5)
export VERTEX_LOCATION=us-east5
# Or use GOOGLE_CLOUD_LOCATION
```

> Google Vertex AI requires authentication via `gcloud auth application-default login` or service account. OpenCode automatically uses Application Default Credentials.

---

### xAI Grok

| Model | Description |
|-------|-------------|
| `grok-2` | Latest version |
| `grok-2-mini` | Budget option |

**Configuration**:
```bash
/connect  # Search xAI
```

**Get API Key**: [console.x.ai](https://console.x.ai)

---

### Mistral

Open-source model leader, supports Mistral Large, Codestral, etc.

| Model | Description |
|-------|-------------|
| `mistral-large-latest` | Most capable |
| `mistral-small-latest` | Fast response |
| `codestral-latest` | Code optimized |

```bash
/connect  # Search Mistral
```

**Get API Key**: [console.mistral.ai](https://console.mistral.ai)

---

### Cohere

Enterprise NLP capabilities, supports Rerank, Embed.

```bash
/connect  # Search Cohere
```

**Get API Key**: [dashboard.cohere.com](https://dashboard.cohere.com)

---

### Perplexity

Integrated search capabilities, real-time information.

```bash
/connect  # Search Perplexity
```

**Get API Key**: [perplexity.ai/settings/api](https://www.perplexity.ai/settings/api)

> API Key format: `pplx-...`

---

### GitHub Copilot

Use Copilot subscription.

```bash
/connect  # Search GitHub Copilot
# Visit github.com/login/device to enter authorization code
```

> Some models require Pro+ subscription, certain models need to be manually enabled in GitHub Copilot settings.

---

## DeepSeek

Excellent value, works globally. Also popular in China for direct local access.

| Model | Description |
|-------|-------------|
| `deepseek-chat` | General chat |
| `deepseek-reasoner` | Reasoning model (R1) |

**Configuration**:
```bash
# 1. Run /connect, search DeepSeek
/connect

# 2. Enter API Key

# 3. Select model
/models
```

**Get API Key**: [platform.deepseek.com](https://platform.deepseek.com)

---

## Chinese Models

### Moonshot AI

Kimi K2 model.

| Model | Description |
|-------|-------------|
| `kimi-k2` | Latest model |

**Configuration**:
```bash
/connect  # Search Moonshot AI
```

**Get API Key**: [platform.moonshot.ai](https://platform.moonshot.ai)

---

### MiniMax

| Model | Description |
|-------|-------------|
| `M2.1` | Latest model |

**Configuration**:
```bash
/connect  # Search MiniMax
```

**Get API Key**: [platform.minimax.io](https://platform.minimax.io)

---

### Z.AI (Zhipu)

GLM series models.

| Model | Description |
|-------|-------------|
| `GLM-4.7` | Latest model |

**Configuration**:
```bash
/connect  # Search Z.AI
# If subscribed to GLM Coding Plan, select Z.AI Coding Plan
```

**Get API Key**: [z.ai](https://z.ai/manage-apikey/apikey-list)

---

## Cloud Platforms

### Amazon Bedrock

```bash
# Environment variable
AWS_PROFILE=my-profile opencode

# Or config file
```

```json title="opencode.json"
{
  "$schema": "https://opencode.ai/config.json",
  "provider": {
    "amazon-bedrock": {
      "options": {
        "region": "us-east-1",
        "profile": "my-aws-profile"
      }
    }
  }
}
```

---

### Azure OpenAI

```bash
/connect  # Search Azure OpenAI
```

> - If you encounter "I'm sorry, but I cannot assist" error, change content filter from DefaultV2 to Default.
> - Azure OpenAI is configured via `/connect`, credentials are automatically stored.

---

### Azure Cognitive Services

```bash
/connect  # Search Azure Cognitive Services

# Set resource name
export AZURE_COGNITIVE_SERVICES_RESOURCE_NAME=your-resource-name
```

---

### Cloudflare Workers AI

Cloudflare edge network, global low latency.

```bash
/connect  # Search Cloudflare Workers AI

# Or set environment variables
export CLOUDFLARE_API_KEY=your-api-token
export CLOUDFLARE_ACCOUNT_ID=your-account-id
```

**Get API Token**: [dash.cloudflare.com](https://dash.cloudflare.com) → My Profile → API Tokens

---

### GitLab

GitLab Duo Chat, deeply integrated with GitLab.

```bash
/connect  # Search GitLab

# For enterprise instances
export GITLAB_INSTANCE_URL=https://gitlab.company.com
```

**Get Token**: [gitlab.com](https://gitlab.com) → Settings → Access Tokens

> Token format: `glpat-...`

---

## Aggregation Platforms

### OpenRouter

Access 100+ models with one API Key.

```bash
/connect  # Search OpenRouter
```

**Custom Models**:
```json title="opencode.json"
{
  "$schema": "https://opencode.ai/config.json",
  "provider": {
    "openrouter": {
      "models": {
        "moonshotai/kimi-k2": {
          "options": {
            "provider": {
              "order": ["baseten"],
              "allow_fallbacks": false
            }
          }
        }
      }
    }
  }
}
```

**Get API Key**: [openrouter.ai](https://openrouter.ai)

---

### Groq

Ultra-fast inference.

```bash
/connect  # Search Groq
```

**Get API Key**: [console.groq.com](https://console.groq.com)

---

### Cerebras

Ultra-fast inference, supports Qwen3 Coder 480B.

```bash
/connect  # Search Cerebras
```

**Get API Key**: [inference.cerebras.ai](https://inference.cerebras.ai)

---

### Fireworks AI

```bash
/connect  # Search Fireworks AI
```

**Get API Key**: [app.fireworks.ai](https://app.fireworks.ai)

---

### Deep Infra

```bash
/connect  # Search Deep Infra
```

**Get API Key**: [deepinfra.com/dash](https://deepinfra.com/dash)

---

### Together AI

```bash
/connect  # Search Together AI
```

**Get API Key**: [api.together.ai](https://api.together.ai)

---

### Hugging Face

Access open-source models from 17+ providers.

```bash
/connect  # Search Hugging Face
```

**Get Token**: [huggingface.co/settings/tokens](https://huggingface.co/settings/tokens/new?ownUserPermissions=inference.serverless.write&tokenType=fineGrained)

---

### Baseten

```bash
/connect  # Search Baseten
```

**Get API Key**: [app.baseten.co](https://app.baseten.co)

---

### Cortecs

Supports Kimi K2 Instruct.

```bash
/connect  # Search Cortecs
```

**Get API Key**: [cortecs.ai](https://cortecs.ai)

---

### Nebius Token Factory

```bash
/connect  # Search Nebius Token Factory
```

**Get API Key**: [tokenfactory.nebius.com](https://tokenfactory.nebius.com)

---

### IO.NET

Provides 17+ models.

```bash
/connect  # Search IO.NET
```

**Get API Key**: [ai.io.net](https://ai.io.net)

---

### Venice AI

```bash
/connect  # Search Venice AI
```

**Get API Key**: [venice.ai](https://venice.ai)

---

### OVHcloud AI Endpoints

```bash
/connect  # Search OVHcloud AI Endpoints
```

**Get API Key**: [ovh.com/manager](https://ovh.com/manager) → Public Cloud → AI & Machine Learning → AI Endpoints

---

### SAP AI Core

Access 40+ models (OpenAI, Anthropic, Google, Amazon, Meta, etc.).

```bash
/connect  # Search SAP AI Core
```

Requires Service Key JSON (containing `clientid`, `clientsecret`, `url`, `serviceurls.AI_API_URL`).

---

### Cloudflare AI Gateway

Unified access to multiple providers via Cloudflare, with unified billing.

```bash
# Set environment variables
export CLOUDFLARE_ACCOUNT_ID=your-account-id
export CLOUDFLARE_GATEWAY_ID=your-gateway-id

/connect  # Search Cloudflare AI Gateway
```

---

### Vercel AI Gateway

Unified access to multiple providers via Vercel, at-cost pricing with no markup.

```bash
/connect  # Search Vercel AI Gateway
```

**Configure Routing Order**:
```json title="opencode.json"
{
  "$schema": "https://opencode.ai/config.json",
  "provider": {
    "vercel": {
      "models": {
        "anthropic/claude-sonnet-4": {
          "options": {
            "order": ["anthropic", "vertex"]
          }
        }
      }
    }
  }
}
```

---

### Helicone

LLM observability platform, provides logging, monitoring and analytics.

```bash
/connect  # Search Helicone
```

**Get API Key**: [helicone.ai](https://helicone.ai)

**Custom Headers**:
```json title="opencode.json"
{
  "$schema": "https://opencode.ai/config.json",
  "provider": {
    "helicone": {
      "npm": "@ai-sdk/openai-compatible",
      "name": "Helicone",
      "options": {
        "baseURL": "https://ai-gateway.helicone.ai",
        "headers": {
          "Helicone-Cache-Enabled": "true",
          "Helicone-User-Id": "opencode"
        }
      }
    }
  }
}
```

---

### ZenMux

```bash
/connect  # Search ZenMux
```

**Get API Key**: [zenmux.ai/settings/keys](https://zenmux.ai/settings/keys)

---

### Ollama Cloud

Cloud-based Ollama service.

```bash
/connect  # Search Ollama Cloud
```

> Pull model info locally first: `ollama pull gpt-oss:20b-cloud`

**Get API Key**: [ollama.com](https://ollama.com) → Settings → Keys

---

## Local Models

### Ollama

```json title="opencode.json"
{
  "$schema": "https://opencode.ai/config.json",
  "provider": {
    "ollama": {
      "npm": "@ai-sdk/openai-compatible",
      "name": "Ollama (local)",
      "options": {
        "baseURL": "http://localhost:11434/v1"
      },
      "models": {
        "llama3.1": {
          "name": "Llama 3.1"
        }
      }
    }
  }
}
```

> If tool calling doesn't work, try increasing Ollama's `num_ctx`, recommended 16k-32k.

**Install**: [ollama.ai](https://ollama.ai)

---

### LM Studio

```json title="opencode.json"
{
  "$schema": "https://opencode.ai/config.json",
  "provider": {
    "lmstudio": {
      "npm": "@ai-sdk/openai-compatible",
      "name": "LM Studio (local)",
      "options": {
        "baseURL": "http://127.0.0.1:1234/v1"
      },
      "models": {
        "google/gemma-3n-e4b": {
          "name": "Gemma 3n-e4b (local)"
        }
      }
    }
  }
}
```

**Install**: [lmstudio.ai](https://lmstudio.ai)

---

### llama.cpp

```json title="opencode.json"
{
  "$schema": "https://opencode.ai/config.json",
  "provider": {
    "llama.cpp": {
      "npm": "@ai-sdk/openai-compatible",
      "name": "llama-server (local)",
      "options": {
        "baseURL": "http://127.0.0.1:8080/v1"
      },
      "models": {
        "qwen3-coder:a3b": {
          "name": "Qwen3-Coder: a3b-30b (local)",
          "limit": {
            "context": 128000,
            "output": 65536
          }
        }
      }
    }
  }
}
```

---

## Custom Providers

Add any OpenAI-compatible provider:

```bash
# 1. Run /connect, select Other
/connect

# 2. Enter provider ID (e.g., myprovider)

# 3. Enter API Key
```

```json title="opencode.json"
{
  "$schema": "https://opencode.ai/config.json",
  "provider": {
    "myprovider": {
      "npm": "@ai-sdk/openai-compatible",
      "name": "My Provider",
      "options": {
        "baseURL": "https://api.myprovider.com/v1"
      },
      "models": {
        "my-model": {
          "name": "My Model",
          "limit": {
            "context": 200000,
            "output": 65536
          }
        }
      }
    }
  }
}
```

**Configuration Options**:
- `npm` - AI SDK package name, use `@ai-sdk/openai-compatible` for OpenAI-compatible
- `name` - UI display name
- `options.baseURL` - API endpoint
- `options.apiKey` - API Key (optional, set when not using auth)
- `options.headers` - Custom request headers
- `models` - Available models list
- `limit.context` - Max input tokens
- `limit.output` - Max output tokens

---

## Custom Base URL

Set custom endpoints for any provider (e.g., proxy services):

```json title="opencode.json"
{
  "$schema": "https://opencode.ai/config.json",
  "provider": {
    "anthropic": {
      "options": {
        "baseURL": "https://my-proxy.com/v1"
      }
    }
  }
}
```

---

## Model Selection Guide

| Requirement | Recommendation | Reason |
|-------------|----------------|--------|
| Easiest to start | Claude Sonnet 4 | Best coding, reliable |
| Best reasoning | Claude Opus 4 | Industry leading |
| Best value | DeepSeek | Affordable, capable |
| Best coding | Claude Sonnet 4 | Professional programming |
| Long documents | Gemini 1.5 Pro | Ultra-long context |
| Fully offline | Ollama + Llama3.1 | Local runtime |
| Multi-model access | OpenRouter | One key for all |

---

## Troubleshooting

1. **Check Authentication**: Run `opencode auth list` to view configured credentials

2. **Custom Provider Issues**:
   - Ensure provider ID in `/connect` matches config file
   - Use correct npm package (e.g., `@ai-sdk/openai-compatible`)
   - Check `options.baseURL` is correct

---

## Related Resources

- [Connect Models](/en/1-start/04-connect) - Configuration tutorial
- [Config Reference](/en/appendix/config-ref) - Config file details
