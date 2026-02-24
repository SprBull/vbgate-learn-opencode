---
title: "Keyboard Shortcuts Reference"
description: "Complete reference for all OpenCode keyboard shortcuts"
---

# Keyboard Shortcuts Reference

> Print this page and stick it next to your monitor - muscle memory in three days

---

## Leader Key

OpenCode uses a **Leader Key** to avoid conflicts with terminal shortcuts.

Default Leader Key: `Ctrl+X`

Usage: Press `Ctrl+X`, release, then press the second key.

---

## TUI Shortcuts

### Basic Operations

| Shortcut | Action | Description |
|----------|--------|-------------|
| `Enter` | Send message | Send current input |
| `Shift+Enter` | New line | Add newline in input box |
| `Tab` | Switch Agent | Cycle through primary agents |
| `Shift+Tab` | Reverse switch | Reverse cycle through primary agents |
| `Escape` | Interrupt | Stop current AI response |
| `Ctrl+C` | Clear input | Clear input box content |
| `Ctrl+D` | Exit | Close OpenCode |
| `Ctrl+P` | Command list | Open command palette |

### Leader Key Operations

| Shortcut | Action | Description |
|----------|--------|-------------|
| `Leader` → `n` | New session | Same as /new |
| `Leader` → `l` | Session list | Same as /sessions |
| `Leader` → `m` | Model list | Same as /models |
| `Leader` → `a` | Agent list | Select Agent |
| `Leader` → `t` | Theme list | Same as /theme |
| `Leader` → `e` | Editor | Open external editor |
| `Leader` → `c` | Compact | Compact current session context |
| `Leader` → `u` | Undo | Undo last change |
| `Leader` → `r` | Redo | Redo last undo |
| `Leader` → `x` | Export | Export current session |
| `Leader` → `s` | Status | View status |
| `Leader` → `b` | Sidebar | Toggle sidebar display |
| `Leader` → `g` | Timeline | Session timeline |
| `Leader` → `y` | Copy | Copy message |
| `Leader` → `h` | Hide details | Toggle details display |
| `Leader` → `q` | Quit | Close OpenCode |

### Session Navigation

| Shortcut | Action | Description |
|----------|--------|-------------|
| `Leader` → `→` | Child session | Switch to child Agent session |
| `Leader` → `←` | Reverse child | Reverse cycle child sessions |
| `Leader` → `↑` | Parent session | Return to parent session |

### Message Scrolling

| Shortcut | Action |
|----------|--------|
| `Page Up` | Scroll up one page |
| `Page Down` | Scroll down one page |
| `Ctrl+Alt+U` | Scroll up half page |
| `Ctrl+Alt+D` | Scroll down half page |
| `Ctrl+G` / `Home` | Jump to top |
| `Ctrl+Alt+G` / `End` | Jump to bottom |

### Input Area Operations

| Shortcut | Action |
|----------|--------|
| `Ctrl+A` | Move cursor to line start |
| `Ctrl+E` | Move cursor to line end |
| `Ctrl+B` | Move cursor back one character |
| `Ctrl+F` | Move cursor forward one character |
| `Alt+B` | Move cursor back one word |
| `Alt+F` | Move cursor forward one word |
| `Ctrl+K` | Delete to end of line |
| `Ctrl+U` | Delete to start of line |
| `Ctrl+W` | Delete previous word |
| `Alt+D` | Delete next word |
| `Ctrl+D` | Delete current character |
| `↑` / `↓` | Browse input history |

### Model Switching

| Shortcut | Action |
|----------|--------|
| `F2` | Cycle recent models |
| `Shift+F2` | Reverse cycle |
| `Ctrl+T` | Cycle variants |

### Permission Confirmation

| Shortcut | Action |
|----------|--------|
| `y` | Allow |
| `n` | Deny |
| `a` | Always allow (this session) |

---

## IDE Extension Shortcuts

<AdInArticle />

### VS Code / Cursor

| Shortcut (macOS) | Shortcut (Win/Linux) | Action |
|------------------|----------------------|--------|
| `Cmd+Esc` | `Ctrl+Esc` | Open OpenCode panel |
| `Cmd+Shift+Esc` | `Ctrl+Shift+Esc` | New session |
| `Cmd+Option+K` | `Alt+Ctrl+K` | Insert file reference |

---

## Desktop Input Shortcuts

OpenCode desktop app input box supports Readline/Emacs style shortcuts. These are built-in and cannot be configured via `opencode.json`:

