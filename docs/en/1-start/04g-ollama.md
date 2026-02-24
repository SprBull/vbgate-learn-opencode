---
title: "Connect Ollama (Local Models)"
subtitle: "Fully offline, completely free"
course: "OpenCode Practical Course"
stage: "Stage 1"
lesson: "1.4g"
duration: "30 minutes"
practice: "10 minutes"
level: "Beginner"
description: "Install Ollama, choose a suitable local model, and complete your first offline conversation in OpenCode."
tags:
  - "Models"
  - "Ollama"
  - "Local"
  - "Offline"
prerequisite:
  - "1.2 Installation"
---

# Connect Ollama (Local Models)

Ollama lets you run local models on your own computer: **all data stays on your machine, ideal for sensitive information and confidential projects**. No API Key needed, works offline.

---

## What You'll Be Able to Do

> No hype, just things you can do right away

- Use OpenCode to handle sensitive data in a completely offline environment where data never leaves your machine
- Install and verify that Ollama is working properly
- Choose and download a suitable local model based on your hardware
- Configure and use Ollama local models in OpenCode, completing your first conversation

<!-- 📹 Demo: Local Ollama + OpenCode first conversation -->

---

## Your Current Dilemma

> If you're experiencing these, this lesson is for you

- You have many sensitive files on your desktop (financial data, customer information, personal privacy, etc.) and don't want to upload them to third-party AI models
- You're developing highly confidential projects where code and documents **absolutely cannot** leave company computers
- You have strict data privacy requirements—even if AI providers promise not to save data, you don't want any data leaving your machine
- Your network environment is restricted and you need to use AI assistants offline
- You entered `/connect` looking for local Ollama but only see **Ollama Cloud** and don't know what to do next

---

## When to Use This

> Core value of local models: **Privacy First**

- When you need to:
  - Handle sensitive data (financial reports, customer data, personal privacy)
  - Develop confidential projects (trade secrets, patent code, security systems)
  - Ensure data never leaves your machine (zero-trust principle, compliance requirements)

- And you don't want to:
  - Upload desktop files or Excel content to third parties
  - Let project code leave your computer
  - Depend on network connection to use AI

::: tip 💡 Local Models vs Cloud Models
| Scenario | Local Model (Ollama) | Cloud Model |
|-----|------------------|---------|
| Processing sensitive Excel data | ✅ Data stays local | ❌ Needs upload |
| Developing confidential projects | ✅ Code processed locally | ❌ Needs upload |
| Daily development tasks | ⚠️ Weaker capability | ✅ Stronger capability |
| Fully offline use | ✅ Supported | ❌ Requires network |
:::

---

## 🎒 Before You Start

> Make sure you've completed the following, otherwise stop here

- [ ] Completed [1.2 Installation](./02-install), can run `opencode --version`
- [ ] Your hard drive has at least 10GB free space (model files get big quickly)
- [ ] You roughly know your machine's RAM/VRAM capacity (not critical if you don't, recommendations below)

---

## Core Concept

> First explain "how to think", not commands

- **Core advantage of local models: Privacy and Confidentiality**
  - All data is processed locally, nothing is sent to third-party servers
  - Suitable for: financial data, customer information, personal privacy, trade secrets, patent code, etc.
