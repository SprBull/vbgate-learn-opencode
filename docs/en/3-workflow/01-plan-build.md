---
title: "Plan vs Build: Planning and Execution"
subtitle: "Two modes, two purposes"
course: "OpenCode Practical Course"
stage: "Stage 3"
lesson: "3.1"
duration: "10 min"
practice: "15 min"
level: "Beginner"
description: "Understand Plan Agent (read-only analysis) and Build Agent (read-write execution), master the permission system, switch flexibly with Tab key, and master efficient AI programming workflow."
tags:
  - Plan
  - Build
  - Mode
prerequisite:
  - "2.1 Interface and Basic Operations"
---

# Plan vs Build: Planning and Execution

> 💡 **One-liner**: Plan Agent is read-only analysis, Build Agent is read-write execution. Press <kbd>Tab</kbd> to switch.

## 📝 Course Notes

Key takeaways from this lesson:

<img src="/images/3-workflow/plan-build-notes.mini.jpeg"
     alt="Plan vs Build: Planning and Execution Notes"
     data-zoom-src="/images/3-workflow/plan-build-notes.jpeg" />

---

## What You'll Be Able to Do

- Understand the difference between Plan and Build Primary Agents
- Know when to use Plan and when to use Build
- Proficiently switch Agents with <kbd>Tab</kbd>
- Let AI track complex task progress with TODO

<!-- 📹 Demo: Mode switching demo -->
<!-- TODO: Demo GIF to be recorded -->
<!-- ![Plan vs Build Demo](/images/3-workflow/plan-build-demo.gif) -->

---

## Your Current Challenges

- AI modifies files immediately, sometimes incorrectly
- Want AI to analyze before acting, but don't know how to control it
- Don't know when AI should be read-only vs read-write
- Complex tasks get stuck halfway, don't know AI's progress

---

## When to Use This

- When you need to: control whether AI modifies files
- And you don't want: AI to change code before you've thought it through

---

## 🎒 Prerequisites

> Make sure you've completed the following:

- [ ] Completed [2.1 Interface and Basic Operations](../2-daily/01-interface)
- [ ] Have a project directory with code

---

## Core Concepts

### What are Plan and Build

Plan and Build are two built-in **Primary Agents** in OpenCode.

- **Primary Agent**: A main assistant you can directly converse with, switch with <kbd>Tab</kbd>
- **Subagent**: An expert assistant invoked by Primary Agent, mentioned with `@` (see [3.2 Understanding Agents](./02-agents))

OpenCode provides two Primary Agents by default:

| Agent | Type | Description |
|-------|------|-------------|
| **Build** | Primary | Default assistant, all tools available, suitable for development work |
| **Plan** | Primary | Restricted assistant, permission-based, suitable for analysis and planning |

### Permission System

Plan Agent uses a **permission isolation** mechanism to protect your code—it's prohibited from editing source code, only allowed to edit plan files:

| Permission | Plan Agent | Build Agent |
|------|-----------|------------|
| `edit` (write/modify files) | **deny** (source code forbidden, plan files only) | allow |
| `bash` (execute commands) | allow | allow |
| `read`, `grep`, `glob`, etc. | allow | allow |

> ⚠️ **Note**: Plan Agent can edit `.opencode/plans/*.md` plan files, but cannot edit project source code.

### When to Use Plan

- Analyze code structure without modifications
- Let AI do planning and design
- Code review
- Understand unfamiliar codebases

### When to Use Build

- Let AI write new features
- Let AI fix bugs
- Let AI refactor code
- Let AI create/modify files

### Mode Selection Quick Reference

| Your Need | Recommended Mode | Reason |
|---------|---------|------|
| Write new feature | Build | Direct development is efficient |
| Fix simple bug | Build | Impact scope is clear |
| Refactor core module | Plan first, then Build | Analyze impact before acting |
| Learn new codebase | Plan | Safe exploration, no accidental changes |
| Unsure of change impact | Plan | Analyze first, then decide |
| Quick prototype validation | Build | Iteration speed priority |
| Team collaboration task | Plan first, then Build | Plan is reviewable, execution is traceable |
| Code review | Plan | Read-only analysis, no modifications |

