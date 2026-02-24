---
title: "opencode.json Configuration Reference"
description: "Complete reference manual for opencode.json configuration file, covering all available fields"
---

# opencode.json Configuration Reference

> This document is the complete reference manual for the OpenCode configuration file, explaining every field available in `opencode.json`.

## 📝 Course Notes

Key takeaways from this lesson:

<img src="/images/appendix/config-ref-notes.mini.jpeg"
     alt="Configuration Options Reference Notes"
     data-zoom-src="/images/appendix/config-ref-notes.jpeg" />

---

## Configuration File Location and Priority

OpenCode loads configuration in the following order (priority from low to high, later overrides earlier):

| Priority | Location | Description |
|----------|----------|-------------|
| 1 (lowest) | Remote `.well-known/opencode` | Remote organization default config (obtained via Auth mechanism) |
| 2 | `~/.config/opencode/opencode.json` | Global user configuration |
| 3 | `OPENCODE_CONFIG` environment variable | Custom configuration file path |
| 4 | `./opencode.json` | Project root directory configuration |
| 5 | `./.opencode/opencode.json` | Project .opencode directory configuration |
| 6 | `OPENCODE_CONFIG_CONTENT` environment variable | Inline configuration content (JSON string) |
| 7 (highest) | Managed configuration directory | Enterprise deployment, administrator controlled |

**Managed Configuration Directory** (enterprise deployment, highest priority):

| Platform | Path |
|----------|------|
| macOS | `/Library/Application Support/opencode` |
| Windows | `%ProgramData%\opencode` |
| Linux | `/etc/opencode` |

---

## Top Level Configuration

Fields contained in the root object of the configuration file.

### Basic Settings

| Field | Type | Description | Default |
|-------|------|-------------|---------|
| `username` | string | Username displayed in conversations. If not set, uses system username. | System user |
| `theme` | string | Interface theme name. See [Theme List](../5-advanced/06a-themes). | - |
| `autoupdate` | boolean \| "notify" | Auto-update behavior. `true`=auto update, `false`=disabled, `"notify"`=notify only. | - |
| `logLevel` | enum | Log level. Options: `"DEBUG"`, `"INFO"`, `"WARN"`, `"ERROR"`. | - |
| `snapshot` | boolean | Whether to enable Git snapshot backup mechanism. Set to `false` to disable. | Enabled when not set |

### Model and Agent

| Field | Type | Description |
|-------|------|-------------|
| `model` | string | Primary model ID (format: `provider/model`), used for complex tasks. |
| `small_model` | string | Small model ID, used for simple tasks like title generation, summaries, etc. |
| `default_agent` | string | Default Primary Agent name to start. Defaults to `build`. |

### Behavior Control

| Field | Type | Description | Default |
|-------|------|-------------|---------|
| `share` | enum | Session sharing behavior. `"manual"`, `"auto"`, `"disabled"`. | `"manual"` |
| `disabled_providers` | string[] | List of disabled providers. Won't load even with API key. | `[]` |
| `enabled_providers` | string[] | List of only enabled providers. When set, providers not in list are ignored. | - |

---

## Interface Configuration (tui)

Controls Terminal User Interface (TUI) display behavior.

```json
"tui": {
  "scroll_speed": 3,
  "diff_style": "auto"
}
```

| Field | Type | Description | Default |
|-------|------|-------------|---------|
| `scroll_speed` | number | Mouse wheel scroll speed multiplier (minimum 0.001). | 3 |
| `scroll_acceleration` | object | Scroll acceleration configuration. | - |
| `scroll_acceleration.enabled` | boolean | Whether to enable macOS-style inertial scrolling acceleration. | `false` |
| `diff_style` | enum | Diff display style. `"auto"`(adaptive), `"stacked"`(always single column). | `"auto"` |

---

## Provider Configuration (provider)

Configure model provider API keys, endpoints, and model parameters.

**Key name**: `provider` (singular)  
**Type**: `Record<string, ProviderConfig>`

```json
"provider": {
  "anthropic": {
    "options": {
      "apiKey": "sk-...",
      "timeout": 600000
    }
  }
}
```

### Common Options (options)

`options` fields supported by all providers:

