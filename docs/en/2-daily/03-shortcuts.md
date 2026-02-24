---
title: "Essential Keyboard Shortcuts"
subtitle: "15 shortcuts to double your productivity"
course: "OpenCode Practical Course"
stage: "Phase 2"
lesson: "2.3"
duration: "8 min"
practice: "10 min"
level: "Beginner"
description: "15 hand-picked practical shortcuts to double your daily productivity."
tags:
  - "shortcuts"
  - "productivity"
  - "daily use"
prerequisite:
  - "2.1 Interface & Operations"
---

# Essential Keyboard Shortcuts

> 💡 **TL;DR**: Master these 15 shortcuts to double your daily productivity.

## 📝 Course Notes

Key takeaways from this lesson:

<img src="/images/2-daily/03-shortcuts-notes.mini.jpeg" 
     alt="Essential shortcuts cheat sheet" 
     data-zoom-src="/images/2-daily/03-shortcuts-notes.jpeg" />

---

## What You'll Be Able to Do

- Quickly create/switch sessions with shortcuts
- One-key model and Agent switching
- Quickly undo, redo, and copy messages
- Navigate long conversations with page keys

---

## Your Current Pain Points

- Typing `/new` every time to create a new session
- Typing `/models` to switch models
- Not knowing how to undo operations
- Slowly scrolling through long conversations

---

## When to Use This

- When you need to: work frequently in OpenCode
- And don't want to: type commands every time

---

## 🎒 Prerequisites

> Make sure you've completed the following:

- [ ] Completed [2.1 Interface & Operations](./01-interface)
- [ ] Can have normal conversations with AI

---

## Core Concepts

### The Leader Key Mechanism (Important!)

OpenCode uses a **Leader key** (default <kbd>Ctrl</kbd>+<kbd>X</kbd>) as a shortcut prefix to avoid conflicts with terminal shortcuts.

::: info 🤔 What is a Leader Key?
A Leader key is similar to Vim's `<Leader>` or "combo keys" in games. It's not a function key itself, but a **prefix key**.

After pressing the Leader key, OpenCode waits for you to press a letter key. The combination forms a complete shortcut.
:::

**How to Use (Three-Step Method)**:

```
┌─────────────────────────────────────────────────────────────┐
│  Step 1           Step 2           Step 3                   │
│  Press Ctrl+X  →  Release all  →  Press letter (e.g. N)     │
│                                                             │
│  ⚠️ Key: Step 2 must release! Don't hold all three keys!    │
└─────────────────────────────────────────────────────────────┘
```

**Examples**:

| What You Want | Correct Operation | Wrong Operation |
|--------------|-------------------|-----------------|
| New session | Press Ctrl+X → Release → Press N | ❌ Press Ctrl+X+N simultaneously |
| Open session list | Press Ctrl+X → Release → Press L | ❌ Hold Ctrl, press X then L |
| Switch model | Press Ctrl+X → Release → Press M | ❌ Press too fast without releasing |

::: tip 💡 Practice Tip
Initially, **deliberately slow down**: after pressing Ctrl+X, mentally count "1", then press the letter key. You'll naturally speed up with practice.
:::

### Selection Criteria

From 60+ shortcuts, selected based on:

1. **High frequency** - Used almost daily
2. **Time-saving** - Much faster than typing commands
3. **Easy to remember** - Follows a pattern

---

## 15 Essential Shortcuts

<AdInArticle />

### 🔥 Tier 1: Daily Essentials

These 8 are the most frequently used - memorize these first:

