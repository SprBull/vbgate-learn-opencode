---
title: "Experimental Features Overview"
description: "Complete list of OpenCode experimental features, how to enable them, and use cases"
---

# Experimental Features Overview

> OpenCode's experimental features are under active development and may change at any time. This page summarizes all available experimental features and how to enable them.

---

## What are Experimental Features?

Experimental features are new capabilities that the OpenCode team is developing, allowing users to experience and provide feedback before official release.

**Characteristics**:
- Features may be incomplete
- APIs may change at any time
- Some features require additional dependencies

**Enabling Principles**:
- Enable only what you need, not everything
- Disable if you encounter issues
- Follow the changelog to stay updated

---

## Quick Enable

### Option 1: Enable All at Once

```bash
# macOS / Linux: Add to ~/.zshrc or ~/.bashrc
export OPENCODE_EXPERIMENTAL=true

# Then reload
source ~/.zshrc
```

### Option 2: Enable Individual Features

```bash
# Enable only the features you need
export OPENCODE_EXPERIMENTAL_LSP_TOOL=true
export OPENCODE_EXPERIMENTAL_PLAN_MODE=true
```

---

## Experimental Features List

### 🌐 Web Search

| Variable | Description | Related Tutorial |
|----------|-------------|------------------|
| `OPENCODE_ENABLE_EXA` | Enable websearch tool, allowing AI to search the internet | [5.23 Web Search & Fetch](/en/5-advanced/23-web-search) |

**How to Enable**:
```bash
export OPENCODE_ENABLE_EXA=true
```

**Use Cases**:
- Look up the latest technical documentation and API usage
- Search for solutions to error messages
- Learn about the latest version features of libraries

::: tip Zen Users
If you use OpenCode Zen hosted models, websearch is automatically enabled with no configuration needed.
:::

---

### 🔧 LSP Enhancements

| Variable | Description | Related Tutorial |
|----------|-------------|------------------|
| `OPENCODE_EXPERIMENTAL_LSP_TOOL` | Enable LSP tools (go to definition, find references, etc.) | [5.19 LSP Code Intelligence](/en/5-advanced/19-lsp) |
| `OPENCODE_EXPERIMENTAL_LSP_TY` | Enable experimental ty Python server (replaces pyright) | [5.19 LSP Code Intelligence](/en/5-advanced/19-lsp) |

**How to Enable**:
```bash
export OPENCODE_EXPERIMENTAL_LSP_TOOL=true
export OPENCODE_EXPERIMENTAL_LSP_TY=true
```

**Use Cases**:
- Allow AI to perform LSP operations like "go to definition" and "find all references"
- Use a faster type checker for Python projects

---

### 📋 Workflow Enhancements

| Variable | Description | Related Tutorial |
|----------|-------------|------------------|
| `OPENCODE_EXPERIMENTAL_PLAN_MODE` | Enable plan mode (separate plan/build) | [3.1 Plan & Build](/en/3-workflow/01-plan-build) |

**How to Enable**:
```bash
export OPENCODE_EXPERIMENTAL_PLAN_MODE=true
```

**Use Cases**:
- Large refactoring tasks: Let AI research and generate a plan first, then execute after review
- Uncertain about best approach: Plan multiple options first, then choose before starting
- Need manual review: Plan files can be saved, shared, and iterated

**New Tools**:
- `plan_enter`: Switch to plan mode
- `plan_exit`: Plan complete, ask whether to switch to build mode

---

### 🎨 UI & Interaction

| Variable | Description |
|----------|-------------|
| `OPENCODE_EXPERIMENTAL_ICON_DISCOVERY` | Auto-discover project icons (displayed in UI) |
| `OPENCODE_EXPERIMENTAL_MARKDOWN` | Enable experimental Markdown rendering component |
| `OPENCODE_EXPERIMENTAL_DISABLE_COPY_ON_SELECT` | Disable auto-copy when selecting text in TUI |

**How to Enable**:
```bash
export OPENCODE_EXPERIMENTAL_ICON_DISCOVERY=true
export OPENCODE_EXPERIMENTAL_MARKDOWN=true
```

---

### ⚡ Performance & Formatting

| Variable | Description | Related Tutorial |
|----------|-------------|------------------|
| `OPENCODE_EXPERIMENTAL_OXFMT` | Enable oxfmt formatter (written in Rust, high performance) | [5.18 Code Formatters](/en/5-advanced/18-formatters) |
| `OPENCODE_EXPERIMENTAL_FILEWATCHER` | Enable file watcher for entire directories |
| `OPENCODE_EXPERIMENTAL_DISABLE_FILEWATCHER` | Disable file watcher |

**How to Enable**:
```bash
export OPENCODE_EXPERIMENTAL_OXFMT=true
```

**Prerequisites for oxfmt**:
- Project has `oxfmt` dependency in `package.json`
- Experimental flag is enabled

---

### ⏱️ Timeouts & Limits

