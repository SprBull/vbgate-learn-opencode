---
title: "5.12c Hook Tutorial"
subtitle: "Complete guide to plugin hooks and configuration hooks"
course: "OpenCode Practical Course"
stage: "Stage 5"
lesson: "5.12c"
duration: "25 minutes"
practice: "30 minutes"
level: "Advanced"
description: "Systematically learn OpenCode Hooks (plugin hooks / configuration hooks), master event subscription, tool interception, LLM parameter modification, permission control and other key capabilities."
tags:
  - "hook"
  - "plugin"
  - "extension"
prerequisite:
  - "5.12a Plugin Basics"
  - "5.12b Advanced Plugins (recommended)"
---

# Hook Tutorial

## 📝 Course Notes

Key knowledge points from this lesson:

<img src="/images/5-advanced/hooks-notes.mini.jpeg" 
     alt="5.12c Hook Tutorial Notes" 
     data-zoom-src="/images/5-advanced/hooks-notes.jpeg" />

---

> 💡 **One-line summary**: Hooks are OpenCode's "extension interface" - you can execute logic when events occur, or intercept and modify data in critical workflows.

---

## What You'll Be Able to Do

- Know which Hooks OpenCode supports (plugin hooks / configuration hooks)
- Choose the right Hook: event listening vs functionality interception
- Write common Hooks: notifications, auditing, security interception, parameter tuning, context compression enhancement

---

## Your Current Challenges

- Want to automatically run scripts after a session completes, but don't know where to configure it
- Want to prevent AI from reading certain sensitive files, but can't find the right place to intercept
- See others mention "Hook" but don't understand its relationship with plugins
- Want to automatically adjust LLM parameters based on different Agents, but don't know where to start

---

## When to Use This

- When you need to:
  - Execute custom logic when specific events occur (notifications, logs, auditing)
  - Intercept tool calls and modify parameters or block execution
  - Modify LLM call parameters (temperature, top_p, etc.)
  - Customize permission decision logic
  - Enhance session compression context
- And you don't want to:
  - Modify OpenCode source code
  - Manually execute these operations every time

---

## 🎒 Before You Start

- [ ] Completed [5.12a Plugin Basics](./12a-plugins-basics)
- [ ] Completed [5.12b Advanced Plugins](./12b-plugins-advanced) (recommended)
- [ ] Have a running OpenCode project
- [ ] Can access `~/.config/opencode/` or the project's `.opencode/` folder

---

## Core Concepts

- Hooks are essentially a set of "pluggable callback functions"
- OpenCode triggers Hooks at specific times, giving you control
- There are two Hook approaches:
  - **Plugin Hooks**: Write code, return hooks object (more powerful, more flexible)
  - **Configuration Hooks**: Configure commands in `opencode.json` (simpler, but limited functionality)
- Event Hooks passively listen without modifications (logs, notifications)
- Functional Hooks actively intercept and can modify data (parameter modification, permission control)

---

### 🆕 New Hooks in v1.1.65

| Hook | Description | Use Case |
|-----|------|------|
| `tool.definition` | Modify tool definitions | Customize tool descriptions, adjust parameter schemas |
| `command.execute.before` | Intercept before command execution | Modify command arguments, add logging |
| `shell.env` | Before shell execution | Inject environment variables |

---

## Follow Along

### Step 1: Create Your First Plugin Hook

**Why**  
Start with the simplest session completion notification to verify the entire workflow works.

```bash
# Create plugin file in project directory
mkdir -p .opencode/plugin
```

```ts
// .opencode/plugin/notify.ts
import type { Plugin } from "@opencode-ai/plugin"

export const NotifyPlugin: Plugin = async ({ $ }) => {
  return {
    event: async ({ event }) => {
      if (event.type === "session.idle") {
        await $`osascript -e 'display notification "Session completed" with title "OpenCode"'`
      }
    },
  }
}
```

**You should see**:  
OpenCode loads this plugin at startup, and you'll receive a notification when a session completes.

---

### Step 2: Implement Sensitive File Interception

<AdInArticle />

**Why**  
Use the `tool.execute.before` Hook to intercept tool calls and prevent AI from reading sensitive files.

```ts
// .opencode/plugin/guard.ts
import type { Plugin } from "@opencode-ai/plugin"

export const GuardPlugin: Plugin = async () => {
  return {
    "tool.execute.before": async (input, output) => {
      if (input.tool !== "read") return

      const filePath = String(output.args.filePath)
      const sensitivePatterns = [".env", ".pem", ".key", "credentials"]

      for (const pattern of sensitivePatterns) {
        if (filePath.includes(pattern)) {
          throw new Error(`Security policy: Reading sensitive files is prohibited: ${filePath}`)
        }
      }
    },
  }
}
```

**You should see**:  
When attempting to have AI read a `.env` file, an error is thrown and execution is blocked.

---

### Step 3: Adjust LLM Parameters Based on Agent

