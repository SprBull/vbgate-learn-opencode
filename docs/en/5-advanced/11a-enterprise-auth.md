---
title: "5.11a Enterprise Authentication Integration"
subtitle: "Connecting your unified authentication and organization default settings"
course: "OpenCode Practical Course"
stage: "Stage 5"
lesson: "5.11a"
duration: "30 minutes"
practice: "35 minutes"
level: "Advanced"
description: "Connect company unified authentication, inject tokens saved during login into OpenCode process environment variables, and distribute organization default configurations (short-term token renewal via plugins)."
tags:
  - "Enterprise"
  - "Authentication"
  - "Configuration"
  - "Plugin"
prerequisite:
  - "5.1 Configuration Deep Dive"
  - "5.11 Enterprise Features"
---

# Enterprise Authentication Integration

> 💡 **One-liner**: Connect your company's unified login token to OpenCode, so your team doesn't need to manually enter keys and can use internal models by default.

## 📝 Course Notes

Key takeaways from this lesson:

<img src="/images/5-advanced/enterprise-auth-notes.mini.jpeg"
     alt="5.11a Enterprise Authentication Integration Notes"
     data-zoom-src="/images/5-advanced/enterprise-auth-notes.jpeg" />

---

You can think of this lesson as one goal: **Make OpenCode "work out of the box" on your company's internal network**.

This lesson gives you 3 paths (from simplest to most flexible):

1) Environment Variables: You inject the Token yourselves, OpenCode just reads it

2) well-known: Execute `auth.command` once during login to save the token; subsequent startups only inject the saved token + fetch organization default configs (no auto-renewal)

3) Authentication Plugin: When you need OAuth/refresh/signing/modifying headers/params, implement via plugin

::: tip 💡 How to Read This Lesson Quickly
- First, look at the "3 Integration Methods Comparison" diagram, pick the path that best fits your team
- Then jump directly to the corresponding steps: Method A (Environment Variables) / Method B (well-known) / Method C (Plugin Authentication)
:::

## What You'll Be Able to Do

- Connect your company's unified authentication Token to OpenCode (no manual key entry per person)
- Use `/.well-known/opencode` to distribute default configurations to your team (e.g., force internal AI gateway)
- Distinguish: when environment variables are enough, when to use well-known, and when you must write an authentication plugin

<img src="/images/5-advanced/11a-auth-3ways.mini.jpeg"
     alt="Three Integration Methods Comparison"
     data-zoom-src="/images/5-advanced/11a-auth-3ways.jpeg" />

---

## Your Current Challenge

- Your company has unified authentication (SSO/unified gateway), but OpenCode defaults to Provider Key configuration
- Having everyone copy-paste tokens: cumbersome, prone to expiration, and easy to leak
- You want: when team members run OpenCode, it automatically carries company credentials and only uses internal models by default

---

## When to Use This Approach

- You can get a Token with a single command (e.g., `corpctl token`, `sso login --print-token`)
- You have an internal domain that can serve `https://<host>/.well-known/opencode`
- You want to centrally manage "default model, default Provider, disable external Providers" configurations

---

## 🎒 Before You Start

