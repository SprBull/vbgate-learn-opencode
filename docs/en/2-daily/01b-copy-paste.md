---
title: "2.1b How to Copy Content"
subtitle: "Goodbye Ctrl+C Confusion"
course: "OpenCode Practical Course"
stage: "Phase 2"
lesson: "2.1b"
duration: "5 min"
practice: "5 min"
level: "Beginner"
description: "Why can't Ctrl+C copy? Learn three efficient ways to copy in OpenCode."
tags:
  - "Copy Paste"
  - "Basic Operations"
  - "Windows"
  - "Mac"
prerequisite:
  - "2.1 Interface & Operations"
---

# 2.1b How to Copy Content

> 💡 **First Question from Beginners**: "Why does the program exit when I press Ctrl+C?!"

## 📝 Course Notes

Key takeaways from this lesson:

<img src="/images/2-daily/01b-copy-paste-notes.mini.jpeg" alt="Copy operations cheat sheet" data-zoom-src="/images/2-daily/01b-copy-paste-notes.jpeg" />

---

## What You'll Learn

- Understand why Ctrl+C doesn't work for copying
- Master the "magic" of copy-on-selection with your mouse
- Learn to copy AI's long responses with one keystroke
- Solve text selection issues in Windows terminals

---

## 💥 Why Doesn't Ctrl+C Work?

For users accustomed to Word and browsers, this might be the biggest culture shock.

In the terminal world (the black box where OpenCode runs), `Ctrl+C` is typically used as an interrupt signal, not a copy shortcut.

- **In Word**: `Ctrl+C` = 📷 **Take a snapshot** (copy content)
- **In Terminal**: `Ctrl+C` = 🛑 **Interrupt**

Therefore, pressing `Ctrl+C` in OpenCode doesn't copy the selected content.

---

## 🚀 Method 1: Mouse Flow (Most Intuitive)

This is a "hidden skill" specially designed by OpenCode for modern users, **works on both Windows and Mac**.

### Steps

1. **Press and hold the left mouse button**, drag to select the text you want to copy.
2. **Release the left mouse button**.
3. **Done!** 🎉

Yes, you read that right. You don't need to right-click or press any key. The moment you **release the mouse**, OpenCode automatically copies the selected content to the clipboard and shows `Copied to clipboard`.

---

## ⌨️ Method 2: Keyboard Flow (Fastest)

When you only want **what the AI just said** (like a big chunk of code), dragging with the mouse is too tedious.

### Steps

1. Press the **Leader key** (default is <kbd>Ctrl</kbd>+<kbd>X</kbd>).
2. Release all keys.
3. Press <kbd>Y</kbd>.

**Memory trick**: `Y` = **Y**ank (this is programmer slang for "copy").

> Want more shortcuts? Check out **[2.3 Recommended Shortcuts](./03-shortcuts)**.

---

## 📜 Method 3: Command Flow (Most Complete)

When you want to save **the entire conversation history** (what you said + what the AI said) to share with friends or save to a document.

### Steps

1. Type `/copy` in the input box.
2. Press <kbd>Enter</kbd>.

The entire conversation history will be copied completely.

---

## 🛡️ Last Resort: Force System Copy

If the "magic" above doesn't work, or you just want to use the native system copy method.

| System | Operation |
|--------|-----------|
| **Mac** | Hold <kbd>Option (⌥)</kbd> + mouse drag select → <kbd>Command</kbd>+<kbd>C</kbd> |
| **Windows** (before v1.1.64) | Hold <kbd>Shift</kbd> + mouse drag select → <kbd>Right click</kbd> or <kbd>Enter</kbd> |
| **Windows** (v1.1.64+) | Direct mouse drag select → auto copy or <kbd>Ctrl</kbd>+<kbd>C</kbd> |

**Use Cases**:
- When OpenCode is frozen and unresponsive
- When you want to precisely copy error messages
- When the terminal window is hijacked by another program

---

## Follow Along