| Shortcut | Action |
|----------|--------|
| `Ctrl+A` | Move to line start |
| `Ctrl+E` | Move to line end |
| `Ctrl+B` | Move cursor back one character |
| `Ctrl+F` | Move cursor forward one character |
| `Alt+B` | Move cursor back one word |
| `Alt+F` | Move cursor forward one word |
| `Ctrl+D` | Delete character under cursor |
| `Ctrl+K` | Delete to end of line |
| `Ctrl+U` | Delete to start of line |
| `Ctrl+W` | Delete previous word |
| `Alt+D` | Delete next word |
| `Ctrl+T` | Transpose characters |
| `Ctrl+G` | Cancel popup / interrupt response |

---

## Custom Shortcuts

Configure in `opencode.json`:

```json
{
  "$schema": "https://opencode.ai/config.json",
  "keybinds": {
    "leader": "ctrl+x",
    "session_new": "<leader>n",
    "session_list": "<leader>l",
    "model_list": "<leader>m"
  }
}
```

### Disable Shortcuts

Set to `"none"` to disable:

```json
{
  "keybinds": {
    "session_compact": "none"
  }
}
```

### Multiple Key Bindings

Separate multiple keys with commas:

```json
{
  "keybinds": {
    "app_exit": "ctrl+c,ctrl+d,<leader>q"
  }
}
```

---

## All Configurable Key Bindings

