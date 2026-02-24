---
title: "5.1a Configuration Basics"
subtitle: "opencode.json Core Configuration"
course: "OpenCode Practical Course"
stage: "Stage 5"
lesson: "5.1a"
duration: "15 minutes"
level: "Advanced"
description: "Learn opencode.json core configuration to control OpenCode's basic behavior and customize your development environment."
tags:
  - "Configuration"
  - "JSON"
  - "Basics"
prerequisite:
  - "2.1 Interface and Basic Operations"
---

# 5.1a Configuration Basics

> Control OpenCode's core behavior through the opencode.json configuration file.

## 📝 Course Notes

Key takeaways from this lesson:

<img src="/images/5-advanced/config-basics-notes.mini.jpeg" alt="Configuration Basics Notes" data-zoom-src="/images/5-advanced/config-basics-notes.jpeg" />

---

## What You'll Learn

- Understand configuration file locations and priority
- Master model and Provider configuration
- Use variable substitution for dynamic configuration
- Configure username and auto-update

---

## Your Current Challenge

- Have to manually set things up every time, don't know how to save configuration
- Don't want to write API Keys in plain text in configuration
- Don't know how to configure multiple Providers

---

## When to Use This

- When you need to: Personalize OpenCode's behavior
- And don't want to: Reset everything each time you start

---

## Configuration File Locations

OpenCode loads configuration in the following order, from lowest to highest priority (later ones override earlier ones):

| Priority | Location | Description |
|-------|-----|------|
| 1 (lowest) | Remote `.well-known/opencode` | Remote organization default config (obtained via Auth mechanism) |
| 2 | `~/.config/opencode/opencode.json` | Global user configuration |
| 3 | `OPENCODE_CONFIG` environment variable | Custom config file path |
| 4 | `./opencode.json` | Project root directory configuration |
| 5 | `./.opencode/opencode.json` | Project .opencode directory configuration |
| 6 | `OPENCODE_CONFIG_CONTENT` environment variable | Inline config content (JSON string) |
| 7 (highest) | Managed config directory | Enterprise deployment, admin-controlled |

> Configuration files are **merged**, not replaced. Later configurations override conflicting keys from earlier ones, but non-conflicting settings are preserved.

::: details Managed Config Directory (Enterprise Deployment)
In enterprise environments, administrators can place configuration in system-level directories with the highest priority, overriding all user and project configurations:

| Platform | Path |
|------|------|
| macOS | `/Library/Application Support/opencode` |
| Windows | `%ProgramData%\opencode` |
| Linux | `/etc/opencode` |

Regular users generally don't need this, just be aware it exists.
:::

### Configuration Directory Structure

```
~/.config/opencode/
├── opencode.json       # Global configuration
├── AGENTS.md           # Global rules
├── agent/              # Global Agents
├── command/            # Global commands
└── plugin/             # Global plugins

Project directory/
├── opencode.json       # Project configuration (priority 4)
├── AGENTS.md           # Project rules
└── .opencode/
    ├── opencode.json   # Project configuration (priority 5, recommended)
    ├── agent/          # Project Agents
    ├── command/        # Project commands
    └── plugin/         # Project plugins
```

---

## Configuration Format

Supports JSON and JSONC (JSON with comments):

```jsonc
{
  "$schema": "https://opencode.ai/config.json",
  // This is a comment, JSONC format supports it
  "model": "anthropic/claude-opus-4-5-thinking"
}
```

> Configuration filename can be `opencode.json` or `opencode.jsonc`.

---

## Model Configuration
<AdInArticle />

### Main Model and Small Model

```json
{
  "$schema": "https://opencode.ai/config.json",
  "model": "anthropic/claude-opus-4-5-thinking",
  "small_model": "anthropic/claude-haiku-4-5"
}
```

| Field | Description |
|-----|------|
| `model` | Main model (format: provider/model) |
| `small_model` | Small model for simple tasks (like generating titles) |

> `small_model` configures a cheaper model for lightweight tasks. If not set, OpenCode will try to use a cheaper model provided by the Provider, otherwise falls back to the main model.

### Default Agent

```json
{
  "default_agent": "build"
}
```

Sets the default primary agent to use (must be primary mode). Options:
- `"build"` - Default, all tools available
- `"plan"` - Read-only mode, editing requires confirmation
- Or a custom primary agent name you've defined

---

## Provider Configuration

### Basic Configuration

```json
{
  "$schema": "https://opencode.ai/config.json",
  "provider": {
    "anthropic": {
      "options": {
        "apiKey": "{env:ANTHROPIC_API_KEY}",
        "baseURL": "https://api.anthropic.com",
        "timeout": 600000,
        "setCacheKey": true
      }
    }
  }
}
```