### Step 1: Experience Ctrl+C
1. Type a few characters in the input box (don't send it).
2. Press <kbd>Ctrl</kbd>+<kbd>C</kbd>.
3. Did the input box get cleared? That's because Ctrl+C was recognized as an interrupt signal.

### Step 2: Experience "Auto Copy"
1. Let the AI say something (e.g., type `hi`).
2. Use your mouse to select a few words from the AI's response.
3. **Release the mouse**.
4. Open a notepad and press `Ctrl+V` to paste.
5. Did it work?

### Step 3: Experience "Force Copy"
1. Go back to OpenCode.
2. **Mac users**: Hold <kbd>Option</kbd>, **Windows users**: Hold <kbd>Shift</kbd>.
3. Drag select some text with your mouse.
4. This method bypasses OpenCode and uses the terminal system's selection function directly.

---

## 🚑 Troubleshooting: What If Garbled Text Appears?

**Symptom**: If you're a Windows user, after pressing `Ctrl+C` to exit, you might see garbled text like `[555;38;16M` appearing on screen when you move the mouse.

**Cause**:
- OpenCode enables "mouse tracking mode" on startup.
- `Ctrl+C` on Windows is a forceful termination signal (SIGINT).
- This causes OpenCode to be killed before it can tell the terminal to "disable mouse tracking".
- The terminal thinks you're still in the program and keeps sending mouse coordinates to the screen, which appears as garbled text.

> 🐛 **Known Issue**: As of OpenCode **v1.1.25**, this issue is not fully resolved on Windows. This is a low-level technical limitation, we recommend following the table below.

**Solutions**:
1. **Quick Fix**: Close the current terminal window and reopen it.
2. **Prevention (Highly Recommended)**: Don't use `Ctrl+C` to exit! Use **Ctrl+D** instead.

| Exit Method | Nature | Result |
|-------------|--------|--------|
| <kbd>Ctrl</kbd>+<kbd>C</kbd> | 🔪 **Force Kill** | Prone to mouse garbled text, not recommended |
| <kbd>Ctrl</kbd>+<kbd>D</kbd> | 👋 **Graceful Exit** | Clean exit with automatic cleanup, **recommended** |

> **Tip**: `Ctrl+D` triggers OpenCode's cleanup logic, ensuring mouse mode is properly disabled.

---

## 🎉 Good News: Major Windows Experience Improvements (v1.1.64+)

> 🪟 **Windows Exclusive**: If you're using **OpenCode v1.1.64 or later**, congratulations!

Starting from v1.1.64, the text selection experience on Windows has been greatly improved:

| Improvement | Before | Now |
|-------------|--------|-----|
| Mouse selection | Required holding Shift | Direct drag select works |
| Ctrl+C copy | Not supported | Supports manual copy of selected content |

**Now Windows users can**:
- Select text directly with the mouse like a normal text editor
- Press `Ctrl+C` to manually copy after selection (if auto copy doesn't trigger)

> 📌 **Version Check**: Type `/version` to check your OpenCode version.

---

## 📚 Further Reading

- Want to master more shortcuts?
  👉 **[2.3 Recommended Shortcuts](./03-shortcuts)**

- Want to customize shortcuts (like changing Ctrl+C back)?
  👉 **[5.6b Shortcut Customization](../5-advanced/06b-keybinds)**

---

## Next Lesson Preview

> Next lesson: **[AI's Basic Tools](./01c-basic-tools)**.
>
> You'll learn:
> - What are the 6 basic tools AI has and what each does
> - The "read before write" rule and edit's smart matching
> - Why you shouldn't let AI use bash for file operations

---

## Appendix: Source Code Reference

<details>
<summary><strong>Click to expand source code locations</strong></summary>

> Last updated: 2026-02-14 (v1.1.64)

OpenCode's "copy on mouse release" logic is not a terminal default behavior, but an advanced feature written in code:

| Feature | File Path | Key Logic |
|---------|-----------|-----------|
| Mouse copy logic | [`src/cli/cmd/tui/app.tsx`](https://github.com/anomalyco/opencode/blob/dev/packages/opencode/src/cli/cmd/tui/app.tsx) | `onMouseUp` event listener |
| Clipboard utility | [`src/cli/cmd/tui/util/clipboard.ts`](https://github.com/anomalyco/opencode/blob/dev/packages/opencode/src/cli/cmd/tui/util/clipboard.ts) | Cross-platform clipboard support |
| Windows selection improvement (v1.1.64) | Search keywords `windows`, `win32`, `selection` | `packages/opencode/src/` |

**Source code search command**:
```bash
grep -rn "windows\|win32\|selection" packages/opencode/src/
```

**Core code snippet (`app.tsx`)**:
```typescript
// When mouse is released
onMouseUp={async () => {
  // 1. Get selected text
  const text = renderer.getSelection()?.getSelectedText()
  if (text && text.length > 0) {
    // 2. Call clipboard API to copy
    await Clipboard.copy(text)
    // 3. Notify user
    toast.show({ message: "Copied to clipboard" })
    // 4. Clear selection state
    renderer.clearSelection()
  }
}}
```
</details>