**Simple rule**: Unsure → Use Plan first; Confirmed → Use Build directly

---

## Available Tools
<AdInArticle />

Plan Agent can use read-only tools, Build Agent can use all tools:

### Read-Only Tools (Available to Both Plan and Build)

| Tool | Description |
|------|------|
| `read` | Read file contents |
| `grep` | Search file contents |
| `glob` | Find files by pattern |
| `list` | List directory contents |
| `webfetch` | Fetch web content |

### Read-Write Tools (Only Build by Default)

| Tool | Description |
|------|------|
| `write` | Create new files |
| `edit` | Modify existing files |
| `bash` | Execute Shell commands |

---

## Configuration (Optional)

The default configuration is sufficient for daily use. If you need to customize Agent behavior, configure in `opencode.jsonc`:

```jsonc title="opencode.jsonc"
{
  "$schema": "https://opencode.ai/config.json",
  "agent": {
    // Build Agent configuration
    "build": {
      "mode": "primary",
      "model": "anthropic/claude-opus-4-5-thinking",
      "temperature": 0.3,
      "permission": {
        "edit": "allow",
        "bash": "allow"
      }
    },
    // Plan Agent configuration
    "plan": {
      "mode": "primary",
      "model": "anthropic/claude-opus-4-5-thinking",
      "temperature": 0.1,
      "permission": {
        "edit": {
          "*": "deny",                    // Deny editing all source code
          ".opencode/plans/*.md": "allow" // Only allow editing plan files
        },
        "bash": "allow"
      }
    }
  }
}
```

**Configuration Options**:

- `model`: Model to use, format is `provider/model-id`
- `temperature`: Controls randomness (0-1), lower values are more focused
- `permission.edit`: File edit permission
  - `"allow"`: Allow editing
  - `"deny"`: Deny editing
  - Can also specify path rules, e.g., `{ "*": "deny", ".opencode/plans/*.md": "allow" }`
- `permission.bash`: Command execution permission (`allow`/`deny`)

> 💡 **Tip**: The configuration file supports JSONC format, you can add `//` comments.

---

## Follow Along

### Step 1: Confirm Current Agent

**Why**  
First see which Agent is currently active.

Look at the right side of the status bar, it will show `Plan` or `Build`.

### Step 2: Switch to Plan Agent

**Why**  
Preparing for read-only analysis.

Press <kbd>Tab</kbd> until the status bar shows `Plan`.

### Step 3: Analyze Code with Plan Agent

**Why**  
Experience read-only analysis, AI won't modify any files.

Enter:

```
@src/main.ts Analyze this file's structure, list all functions and their purposes
```

**You should see**: AI uses the `read` tool to read the file and analyze structure. Since Plan Agent is prohibited from editing source code, AI won't directly modify files.

### Step 4: Switch to Build Agent

**Why**  
Preparing to let AI modify code.

Press <kbd>Tab</kbd>, status bar shows `Build`.

### Step 5: Refactor Code with Build Agent

**Why**  
Experience read-write mode, AI will actually modify files.

Enter:

```
Add detailed JSDoc comments to @src/main.ts
```

**You should see**: AI uses the `edit` tool to modify the file and add comments. You can review the changes and decide whether to accept.

### Step 6: Undo Changes (Optional)

**Why**  
If not satisfied, you can undo.

```
/undo
```

---

## Tip: Let AI Track Task Progress

For complex tasks, explicitly tell AI to track progress with TODO:

| What You Say | What AI Does |
|---------|------------|
| "Track progress with TODO" | Creates task list, updates status step by step |
| "Complete in steps" | Automatically breaks down tasks, updates while working |
| "How's the current progress?" | Reports completed/in-progress/pending |

**Example Conversation**:

```
You: Help me refactor the user authentication module, track progress with TODO

AI: Sure, I'll create a task list first:
    ✅ 1. Analyze existing code structure
    🔄 2. Design new authentication flow
    ⏳ 3. Rewrite authentication logic
    ⏳ 4. Update test cases
    ⏳ 5. Verify functionality

    Starting the first item...

You: Current progress?

AI: Let me check...
    ✅ 1. Analyze existing code structure (completed)
    ✅ 2. Design new authentication flow (completed)
    🔄 3. Rewrite authentication logic (in progress, ~5 min remaining)
    ⏳ 4. Update test cases
    ⏳ 5. Verify functionality
```

**When to Use This Tip**:

- Task requires more than 3 steps
- You might leave midway and want to know progress when returning
- You want AI to execute methodically without missing steps

> 💡 **How it works**: AI has internal `todoread` and `todowrite` tools. You don't need to know the details, just say "track with TODO" in your prompt.

---

## Checklist ✅

> All must pass to continue

- [ ] <kbd>Tab</kbd> can switch between Plan Agent and Build Agent
- [ ] Plan Agent is prohibited from editing source code, only `.opencode/plans/*.md` plan files
- [ ] Build Agent can freely modify files and execute commands
- [ ] Know how to let AI track task progress with TODO

---

## Common Pitfalls

| Symptom | Cause | Solution |
|-----|-----|-----|
| Want AI to modify files but it doesn't | Might be in Plan Agent, which is prohibited from editing source code | Press Tab to switch to Build |
| AI modified files it shouldn't | In Build Agent, permission is `allow` | Use `/undo` to revert, use Plan to analyze first next time |
| Plan Agent can't edit source code | This is by design, Plan can only edit plan files | Switch to Build to make modifications |

---

## Advanced Features (Just Be Aware)

### temperature: Control Randomness

Plan Agent typically uses lower `temperature` (e.g., 0.1) for more focused and deterministic output; Build Agent uses medium values (e.g., 0.3) to balance focus and creativity.

### maxSteps: Limit Iterations

You can set the maximum number of tool calls an Agent can execute to avoid over-operation or excessive costs.

```jsonc
{
  "agent": {
    "plan": {
      "steps": 5  // Maximum 5 tool calls
    }
  }
}
```

### Custom Keybinds

By default, <kbd>Tab</kbd> switches Agents, but you can modify `agent_cycle` keybinding in configuration:

```jsonc
{
  "keybinds": {
    "agent_cycle": "tab",           // Switch to next Agent (default)
    "agent_cycle_reverse": "shift+tab"  // Switch to previous Agent (default)
  }
}
```

### plan_enter / plan_exit: AI Auto-Switches Modes

::: warning ⚠️ Experimental Feature
These two tools are currently **experimental features** and require all of the following conditions:

1. Enable experimental mode: Set `OPENCODE_EXPERIMENTAL=true` or `OPENCODE_EXPERIMENTAL_PLAN_MODE=true`
2. Use CLI client: Run OpenCode in terminal (not Web/IDE integration)

Future versions may officially release this feature, and this tutorial will be updated accordingly.
:::

Besides manually pressing <kbd>Tab</kbd> to switch, AI can also **actively call tools** to switch modes:

| Tool | Purpose | Available To |
|------|------|-----------|
| `plan_enter` | Enter Plan mode | Build Agent |
| `plan_exit` | Exit Plan mode, return to Build | Plan Agent |

**Workflow**:

```
You: This module needs refactoring, help me analyze first, don't modify directly

AI: [Calls plan_enter tool]
    → Confirmation popup: Switch to Plan mode?
    → You choose Yes
    → AI analyzes code in Plan mode
    → Generates plan file .opencode/plans/xxx.md

You: The plan looks good, start implementing

AI: [Calls plan_exit tool]
    → Confirmation popup: Switch to Build mode?
    → You choose Yes
    → AI executes modifications in Build mode
```