- [ ] Read [5.1 Configuration Deep Dive](./01a-config-basics)
- [ ] Prepare an internal domain, e.g., `https://ai.company.internal`
- [ ] Prepare a command to get a Token (recommended non-interactive: outputs token directly to stdout, doesn't depend on stdin interaction)

::: info ℹ️ What Does "Token" Mean Here?
OpenCode's Provider typically needs a string: API Key, Bearer Token, or a temporary credential from a gateway.

The goal of this lesson is: automatically put this string into an environment variable so OpenCode's Provider can read it.
:::

---

## Core Concept

OpenCode has an entry point well-suited for enterprise intranets: `opencode auth login <url>`.

- It requests `<url>/.well-known/opencode`, reads `auth.command` and `auth.env`, then executes `auth.command` locally to get and save the Token (source: `packages/opencode/src/cli/cmd/auth.ts`).
- When OpenCode starts and loads config, if it finds a saved `type: "wellknown"` credential, it sets `process.env[auth.env]=token` at runtime, and merges the `config` from `<url>/.well-known/opencode` as "organization default configuration" (source: `packages/opencode/src/config/config.ts`).

The 3 most common enterprise integration methods (from least to most code changes):

1. Environment Variables: You inject Token into environment variables yourselves, OpenCode just reads it
2. well-known: OpenCode handles "get Token + inject env + distribute default config"
3. Authentication Plugin: When you need OAuth/refresh/signing/modify request headers, use a plugin to implement login flow and request rewriting

::: info 🤔 What is well-known?
`/.well-known/` is a convention for a "fixed directory", commonly used for **service discovery**: clients just access a fixed path to get machine-readable configuration.

OpenCode defines an endpoint for enterprise scenarios: `/.well-known/opencode`.

It returns a JSON, typically containing two parts:

- `auth`: Tells OpenCode what command to use to get the Token (`auth.command`), and which environment variable to inject the Token into (`auth.env`)
- `config`: Organization default configuration (merged into OpenCode's configuration system)

Note: OpenCode directly runs `auth.command` (source: `packages/opencode/src/cli/cmd/auth.ts`). It also fetches and merges `config` on startup (source: `packages/opencode/src/config/config.ts`).

If `config` contains `plugin`, OpenCode may automatically install the plugin package and `import()` it (source: `packages/opencode/src/plugin/index.ts`).

Simply put: treat `/.well-known/opencode` as "the configuration entry point distributed by the organization to development machines", and only deploy it on controllable, trusted internal domain names.
:::

::: details 📦 well-known Distributes "Default Values", Not "Enforced Policies"
OpenCode's configuration merge order (low → high) is:

1) Remote `/.well-known/opencode` (organization defaults)

2) Global config (`~/.config/opencode/{config.json,opencode.json,opencode.jsonc}`)

3) Custom config path (`OPENCODE_CONFIG`)

4) Project config (`opencode.json{,c}`)

5) `.opencode/` directory config (including `.opencode/opencode.json{,c}` and `.opencode/plugin/`, etc.)

5.1) You can also use `OPENCODE_CONFIG_DIR` to specify an additional config directory (it will be loaded as part of directory sources, source: `packages/opencode/src/config/config.ts`)

6) Inline config (`OPENCODE_CONFIG_CONTENT`)

(Enterprise Edition) managed config directory overrides all above sources (source comment: `packages/opencode/src/config/config.ts`).

So `wellknown.config` is better suited for "team default out-of-box experience".

But there's an exception: array fields like `plugin`/`instructions` are "merged and deduplicated" during merge, not simply overwritten (source: merge logic in `packages/opencode/src/config/config.ts`: uses `Set` to deduplicate by complete string value).

Among these, `plugin` does another "deduplicate by plugin name" pass, and higher priority sources override same-name plugins from lower priority sources (source: `deduplicatePlugins()` in `packages/opencode/src/config/config.ts`).

If you want to force everyone to only use the internal gateway, you typically need Enterprise Edition centralized management, or coordinate with IT/mirroring/permission policies to restrict local override entry points.
:::

---

## Follow Along

### Step 1: Choose Your Integration Method

**Why**  
Choosing the right method avoids wasted effort later.

| Your Situation | Choose |
|---|---|
| Already have a fixed Key (or can easily inject Token in K8s/CI) | Environment Variables |
| Can output Token with a command, and want to distribute default configs uniformly | well-known |
| Must use OAuth/device code/auto-refresh/signing/modify headers/params | Authentication Plugin |

### Step 2 (Method A): Environment Variables Only (Simplest)

**Why**  
If you can already put Token into environment variables (local / K8s / CI), OpenCode doesn't need any additional authentication mechanism.

1) Configure an internal provider in `opencode.json`, and specify which environment variable to read the key from:

