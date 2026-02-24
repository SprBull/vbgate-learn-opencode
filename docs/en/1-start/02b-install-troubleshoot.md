---
title: "Installation Failed?"
subtitle: "Installation Troubleshooting Guide"
course: "OpenCode Practical Course"
stage: "Phase 1"
lesson: "1.2b"
duration: "10 minutes"
level: "Beginner"
description: "Solutions to common OpenCode installation issues: command not found, network timeout, permission denied, PATH configuration, etc."
tags:
  - "Installation"
  - "Troubleshooting"
  - "Debugging"
prerequisite:
  - "1.2 Installation"
---

# Installation Failed?

> Encountering issues during installation? Here's a systematic troubleshooting guide.

---

## Issue 1: `command not found` / `'opencode' is not recognized`

**Symptoms:**

```bash
zsh: command not found: opencode
# Or on Windows
'opencode' is not recognized as an internal or external command
```

**Troubleshooting Steps:**

### 1. Confirm You Restarted the Terminal

Did you really close and reopen the window? Not just open a new tab—close the entire window.

### 2. Check Where OpenCode Was Installed

**macOS/Linux (official script installation):**

```bash
ls -la ~/.opencode/bin/opencode
```

If the file exists, the installation succeeded—it's just a PATH issue.

**Check if PATH includes the installation directory:**

```bash
echo $PATH | tr ':' '\n' | grep opencode
```

If there's no output, the PATH isn't configured correctly.

### 3. Manually Add to PATH

**macOS/Linux (zsh):**

```bash
echo 'export PATH="$HOME/.opencode/bin:$PATH"' >> ~/.zshrc
source ~/.zshrc
```

**macOS/Linux (bash):**

```bash
echo 'export PATH="$HOME/.opencode/bin:$PATH"' >> ~/.bashrc
source ~/.bashrc
```

**Windows (Scoop installation):**

Scoop automatically configures PATH. If it's not working, restart PowerShell.

---

## Issue 2: Network Error / Download Timeout

<AdInArticle />

**Symptoms:**

```
curl: (7) Failed to connect to opencode.ai port 443
# Or
Error: connect ETIMEDOUT
```

**Troubleshooting Steps:**

### 1. Confirm Network Is Working

```bash
curl -I https://www.google.com
```

If Google is also unreachable, it's a network issue, not an OpenCode issue.

### 2. Check If You Need a Proxy

If you're on a corporate/school network, you may need to configure a proxy. See [1.3 Network Configuration](./03-network).

### 3. Try Alternative Installation Methods

The official script downloads from GitHub. If GitHub access is slow, try:

- **npm installation** (npm has mirrors available):
  ```bash
  npm install -g opencode-ai
  ```

- **Homebrew installation** (brew has mirrors available):
  ```bash
  brew install anomalyco/tap/opencode
  ```

For more installation methods, see [1.2a Alternative Installation Methods](./02a-install-alternatives).

---

## Issue 3: GitHub API Rate Limiting

**Symptoms:**

```
error: rate limit exceeded
```

**Cause:**

GitHub API has rate limits for anonymous requests (60 requests/hour).

**Solutions:**

1. Wait an hour and retry
2. Or use alternative installation methods (npm, Homebrew, etc.)

---

## Issue 4: Installation Script Reports Missing Tools

**Symptoms:**

```
Error: 'tar' is required but not installed.
# Or
Error: 'unzip' is required but not installed.
```

**Solution:**

Install the missing tools:

```bash
# macOS (usually pre-installed)
# If not, install Xcode Command Line Tools:
xcode-select --install

# Ubuntu/Debian
sudo apt install -y tar unzip

# CentOS/RHEL
sudo yum install -y tar unzip
```

---

## Issue 5: Windows Execution Policy Restriction

**Symptoms (when installing Scoop):**

```
Running scripts is disabled on this system
```

**Solution:**

Run the following command (only needed once):

```powershell
Set-ExecutionPolicy -ExecutionPolicy RemoteSigned -Scope CurrentUser
```

If corporate policy doesn't allow changing the execution policy, you can use Chocolatey (requires admin rights) or download the binary directly.

---

## Issue 6: Finding the Binary Location

```bash
# macOS/Linux
which opencode

# Windows PowerShell
Get-Command opencode | Select-Object Source
```

---

## Issue 7: macOS Desktop App Won't Launch

**Symptoms:**

Double-clicking OpenCode.app shows no response, or a dialog appears saying "cannot be opened because it cannot verify the developer."

**Cause:**

This typically happens when:
- The installation package was downloaded from unofficial sources (e.g., third-party websites)
- A self-compiled development version
- Incomplete download due to network issues

Official desktop releases are signed and notarized by Apple and normally won't trigger this issue. If you downloaded from official sources but still encounter blocking, use this command to resolve:

```bash
xattr -cr /Applications/OpenCode.app
```

Then double-click to open again.

::: tip Note
This command clears the app's quarantine flag, telling macOS you trust this application. You only need to run it once.
:::

---

## Issue 8: Clean Uninstall and Reinstall

OpenCode provides an uninstall command:

```bash
opencode uninstall
```

It will prompt you about what to delete (configuration, data, cache, etc.).

If the `opencode` command doesn't work at all, you can manually delete:

**macOS/Linux (official script installation):**

```bash
# Delete binary
rm -rf ~/.opencode/bin

# Delete configuration
rm -rf ~/.config/opencode

# Delete data, cache, and state
rm -rf ~/.local/share/opencode
rm -rf ~/.cache/opencode
rm -rf ~/.local/state/opencode
```

**Homebrew installation:**

```bash
brew uninstall opencode
```

**npm/pnpm/Yarn installation:**

```bash
# npm
npm uninstall -g opencode-ai

# pnpm
pnpm uninstall -g opencode-ai

# Yarn
yarn global remove opencode-ai
```

**Scoop installation:**

```powershell
scoop uninstall opencode
```

**Chocolatey installation:**

```powershell
choco uninstall opencode
```

---

## Still Can't Figure It Out?

1. Check the [Official Troubleshooting Documentation](https://opencode.ai/docs/troubleshooting/)
2. Search or ask questions on [GitHub Issues](https://github.com/anomalyco/opencode/issues)

---

## Next Steps

After resolving the issue, go back to [1.2 Installation](./02-install) to verify the installation succeeded.

::: tip Still Stuck?
[Join the community](/en/community) and connect with 2000+ fellow learners for real-time Q&A.
:::