| Variable | Type | Description |
|----------|------|-------------|
| `OPENCODE_EXPERIMENTAL_BASH_DEFAULT_TIMEOUT_MS` | number | Default timeout for Bash commands (milliseconds) |
| `OPENCODE_EXPERIMENTAL_OUTPUT_TOKEN_MAX` | number | Maximum output tokens for LLM responses |

**Example**:
```bash
# Set bash timeout to 2 minutes
export OPENCODE_EXPERIMENTAL_BASH_DEFAULT_TIMEOUT_MS=120000

# Limit LLM output to max 8192 tokens
export OPENCODE_EXPERIMENTAL_OUTPUT_TOKEN_MAX=8192
```

---

## experimental Configuration in opencode.json

Besides environment variables, `opencode.json` also has an `experimental` field for configuring another category of experimental features:

```json
{
  "experimental": {
    "batch_tool": true,           // Enable batch operation tools
    "openTelemetry": true,        // Enable OpenTelemetry tracing
    "disable_paste_summary": true, // Disable auto-summary for pasted text
    "continue_loop_on_deny": true, // Continue thinking when tool is denied
    "primary_tools": ["tool1"],   // Tools restricted to Primary Agent
    "mcp_timeout": 30000          // MCP request timeout (milliseconds)
  }
}
```

| Field | Description |
|-------|-------------|
| `batch_tool` | Enable batch tools for executing multiple operations at once |
| `openTelemetry` | Enable OpenTelemetry for performance monitoring and tracing |
| `disable_paste_summary` | Don't auto-generate summaries when pasting large text |
| `continue_loop_on_deny` | When user denies a tool call, Agent continues thinking instead of stopping |
| `primary_tools` | Specify a list of tools restricted to Primary Agent |
| `mcp_timeout` | Global timeout for MCP requests (milliseconds) |

---

## Complete Configuration Example

Here's a "full-featured" experimental configuration example. Copy what you need:

```bash
# ═══════════════════════════════════════════════════════════════
# OpenCode Experimental Features Configuration
# Add to ~/.zshrc or ~/.bashrc, then source it
# ═══════════════════════════════════════════════════════════════

# Enable all experimental features at once (the individual switches below are automatically included)
# export OPENCODE_EXPERIMENTAL=true

# ───────────────────────────────────────────────────────────────
# Web Search (requires Exa API, or use Zen hosted models for auto-enable)
# ───────────────────────────────────────────────────────────────
export OPENCODE_ENABLE_EXA=true           # Enable websearch tool

# ───────────────────────────────────────────────────────────────
# LSP (Language Server Protocol) Enhancements
# ───────────────────────────────────────────────────────────────
export OPENCODE_EXPERIMENTAL_LSP_TOOL=true  # Enable LSP tools
export OPENCODE_EXPERIMENTAL_LSP_TY=true    # Enable experimental ty Python server

# ───────────────────────────────────────────────────────────────
# UI & Interaction
# ───────────────────────────────────────────────────────────────
export OPENCODE_EXPERIMENTAL_MARKDOWN=true         # Experimental Markdown rendering
export OPENCODE_EXPERIMENTAL_ICON_DISCOVERY=true   # Auto-discover project icons

# ───────────────────────────────────────────────────────────────
# Workflow Enhancements
# ───────────────────────────────────────────────────────────────
export OPENCODE_EXPERIMENTAL_PLAN_MODE=true  # Enable plan mode

# ───────────────────────────────────────────────────────────────
# Performance & Formatting
# ───────────────────────────────────────────────────────────────
export OPENCODE_EXPERIMENTAL_OXFMT=true      # Enable oxfmt formatter

# ───────────────────────────────────────────────────────────────
# Timeouts & Limits (optional)
# ───────────────────────────────────────────────────────────────
# export OPENCODE_EXPERIMENTAL_BASH_DEFAULT_TIMEOUT_MS=120000
# export OPENCODE_EXPERIMENTAL_OUTPUT_TOKEN_MAX=8192
```

---

## FAQ

### No effect after enabling?

1. **Confirm configuration has been reloaded**:
   ```bash
   source ~/.zshrc  # or source ~/.bashrc
   ```

2. **Confirm OpenCode has been restarted**: Environment variables are read at process startup

3. **Confirm variable is set**:
   ```bash
   env | grep OPENCODE
   ```

### Feature is unstable?

Experimental features may have issues:
- Check the [Changelog](/en/changelog/) for latest changes
- Disable the problematic feature if issues occur
- Report issues on [GitHub Issues](https://github.com/anomalyco/opencode/issues)

### How to disable a feature?

Simply remove or comment out the corresponding environment variable:
```bash
# export OPENCODE_EXPERIMENTAL_PLAN_MODE=true  # Commented out = disabled
```

---

## Related Resources

- [CLI Environment Variables Reference](/en/appendix/cli) - Complete list of all environment variables
- [Configuration Options Reference](/en/appendix/config-ref) - opencode.json configuration details
- [Changelog](/en/changelog/) - Learn about feature changes
