---
title: "Alternative Installation Methods"
subtitle: "Other options beyond the official script"
course: "OpenCode Practical Course"
stage: "Stage 1"
lesson: "1.2a"
duration: "5 minutes"
level: "Beginner"
description: "Various ways to install OpenCode: npm, Homebrew, Chocolatey, Scoop, Docker, manual download, etc."
tags:
  - Installation
  - npm
  - Homebrew
  - Docker
prerequisite:
  - "1.2 Installation"
---

# Alternative Installation Methods

> The official `curl ... | bash` script doesn't work for you? Here are other options.

---

## When to Use This Page

- Official installation script times out
- You prefer package managers (npm, Homebrew, Scoop, etc.)
- Company computer has installation restrictions
- You want to try Docker without installing on your system

---

## macOS / Linux

### Homebrew (Recommended)

```bash
brew install anomalyco/tap/opencode
```

::: warning Note
The official Homebrew formula is `anomalyco/tap/opencode`. The community-maintained `brew install opencode` updates slowly and is not recommended.
:::

### npm / pnpm / bun / yarn

Requires Node.js 18+ (22+ recommended).

::: code-group

```bash [npm]
npm install -g opencode-ai
```

```bash [pnpm]
pnpm install -g opencode-ai
```

```bash [bun]
bun install -g opencode-ai
```

```bash [yarn]
yarn global add opencode-ai
```

:::

### Arch Linux

```bash
sudo pacman -S opencode    # Stable version (recommended)
paru -S opencode-bin       # AUR latest version
```

---

## Windows
<AdInArticle />

### Chocolatey

Run PowerShell as Administrator:

```powershell
choco install opencode
```

### Scoop (Recommended)

Run as regular user:

```powershell
scoop bucket add extras
scoop install extras/opencode
```

::: details Haven't installed Scoop?
Run the following commands **in order**:

```powershell
Set-ExecutionPolicy -ExecutionPolicy RemoteSigned -Scope CurrentUser
```

```powershell
Invoke-RestMethod -Uri https://get.scoop.sh | Invoke-Expression
```

```powershell
scoop install git
```

If your PowerShell is running as **Administrator**, use this instead when installing Scoop:

```powershell
iex "& {$(irm get.scoop.sh)} -RunAsAdmin"
```
:::

### npm

Requires Node.js 18+:

```powershell
npm install -g opencode-ai
```

### Mise

```powershell
mise use -g github:anomalyco/opencode
```

---

## Docker (Great for Trying Out)

Don't want to install on your system? Try with Docker:

```bash
docker run -it --rm ghcr.io/anomalyco/opencode
```

::: warning Limitation
OpenCode running in Docker can only access files inside the container by default. If you want it to read/write files on your computer, you need to mount a directory:

```bash
docker run -it --rm -v $(pwd):/workspace -w /workspace ghcr.io/anomalyco/opencode
```

Not very beginner-friendly. Recommend using the one-line script or package manager first.
:::

---

## Manual Download

Download the binary for your platform from [GitHub Releases](https://github.com/anomalyco/opencode/releases), extract it, and place it in a PATH directory.

---

## Installation Script Advanced Parameters

The official installation script `curl -fsSL https://opencode.ai/install | bash` supports these parameters:

```bash
# Install a specific version
curl -fsSL https://opencode.ai/install | bash -s -- --version 1.1.6

# Don't modify shell config (don't auto-add to PATH)
curl -fsSL https://opencode.ai/install | bash -s -- --no-modify-path

# Install from local binary
./install --binary /path/to/opencode
```

### Installation Location

The official script installs to `$HOME/.opencode/bin` by default. To install elsewhere, move the binary after installation:

```bash
# Move to /usr/local/bin after installation
sudo mv ~/.opencode/bin/opencode /usr/local/bin/opencode
```

---

## Installation Locations

| Method | Binary Location | Config Location |
|--------|-----------------|-----------------|
| Official Script | `~/.opencode/bin/opencode` | `~/.config/opencode/opencode.json` |
| npm/pnpm/bun/yarn | Global node_modules | Same as above |
| Homebrew | `/opt/homebrew/bin/opencode` or `/usr/local/bin/opencode` | Same as above |
| Scoop | `~/scoop/apps/opencode/current/opencode.exe` | Same as above |
| Chocolatey | `C:\ProgramData\chocolatey\bin\opencode.exe` | Same as above |

---

## Next Steps

After installation, go back to [1.2 Installation](/en/1-start/02-install) and follow the "Verify Installation" step to confirm `opencode --version` outputs correctly.

If you encounter issues, see [1.2b Troubleshooting Installation](/en/1-start/02b-install-troubleshoot)
