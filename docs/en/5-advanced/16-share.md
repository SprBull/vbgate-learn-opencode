---
title: "5.16 Session Sharing"
subtitle: "Create public conversation links"
course: "OpenCode Practical Course"
stage: "Stage 5"
lesson: "5.16"
duration: "10 minutes"
level: "Advanced"
description: "Create public links for OpenCode conversations to facilitate team collaboration and getting help."
tags:
  - "Sharing"
  - "Collaboration"
prerequisite:
  - "5.1 Configuration Guide"
---

# Session Sharing

## 📝 Course Notes

Key takeaways from this lesson:

<img src="/images/5-advanced/share-notes.mini.jpeg" 
     alt="5.16 Session Sharing Notes" 
     data-zoom-src="/images/5-advanced/share-notes.jpeg" />

OpenCode's sharing feature allows you to create public links to conversations, making it easy to collaborate with your team or get help.

> Shared conversations are publicly accessible to anyone with the link.

## How It Works

When sharing a conversation, OpenCode:

1. Creates a unique public URL for the session
2. Syncs the conversation history to the server
3. Makes the conversation accessible via a shareable link: `opncd.ai/s/<share-id>`

## Sharing Modes

OpenCode supports three sharing modes:

### Manual Mode (Default)

Manual sharing mode is used by default. Sessions are not automatically shared, but you can use the `/share` command to share manually:

```
/share
```

This generates a unique URL and copies it to your clipboard.

To explicitly set manual mode in your configuration:

```json
{
  "$schema": "https://opncd.ai/config.json",
  "share": "manual"
}
```

### Auto Sharing

Enable automatic sharing for all new conversations by setting `share` to `"auto"` in your configuration:

```json
{
  "$schema": "https://opncd.ai/config.json",
  "share": "auto"
}
```

With auto sharing enabled, every new conversation is automatically shared and generates a link.

### Disable Sharing

Completely disable sharing by setting `share` to `"disabled"`:

```json
{
  "$schema": "https://opncd.ai/config.json",
  "share": "disabled"
}
```

To enforce this setting across your team, add it to your project's `opencode.json` and commit it to Git.

## Unshare

To stop sharing a conversation and remove it from public access:

```
/unshare
```

This removes the share link and deletes the data associated with the conversation.

## Privacy Considerations

When sharing conversations, keep in mind:

### Data Retention

Shared conversations remain accessible until you explicitly unshare them, including:

- Complete conversation history
- All messages and responses
- Session metadata

### Recommendations

- Only share conversations without sensitive information
- Review conversation content before sharing
- Unshare after collaboration is complete
- Avoid sharing conversations with proprietary code or confidential data
- Disable sharing entirely for sensitive projects

## Enterprise Edition

For enterprise deployments, the sharing feature can be:

- **Completely disabled** for security compliance
- **Restricted** to only SSO-authenticated users
- **Self-hosted** on your own infrastructure

Learn more about [Enterprise Edition](/en/5-advanced/11-enterprise.md).