> Source: [keybinds.mdx](https://github.com/anomalyco/opencode/blob/dev/packages/web/src/content/docs/keybinds.mdx)

### Basic Bindings

| Key Name | Default | Description |
|----------|---------|-------------|
| `leader` | `ctrl+x` | Leader key |
| `app_exit` | `ctrl+c,ctrl+d,<leader>q` | Exit |

### Session Management

| Key Name | Default | Description |
|----------|---------|-------------|
| `session_new` | `<leader>n` | New session |
| `session_list` | `<leader>l` | Session list |
| `session_export` | `<leader>x` | Export session |
| `session_interrupt` | `escape` | Interrupt response |
| `session_compact` | `<leader>c` | Compact context |
| `session_timeline` | `<leader>g` | Timeline |
| `session_child_cycle` | `<leader>right` | Cycle child sessions |
| `session_child_cycle_reverse` | `<leader>left` | Reverse cycle child sessions |
| `session_parent` | `<leader>up` | Return to parent session |
| `session_fork` | `none` | Fork session |
| `session_rename` | `ctrl+r` | Rename session |
| `session_delete` | `ctrl+d` | Delete session |
| `session_share` | `none` | Share session |
| `session_unshare` | `none` | Unshare session |

### Model & Agent

| Key Name | Default | Description |
|----------|---------|-------------|
| `model_list` | `<leader>m` | Model list |
| `model_cycle_recent` | `f2` | Cycle recent models |
| `model_cycle_recent_reverse` | `shift+f2` | Reverse cycle recent models |
| `model_cycle_favorite` | `none` | Cycle favorite models |
| `model_cycle_favorite_reverse` | `none` | Reverse cycle favorite models |
| `variant_cycle` | `ctrl+t` | Cycle model variants |
| `agent_list` | `<leader>a` | Agent list |
| `agent_cycle` | `tab` | Cycle agents |
| `agent_cycle_reverse` | `shift+tab` | Reverse cycle agents |

### Interface Control

| Key Name | Default | Description |
|----------|---------|-------------|
| `theme_list` | `<leader>t` | Theme list |
| `editor_open` | `<leader>e` | Open editor |
| `sidebar_toggle` | `<leader>b` | Toggle sidebar |
| `scrollbar_toggle` | `none` | Toggle scrollbar |
| `username_toggle` | `none` | Toggle username display |
| `status_view` | `<leader>s` | Status view |
| `tool_details` | `none` | Tool details |
| `command_list` | `ctrl+p` | Command palette |
| `tips_toggle` | `<leader>h` | Toggle tips display |

### Message Operations

| Key Name | Default | Description |
|----------|---------|-------------|
| `messages_undo` | `<leader>u` | Undo |
| `messages_redo` | `<leader>r` | Redo |
| `messages_copy` | `<leader>y` | Copy |
| `messages_toggle_conceal` | `<leader>h` | Toggle detail hiding |
| `messages_next` | `none` | Next message |
| `messages_previous` | `none` | Previous message |
| `messages_last_user` | `none` | Jump to last user message |
| `messages_page_up` | `pageup,ctrl+alt+b` | Page up |
| `messages_page_down` | `pagedown,ctrl+alt+f` | Page down |
| `messages_half_page_up` | `ctrl+alt+u` | Half page up |
| `messages_half_page_down` | `ctrl+alt+d` | Half page down |
| `messages_first` | `ctrl+g,home` | Jump to top |
| `messages_last` | `ctrl+alt+g,end` | Jump to bottom |

### Input Box Operations

| Key Name | Default | Description |
|----------|---------|-------------|
| `input_submit` | `return` | Submit |
| `input_newline` | `shift+return,ctrl+return,alt+return,ctrl+j` | New line |
| `input_clear` | `ctrl+c` | Clear input |
| `input_paste` | `ctrl+v` | Paste |
| `input_move_left` | `left,ctrl+b` | Move cursor left |
| `input_move_right` | `right,ctrl+f` | Move cursor right |
| `input_move_up` | `up` | Move cursor up |
| `input_move_down` | `down` | Move cursor down |
| `input_select_left` | `shift+left` | Select left |
| `input_select_right` | `shift+right` | Select right |
| `input_select_up` | `shift+up` | Select up |
| `input_select_down` | `shift+down` | Select down |
| `input_line_home` | `ctrl+a` | Line start |
| `input_line_end` | `ctrl+e` | Line end |
| `input_select_line_home` | `ctrl+shift+a` | Select to line start |
| `input_select_line_end` | `ctrl+shift+e` | Select to line end |
| `input_visual_line_home` | `alt+a` | Visual line start |
| `input_visual_line_end` | `alt+e` | Visual line end |
| `input_select_visual_line_home` | `alt+shift+a` | Select to visual line start |
| `input_select_visual_line_end` | `alt+shift+e` | Select to visual line end |
| `input_buffer_home` | `home` | Buffer start |
| `input_buffer_end` | `end` | Buffer end |
| `input_select_buffer_home` | `shift+home` | Select to buffer start |
| `input_select_buffer_end` | `shift+end` | Select to buffer end |
| `input_delete_line` | `ctrl+shift+d` | Delete line |
| `input_delete_to_line_end` | `ctrl+k` | Delete to line end |
| `input_delete_to_line_start` | `ctrl+u` | Delete to line start |
| `input_backspace` | `backspace,shift+backspace` | Backspace |
| `input_delete` | `ctrl+d,delete,shift+delete` | Delete |
| `input_undo` | `ctrl+-,super+z` | Undo input |
| `input_redo` | `ctrl+.,super+shift+z` | Redo input |
| `input_word_forward` | `alt+f,alt+right,ctrl+right` | Next word |
| `input_word_backward` | `alt+b,alt+left,ctrl+left` | Previous word |
| `input_select_word_forward` | `alt+shift+f,alt+shift+right` | Select next word |
| `input_select_word_backward` | `alt+shift+b,alt+shift+left` | Select previous word |
| `input_delete_word_forward` | `alt+d,alt+delete,ctrl+delete` | Delete next word |
| `input_delete_word_backward` | `ctrl+w,ctrl+backspace,alt+backspace` | Delete previous word |

### History & Terminal

| Key Name | Default | Description |
|----------|---------|-------------|
| `history_previous` | `up` | Previous history |
| `history_next` | `down` | Next history |
| `terminal_suspend` | `ctrl+z` | Suspend terminal |
| `terminal_title_toggle` | `none` | Toggle terminal title |

---

## Shift+Enter Configuration

Some terminals don't send `Shift+Enter` by default.

### Windows Terminal Configuration

Edit `settings.json`:

```json
{
  "actions": [
    {
      "command": {
        "action": "sendInput",
        "input": "\u001b[13;2u"
      },
      "id": "User.sendInput.ShiftEnterCustom"
    }
  ],
  "keybindings": [
    {
      "keys": "shift+enter",
      "id": "User.sendInput.ShiftEnterCustom"
    }
  ]
}
```

---

## Quick Mnemonic

```
Tab switches Agents, Ctrl+C clears
Leader plus letters, functions appear
n for new, l for list, m for models
u for undo, r for redo, no worries
Arrow keys left and right, child sessions go back and forth
```

---

## Related Resources

- [Configuration Reference](/en/appendix/config-ref) - Complete configuration guide
- [5.6b Keybinds](/en/5-advanced/06b-keybinds) - Keybind customization tutorial
- [5.6a Themes](/en/5-advanced/06a-themes) - Theme customization tutorial
