---
title: 连接 GitHub Copilot
subtitle: 复用已有订阅
course: OpenCode 中文实战课
stage: 第一阶段
lesson: "1.4j"
duration: 10 分钟
practice: 5 分钟
level: 新手
description: 如果你已有 GitHub Copilot 订阅，可以在 OpenCode 中复用，无需额外购买 API。
tags:
  - 模型
  - GitHub
  - Copilot
  - OAuth
prerequisite:
  - 1.2 安装
---

# 连接 GitHub Copilot

> 预计时间：5-10 分钟

如果你**已经订阅了 GitHub Copilot**（个人版 $10/月或企业版），可以在 OpenCode 中复用这个订阅来调用 GPT-4o、Claude 等模型，无需额外购买 API。

::: tip 适合谁？
- 已有 GitHub Copilot 订阅的用户
- 不想单独购买 OpenAI/Anthropic API 的用户
- 想在终端里复用 Copilot 模型的用户
:::

如果你没有 Copilot 订阅，建议跳过这篇，去看其他连接教程。

---

## 学完你能做什么

- 在 OpenCode 中连接 GitHub Copilot
- 使用 Copilot 提供的模型（GPT-4o、Claude 等）
- 发送第一句话并收到回复

---

## 🎒 开始前的准备

- [ ] 完成了 [1.2 安装](./02-install)，能运行 `opencode`
- [ ] **已有 GitHub Copilot 订阅**（个人版或企业版）
- [ ] 能访问 `github.com`

---

## 跟我做

### 第 1 步：确认你的 Copilot 订阅

访问 GitHub 设置页面确认：

https://github.com/settings/copilot

你应该能看到类似这样的状态：

```
GitHub Copilot
Status: Active
```

如果显示未订阅，需要先订阅 GitHub Copilot 才能继续。

---

### 第 2 步：在 OpenCode 中启动连接

启动 OpenCode：

```bash
opencode
```

在输入框输入：

```
/connect
```

在提供商列表中搜索 `GitHub Copilot`，选择它。

---

### 第 3 步：完成 OAuth 授权

选择 GitHub Copilot 后，OpenCode 会显示一个授权链接：

```
Please visit: https://github.com/login/device
And enter code: XXXX-XXXX
```

**操作步骤**：

1. 打开浏览器，访问 `https://github.com/login/device`
2. 输入屏幕上显示的设备码（如 `XXXX-XXXX`）
3. 点击「Authorize」授权 OpenCode

::: info 自动打开浏览器
如果你的终端支持，OpenCode 会自动打开浏览器。如果没有自动打开，手动复制链接即可。
:::

授权成功后，OpenCode 会显示：

```
✓ Provider added successfully!
```

---

### 第 4 步：选择模型

连接成功后，输入：

```
/models
```

你会看到 GitHub Copilot 提供的模型：

| 模型 | 说明 |
|------|------|
| `gpt-4o` | 推荐，旗舰多模态模型 |
| `gpt-4o-mini` | 快速，低成本 |
| `claude-sonnet-4-5` | Claude 最新平衡版 |
| `claude-3-5-haiku` | Claude 快速版 |
| `o1` | 推理增强模型 |
| `o1-mini` | 快速推理 |

选择一个模型即可开始对话。

::: warning 部分模型需要 Pro+ 订阅
像 `o1`、`claude-sonnet-4-5` 等高级模型可能需要 GitHub Copilot Pro+ 订阅。如果你用的是普通订阅，可能只能用部分模型。
:::

---

### 第 5 步：发送第一句话（验证成功）

在输入框输入：

```
你好，请介绍一下你自己
```

能收到回复就说明连接成功。

---

## 检查点 ✅

- [ ] `/models` 里能看到 Copilot 提供的模型
- [ ] 发送消息能收到 AI 回复
- [ ] 没有报错（如 `unauthorized` / `subscription required`）

---

## 踩坑提醒

| 现象 | 原因 | 解决 |
|-----|------|------|
| `unauthorized` | OAuth 授权失败或过期 | 重新运行 `/connect` 选择 GitHub Copilot |
| `subscription required` | 没有 Copilot 订阅 | 先订阅 GitHub Copilot |
| 找不到某个模型 | 订阅等级不够 | 升级到 Pro+ 或换用其他模型 |
| 授权页面显示错误 | 设备码过期 | 重新运行 `/connect`，在 5 分钟内完成授权 |
| 提示 `reauthenticate` | Token 过期 | 重新授权 |

---

## 重新授权

如果 Token 过期或授权出问题，可以用以下方式重新认证：

**方式一：TUI 内重新连接**

```
/connect
```

选择 GitHub Copilot，按提示重新授权。

**方式二：终端命令**

```bash
opencode auth login
# 选择 GitHub Copilot
```

---

## 下一步

- 回到 [1.4 总览](./04-connect) 选择下一条路线，或进入 [2.1 界面与基础操作](../2-daily/01-interface)

::: tip 遇到问题？
配置过程中卡住了？[加入社群](/community)，和 2000+ 同路人一起交流，实时答疑。
:::