**Why**  
Different scenarios require different parameter configurations. Use the `chat.params` Hook to automatically adjust them.

```ts
// .opencode/plugin/params.ts
import type { Plugin } from "@opencode-ai/plugin"

export const ParamsPlugin: Plugin = async () => {
  return {
    "chat.params": async (input, output) => {
      // Code generation needs more deterministic output
      if (input.agent === "code") {
        output.temperature = 0.2
      }

      // Planning tasks need more creativity
      if (input.agent === "plan") {
        output.temperature = 0.7
      }

      // Add custom tracing headers
      output.options["X-Trace-Session"] = input.sessionID
    },
  }
}
```

**You should see**:  
LLM parameters automatically change for different Agent sessions.

---

### Step 4: Auto-Decision on Permission Requests

**Why**  
Reduce manual confirmations by automatically approving safe operations.

```ts
// .opencode/plugin/auto-permit.ts
import type { Plugin } from "@opencode-ai/plugin"

export const AutoPermitPlugin: Plugin = async () => {
  return {
    "permission.ask": async (input, output) => {
      // Automatically allow read operations
      if (input.tool === "read") {
        output.status = "allow"
        return
      }

      // Automatically deny dangerous commands
      if (input.tool === "bash" && String(input.metadata?.command).includes("rm -rf")) {
        output.status = "deny"
        return
      }

      // Keep asking for other operations
      output.status = "ask"
    },
  }
}
```

**You should see**:  
Reading files no longer prompts for permission, but delete commands are blocked.

---

### Step 5: Enhance Session Compression Context

**Why**  
When conversations become too long and need compression, inject project-specific key information.

```ts
// .opencode/plugin/compaction.ts
import type { Plugin } from "@opencode-ai/plugin"

export const CompactionPlugin: Plugin = async () => {
  return {
    "experimental.session.compacting": async (input, output) => {
      output.context.push(`
