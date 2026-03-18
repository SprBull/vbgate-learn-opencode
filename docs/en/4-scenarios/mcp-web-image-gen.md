---
title: "Automate Web-Based Image Generation with MCP: Jimeng and Gemini Practice"
subtitle: "AI Image Generation Automation, Save Locally"
course: "OpenCode Practical Course"
stage: "Stage 4"
lesson: "A5"
duration: "12 minutes"
practice: "15 minutes"
level: "Advanced"
description: "Learn to use Chrome DevTools MCP to automate Jimeng and Gemini web-based image generation tools, automatically generate images and save them locally."
tags:
  - MCP
  - Chrome
  - AI Image Generation
  - Automation
prerequisite:
  - "5.7c Chrome DevTools MCP"
---

# Automate Web-Based Image Generation with MCP

> 💡 **One-line summary**: Let AI control your browser to automatically generate and download images from Jimeng/Gemini.

---

## What You'll Be Able to Do

- Automatically open Jimeng/Gemini web interfaces with AI
- Enter prompts to generate images automatically
- Download images to a specified local directory
- Batch generate and download images without manual operation

---

## Your Current Struggles

- Want to batch generate images, but web interfaces require clicking each one individually
- Downloading images requires manual right-click and "Save As", which is inefficient
- API versions either lack quotas or require payment
- You have existing web tools but can't automate them

---

## When to Use This Approach

- When you need: Batch generate images, but don't want to operate manually
- And don't want: Integrate separate APIs for each AI image generation tool
- Especially: You're already using the web version and just want to make it more automated

---

## Core Concept

```
┌─────────────────────────────────────────────────────────────┐
│                    Web Image Generation Automation Flow       │
├─────────────────────────────────────────────────────────────┤
│                                                             │
│  ┌─────────┐    ┌─────────────┐    ┌─────────────┐         │
│  │ Open Web│ →  │ Enter Prompt│ →  │ Wait Gen.   │         │
│  └─────────┘    └─────────────┘    └─────────────┘         │
│                                          │                  │
│                                          ▼                  │
│  ┌─────────────┐    ┌─────────────┐    ┌─────────────┐     │
│  │ Save Local  │ ←  │ Click DL    │ ←  │ Locate Img  │     │
│  └─────────────┘    └─────────────┘    └─────────────┘     │
│                                                             │
└─────────────────────────────────────────────────────────────┘
```

Key points:
1. **MCP takes over browser** — No API needed, operate web page directly
2. **Wait for generation to complete** — Use `wait_for` to wait for specific text to appear
3. **Auto-download** — Click download button, browser automatically saves

---

## 🎒 Before You Start

> Make sure you've completed the following:

- [ ] Completed [5.7c Chrome DevTools MCP](/en/5-advanced/07c-mcp-chrome-devtools)
- [ ] Chrome browser has remote debugging enabled
- [ ] Have a Jimeng account (https://jimeng.jianying.com)
- [ ] Have a Gemini account (https://gemini.google.com)

---

## Scenario 1: Jimeng AI Image Generation

### Step 1: Open Jimeng Page

**Why**
Let MCP open a new page and automatically navigate to Jimeng's image generation page.

Tell AI directly:

```
Open Jimeng AI, the URL is https://jimeng.jianying.com
```

AI will call `chrome-devtools_new_page` tool to open the page.

**You should see**: Browser opens a new tab showing Jimeng homepage.

### Step 2: Enter Image Generation Mode

**Why**
Jimeng has multiple features (video, image, digital human, etc.), need to enter the image generation module.

AI will:
1. Take a page snapshot (`take_snapshot`)
2. Find the "Image Generation" (图片生成) button
3. Click to enter

**You should see**: Page jumps to image generation interface with an input box.

### Step 3: Enter Prompt

**Why**
Tell AI what you want to generate.

```
Enter prompt: Epic duel between cosmic hero and eastern myth monkey king, movie-level special effects
```

AI will call `fill` tool to fill the text into the input box.

::: warning About Sensitive Words
Jimeng has content moderation. Writing "Ultraman" (奥特曼) or "Sun Wukong" (孙悟空) directly may be blocked.

Alternative descriptions:
- Ultraman → Cosmic hero, Giant of Light
- Sun Wukong → Eastern myth monkey king, Monkey King
:::

### Step 4: Click Generate and Wait

**Why**
Trigger generation, then wait for image to complete.

AI will:
1. Click generate button
2. Use `wait_for` to wait for "Download" (下载) or "Complete" (完成) text to appear

**Wait time**: Usually 30-60 seconds, depending on server load.

### Step 5: Download Image to Local

**Why**
Save the generated image to your computer.

AI will:
1. Click image to open preview
2. Find "Download" (下载) button
3. Click download

Image will be saved to browser's default download directory:
- macOS: `~/Downloads/` or `~/下载/`
- Windows: `C:\Users\YourUsername\Downloads\`
- Linux: `~/Downloads/` or `~/下载/`

### Jimeng Complete Example Dialogue

```
You: Open Jimeng, generate a "cyberpunk-style ancient city wall", download to desktop

AI:
1. Open https://jimeng.jianying.com/ai-tool/generate
2. Enter prompt
3. Click generate
4. Wait for completion (about 45 seconds)
5. Click download
6. Image saved to ~/Downloads/jimeng-xxx.png
```

### Jimeng Common Issues

| Issue | Cause | Solution |
|-------|-------|----------|
| Prompt blocked | Sensitive word filtering | Use alternative descriptions, e.g., "Cosmic hero" instead of "Ultraman" |
| Download no response | First download has watermark settings popup | AI will handle automatically, or manually click "Save Settings" once |
| Generation too slow | High server load | Wait patiently, can open multiple sessions simultaneously |

---

## Scenario 2: Gemini Image Generation

### Step 1: Open Gemini

```
Open Gemini, the URL is https://gemini.google.com/app
```

**You should see**: Gemini chat interface with an input box.

### Step 2: Enter Image Generation Prompt

```
Generate a red apple, realistic style, with glossy texture
```

Gemini will automatically recognize this as an image generation request and call its built-in image generation feature.

### Step 3: Wait for Generation to Complete

AI uses `wait_for` to wait for buttons like "Download" (下载) or "Copy" (复制) to appear.

**Wait time**: Usually 15-30 seconds.

### Step 4: Download Image

After Gemini generates images, there will be several buttons:
- Share image
- Copy image
- **Download full-size image** ← Click this

AI will click the download button, and the image saves to the download directory.

### Gemini Complete Example Dialogue

```
You: Open Gemini, generate a "seaside lighthouse at sunset", download locally

AI:
1. Open https://gemini.google.com/app
2. Enter: Generate a seaside lighthouse at sunset
3. Wait for generation (about 20 seconds)
4. Click "Download full-size image"
5. Image saved to ~/Downloads/
```

### Gemini vs Jimeng Comparison

| Comparison | Gemini | Jimeng |
|------------|--------|--------|
| Access | Requires VPN | Direct domestic access |
| Generation Speed | Faster (15-30 seconds) | Slower (30-60 seconds) |
| Content Moderation | Relatively lenient | Strict (sensitive word blocking) |
| Image Count | Usually 1 | Usually 4 |
| Download Method | Direct download | Need to handle watermark settings |

---

## Advanced: Batch Generation

### Batch Generate Multiple Images

```
Help me generate these 5 images, all download to the images folder on desktop:

1. Cyberpunk-style street
2. Ink wash style landscape
3. Cartoon-style cute cat
4. Realistic-style coffee cup
5. Abstract art style universe
```

AI will sequentially:
1. Open image generation website
2. Enter each prompt
3. Wait for generation
4. Download and save
5. Continue to next one

### Auto-Rename Downloaded Files

Downloaded filenames are usually random strings. You can ask AI to help rename:

```
Rename the just-downloaded image to cyberpunk-street.png
```

```bash
mv ~/Downloads/jimeng-2026-03-15-xxx.png ~/Desktop/images/cyberpunk-street.png
```

---

## Checkpoint ✅

- [ ] Jimeng can open normally and generate images
- [ ] Gemini can open normally and generate images
- [ ] Images can be successfully downloaded locally
- [ ] Know where the download directory is
- [ ] Know how to handle sensitive word blocking

---

## Common Pitfalls

| Symptom | Cause | Solution |
|---------|-------|----------|
| Page won't open | Network issue | Gemini needs VPN; Jimeng check account login status |
| Prompt blocked | Content moderation | Use alternative descriptions, avoid brand names/sensitive words |
| Can't find download directory | Different system language | Linux Chinese system is `~/下载/`, English is `~/Downloads/` |
| Image generation failed | Server busy | Wait and retry |
| MCP connection failed | Chrome remote debugging not enabled | Check `chrome://inspect/#remote-debugging` |

---

## Lesson Summary

You learned:

1. **Use MCP to operate web image generation tools** — No API needed, control browser directly
2. **Jimeng practice** — Handle sensitive words, wait for generation, download images
3. **Gemini practice** — Enter prompts, wait for generation, download images
4. **Batch generation** — Let AI complete multiple images in sequence

Core flow: **Open page → Enter prompt → Wait for generation → Download and save**

---

## Further Reading

Want to learn more about MCP automation? Recommended reading:

- **[5.7c Chrome DevTools MCP](/en/5-advanced/07c-mcp-chrome-devtools)** — Complete configuration and usage of MCP browser control
- **[C4 Automation Scripts](./office-automation)** — Use AI to write automation scripts for repetitive tasks