> Note: Configuration key is `provider` (singular), not `providers`.

### Options Field Reference

| Field | Type | Description |
|-----|------|------|
| `apiKey` | string | API key |
| `baseURL` | string | Custom API endpoint (commonly used for proxies) |
| `timeout` | number \| false | Request timeout (milliseconds), default 300000, set to false to disable |
| `setCacheKey` | boolean | Enable prompt cache key (default false) |

### Amazon Bedrock Special Configuration

Amazon Bedrock supports AWS-specific configuration:

```json
{
  "provider": {
    "amazon-bedrock": {
      "options": {
        "region": "us-east-1",
        "profile": "my-aws-profile",
        "endpoint": "https://bedrock-runtime.us-east-1.vpce-xxxxx.amazonaws.com"
      }
    }
  }
}
```

| Field | Description |
|-----|------|
| `region` | AWS region (default from `AWS_REGION` env var or `us-east-1`) |
| `profile` | AWS profile name (from `~/.aws/credentials`) |
| `endpoint` | Custom endpoint URL (for VPC endpoints) |

### Provider Allowlist/Blocklist

Control which Providers to load:

```json
{
  "disabled_providers": ["openai", "gemini"],
  "enabled_providers": ["anthropic"]
}
```

| Field | Description |
|-----|------|
| `disabled_providers` | List of disabled Providers, won't load even with API Key |
| `enabled_providers` | Only enable these Providers, ignore all others |

> `disabled_providers` has higher priority than `enabled_providers`. If a Provider appears in both lists, it will be disabled.

---

## User Configuration

### Custom Username

```json
{
  "username": "Developer"
}
```

Displays a custom username in conversations instead of the system username.

---

## Theme Configuration

```json
{
  "theme": "tokyonight"
}
```

> Note: Configuration key is `theme`, not `tui.theme`.

---

## Auto-Update

```json
{
  "autoupdate": true
}
```

| Value | Description |
|-----|------|
| `true` | Automatically download updates on startup (default) |
| `false` | Disable auto-update |
| `"notify"` | Only notify of new versions, don't auto-update |

---

## Variable Substitution

Variables can be used in configuration to dynamically obtain values:

### Environment Variables

Use `{env:VARIABLE_NAME}` to reference environment variables:

```json
{
  "model": "{env:OPENCODE_MODEL}",
  "provider": {
    "anthropic": {
      "options": {
        "apiKey": "{env:ANTHROPIC_API_KEY}"
      }
    }
  }
}
```

> If the environment variable doesn't exist, it will be replaced with an empty string.

### File Contents

Use `{file:path}` to reference file contents:

```json
{
  "provider": {
    "openai": {
      "options": {
        "apiKey": "{file:~/.secrets/openai-key}"
      }
    }
  }
}
```

File paths support:
- Relative paths from the configuration file
- Absolute paths starting with `/`
- Home directory paths starting with `~`

Variable substitution is useful for:
- Protecting sensitive data (API Keys in separate files)
- Cross-environment configuration (different variables for dev/production)
- Sharing configuration snippets

---

## Complete Basic Configuration Example

```jsonc
{
  "$schema": "https://opencode.ai/config.json",
  
  // Models
  "model": "anthropic/claude-opus-4-5-thinking",
  "small_model": "anthropic/claude-haiku-4-5",
  "default_agent": "build",
  
  // Provider
  "provider": {
    "anthropic": {
      "options": {
        "apiKey": "{env:ANTHROPIC_API_KEY}",
        "timeout": 600000
      }
    }
  },
  
  // Provider control
  "disabled_providers": ["gemini"],
  
  // User
  "username": "Developer",
  
  // Theme
  "theme": "catppuccin",
  
  // Auto-update
  "autoupdate": true
}
```

---

## Common Pitfalls

| Issue | Cause | Solution |
|-----|-----|-----|
| Configuration not taking effect | Priority issue | Project-level config takes precedence over global |
| Variable substitution fails | Environment variable doesn't exist | Confirm the env var is set |
| JSON parsing error | Format error | Use JSONC format or check syntax |
| Used `providers` | Wrong key name | Should be `provider` (singular) |
| Provider not loading | In disabled list | Check `disabled_providers` |

---

## Lesson Summary

You learned:

1. Configuration file locations and priority
2. Model configuration (model, small_model, default_agent)
3. Provider configuration (options, allowlist/blocklist)
4. Variable substitution (environment variables, file contents)
5. Username, theme, and auto-update configuration

---

## Next Lesson Preview

> Next lesson we'll learn advanced configuration, including interface configuration, behavior configuration, and detailed explanations of various feature configurations.