```jsonc
// opencode.json
{
  "$schema": "https://opencode.ai/config.json",
  "provider": {
    "corp-gateway": {
      "name": "Company AI Gateway",
      "env": ["COMPANY_AI_TOKEN"],
      "api": "https://ai-gateway.company.internal/v1",
      "npm": "@ai-sdk/openai-compatible",
      "models": {
        "qwen2.5-72b": {
          "name": "Qwen 2.5 72B",
          "tool_call": true,
          "reasoning": true,
          "temperature": true,
          "limit": { "context": 128000, "output": 8192 }
        }
      }
    }
  },
  "model": "corp-gateway/qwen2.5-72b"
}
```

2) Inject environment variable before running and verify:

::: code-group
```bash [macOS/Linux]
export COMPANY_AI_TOKEN="<your-token>"
opencode run -m corp-gateway/qwen2.5-72b "ping"
```

```powershell [Windows PowerShell]
$env:COMPANY_AI_TOKEN = "<your-token>"
opencode run -m corp-gateway/qwen2.5-72b "ping"
```
:::

**You should see**: `opencode run` returns model output.

::: tip 💡 Great for K8s/CI
Just make `COMPANY_AI_TOKEN` a K8s Secret or CI Secret injection, no need for everyone to log in locally.
:::

### Step 3 (Method B): Use well-known for "Unified Login + Organization Config Distribution"

**Why**  
well-known centralizes "get Token + default config" into one organization entry point: `https://<host>/.well-known/opencode`.

::: warning ⚠️ Token Renewal Boundary
well-known's `auth.command` only runs once when you execute `opencode auth login <url>`, and saves the token locally.

On subsequent OpenCode startups, it only injects this "saved token", no auto-refresh/renewal.

If your tokens are very short-lived (e.g., 1 hour expiration), Method C is more suitable: use a plugin to implement refresh/signing flow.
:::

<img src="/images/5-advanced/11a-auth-wellknown-flow.mini.jpeg"
     alt="well-known Workflow"
     data-zoom-src="/images/5-advanced/11a-auth-wellknown-flow.jpeg" />

#### 3.1 Prepare `/.well-known/opencode` Response

**Why**  
`opencode auth login <url>` behavior is entirely driven by this JSON: it tells OpenCode what command to use to get the Token, which environment variable to put it in, and what organization default configs to distribute.

Here's a minimal working example (you need to return this at `https://ai.company.internal/.well-known/opencode`):

```jsonc
{
  "auth": {
    "command": ["corpctl", "ai", "token", "--format=plain"],
    "env": "COMPANY_AI_TOKEN"
  },
  "config": {
    "$schema": "https://opencode.ai/config.json",

    // Optional: Force disable external Providers (example)
    "disabled_providers": ["openai", "anthropic", "openrouter"],

    // Configure company internal AI Gateway (OpenAI Compatible)
    "provider": {
      "corp-gateway": {
        "name": "Company AI Gateway",
        "env": ["COMPANY_AI_TOKEN"],
        "api": "https://ai-gateway.company.internal/v1",
        "npm": "@ai-sdk/openai-compatible",
        "models": {
          "qwen2.5-72b": {
            "name": "Qwen 2.5 72B",
            "tool_call": true,
            "reasoning": true,
            "temperature": true,
            "limit": { "context": 128000, "output": 8192 }
          }
        }
      }
    },

    // Make team use internal model by default
    "model": "corp-gateway/qwen2.5-72b"
  }
}
```

**You should see**: Browser accessing `https://ai.company.internal/.well-known/opencode` returns the JSON above.

