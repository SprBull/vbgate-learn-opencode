---
title: "5.6b Keybindings"
subtitle: "Muscle Memory for Efficient Operations"
course: "OpenCode Practical Course"
stage: "Stage 5"
lesson: "5.6b"
duration: "10 minutes"
practice: "15 minutes"
level: "Advanced"
description: "Customize 60+ keybindings for a smooth operational experience."
tags:
  - "keybindings"
  - "efficiency"
  - "TUI"
prerequisite:
  - "5.1 Configuration Guide"
---

# 5.6b Keybindings

> 60+ fully customizable keybindings for a smooth operational experience.

## 📝 Course Notes

Key concepts from this lesson:

<img src="/images/5-advanced/06b-keybinds-notes.mini.jpeg" alt="Keybindings Notes" data-zoom-src="/images/5-advanced/06b-keybinds-notes.jpeg" />

---

## What You'll Learn

- Master the Leader key mechanism
- Customize any keybinding
- Disable unwanted keybindings
- Resolve terminal keybinding conflicts

---

## Leader Key

OpenCode uses a **Leader key** to avoid conflicts with terminal shortcuts.

Default Leader key: <kbd>Ctrl</kbd>+<kbd>X</kbd>

**Usage**: Press Leader key, release, then press the second key.

```
Ctrl+X → n    # New session
Ctrl+X → l    # Session list
Ctrl+X → m    # Model list
```

---

## Keybinding Configuration

Configure in `opencode.json`:

```jsonc
{
  "$schema": "https://opencode.ai/config.json",
  "keybinds": {
    // Change Leader key
    "leader": "ctrl+x",
    
    // Custom keybindings
    "session_new": "<leader>n",
    "model_list": "<leader>m",
    
    // Multiple keys for same function (comma-separated)
    "app_exit": "ctrl+c,ctrl+d,<leader>q",
    
    // Disable keybinding
    "session_compact": "none"
  }
}
```

> **Note**: The config key is `keybinds` (plural), this is the only config key that uses plural form!

### Disable Keybindings

Set to `"none"` to disable:

```jsonc
{
  "keybinds": {
    "session_compact": "none",
    "sidebar_toggle": "none"
  }
}
```

### Multiple Key Bindings

Use commas to separate multiple keys:

```jsonc
{
  "keybinds": {
    "input_newline": "shift+return,ctrl+return,alt+return,ctrl+j"
  }
}
```

---

## Complete Keybinding List

### Application Control

| Key Name | Default | Description |
|----------|---------|-------------|
| `leader` | `ctrl+x` | Leader key |
| `app_exit` | `ctrl+c,ctrl+d,<leader>q` | Exit application |
| `terminal_suspend` | `ctrl+z` | Suspend terminal |
| `terminal_title_toggle` | `none` | Toggle terminal title |

### Interface Control

| Key Name | Default | Description |
|----------|---------|-------------|
| `editor_open` | `<leader>e` | Open external editor |
| `theme_list` | `<leader>t` | Theme list |
| `sidebar_toggle` | `<leader>b` | Toggle sidebar |
| `scrollbar_toggle` | `none` | Toggle scrollbar |
| `username_toggle` | `none` | Toggle username display |
| `status_view` | `<leader>s` | Status view |
| `tool_details` | `none` | Toggle tool details |
| `tips_toggle` | `<leader>h` | Toggle homepage tips |

### Session Management

<AdInArticle />

| Key Name | Default | Description |
|----------|---------|-------------|
| `session_new` | `<leader>n` | New session |
| `session_list` | `<leader>l` | Session list |
| `session_export` | `<leader>x` | Export session |
| `session_timeline` | `<leader>g` | Session timeline |
| `session_interrupt` | `escape` | Interrupt response |
| `session_compact` | `<leader>c` | Compact context |
| `session_fork` | `none` | Fork from message |
| `session_rename` | `none` | Rename session |
| `session_share` | `none` | Share session |
| `session_unshare` | `none` | Unshare session |

### Session Navigation

| Key Name | Default | Description |
|----------|---------|-------------|
| `session_child_cycle` | `<leader>right` | Cycle child sessions |
| `session_child_cycle_reverse` | `<leader>left` | Cycle child sessions (reverse) |
| `session_parent` | `<leader>up` | Return to parent session |

### Message Operations