| Field | Type | Description |
|-------|------|-------------|
| `apiKey` | string | API key. Recommend using `{env:VAR}` to reference environment variables. |
| `baseURL` | string | Custom API endpoint address (for proxies or compatible services). |
| `timeout` | number \| false | Request timeout (milliseconds). Default 300000 (5 minutes). `false` disables timeout. |
| `setCacheKey` | boolean | Whether to enable Prompt Cache key (for Anthropic/DeepSeek etc.). Default `false`. |
| `enterpriseUrl` | string | GitHub Enterprise URL (Copilot Provider only). |

### Provider-level Fields

The Provider object itself also supports the following fields:

| Field | Type | Description |
|-------|------|-------------|
| `name` | string | Provider display name. |
| `env` | string[] | Environment variable names list (for auto-detecting API key). |
| `whitelist` | string[] | List of only allowed models. |
| `blacklist` | string[] | List of prohibited models. |

### Model-specific Configuration (models)

Fine-tune specific models:

```json
"provider": {
  "anthropic": {
    "models": {
      "claude-3-7-sonnet": {
        "variants": {
          "thinking": { "disabled": true }
        }
      }
    }
  }
}
```

---

## Agent Configuration (agent)

Define or override Agent behavior.

**Key name**: `agent` (singular)  
**Type**: `Record<string, AgentConfig>`

```json
"agent": {
  "code-reviewer": {
    "mode": "subagent",
    "prompt": "You are a code reviewer...",
    "permission": { "edit": "deny" }
  }
}
```

| Field | Type | Description |
|-------|------|-------------|
| `description` | string | Brief description of the Agent, shown in `/agent` list. |
| `mode` | enum | Agent type. `"primary"`(standalone), `"subagent"`, `"all"`. |
| `model` | string | Model ID specific to this Agent. |
| `variant` | string | Default model variant (only effective when using the model configured for this Agent). |
| `prompt` | string | System Prompt (persona instructions). |
| `temperature` | number | Temperature coefficient (0.0 - 1.0). |
| `top_p` | number | Nucleus sampling parameter (0.0 - 1.0). |
| `steps` | number | Maximum automatic iteration steps. |
| `color` | string | Display color in interface (Hex format, e.g. `#FF0000`), or theme color name (e.g. `primary`). |
| `hidden` | boolean | Whether to hide this Agent in `@` autocomplete menu. |
| `permission` | object | Agent-specific permission configuration (overrides global permissions). |
| `disable` | boolean | Whether to disable this Agent. |

---

## Permission Configuration (permission)

Control OpenCode's access to system resources.

**Key name**: `permission` (singular)  
**Type**: `Record<string, Rule | Action>`

Value can be one of the following strings (Action):
- `"allow"`: Auto-allow
- `"ask"`: Ask each time
- `"deny"`: Deny

Can also be an object (Rule) for finer control.

```json
"permission": {
  "edit": "ask",
  "bash": {
    "*": "ask",
    "git *": "allow",
    "rm *": "deny"
  }
}
```

**Available Permissions**:
- `read`: Read files
- `edit`: Edit/write files
- `bash`: Execute commands
- `glob`: File search
- `grep`: Content search
- `list`: List directory
- `task`: Call sub-Agent
- `external_directory`: Access external directories
- `todowrite`: TODO write
- `todoread`: TODO read
- `question`: Question tool
- `webfetch`: Access web pages
- `websearch`: Search engine
- `codesearch`: Code search
- `lsp`: LSP operations
- `doom_loop`: Infinite loop detection
- `skill`: Skill invocation

---

## Command Configuration (command)

Define custom slash commands.

**Key name**: `command` (singular)  
**Type**: `Record<string, CommandConfig>`

```json
"command": {
  "commit": {
    "template": "Generate a commit message for these changes:\n$DIFF",
    "agent": "build"
  }
}
```

| Field | Type | Description |
|-------|------|-------------|
| `template` | string | Prompt template. Supports variables like `$ARGUMENTS`. |
| `description` | string | Command description. |
| `agent` | string | Agent to execute this command. |
| `model` | string | Model to execute this command. |
| `subtask` | boolean | Whether to run as a subtask. |

---

## Keybinds Configuration (keybinds)

Customize keyboard shortcuts.

**Key name**: `keybinds` (**plural**)

```json
"keybinds": {
  "leader": "ctrl+x",
  "session_new": "<leader>n"
}
```

Common options (see [Keybinds Reference](./keybinds.md) for complete list):

