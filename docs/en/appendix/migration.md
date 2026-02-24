---
title: "Migration Guide"
description: "Complete guide for migrating from OpenCode 0.x to 1.0"
---

# Migration Guide

> 💡 **If your OpenCode version is 1.0 or above, you don't need to read this.**

Smooth upgrade from OpenCode 0.x to 1.0

---

## Version Overview

OpenCode 1.0 is a complete rewrite of the TUI.

Migrated from a Go + Bubbletea based TUI to an internal framework OpenTUI (Zig + SolidJS), resolving performance and functionality issues.

The new TUI works the same way as the old version because it connects to the same OpenCode server.

---

## Upgrade Methods

### Automatic Upgrade

```bash
# Upgrade to 1.0
opencode upgrade 1.0.0

# Downgrade back to 0.x
opencode upgrade 0.15.31
```

### Manual Upgrade

```bash
# npm
npm install -g opencode-ai

# Homebrew
brew upgrade opencode

# Scoop
scoop update opencode
```

> Note: If you are using an older version, it may not automatically upgrade to 1.0. Some older versions will automatically fetch the latest version.

---

## UX Changes
<AdInArticle />

1. **More compact session history** - Only shows full details for edit and bash tools

2. **New command bar** - Press `Ctrl+P` to invoke in any context, view all available actions

3. **New session sidebar** - Toggleable display, contains useful information

4. **Some features removed** - Removed some features that were uncertain if anyone was using. If important features are missing, please submit an Issue

---

## Breaking Changes

### Keybinding Renames

| Old Name | New Name |
|----------|----------|
| `messages_revert` | `messages_undo` |
| `switch_agent` | `agent_cycle` |
| `switch_agent_reverse` | `agent_cycle_reverse` |
| `switch_mode` | `agent_cycle` |
| `switch_mode_reverse` | `agent_cycle_reverse` |

### Keybinding Removals

The following keybindings have been removed:

- `messages_layout_toggle`
- `messages_next`
- `messages_previous`
- `file_diff_toggle`
- `file_search`
- `file_close`
- `file_list`
- `app_help`
- `project_init`
- `tool_details`
- `thinking_blocks`

If your configuration uses these keybindings, you need to remove them.

---

## Migration Checklist

### Before Upgrade

- [ ] Backup current configuration files
- [ ] Record current models and settings in use
- [ ] Export important session records

### During Upgrade

- [ ] Run `opencode upgrade 1.0.0`
- [ ] Check keybinding configuration, remove deprecated bindings
- [ ] Update renamed keybindings

### After Upgrade

- [ ] Verify `opencode --version` shows 1.x
- [ ] Test model connection `/models`
- [ ] Test basic conversation functionality
- [ ] Verify custom Agents and Skills
- [ ] Familiarize with new command bar (Ctrl+P)

---

## Rollback Plan

If you encounter issues and need to rollback:

```bash
# Downgrade to 0.x
opencode upgrade 0.15.31
```

---

## Getting Help

- [Troubleshooting](/en/appendix/troubleshoot) - Troubleshooting guide
- [GitHub Issues](https://github.com/anomalyco/opencode/issues) - Report issues

---

## Related Resources

- [CLI Command Reference](/en/appendix/cli) - 1.0 command details
- [Keybinding Reference](/en/appendix/keybinds) - Keyboard shortcut configuration
- [Changelog](https://github.com/anomalyco/opencode/releases) - Version history