| Key Name | Default | Description |
|----------|---------|-------------|
| `messages_copy` | `<leader>y` | Copy message |
| `messages_undo` | `<leader>u` | Undo message |
| `messages_redo` | `<leader>r` | Redo message |
| `messages_toggle_conceal` | `<leader>h` | Toggle code block folding |

### Message Scrolling

| Key Name | Default | Description |
|----------|---------|-------------|
| `messages_page_up` | `pageup` | Page up |
| `messages_page_down` | `pagedown` | Page down |
| `messages_half_page_up` | `ctrl+alt+u` | Half page up |
| `messages_half_page_down` | `ctrl+alt+d` | Half page down |
| `messages_first` | `ctrl+g,home` | Jump to first |
| `messages_last` | `ctrl+alt+g,end` | Jump to last |
| `messages_next` | `none` | Next message |
| `messages_previous` | `none` | Previous message |
| `messages_last_user` | `none` | Last user message |

### Model & Agent

| Key Name | Default | Description |
|----------|---------|-------------|
| `model_list` | `<leader>m` | Model list |
| `model_cycle_recent` | `f2` | Cycle recent models |
| `model_cycle_recent_reverse` | `shift+f2` | Cycle recent (reverse) |
| `model_cycle_favorite` | `none` | Cycle favorite models |
| `model_cycle_favorite_reverse` | `none` | Cycle favorites (reverse) |
| `variant_cycle` | `ctrl+t` | Cycle model variants |
| `agent_list` | `<leader>a` | Agent list |
| `agent_cycle` | `tab` | Cycle Agent |
| `agent_cycle_reverse` | `shift+tab` | Cycle Agent (reverse) |
| `command_list` | `ctrl+p` | Command palette |

### Input Area Basics

| Key Name | Default | Description |
|----------|---------|-------------|
| `input_submit` | `return` | Send message |
| `input_newline` | `shift+return,ctrl+return,alt+return,ctrl+j` | New line |
| `input_clear` | `ctrl+c` | Clear input |
| `input_paste` | `ctrl+v` | Paste |
| `input_undo` | `ctrl+-,super+z` | Undo input |
| `input_redo` | `ctrl+.,super+shift+z` | Redo input |

### Input Area Cursor Movement

| Key Name | Default | Description |
|----------|---------|-------------|
| `input_move_left` | `left,ctrl+b` | Move left one character |
| `input_move_right` | `right,ctrl+f` | Move right one character |
| `input_move_up` | `up` | Move up one line |
| `input_move_down` | `down` | Move down one line |
| `input_word_forward` | `alt+f,alt+right,ctrl+right` | Move forward one word |
| `input_word_backward` | `alt+b,alt+left,ctrl+left` | Move backward one word |
| `input_line_home` | `ctrl+a` | Move to line start |
| `input_line_end` | `ctrl+e` | Move to line end |
| `input_visual_line_home` | `alt+a` | Move to visual line start |
| `input_visual_line_end` | `alt+e` | Move to visual line end |
| `input_buffer_home` | `home` | Move to buffer start |
| `input_buffer_end` | `end` | Move to buffer end |

### Input Area Selection

| Key Name | Default | Description |
|----------|---------|-------------|
| `input_select_left` | `shift+left` | Select left |
| `input_select_right` | `shift+right` | Select right |
| `input_select_up` | `shift+up` | Select up |
| `input_select_down` | `shift+down` | Select down |
| `input_select_word_forward` | `alt+shift+f,alt+shift+right` | Select next word |
| `input_select_word_backward` | `alt+shift+b,alt+shift+left` | Select previous word |
| `input_select_line_home` | `ctrl+shift+a` | Select to line start |
| `input_select_line_end` | `ctrl+shift+e` | Select to line end |
| `input_select_visual_line_home` | `alt+shift+a` | Select to visual line start |
| `input_select_visual_line_end` | `alt+shift+e` | Select to visual line end |
| `input_select_buffer_home` | `shift+home` | Select to buffer start |
| `input_select_buffer_end` | `shift+end` | Select to buffer end |

### Input Area Deletion

| Key Name | Default | Description |
|----------|---------|-------------|
| `input_backspace` | `backspace,shift+backspace` | Backspace |
| `input_delete` | `ctrl+d,delete,shift+delete` | Delete character |
| `input_delete_line` | `ctrl+shift+d` | Delete entire line |
| `input_delete_to_line_end` | `ctrl+k` | Delete to line end |
| `input_delete_to_line_start` | `ctrl+u` | Delete to line start |
| `input_delete_word_forward` | `alt+d,alt+delete,ctrl+delete` | Delete next word |
| `input_delete_word_backward` | `ctrl+w,ctrl+backspace,alt+backspace` | Delete previous word |