## Project Key Information
- Files being modified: src/**
- Key constraints: Prohibit reading .env, key files
- Current task: Implement Hook tutorial and add to sidebar
- Important decisions: Use TypeScript strict mode
`)
    },
  }
}
```

**You should see**:  
When a conversation is compressed, the compressed context will include your custom information.

---

### Step 6: Modify Tool Definitions (v1.1.65+)

**Why**  
In certain scenarios, you may need to modify a tool's description or parameter schema to help AI better understand the tool's purpose, or add additional constraints.

```ts
// .opencode/plugin/tool-definition.ts
import type { Plugin } from "@opencode-ai/plugin"

export const ToolDefinitionPlugin: Plugin = async () => {
  return {
    "tool.definition": async (input, output) => {
      // Add description for read tool
      if (input.toolID === "read") {
        output.description = "Read file contents. Supports text files and images. Path must be absolute."
      }

      // Add security warning for bash tool
      if (input.toolID === "bash") {
        output.description += "\n\n⚠️ Warning: Dangerous commands (like rm -rf) require user confirmation."
      }

      // Modify parameter schema (e.g., add default values or constraints)
      if (input.toolID === "write" && output.parameters?.properties?.filePath) {
        output.parameters.properties.filePath.description = "Absolute file path, must start with /"
      }
    },
  }
}
```

**You should see**:  
AI uses the modified descriptions and parameter definitions when calling tools.

---

## Checklist ✅

- [ ] Plugin files are in `.opencode/plugin/` directory
- [ ] OpenCode loads plugins at startup (check startup logs)
- [ ] Received notification after session completes
- [ ] Error thrown when attempting to read `.env`
- [ ] Parameters change for different Agent sessions
- [ ] Permission request behavior matches expectations
- [ ] (v1.1.65+) Tool definitions successfully modified

---

## Common Pitfalls

| Issue | Cause | Solution |
|-----|-----|-----|
| Plugin not loaded | Wrong file extension | Ensure it's a `.ts` or `.js` file |
| `output` modification ineffective | Returned new object instead of modifying original | Directly modify `output.xxx = ...` |
| Event not triggered | `event.type` typo | Use TypeScript for type hints |
| Experimental Hook fails | API changed after version update | Check changelog, adjust code |
| Configuration Hook not working | Execution logic may not be implemented | Prefer plugin Hooks |
| Multiple plugins conflict | Duplicate Hook definitions | Check for duplicate Hook implementations |

---

## Lesson Summary

You learned:

1. Understanding the two types of Hooks (plugin hooks / configuration hooks)
2. Choosing the right Hook type for your problem
3. Implementing common Hook scenarios (notifications, interception, parameter tuning, permissions, compression)
4. Following Hook writing best practices

---

## Next Lesson Preview

> In the next lesson, we'll learn about custom tools, which will use the Hook and plugin knowledge from this lesson.

---

## Quick Reference: Common Hooks

| Hook | Trigger Timing | Use Case | Can Modify Data |
|-----|---------|------|---------------|
| `event` | All events | Unified subscription, logs/notifications/stats | ❌ |
| `config` | After config loaded | Initialize plugins, modify config | ✅ |
| `tool.execute.before` | Before tool execution | Intercept/modify parameters, block execution | ✅ |
| `tool.execute.after` | After tool execution | Record results, modify output | ✅ |
| `chat.message` | When new message received | Record/modify message content | ✅ |
| `chat.params` | Before LLM call | Modify temperature/Top-P/Top-K | ✅ |
| `permission.ask` | When permission requested | Auto allow/deny | ✅ |
| `tool` | Tool registration | Add custom tools | - |
| `experimental.session.compacting` | Before session compression | Inject project key info | ✅ |
| `tool.definition` | Tool registration | Modify tool description/parameters | ✅ |
| `command.execute.before` | Before command execution | Intercept/modify command arguments | ✅ |
| `shell.env` | Before shell execution | Inject environment variables | ✅ |
| `auth` | Authentication flow | Custom authentication method | - |

---

## Quick Reference: Common Events

| Event | Description | Hook Use Case |
|-----|------|-----------|
| `session.idle` | Session complete (idle) | Send notifications, cleanup resources, record duration |
| `session.created` | New session created | Initialize session-level state |
| `file.edited` | File edited | Trigger formatting, trigger build |
| `message.updated` | Message updated | Record conversation history, statistics |
| `tool.execute.after` | After tool execution | Record logs, audit trail |
| `tool.execute.before` | Before tool execution | Parameter validation, permission check |
| `permission.replied` | User responded to permission | Record permission decisions |
| `command.executed` | After command execution | Command auditing |
| `session.error` | Session error | Error reporting, notifications |
| `server.connected` | Server connected | Connection status notification |

---

## Appendix: Source Code Reference

<details>
<summary><strong>Click to expand source code locations</strong></summary>

| Feature | File Path | Line |
|-----|---------|------|
| Hook type definitions | [`packages/plugin/src/index.ts`](https://github.com/anomalyco/opencode/blob/dev/packages/plugin/src/index.ts) | 148-231 |
| `tool.definition` Hook definition | [`packages/plugin/src/index.ts`](https://github.com/anomalyco/opencode/blob/dev/packages/plugin/src/index.ts) | 227-230 |
| `tool.definition` Hook trigger | [`packages/opencode/src/tool/registry.ts`](https://github.com/anomalyco/opencode/blob/dev/packages/opencode/src/tool/registry.ts) | 157 |
| Plugin loading logic | [`packages/opencode/src/plugin/index.ts`](https://github.com/anomalyco/opencode/blob/dev/packages/opencode/src/plugin/index.ts) | 20-82 |
| Plugin directory scanning | [`packages/opencode/src/config/config.ts`](https://github.com/anomalyco/opencode/blob/dev/packages/opencode/src/config/config.ts) | 322-335 |
| Plugin deduplication logic | [`packages/opencode/src/config/config.ts`](https://github.com/anomalyco/opencode/blob/dev/packages/opencode/src/config/config.ts) | 369-387 |
| Configuration Hook Schema | [`packages/opencode/src/config/config.ts`](https://github.com/anomalyco/opencode/blob/dev/packages/opencode/src/config/config.ts) | 1009-1030 |

**Key Code Snippets**:

```typescript
// Hook type definitions
export interface Hooks {
  event?: (input: { event: Event }) => Promise<void>
  config?: (input: Config) => Promise<void>
  tool?: { [key: string]: ToolDefinition }
  auth?: AuthHook
  "chat.message"?: (input: {...}, output: {...}) => Promise<void>
  "chat.params"?: (input: {...}, output: {...}) => Promise<void>
  "permission.ask"?: (input: Permission, output: {...}) => Promise<void>
  "tool.execute.before"?: (input: {...}, output: {...}) => Promise<void>
  "tool.execute.after"?: (input: {...}, output: {...}) => Promise<void>
  "command.execute.before"?: (input: { command: string; sessionID: string; arguments: string }, output: {...}) => Promise<void>
  "shell.env"?: (input: { cwd: string }, output: { env: Record<string, string> }) => Promise<void>
  "tool.definition"?: (input: { toolID: string }, output: { description: string; parameters: any }) => Promise<void>
  "experimental.chat.messages.transform"?: (input: {}, output: {...}) => Promise<void>
  "experimental.chat.system.transform"?: (input: {}, output: {...}) => Promise<void>
  "experimental.session.compacting"?: (input: {...}, output: {...}) => Promise<void>
  "experimental.text.complete"?: (input: {...}, output: {...}) => Promise<void>
}

// Plugin loading
export async function trigger<Name extends keyof Required<Hooks>>(name: Name, input: Input, output: Output): Promise<Output> {
  if (!name) return output
  for (const hook of await state().then((x) => x.hooks)) {
    const fn = hook[name]
    if (!fn) continue
    await fn(input, output)
  }
  return output
}
```

</details>