- `/connect` is only for saving API keys (that's why you see Ollama Cloud); local Ollama doesn't need a key, you need to configure the provider in `opencode.json` to make it appear in `/models`
- Running local models mainly depends on **RAM/VRAM**: larger models need more resources
- Don't chase 70B right away as a beginner: start with 7B/8B to get the workflow working, then upgrade
- When choosing models, consider both:
  - **Parameter size (B)**: Generally larger means stronger
  - **Use case**: For coding, prefer `*-coder`; for general chat, choose `llama`/`qwen`/`gemma`

---

## Follow Along

> Step by step, assuming you might make mistakes

### Step 1: Install Ollama

**Why**  
You need a local model runtime that will start a service on your machine, so OpenCode can connect to it.

::: code-group

```bash [macOS]
brew install ollama
```

```bash [Linux]
curl -fsSL https://ollama.com/install.sh | sh
```

```powershell [Windows]
# Download installer from official website
# https://ollama.com/download
```

:::

Verify installation:

```bash
ollama --version
```

**You should see**: Version number output (e.g., `ollama version x.y.z`).

### Step 2: Choose a Model Suitable for Your Hardware and Download

**Why**  
If you choose a model that's too large, common results are: long download time, slow execution, or even insufficient memory/VRAM.

First, remember this selection rule (experience-based, good enough for beginners):

- **3B~8B**: Entry-level/lightweight, can run on 16GB RAM computers
- **14B**: Noticeably stronger, usually needs 16GB VRAM or 32GB+ RAM for comfortable use
- **27B~32B**: High-quality local assistant, recommends 24GB~32GB VRAM or 48GB+ RAM
- **70B/72B**: Local "ceiling" level, usually needs 48GB+ VRAM (or multi-card/CPU hybrid offload, speed will drop noticeably)

::: tip Download Size ≠ Runtime Usage
The GB shown on Ollama model pages is "download file size". Runtime also needs additional KV cache (longer context uses more RAM/VRAM).

Recommend reserving at least 1.2~1.5x "download size" as available RAM/VRAM headroom.
:::

**Popular Model Recommendations (by Use Case)**:

- General chat (lightweight): `llama3.2:3b` (~2.0GB download)
- General chat (stronger): `llama3.1:8b` (~4.9GB download)
- Chinese/General capability: `qwen2.5:7b` (~4.7GB download), `qwen2.5:14b` (~9.0GB download)
- Coding priority: `qwen2.5-coder:7b` (~4.7GB download), `qwen2.5-coder:14b` (~9.0GB download), `qwen2.5-coder:32b` (~20GB download)
- Other common: `gemma2:9b` (~5.4GB download), `mistral:7b` (~4.4GB download)

**Choose by Hardware (Experience-Based)**:

| Your Hardware | Recommended Parameter Size | Recommended Models (Examples) |
|---|---|---|
| MacBook (Apple Silicon) 16GB Unified Memory (e.g., M4 16GB) | 3B~8B | `llama3.2:3b` / `llama3.1:8b` / `qwen2.5-coder:7b` |
| Discrete GPU 16GB VRAM (e.g., 16GB VRAM NVIDIA/AMD) | 7B~14B | `qwen2.5-coder:14b` / `qwen2.5:14b` / `gemma2:9b` |
| Discrete GPU 24GB VRAM | 14B~32B | `qwen2.5-coder:32b` / `qwen2.5:32b` / `gemma2:27b` |
| Discrete GPU 32GB VRAM (e.g., RTX 5090 32GB) | 32B | `qwen2.5-coder:32b` / `qwen2.5:32b` |
| Discrete GPU 48GB+ VRAM | 70B/72B | `llama3.1:70b` / `qwen2.5:72b` |

::: warning About "What Can a 5090 Run"
The key isn't the model number, but your **VRAM size**.

If your 5090 has 24GB~32GB VRAM, it's generally better suited for 32B class; 70B/72B often needs 48GB+ VRAM, or CPU hybrid offload (will run but slower).
:::

Start downloading (choose one, recommend getting the workflow working first):

```bash
# Coding priority (recommended)
ollama pull qwen2.5-coder:7b

# General chat
ollama pull llama3.1:8b

# Lighter weight
ollama pull llama3.2:3b
```

**You should see**: Download progress and success message like `pulling manifest ... success`.

### Step 3: Start Ollama Service

**Why**  
OpenCode needs to communicate with Ollama through a local HTTP service.

Run in terminal:

```bash
ollama serve
```

**You should see**: `Listening on 127.0.0.1:11434` (keep this terminal window open).

### Step 4: Configure "Local Ollama Provider" in OpenCode (Copy-Paste Ready)

**Why**  
Only seeing **Ollama Cloud** in `/connect` is normal: `/connect` only handles saving API keys (to `~/.local/share/opencode/auth.json`).

Local Ollama doesn't need a key, so the correct approach is: configure a provider in `opencode.json`, putting Ollama's OpenAI-compatible address in it.

**Where to Put the Config? (Choose One)**

- Global: `~/.config/opencode/opencode.json` (works for all projects)
- Project-level: put `opencode.json` in the current project root (only affects this project)

If you're unsure which path OpenCode is reading, you can run:

```bash
opencode debug paths
```

**Copy-Paste Ready Config (Local Ollama)**:

```json
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
        "qwen2.5-coder:7b": { "name": "Qwen2.5 Coder 7B (local)" },
        "llama3.1:8b": { "name": "Llama 3.1 8B (local)" },
        "llama3.2:3b": { "name": "Llama 3.2 3B (local)" }
      }
    }
  }
}
```

::: tip Two Easily Overlooked Points
1. The key in `models` (e.g., `qwen2.5-coder:7b`) should match the model name you `ollama pull`ed.
2. This config only "declares the list of available models" in OpenCode; it doesn't download models for you. Downloading still requires `ollama pull ...`.
:::

**You should see**: After saving the config and restarting OpenCode, models under `Ollama (local)` will appear in `/models` (verify in next step).

### Step 5: Restart OpenCode, Select Local Model, and Send First Message

**Why**  
OpenCode reads `opencode.json` at startup; you usually need to restart once after changing config.

Open a new terminal:

```bash
opencode
```

Enter:

```
/models
```

Select the model you just downloaded and configured, then send:

```
Hello, please introduce yourself
```

**You should see**: The model starts outputting a response (local models might be a bit slower than cloud).

<!-- 📹 Operation demo: from downloading model to first conversation -->

---

## Why Use Local Models?

> Local models vs Cloud models: Choosing the right scenario matters

### Two Core Values of Local Models

**1. Privacy Protection: Data Never Leaves Your Machine**

When using local models, all your data (including file contents, code, conversation history) is processed on your own computer, not sent to any third-party servers.

**Typical Use Cases:**
- Processing sensitive Excel data (financial reports, customer data, payroll, etc.)
- Analyzing desktop files and folders (containing personal privacy or trade secrets)
- Organizing personal documents (ID numbers, bank information, health records, etc.)

::: warning ⚠️ Why This Matters
Even if AI service providers promise "not to save your data", the data does **get transmitted to their servers**. For strict compliance requirements (like finance, healthcare, government), this may violate regulations.
:::

**2. Project Confidentiality: Code Never Leaves Your Machine**

When developing highly confidential projects, using local models ensures code and documents are always processed on your computer.

**Typical Use Cases:**
- Developing trade secret projects (unreleased products, patent technology)
- Security-related development (security tools, encryption systems, protection systems)
- Client-commissioned projects (signed NDAs, code cannot be shared)
- Enterprise internal projects (source code contains internal secrets)

::: tip 💡 When You Must Use Local Models
If any of these apply, **strongly recommend using local models**:
- ✅ Project has NDA or compliance requirements
- ✅ Code involves patent technology or trade secrets
- ✅ Data involves personal privacy (ID, bank cards, medical records)
- ✅ Data belongs to clients or partners (needs confidentiality)
- ✅ Company security policy prohibits uploading data to external services
:::

### Limitations of Local Models

While local models are great for privacy, they have limitations:

| Aspect | Local Models | Cloud Models |
|-----|---------|---------|
| **Privacy & Security** | ⭐⭐⭐⭐⭐ Data stays local | ⭐⭐ Data needs upload |
| **Model Capability** | ⭐⭐⭐ Relatively weaker | ⭐⭐⭐⭐⭐ Stronger |
| **Response Speed** | ⭐⭐ Depends on hardware | ⭐⭐⭐⭐⭐ Faster |
| **Cost** | ⭐⭐⭐⭐⭐ Free (needs hardware) | ⭐⭐ Requires payment |
| **Network Requirement** | ⭐⭐⭐⭐⭐ Works offline | ⭐ Needs network |

::: tip 💡 Recommended Usage Strategy
**For most users:**
- Sensitive data, confidential projects → Local models
- Daily development, non-sensitive tasks → Cloud models (stronger capability)

**Hybrid strategy:**
1. First use local models for sensitive parts
2. Then use cloud models for non-sensitive parts (if needed)
:::

---

## Checklist ✅

> Must pass all items to continue; if any fails, go back to the corresponding step

- [ ] `ollama --version` outputs a version number
- [ ] `ollama serve` listens on `127.0.0.1:11434`
- [ ] `opencode.json` has `baseURL: http://localhost:11434/v1` configured
- [ ] In OpenCode, `/models` shows `Ollama (local)` and your configured models
- [ ] Sending a message receives a response

---

## Common Pitfalls

> 80% of people get stuck here

| Symptom | Cause | Solution |
|-----|-----|-----|
| Only Ollama Cloud in `/connect` | `/connect` only saves API keys | Configure `opencode.json` per Step 4, then use `/models` to select local model |
| Can't see `Ollama (local)` in `/models` | Config file location wrong / JSON syntax error / didn't restart OpenCode | Run `opencode debug paths` to find config directory; check JSON; restart OpenCode |
| `connection refused` | Ollama service not started | Run `ollama serve` first, then go back to OpenCode `/models` |
| Download very slow | Network issues or slow mirror | Try again at different time; download smaller model first (3B/7B) |
| Freezes / out of memory error | Model too large | Go down one tier (e.g., 14B → 7B/8B; 32B → 14B) |
| Response very slow | Running on CPU / insufficient resources / first load | Close resource-heavy apps first; try smaller model; first load being slow is normal |
| Port already in use | `ollama serve` already running | Don't start multiple times; keep one service process |

::: warning Ollama Notes
1. Before using OpenCode each time, start `ollama serve` first
2. Local models aren't as capable as Claude, DeepSeek; may struggle with complex tasks
3. If your computer gets hot and fans spin loudly, that's normal
:::

---

## Lesson Summary

You learned:

1. Understand the core value of local models: **Privacy protection and project confidentiality**
2. Install and verify Ollama
3. Choose and download suitable local models based on hardware
4. Configure and use Ollama local models in `opencode.json` to complete first conversation

---

## Next Lesson Preview

> You've got the local model workflow working. Next is the final lesson of Stage 1: Auto-update.

::: tip Quick Preview
OpenCode auto-updates by default, usually nothing to worry about. Want to know more? → [1.5 Auto-update](./05-update)
:::

::: tip Having Issues?
Local model loading slow? [Join the community](/en/community) and connect with 2000+ fellow learners for real-time Q&A.
:::
