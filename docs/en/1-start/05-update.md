---
title: "Auto-Update: You Don't Need to Worry About It"
subtitle: "OpenCode updates automatically by default, but if you want to know more..."
course: "OpenCode Practical Course"
stage: "Stage 1"
lesson: "1.5"
duration: "3 minutes"
practice: "2 minutes"
level: "Beginner"
description: "OpenCode automatically checks and downloads new versions on startup, enabled by default. This lesson teaches you manual updates and configuration options."
tags:
  - "Update"
  - "Upgrade"
  - "Maintenance"
prerequisite:
  - "1.2 Installation"
---

# Auto-Update: You Don't Need to Worry About It

## What You'll Learn

- Know that OpenCode updates automatically (default behavior)
- Manually update to the latest version when needed
- Understand how to disable/enable auto-update

---

## Your Current Pain Points

- Worried about bugs or security issues in old versions
- Seeing a new version prompt but don't know how to update
- Want to stay up-to-date but afraid updates might cause problems

---

## When to Use This

- **Default**: Don't worry about it, OpenCode will auto-update
- **Special cases**: Need manual update, specific version, or disable auto-update

---

## 🎒 Prerequisites

> Make sure you've completed the following:

- [x] OpenCode installed ([1.2 Installation](/en/1-start/02-install))

---

## Core Concepts

1. **Default behavior**: OpenCode automatically checks and downloads updates on startup
2. **Configuration control**: Can be controlled via the `autoupdate` option in config file
3. **Manual update**: `opencode upgrade` command

---

## Follow Along

### Important Note: You Can Skip This Lesson

**Why?**

OpenCode's default installation methods (`curl | bash` or `brew install`) already have **auto-update** configured. Every time it starts, it will:
1. Check for new versions in the background
2. Automatically download updates
3. Use the new version on next startup

**For you**: You don't need to do anything, it will stay up-to-date.

**When do you need this lesson?**
- You want to know more details (technical curiosity)
- You need to manually update to a specific version
- You want to disable auto-update

---

### Step 1: Manual Update (Optional)
<AdInArticle />

**When do you need a manual update?**

- Auto-update failed (network issues)
- You want to upgrade to the latest version immediately
- You want to upgrade to a specific version

**Upgrade to the latest version:**

```bash
opencode upgrade
```

**You'll see:**

```
┌  Upgrade
│
●  Using method: curl
●  From 1.1.5 → 1.1.6
◇  Upgrading...
│
└  Upgrade complete
```

**Upgrade to a specific version:**

```bash
opencode upgrade 1.1.5
```

Or with `v` prefix:

```bash
opencode upgrade v1.1.5
```

**Update using a specific installation method:**

```bash
opencode upgrade --method npm
```

Supported methods: `curl`, `npm`, `pnpm`, `bun`, `brew`

---

### Step 2: Configure Auto-Update (Optional)

Auto-update is controlled by the `autoupdate` field in the config file.

**Edit the config file:**

**macOS/Linux:**

```bash
# Open with your preferred editor
vim ~/.config/opencode/opencode.json
# or
code ~/.config/opencode/opencode.json
```

**Windows:**

```powershell
notepad $env:USERPROFILE\.config\opencode\opencode.json
```

**Configuration:**

```json
{
  "$schema": "https://opencode.ai/config.json",
  "autoupdate": false
}
```

Three possible values:
- `true`: Automatically download updates (default)
- `false`: Don't check for updates
- `"notify"`: Notify when new version is available, but don't auto-download

::: tip Environment Variable Method
You can also disable auto-update via environment variable:
```bash
export OPENCODE_DISABLE_AUTOUPDATE=true
```
:::

---

## Checklist ✅

> All items must pass to continue; if any fail, see "Troubleshooting" below

- [ ] Know that OpenCode auto-updates by default
- [ ] (Optional) Know the `opencode upgrade` command
- [ ] (Optional) Know how to configure `autoupdate`

---

## Troubleshooting

### Issue 1: Network Timeout, Download Failed

**Symptom:**

```
Error: connect ETIMEDOUT
```

**Cause:**
Network unreachable or GitHub connection timeout

**Solution:**
1. Check your network
2. Use a proxy (see [1.3 Network Configuration](/en/1-start/03-network))
3. Or temporarily disable auto-update, manually update when network is better

---

### Issue 2: Want to Downgrade to an Older Version

**Scenario:**
New version has bugs, want to rollback

**Solution:**

```bash
opencode upgrade 1.1.5
```

Downgrade and upgrade use the same command, just specify the older version number

---

### Issue 3: Manual Update Shows "rate limit exceeded"

**Symptom:**

```
error: rate limit exceeded
```

**Cause:**
GitHub API has request rate limits:
- Unauthenticated requests: 60/hour
- Authenticated requests: 2000+/hour

OpenCode's `opencode upgrade` calls GitHub API to check for the latest version. If called multiple times in a short period, it will trigger rate limit restrictions.

**Solutions (3 options):**

**Method 1: Wait about 1 hour and retry**

```bash
# GitHub API rate limit resets every hour
opencode upgrade
```

**Method 2: Manually specify version number (bypass API call)**

```bash
# Specify version directly, doesn't call latest() API
opencode upgrade 1.1.6
```

**Method 3: Use npm installation method (if you have Node.js)**

```bash
# npm registry has no rate limit
npm install -g opencode-ai@latest
```

::: tip How to Avoid This Issue
- Try to use OpenCode's auto-update feature, avoid frequent manual `opencode upgrade`
- Don't execute `opencode upgrade` command multiple times in a short period
:::

---

## Lesson Summary

You learned:

1. OpenCode auto-updates by default, most users don't need to worry about it
2. Use `opencode upgrade` for manual updates when needed
3. Can disable/enable auto-update via the `autoupdate` field in config file

---

## Next Lesson Preview

> Next we'll learn **[2.1 Interface & Basic Operations](/en/2-daily/01-interface.md)** and start actually using OpenCode.
>
> You'll learn:
> - Understanding the TUI interface
> - Using `@` to reference files
> - Using `!` to execute commands
> - Using `/` slash commands