::: warning ⚠️ Key Points
- `auth.command` must be runnable on development machines/containers; its stdout will be treated as the Token.
- `auth.env` is the environment variable name. When OpenCode starts, it sets `process.env[auth.env]=token` in the current process (not equivalent to writing to your system's global environment variables).
:::

#### 3.2 Use `opencode auth login` to Save Credentials Locally

**Why**  
This step saves a `type: "wellknown"` credential to the local `auth.json`. After this, every OpenCode startup will automatically inject the environment variable and fetch remote `config`.

```bash
opencode auth login https://ai.company.internal
```

**You should see**: Terminal output similar to:

- `Running \`corpctl ai token --format=plain\``
- `Logged into https://ai.company.internal`

#### 3.3 Confirm Credentials Exist

**Why**  
You need to confirm OpenCode actually saved the well-known credential to avoid "why isn't the config working" later.

```bash
opencode auth list
```

**You should see**: The list contains an entry like `https://ai.company.internal wellknown` (provider name may display as URL directly).

#### 3.4 Verify Organization Default Config Works (Run `run` Once)

**Why**  
The fastest verification: run `opencode run` once and see if it can complete tasks using your internal model.

```bash
opencode run -m corp-gateway/qwen2.5-72b "Explain the key points of this text in 3 sentences: ..."
```

**You should see**: Normal model output returned; if failed, usually shows authentication/model not found/network error.

### Step 4 (Method C): Write a Plugin for Unified Authentication (Most Flexible)

**Why**  
When you're not just "running a command to output Token", but need OAuth, auto-refresh, request signing, dynamic header/param modification, plugins are the most reliable solution.

#### 4.1 Write an Authentication Plugin Skeleton

Place the file at `.opencode/plugin/corp-auth.ts`:

```ts
import type { Plugin } from "@opencode-ai/plugin"

const plugin: Plugin = async () => {
  return {
    auth: {
      // Must match your configured provider id
      provider: "corp-gateway",
      methods: [
        {
          type: "api",
          label: "Login with Company SSO",
          async authorize() {
            // Replace with your token retrieval logic: CLI/HTTP/local cache, etc.
            const token = "<replace-me>"
            return { type: "success", key: token }
          },
        },
      ],
      async loader(getAuth) {
        const auth = await getAuth()
        if (!auth || auth.type !== "api") return {}
        return {
          apiKey: auth.key,
          // headers: { "X-Tenant": "..." },
        }
      },
    },

    // To really modify headers/params/signing, these hooks are more direct
    // "chat.headers": async (_input, output) => { output.headers["X-Sign"] = "..." },
    // "chat.params": async (_input, output) => { output.options["seed"] = 1 },
  }
}

export default plugin
```

#### 4.2 Let OpenCode Load Your Plugin

**Recommended**: After placing the plugin file in `.opencode/plugin/` directory, OpenCode will automatically scan and load it (no need to write `opencode.json`).

::: details 📦 I Really Want to Put It in opencode.json
You can write a relative path, and OpenCode will resolve it to an importable `file://...` URL when loading config:

```jsonc
// opencode.json
{
  "plugin": ["./.opencode/plugin/corp-auth.ts"]
}
```
:::

#### 4.3 Use `opencode auth login` for Plugin Login

```bash
opencode auth login
```

**You should see**:

- Providers in the selector come from models.dev list; your custom provider (e.g., `corp-gateway`) usually won't appear here
- So the common approach is: select `Other` first, then enter provider id: `corp-gateway`, then proceed to the login flow defined in your plugin `methods`

---

## Checklist ✅

- [ ] Method A: After injecting environment variable, `opencode run -m corp-gateway/qwen2.5-72b ...` works
- [ ] Method B: `https://<host>/.well-known/opencode` returns JSON, and `opencode auth login <url>` succeeds
- [ ] Method C: After enabling plugin, `opencode auth login` can go through plugin login and save credentials
- [ ] Team default model points to internal Provider (`model: "corp-gateway/..."`)

---

## Common Pitfalls

| Symptom | Cause | Solution |
|---|---|---|
| After login, `echo $COMPANY_AI_TOKEN` shows no value in another terminal | well-known's token is written to `process.env` of the current process when OpenCode starts, not to your `.zshrc/.bashrc` | Doesn't affect OpenCode model calls; verify with `opencode run -m corp-gateway/...`; if you really need to see it in shell, `export COMPANY_AI_TOKEN=...` yourself |
| `opencode auth login` directly returns 404/2000+ | `/.well-known/opencode` unreachable | First verify URL is accessible via browser/curl |
| Shows `Failed` / No `Logged into ...` | `auth.command` exit code is not 0 | Ensure command runs on current machine, and stdout outputs Token |
| OpenCode exits with error on startup | Remote well-known fetch failure throws error, interrupts config loading | First ensure `<url>/.well-known/opencode` is reachable; for debugging, use `opencode auth logout` to remove this URL credential before starting |
| `opencode auth login` can't find your provider | Your provider is not in models.dev list | Select `Other`, manually enter provider id (e.g., `corp-gateway`) |
| Login succeeds but config doesn't take effect | Only Token saved, no `config` returned | Add `config` field to well-known JSON |
| Can login in container but not locally (or vice versa) | Command/certificate chain differences | Ensure both container and local machine have company root certificates installed, and `auth.command` works on both |
| Internal gateway returns 401 | Token not read by provider or expired | Check `auth.env` name matches; retest with Step 4 `opencode run -m ...`; if needed, re-run `opencode auth login <url>` |
| Plugin placed in `.opencode/plugin/` but doesn't work | Dependency preparation incomplete: OpenCode calls `installDependencies(dir)` on scanned directories. Only writes if directory lacks `package.json`/`.gitignore`; attempts `bun add @opencode-ai/plugin@<version> --exact` and `bun install` (both `bun` command failures are swallowed; file writes have no catch). Only waits for install when `<dir>/node_modules` doesn't exist; if exists, install triggers in background without waiting | Ensure npm/internal mirror accessible; manually run `bun install` in the directory if needed, or pre-bake dependencies into image/cache (source: `installDependencies()` in `packages/opencode/src/config/config.ts`) |
| Worried well-known is insecure | Remote JSON can distribute `auth.command` (runs locally), and `config` (fetched and merged on startup; `plugin` may trigger plugin installation and execution) | Treat `/.well-known/opencode` as "organization config distribution entry point": only deploy on trusted internal domains; restrict access; audit returned content; avoid distributing `plugin` in remote config unless necessary |

---

## Lesson Summary

You learned:

1. Environment Variables: Simplest, great for K8s/CI
2. well-known: Best for team rollout, unified login and default config distribution
3. Authentication Plugin: Most flexible, for OAuth/refresh/signing/modifying headers/params

---

## Next Lesson Preview

> The next lesson will make authentication and gateway capabilities more flexible: after learning the plugin system, you can write truly "enterprise-grade" custom login flows and request rewrites.
>
> Next: **[5.12a Plugin Basics](./12a-plugins-basics)**.

---

## Appendix: Source Code Reference

<details>
<summary><strong>Click to expand source code locations</strong></summary>

> Last updated: 2026-02-05

| Feature | File Path | Lines |
|---|---|---|
| `opencode auth login <url>`: fetch `/.well-known/opencode` and execute `auth.command`, save `type: wellknown` credential | [`src/cli/cmd/auth.ts`](https://github.com/anomalyco/opencode/blob/dev/packages/opencode/src/cli/cmd/auth.ts#L231-L252) | 231-252 |
| Load well-known on startup: write token to `auth.env` environment variable, merge remote `config` | [`src/config/config.ts`](https://github.com/anomalyco/opencode/blob/dev/packages/opencode/src/config/config.ts#L62-L91) | 62-91 |
| Auth info storage structure (oauth/api/wellknown) and `auth.json` write logic | [`src/auth/index.ts`](https://github.com/anomalyco/opencode/blob/dev/packages/opencode/src/auth/index.ts#L7-L69) | 7-69 |
| Plugin auth hook `auth` type definition (`methods`/`loader`) | [`packages/plugin/src/index.ts`](https://github.com/anomalyco/opencode/blob/dev/packages/plugin/src/index.ts#L37-L156) | 37-156 |
| OpenCode plugin loading mechanism (built-in plugins + plugin list from config) | [`src/plugin/index.ts`](https://github.com/anomalyco/opencode/blob/dev/packages/opencode/src/plugin/index.ts#L15-L90) | 15-90 |
| `opencode run` command parameters (`-m provider/model`) | [`src/cli/cmd/run.ts`](https://github.com/anomalyco/opencode/blob/dev/packages/opencode/src/cli/cmd/run.ts#L28-L94) | 28-94 |

**Key Types**:
- `Auth.WellKnown`: `{ type: "wellknown", key: string, token: string }`
- `AuthHook`: Plugin auth interface, supports `api` / `oauth` methods

</details>
