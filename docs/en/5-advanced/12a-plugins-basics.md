---
title: "5.12a Plugin Basics"
subtitle: "Extending functionality through hooks"
course: "OpenCode Practical Course"
stage: "Stage 5"
lesson: "5.12a"
duration: "20 minutes"
practice: "25 minutes"
level: "Advanced"
description: "Learn OpenCode plugin basics, extend functionality through hooks mechanism, install and configure plugins."
tags:
  - "plugin"
  - "hook"
  - "extension"
prerequisite:
  - "5.1 Configuration Complete"
---

# Plugin Basics

> 💡 **One-line summary**: Plugins let you extend OpenCode's functionality through the hooks mechanism.

## 📝 Course Notes

Key knowledge points from this lesson:

<img src="/images/5-advanced/plugins-basics-notes.mini.jpeg"
     alt="5.12a Plugin Basics Notes"
     data-zoom-src="/images/5-advanced/plugins-basics-notes.jpeg" />

---

## What You'll Learn

- Install and configure plugins
- Create simple local plugins
- Understand the plugin loading mechanism

---

## What are Plugins

Plugins are JavaScript/TypeScript modules that extend OpenCode through the hooks mechanism. You can:

- Add new features (e.g., custom tools, notifications)
- Integrate external services (e.g., time tracking, monitoring)
- Modify default behaviors (e.g., intercept file reads, modify LLM parameters)

For community plugin examples, see [Ecosystem](../appendix/ecosystem#plugins).

---

## Using Plugins

There are two ways to load plugins:

### Loading from Local Files

Place JavaScript or TypeScript files in the plugin directories:

| Directory | Scope |
|-----------|-------|
| `.opencode/plugin/` | Project-level plugins |
| `~/.config/opencode/plugin/` | Global plugins |

`.js` and `.ts` files in these directories are automatically loaded at startup.

### Loading from npm

<AdInArticle />

Specify npm packages in your configuration file:

```jsonc
// opencode.json
{
  "$schema": "https://opencode.ai/config.json",
  "plugin": [
    "opencode-helicone-session",
    "opencode-wakatime",
    "@my-org/custom-plugin"
  ]
}
```

Both regular and scoped packages (`@scope/package`) are supported.

---

## Plugin Installation Mechanism

### npm Plugins

Automatically installed using Bun at startup. Packages and their dependencies are cached at:

```
~/.cache/opencode/node_modules/
```

### Local Plugins

Loaded directly from plugin directories. To use external npm packages, create a `package.json` in the config directory:

```jsonc
// .opencode/package.json
{
  "dependencies": {
    "shescape": "^2.1.0"
  }
}
```

OpenCode runs `bun install` at startup to install these dependencies.

### Built-in Plugins

OpenCode comes with two built-in plugins (can be disabled with `OPENCODE_DISABLE_DEFAULT_PLUGINS=1`):

| Plugin | Function |
|--------|----------|
| `opencode-copilot-auth` | GitHub Copilot authentication |
| `opencode-anthropic-auth` | Anthropic authentication |

---

## Loading Order

Plugins are loaded from all sources, and hooks are executed in this order:

1. Global config (`~/.config/opencode/opencode.json`)
2. Project config (`opencode.json`)
3. Global plugin directory (`~/.config/opencode/plugin/`)
4. Project plugin directory (`.opencode/plugin/`)

**Deduplication Rules**:
- Same npm package with same name and version is loaded only once
- Local plugins and npm plugins with the same name are loaded separately
- Identical functions exported from the same module are initialized only once (prevents duplication from `export default` and named exports)

---

## Creating Plugins

A plugin is a module that exports plugin functions. Each function receives a context object and returns a hooks object.

### Basic Structure

```js
// .opencode/plugin/example.js
export const MyPlugin = async ({ project, client, $, directory, worktree, serverUrl }) => {
  console.log("Plugin initialized!")

  return {
    // Hook implementations
  }
}
```

### Plugin Context Parameters

| Parameter | Type | Description |
|-----------|------|-------------|
| `project` | `Project` | Current project information |
| `directory` | `string` | Current working directory |
| `worktree` | `string` | Git worktree path |
| `client` | `OpencodeClient` | OpenCode SDK client for interacting with AI |
| `$` | `BunShell` | Bun's [shell API](https://bun.sh/docs/runtime/shell) for executing commands |
| `serverUrl` | `URL` | OpenCode server URL (e.g., `http://localhost:4096`) |

### TypeScript Support

When using TypeScript, you can import types from the plugin package:

```ts
// .opencode/plugin/my-plugin.ts
import type { Plugin } from "@opencode-ai/plugin"

export const MyPlugin: Plugin = async ({ project, client, $, directory, worktree, serverUrl }) => {
  return {
    // Type-safe hook implementations
  }
}
```

The plugin package is automatically installed to `.opencode/node_modules/` at startup.

---

## Simple Examples

### Sending Notifications

Send a system notification when a session completes:

```js
// .opencode/plugin/notification.js
export const NotificationPlugin = async ({ $ }) => {
  return {
    event: async ({ event }) => {
      if (event.type === "session.idle") {
        await $`osascript -e 'display notification "Session completed!" with title "OpenCode"'`
      }
    },
  }
}
```

> If you use the OpenCode desktop app, it can automatically send system notifications when a response is ready or a session encounters an error.

### .env File Protection

Prevent OpenCode from reading `.env` files:

```js
// .opencode/plugin/env-protection.js
export const EnvProtection = async () => {
  return {
    "tool.execute.before": async (input, output) => {
      if (input.tool === "read" && output.args.filePath.includes(".env")) {
        throw new Error("Do not read .env files")
      }
    },
  }
}
```

### Logging

Use `client.app.log()` instead of `console.log` for structured logging:

```ts
// .opencode/plugin/my-plugin.ts
export const MyPlugin = async ({ client }) => {
  await client.app.log({
    service: "my-plugin",
    level: "info",
    message: "Plugin initialized",
    extra: { foo: "bar" },
  })

  return {}
}
```

Log levels: `debug`, `info`, `warn`, `error`.

---

## Common Pitfalls

| Issue | Cause | Solution |
|-------|-------|----------|
| Plugin not loaded | Wrong file extension | Ensure it's a `.js` or `.ts` file |
| Dependency not found | No package.json configured | Add `package.json` in `.opencode/` directory |
| TypeScript type errors | Plugin package not installed | OpenCode installs it at startup, or manually run `bun add @opencode-ai/plugin` |
| Plugin executed twice | Both npm and local plugin used | Check config file and plugin directory for duplicates |
| Environment variables not working | Local plugin can't access external packages | Declare dependencies in `.opencode/package.json` |

---

## Lesson Summary

You learned:

1. Two ways to load plugins (local files / npm packages)
2. Plugin loading order and deduplication mechanism
3. Basic structure for creating simple plugins
4. Using `event` and `tool.execute.before` hooks

---

## Next Step

→ [5.12b Advanced Plugins](./12b-plugins-advanced) - Learn all hook types and advanced usage