### History

| Key Name | Default | Description |
|----------|---------|-------------|
| `history_previous` | `up` | Previous history |
| `history_next` | `down` | Next history |

---

## Desktop Version Keybindings

OpenCode Desktop's input field supports Readline/Emacs style keybindings (built-in, not configurable):

| Keybinding | Function |
|------------|----------|
| `Ctrl+A` | Move to line start |
| `Ctrl+E` | Move to line end |
| `Ctrl+B` | Move back one character |
| `Ctrl+F` | Move forward one character |
| `Alt+B` | Move back one word |
| `Alt+F` | Move forward one word |
| `Ctrl+D` | Delete current character |
| `Ctrl+K` | Delete to line end |
| `Ctrl+U` | Delete to line start |
| `Ctrl+W` | Delete previous word |
| `Alt+D` | Delete next word |
| `Ctrl+T` | Transpose characters |
| `Ctrl+G` | Cancel popup / Interrupt response |

---

## Terminal Compatibility

### Shift+Enter Issue

Some terminals don't send the `Shift+Enter` modifier key by default.

**Symptom**: Pressing `Shift+Enter` sends the message instead of creating a new line.

### Windows Terminal Configuration

Edit `settings.json` (path: `%LOCALAPPDATA%\Packages\Microsoft.WindowsTerminal_8wekyb3d8bbwe\LocalState\settings.json`):

Add to the `actions` array:

```json
{
  "command": {
    "action": "sendInput",
    "input": "\u001b[13;2u"
  },
  "id": "User.sendInput.ShiftEnterCustom"
}
```

Add to the `keybindings` array:

```json
{
  "keys": "shift+enter",
  "id": "User.sendInput.ShiftEnterCustom"
}
```

Save and restart Windows Terminal.

### Other Terminals

- **iTerm2**: Supported by default, no configuration needed
- **Alacritty**: Supported by default
- **Kitty**: Supported by default
- **GNOME Terminal**: May need to update to a newer version

---

## Common Configuration Scenarios

### Vim Style

```jsonc
{
  "keybinds": {
    "leader": "space",
    "messages_page_up": "ctrl+u",
    "messages_page_down": "ctrl+d",
    "messages_first": "gg",
    "messages_last": "G"
  }
}
```

### Minimal Mode

Disable uncommon keybindings:

```jsonc
{
  "keybinds": {
    "sidebar_toggle": "none",
    "scrollbar_toggle": "none",
    "session_fork": "none",
    "session_share": "none",
    "session_unshare": "none",
    "tips_toggle": "none"
  }
}
```

### One-Handed Operation

Concentrate common operations on the left hand:

```jsonc
{
  "keybinds": {
    "session_new": "ctrl+n",
    "session_list": "ctrl+l",
    "model_list": "ctrl+m",
    "agent_cycle": "ctrl+tab"
  }
}
```

---

## Troubleshooting

| Symptom | Cause | Solution |
|---------|-------|----------|
| Keybinding not working | Terminal intercepted the key | Check terminal settings or use a different key |
| Shift+Enter doesn't create new line | Terminal doesn't send modifier key | Configure terminal (see above) |
| Configured but no response | Used `keybind` (singular) | Use `keybinds` (plural) |
| Using `null` to disable doesn't work | Syntax error | Use `"none"` string instead |
| Leader key conflict | Conflicts with other programs | Use a different Leader key like `ctrl+space` |
| Ctrl+C doesn't clear input | Intercepted by terminal's SIGINT | Use a different key or accept default behavior |

---

## Keybinding Mnemonic

```
Tab cycles Agent, Ctrl+C clears
Leader plus letter, any function appears
n for new, l for list, m for model
u for undo, r for redo, no need to huddle
Arrow keys left and right, child sessions take flight
```

---

## Lesson Summary

You learned:

1. Using the Leader key mechanism to avoid conflicts
2. Customizing keybindings in `keybinds`
3. Using `"none"` to disable unwanted keybindings
4. Using commas to bind multiple keys
5. Resolving terminal Shift+Enter compatibility issues

---

## Related Resources

- [Quick Reference/Keybindings Cheat Sheet](../appendix/keybinds) - Printable cheat sheet
- [5.6a Theme System](./06a-themes) - Appearance customization
- [5.1 Configuration Guide](./01a-config-basics) - Complete configuration reference