| Shortcut | Function | Notes |
|----------|----------|-------|
| <kbd>Enter</kbd> | Send message | Enter to send |
| <kbd>Shift</kbd>+<kbd>Enter</kbd> | **New line (don't send)** | Use when writing multi-line prompts |
| <kbd>Ctrl</kbd>+<kbd>C</kbd> | Clear input / Close dialog / Exit | See details below |
| <kbd>Escape</kbd> | Interrupt AI response | Press while AI is generating to stop immediately. **Press twice to force interrupt** |
| <kbd>↑</kbd> / <kbd>↓</kbd> | Browse input history | **When input is empty**, use arrow keys to recall previous messages |
| <kbd>Tab</kbd> | Switch Agent | Switch between Plan/Build/different Agents |
| <kbd>Ctrl</kbd>+<kbd>X</kbd> → <kbd>N</kbd> | New session | Leader + N = **N**ew |
| <kbd>Ctrl</kbd>+<kbd>X</kbd> → <kbd>L</kbd> | Session list | Leader + L = **L**ist |

::: tip 💡 Multiple Ways to Create New Lines
Besides <kbd>Shift</kbd>+<kbd>Enter</kbd>, you can also use:
- <kbd>Ctrl</kbd>+<kbd>Enter</kbd>
- <kbd>Alt</kbd>+<kbd>Enter</kbd>
- <kbd>Ctrl</kbd>+<kbd>J</kbd>

Just pick one that feels natural.
:::

::: details 📦 Three Behaviors of Ctrl+C (v1.1.58 update)
- **When dialog is open**: Close dialog (confirmations, selections, etc.)
- **When input has content**: Clear input box (doesn't exit)
- **When input is empty**: Exit OpenCode

⚠️ Note: Although both Ctrl+C and Ctrl+D can exit, their behaviors differ slightly. Ctrl+D sends a direct exit signal, while Ctrl+C first tries to clear the input. This matches terminal behavior that programmers are familiar with.
:::

### ⚡ Tier 2: Productivity Boosters

These 5 significantly improve efficiency:

| Shortcut | Function | Memory Tip |
|----------|----------|------------|
| <kbd>Ctrl</kbd>+<kbd>X</kbd> → <kbd>M</kbd> | Model list | **M**odel |
| <kbd>F2</kbd> | Quick switch recent model | IDE standard |
| <kbd>Ctrl</kbd>+<kbd>X</kbd> → <kbd>U</kbd> | Undo message | **U**ndo |
| <kbd>Ctrl</kbd>+<kbd>X</kbd> → <kbd>R</kbd> | Redo message | **R**edo |
| <kbd>Ctrl</kbd>+<kbd>P</kbd> | Command palette | Same as VS Code |

### 🎯 Tier 3: Nice to Have

These 5 are useful in specific scenarios:

| Shortcut | Function | Use Case |
|----------|----------|----------|
| <kbd>Ctrl</kbd>+<kbd>X</kbd> → <kbd>Y</kbd> | Copy message | Copy AI response |
| <kbd>Ctrl</kbd>+<kbd>X</kbd> → <kbd>C</kbd> | Compress context | When conversation is too long |
| <kbd>Ctrl</kbd>+<kbd>X</kbd> → <kbd>B</kbd> | Toggle sidebar | View session tree |
| <kbd>PageUp</kbd> / <kbd>PageDown</kbd> | Page navigation | Browse long conversations |
| <kbd>Ctrl</kbd>+<kbd>X</kbd> → <kbd>T</kbd> | Theme list | Change the look |

### 🧑‍💻 For Programmers: Input Box Shortcuts

If you've used terminals or Emacs, these will be familiar:

| Shortcut | Function | Readline Style |
|----------|----------|----------------|
| <kbd>Ctrl</kbd>+<kbd>A</kbd> | Jump to line start | ✅ |
| <kbd>Ctrl</kbd>+<kbd>E</kbd> | Jump to line end | ✅ |
| <kbd>Ctrl</kbd>+<kbd>K</kbd> | Delete cursor to line end | ✅ |
| <kbd>Ctrl</kbd>+<kbd>U</kbd> | Delete cursor to line start | ✅ |
| <kbd>Ctrl</kbd>+<kbd>W</kbd> | Delete previous word | ✅ |
| <kbd>Alt</kbd>+<kbd>B</kbd> | Back one word | ✅ |
| <kbd>Alt</kbd>+<kbd>F</kbd> | Forward one word | ✅ |

::: details 📦 What is Readline Style?
Readline is the standard input library for Unix/Linux terminals that defines a common set of shortcuts.

Almost all terminal programs (bash, zsh, python REPL) support these shortcuts. If you work in a terminal daily, these are already muscle memory.

OpenCode fully supports Readline, letting you edit text with familiar keystrokes.
:::

---

## Follow Along

### Step 1: Practice Multi-line Input

**Why**  
When writing multi-line prompts, you need to create new lines without sending.

1. Type `First line` in the input box
2. Press <kbd>Shift</kbd>+<kbd>Enter</kbd>
3. Type `Second line`

**You should see**: Two lines of text in the input box, message not sent

::: warning ⚠️ Common Issue
If <kbd>Shift</kbd>+<kbd>Enter</kbd> sends instead of creating a new line, your terminal doesn't support modifier keys. Solutions:
- Use <kbd>Ctrl</kbd>+<kbd>J</kbd> instead (more universal)
- Or refer to [5.6b Keybinds](../5-advanced/06b-keybinds#terminal-compatibility) to configure your terminal
:::

### Step 2: Practice History Navigation

**Why**  
Resend or modify previous messages without retyping.

1. First send a message: `Hello`
2. After AI replies, make sure the input box is empty
3. Press <kbd>↑</kbd> (up arrow)

**You should see**: The input box automatically fills with `Hello` that you just sent

Continue pressing <kbd>↑</kbd> to browse older history, press <kbd>↓</kbd> to go to more recent messages.

### Step 3: Practice Ctrl+C

**Why**  
Quickly clear input, close dialogs, or exit OpenCode.

**Scenario A - Clear Input**:
1. Type some text in the input box
2. Press <kbd>Ctrl</kbd>+<kbd>C</kbd>

**You should see**: Input box is cleared

**Scenario B - Close Dialog**:
1. Trigger a dialog (e.g., press <kbd>Ctrl</kbd>+<kbd>X</kbd> → <kbd>L</kbd> to open session list)
2. Press <kbd>Ctrl</kbd>+<kbd>C</kbd>

**You should see**: Dialog closes, returns to normal conversation interface

**Scenario C - Exit Application**:
1. Make sure input box is empty and no dialog is open
2. Press <kbd>Ctrl</kbd>+<kbd>C</kbd>

**You should see**: OpenCode exits

### Step 4: Practice Leader Key Combinations

**Why**  
This is OpenCode's core shortcut mechanism.

**Important**: This is a two-step operation, not simultaneous!

1. Press <kbd>Ctrl</kbd>+<kbd>X</kbd>
2. **Release all keys** (this step is crucial!)
3. Press <kbd>N</kbd>

**You should see**: A new session is created

Try opening the session list:

1. Press <kbd>Ctrl</kbd>+<kbd>X</kbd>
2. **Release**
3. Press <kbd>L</kbd>

**You should see**: Session list popup appears

### Step 5: Practice Undo/Redo

**Why**  
Retry when AI's response is unsatisfactory.

1. Send a message to AI
2. After AI replies, press <kbd>Ctrl</kbd>+<kbd>X</kbd> → <kbd>U</kbd>

**You should see**: The message and reply are undone

Press <kbd>Ctrl</kbd>+<kbd>X</kbd> → <kbd>R</kbd> to redo.

### Step 6: Practice Interrupting Response

**Why**  
Stop AI early when response is too long or going in the wrong direction.

1. Send a complex question
2. While AI is responding, press <kbd>Escape</kbd>

**You should see**: AI stops generating

---

## Checklist ✅

> Must pass all to continue

- [ ] <kbd>Shift</kbd>+<kbd>Enter</kbd> creates new line without sending
- [ ] <kbd>↑</kbd> browses input history (when input is empty)
- [ ] <kbd>Ctrl</kbd>+<kbd>C</kbd> clears input, closes dialogs
- [ ] <kbd>Ctrl</kbd>+<kbd>X</kbd> → <kbd>N</kbd> creates new session (remember to release before pressing N)
- [ ] <kbd>Ctrl</kbd>+<kbd>X</kbd> → <kbd>L</kbd> opens session list
- [ ] <kbd>Escape</kbd> interrupts AI response

---

## Common Pitfalls

| Symptom | Cause | Solution |
|---------|-------|----------|
| Shift+Enter sends instead of new line | Terminal doesn't send modifier keys | Use <kbd>Ctrl</kbd>+<kbd>J</kbd>, or configure terminal |
| Ctrl+X then N does nothing | Pressed N without releasing Ctrl+X | **Must release first**, then press N |
| Ctrl+X has no response | Terminal captured the key | Check terminal settings, or try a different terminal |
| **Ctrl+C is not copy** | Used to clear input or exit, not copy | To copy, use <kbd>Ctrl</kbd>+<kbd>X</kbd> → <kbd>Y</kbd> or select with mouse then <kbd>Ctrl</kbd>+<kbd>V</kbd>
| Up arrow doesn't show history | Input box is not empty | First clear input box (Ctrl+C), then press up arrow |
| Tab doesn't switch Agent | Pressed while in input mode | Press Escape to exit input, then press Tab |
| **Ctrl+Z accidentally suspends** | Thought it was undo, actually suspends terminal | OpenCode will pause, need to type `fg` in terminal to resume. Don't use for "undo"! |

---

## Quick Memory Rhyme

```
Enter sends, Shift for new line
Up arrow for history, Ctrl+C clears and exits
New is N, List is L, Model M remember well
Undo U, Redo R, Copy Y with ease
Escape interrupts fast
Tab switches Agents conveniently
Ctrl+Z will suspend, don't use for undo
```

---

## Lesson Summary

You learned:

1. **New line technique**: <kbd>Shift</kbd>+<kbd>Enter</kbd> for new line, <kbd>Enter</kbd> to send
2. **History navigation**: When input is empty, <kbd>↑</kbd>/<kbd>↓</kbd> to browse history
3. **Ctrl+C**: Close dialog / Clear input (has content) or Exit (empty)
4. **Leader key mechanism**: <kbd>Ctrl</kbd>+<kbd>X</kbd> → Release → Letter key
5. **Session management**: N (new), L (list), U (undo)
6. **Programmer bonus**: Full Readline-style shortcut support

---

## Want More?

- [Quick Reference/Shortcuts](../appendix/keybinds) - Complete 60+ shortcuts list
- [5.6b Keybinds](../5-advanced/06b-keybinds) - Custom shortcuts tutorial

---

## Next Lesson Preview

> Next we'll learn about **[Global Rules](./04-global-rules)** to make AI permanently remember your work preferences.
>
> You'll learn:
> - Create rule files, no need to say "reply in English" every time
> - Difference between global rules vs project rules
> - Practical rule examples

---

## Appendix: Source Code Reference

<details>
<summary><strong>Click to expand source code locations</strong></summary>

> Last updated: 2026-01-13

| Feature | File Path | Lines |
|---------|-----------|-------|
| Default shortcuts | [`src/config/config.ts`](https://github.com/anomalyco/opencode/blob/dev/packages/opencode/src/config/config.ts#L616-L754) | 616-754 |
| Shortcut parsing | [`src/util/keybind.ts`](https://github.com/anomalyco/opencode/blob/dev/packages/opencode/src/util/keybind.ts) | Entire file |

**Key Defaults** (from `config.ts`):
- `input_submit = "return"` - Send message (line 668)
- `input_newline = "shift+return,ctrl+return,alt+return,ctrl+j"` - New line (lines 669-673)
- `input_clear = "ctrl+c"` - Clear input (line 666)
- `app_exit = "ctrl+c,ctrl+d,<leader>q"` - Exit application (line 617)
- `history_previous = "up"` - Previous history (line 747)
- `history_next = "down"` - Next history (line 748)
- `agent_cycle = "tab"` - Switch Agent (line 663)
- `leader = "ctrl+x"` - Leader key (line 616)
- `session_new = "<leader>n"` - New session
- `session_list = "<leader>l"` - Session list
- `model_list = "<leader>m"` - Model list
- `messages_undo = "<leader>u"` - Undo message
- `messages_redo = "<leader>r"` - Redo message

</details>