**In Plan mode, AI can only edit plan files** (`.opencode/plans/*.md`), not source code. This ensures safe separation between "planning" and "execution".

### Plan File Storage Location

In Plan mode, AI-generated plan files are saved to:

| Level | Path | Description |
|------|------|------|
| Project-level | `.opencode/plans/<created>-<slug>.md` | Saved in project directory, follows project |
| Global-level | `~/.local/share/opencode/plans/<created>-<slug>.md` | Saved in global directory, shared across projects |

> `created` is creation timestamp, `slug` is URL-friendly format of plan title. Example: `1736854321-refactor-auth.md`

::: tip Storage Location Rules
- **Project has Git (or other VCS)** → Saved to project-level `.opencode/plans/`
- **Project has no VCS** → Saved to global-level `~/.local/share/opencode/plans/`
:::

View plan files:

```bash
# View project-level plans
cat .opencode/plans/*.md

# View global-level plans
cat ~/.local/share/opencode/plans/*.md
```

> 💡 These features can be explored in depth later, understanding them at this stage is sufficient.

---

## Lesson Summary

You learned:

1. Plan and Build are two Primary Agents
2. Switch between Agents with <kbd>Tab</kbd> (or configured `agent_cycle`)
3. Plan is for analysis and planning (prohibited from editing source code), Build is for development and execution (all tools available)
4. Plan Agent can only edit `.opencode/plans/*.md` plan files
5. For complex tasks, tell AI to "track progress with TODO" for methodical execution

---

---

## Appendix: Source Code Reference

<details>
<summary><strong>Click to expand source code locations</strong></summary>

> Last updated: 2026-02-14

| Feature | File Path | Line Numbers |
|-----|---------|------|
| Build Agent definition | [`packages/opencode/src/agent/agent.ts`](https://github.com/anomalyco/opencode/blob/dev/packages/opencode/src/agent/agent.ts#L77-L91) | 77-91 |
| Plan Agent definition | [`packages/opencode/src/agent/agent.ts`](https://github.com/anomalyco/opencode/blob/dev/packages/opencode/src/agent/agent.ts#L92-L114) | 92-114 |
| Default permission rules | [`packages/opencode/src/agent/agent.ts`](https://github.com/anomalyco/opencode/blob/dev/packages/opencode/src/agent/agent.ts#L55-L73) | 55-73 |
| plan_enter tool | [`packages/opencode/src/tool/plan.ts`](https://github.com/anomalyco/opencode/blob/dev/packages/opencode/src/tool/plan.ts#L75-L130) | 75-130 |
| plan_exit tool | [`packages/opencode/src/tool/plan.ts`](https://github.com/anomalyco/opencode/blob/dev/packages/opencode/src/tool/plan.ts#L20-L73) | 20-73 |
| Plan mode prompt | [`packages/opencode/src/session/prompt.ts`](https://github.com/anomalyco/opencode/blob/dev/packages/opencode/src/session/prompt.ts#L1451-L1455) | 1451-1455 |

**Key Constants**:
- `plan_enter`: Tool to switch from Build to Plan
- `plan_exit`: Tool to switch from Plan to Build

**Permission Actions**:
- `allow`: Allow execution
- `deny`: Deny execution
- `ask`: Ask user for confirmation

**Plan Agent Permission Configuration** (source code definition):
```typescript
{
  question: "allow",                        // Can ask you questions
  plan_exit: "allow",                       // Can exit Plan mode
  external_directory: {
    [Global.Path.data + "/plans/*"]: "allow",  // Allow access to global plans directory
  },
  edit: {
    "*": "deny",                           // Deny editing all files
    ".opencode/plans/*.md": "allow",       // Allow editing project plan files
    [Global.Path.data + "/plans/*.md"]: "allow", // Allow editing global plan files
  },
}
```

</details>

---

## Next Lesson Preview

> In the next lesson, we'll explore the Agent system and learn how to invoke different experts to complete tasks.