- `leader`: Prefix key (default `ctrl+x`)
- `app_exit`: Exit application
- `session_new`: New session
- `session_list`: Session list
- `model_list`: Switch model
- `agent_list`: Switch Agent
- `input_submit`: Send message
- `input_newline`: New line

---

## Server Configuration (server)

Configure `opencode serve` or `opencode web` behavior.

```json
"server": {
  "port": 4096,
  "hostname": "0.0.0.0",
  "mdns": true,
  "mdnsDomain": "opencode.local"
}
```

| Field | Type | Description | Default |
|-------|------|-------------|---------|
| `port` | number | Listen port. | 4096 |
| `hostname` | string | Listen address. Defaults to `0.0.0.0` when mdns is enabled. | 127.0.0.1 |
| `mdns` | boolean | Whether to enable mDNS local network discovery. | false |
| `mdnsDomain` | string | Custom domain for mDNS service. | `opencode.local` |
| `cors` | string[] | List of origins allowed for CORS requests. | - |

---

## Experimental Features (experimental)

Enable experimental features in development. **Note: These features are unstable and may change at any time**.

```json
"experimental": {
  "batch_tool": true,
  "openTelemetry": true
}
```

| Field | Type | Description |
|-------|------|-------------|
| `batch_tool` | boolean | Enable batch operation tools. |
| `openTelemetry` | boolean | Enable OpenTelemetry tracing. |
| `disable_paste_summary` | boolean | Disable auto-summary when pasting large text. |
| `continue_loop_on_deny` | boolean | Whether to let Agent continue thinking when tool call is denied (instead of interrupting). |
| `primary_tools` | string[] | Specify list of tools only available to Primary Agent. |
| `mcp_timeout` | number | Global timeout for MCP requests (milliseconds). |

> Hook functionality is implemented through the **plugin system**, not `experimental` configuration. See [Hooks Mechanism](../5-advanced/12c-hooks).

---

## Other Configuration

### compaction
Control context compression behavior.

```json
"compaction": {
  "auto": true,
  "prune": true,
  "reserved": 10000
}
```

| Field | Type | Description | Default |
|-------|------|-------------|---------|
| `auto` | boolean | Auto-trigger compression when context is full. | `true` |
| `prune` | boolean | Remove old tool outputs during compression. | `true` |
| `reserved` | number | Token buffer during compression, reserved window to avoid overflow. | - |

### watcher
Control file system watching.

```json
"watcher": {
  "ignore": ["node_modules/**", ".git/**"]
}
```
- `ignore`: List of file glob patterns to ignore watching.

### instructions
```json
"instructions": ["docs/rules.md", ".cursor/rules/*.md"]
```
List of additional global instruction files.

### plugin
```json
"plugin": ["opencode-helicone-session", "./my-plugin.js"]
```
List of plugins to load. Supports npm package names or local file paths.

### skills
```json
"skills": {
  "paths": ["./skills", "~/shared-skills"],
  "urls": ["https://example.com/.well-known/skills/"]
}
```

| Field | Type | Description |
|-------|------|-------------|
| `paths` | string[] | Additional Skill folder paths. |
| `urls` | string[] | Remote Skill fetch URLs. |

### mcp
Configure Model Context Protocol servers. See [MCP Documentation](../5-advanced/07a-mcp-basics).

### formatter
Configure code formatting tools. See [Formatter Documentation](../5-advanced/18-formatters).

### lsp
Configure LSP servers. See [LSP Documentation](../5-advanced/19-lsp).

### enterprise
```json
"enterprise": {
  "url": "https://github.example.com"
}
```
Configure GitHub Enterprise instance URL.

---

## Appendix: Source Code Reference

<details>
<summary><strong>Click to expand source code locations</strong></summary>

> Last updated: 2026-02-14

All configuration schemas are defined in `packages/opencode/src/config/config.ts`.

| Configuration | Schema | Line Range |
|---------------|--------|------------|
| Top Level Info | `Info` | L1004-L1197 |
| Provider | `Provider` | L951-L1001 |
| Agent | `Agent` | L672-L758 |
| Permission | `Permission` | L621-L652 |
| Keybinds | `Keybinds` | L761-L917 |
| TUI | `TUI` | L919-L931 |
| Server | `Server` | L933-L944 |
| Command | `Command` | L654-L661 |
| Skills | `Skills` | L663-L670 |
| MCP | `Mcp` | L523-L584 |
| Experimental | `experimental` | L1172-L1192 |

</details>
