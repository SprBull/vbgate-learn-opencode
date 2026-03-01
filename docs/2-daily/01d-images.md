---
title: 2.1d 使用图片与 AI 对话
subtitle: 截图、粘贴、提问一气呵成
course: OpenCode 中文实战课
stage: 第二阶段
lesson: "2.1d"
duration: 18 分钟
practice: 10 分钟
level: 新手
description: 学会把截图和本地图片发给 AI，让 AI 看图说话、分析界面、提取文字。
tags:
  - 图片
  - 截图
  - 剪贴板
  - Linux
prerequisite:
  - 2.1c AI 的基础工具
---

# 2.1d 使用图片与 AI 对话

> 💡 **新手进阶**：截图发给 AI，让 bug 无处藏身

## 📝 课程笔记

本课核心知识点整理：

<img src="/images/2-daily/01d-images-notes.mini.jpeg" 
     alt="使用图片与 AI 对话学霸笔记" 
     data-zoom-src="/images/2-daily/01d-images-notes.jpeg" />

---

## 学完你能做什么

- 把屏幕截图直接粘贴给 AI 分析
- 引用本地图片文件让 AI 查看
- 在 Linux 上配置图片粘贴支持
- 知道哪些模型支持图片理解

---

## 你现在的困境

- 遇到报错想截图给 AI 看，不知道怎么发
- 想传设计稿让 AI 给建议，只能打字描述
- Linux 上按 Ctrl+V 粘贴图片没反应

---

## 什么时候用这一招

| 场景 | 例子 |
|------|------|
| 分析报错 | 截图错误弹窗，让 AI 给出解决方案 |
| 界面审查 | 传设计稿让 AI 提改进建议 |
| OCR 文字识别 | 截图 PDF 或网页，让 AI 提取文字 |
| 代码审查 | 截图代码片段，让 AI 解释或重构 |

---

## 🎒 开始前的准备

- [ ] 完成了 [2.1c AI 的基础工具](./01c-basic-tools)
- [ ] 使用支持图片输入的模型（如 GPT-5.2、Claude 4.6、Kimi K2.5 等）
- [ ] Linux 用户：确认是否安装了剪贴板工具（后续有检查方法）

::: warning 模型支持情况
不是所有模型都能看懂图片。

**国际模型**：GPT-5.2、Claude 4.6、Gemini 3.1 等支持图片
**国内模型**：只有 **Kimi K2.5** 支持图片，GLM-5、MiniMax 2.5、DeepSeek、豆包、通义千问等不支持

如果模型不支持，上传图片后会提示错误。
:::

---

## 核心思路

OpenCode 支持三种方式让 AI 看到图片：

1. **粘贴截图**（最常用）：截图后直接 Ctrl+V
2. **引用本地文件**：用 `@图片路径` 或粘贴文件路径
3. **AI 生成图片**：部分模型（如 Copilot）支持让 AI 画图

无论哪种方式，图片在输入框都会显示为 `[Image 1]`、`[Image 2]` 这样的虚拟标记。发送后，AI 就能看到并分析图片内容。

---

## 跟我做

### 第 0 步：各平台截图方法

不同系统的截图快捷键不同，先找到适合你的方式：

| 系统 | 区域截图 | 全屏截图 | 窗口截图 |
|------|---------|---------|---------|
| **Windows** | `Win + Shift + S` | `PrtScn` | `Alt + PrtScn` |
| **Mac** | `Cmd + Shift + 4` | `Cmd + Shift + 3` | `Cmd + Shift + 4` 然后按空格 |
| **Linux (GNOME)** | `PrtScn` 选区域 | `PrtScn` | `Alt + PrtScn` |
| **Linux (KDE)** | `Meta + Shift + S` | `PrtScn` | `Meta + PrtScn` |

::: tip 截图后去哪里了？
- **Windows**：截图后图片在剪贴板，屏幕右下角会出现预览
- **Mac**：截图默认保存到桌面，但按 `Ctrl + Cmd + Shift + 4` 可直接复制到剪贴板
- **Linux**：取决于桌面环境，通常直接复制到剪贴板或弹出保存对话框
:::

---

### 第 1 步：截图并粘贴

**操作**
1. 按上面表格的快捷键截图（推荐用区域截图，只框选需要的内容）
2. 回到 OpenCode 输入框
3. 按 `Ctrl+V`

**你应该看到**
- 输入框出现 `[Image 1]` 标记
- 标记前后可以输入文字描述

```
┌─────────────────────────────────────┐
│  请帮我分析这个报错 [Image 1]        │
└─────────────────────────────────────┘
```

**为什么**  
OpenCode 会自动检测剪贴板里的图片内容，并转换为 base64 格式发送给 AI。

---

### 第 2 步：Linux 用户安装剪贴板工具（如需要）

**什么时候需要这一步**  
如果你按 `Ctrl+V` 后**没有**出现 `[Image 1]`，且你使用的是 Linux，就需要安装剪贴板工具。

**为什么**  
Linux 的 X11/Wayland 图形协议需要额外工具才能读取剪贴板图片。

**操作**

先确认你的显示服务器类型：
```bash
echo $XDG_SESSION_TYPE
```

然后根据结果安装对应工具：

::: code-group

```bash [X11（显示 x11）]
sudo apt install xclip
# 或
sudo apt install xsel
```

```bash [Wayland（显示 wayland）]
sudo apt install wl-clipboard
```

:::

::: tip xsel 作为备选
如果 xclip 在你的系统上不可用，xsel 也可以作为 X11 的备选方案。
:::

安装后**重启 OpenCode**，再试一次 `Ctrl+V`。

**你应该看到**
- 安装完成后，`Ctrl+V` 粘贴图片正常工作
- 输入框出现 `[Image 1]` 标记

---

### 第 3 步：引用本地图片文件

**操作**
1. 在输入框输入 `@`
2. 选择图片文件路径，或直接输入路径
3. 回车确认

或者更简单：
1. 在文件管理器复制图片文件的完整路径
2. 在 OpenCode 输入框粘贴路径

**你应该看到**
- 输入框出现 `[Image 1]` 标记
- 和截图粘贴效果一样

---

### 第 4 步：发送并查看 AI 回复

**操作**
1. 在 `[Image 1]` 前后添加你的问题描述
2. 按 `Enter` 发送

**你应该看到**
- AI 会分析图片内容并给出回答
- 如果是报错截图，AI 会给出修复建议
- 如果是设计稿，AI 会给出改进意见

**示例对话**

```
用户：这个报错是什么意思？[Image 1]

AI：这个错误表示模块找不到。从截图看，问题出在...
```

---

### 第 5 步：删除已添加的图片

**操作**
- 在输入框用 `Backspace` 或 `Delete` 删除 `[Image 1]` 标记

**为什么**  
删除虚拟标记就等同于取消这张图片的发送。图片不会随消息发出。

---

## 检查点 ✅

- [ ] 截图后能成功粘贴到输入框（出现 `[Image 1]`）
- [ ] 引用本地图片文件成功
- [ ] AI 能正确识别并分析图片内容
- [ ] 知道怎么删除已添加的图片

---

## 🚑 故障排除：Ctrl+V 不能粘贴图片

按这个流程一步步排查：

### 第 1 关：确认图片真的在剪贴板

**测试方法**：
- 截图后，打开系统的文本编辑器（记事本/TextEdit）
- 按 `Ctrl+V`，如果能粘贴出文字说明截图工具复制的是文字描述
- **应该粘贴不出东西**，说明图片在剪贴板里

**如果粘贴出了文字**：说明你用的截图工具把图片存到了文件，只把文件名放进了剪贴板。改用系统自带的截图快捷键（见第 0 步表格）。

---

### 第 2 关：Linux 专用检查

**如果是 Linux 且粘贴没反应**：

```bash
# 1. 确认显示服务器类型
echo $XDG_SESSION_TYPE
# 输出应该是 x11 或 wayland

# 2. 检查是否安装了对应工具
# X11 用户：
which xclip
# 或
which xsel

# Wayland 用户：
which wl-paste
```

**如果显示命令没找到**：安装对应工具（见第 2 步）。

**如果已安装但还是不行**：
- 尝试手动读取剪贴板测试工具是否工作：
  ```bash
  # X11
  xclip -selection clipboard -t image/png -o > /tmp/test.png
  # 如果生成了 test.png 文件，说明工具正常

  # Wayland
  wl-paste -t image/png > /tmp/test.png
  ```

---

### 第 3 关：确认不是模型问题

**现象**：能粘贴出 `[Image 1]`，但 AI 说看不到图。

**原因**：你用的模型不支持图片输入。

**支持图片的模型**（截至 2026 年 3 月）：

| 提供商 | 支持图片的模型 |
|--------|---------------|
| OpenAI | GPT-5.2、GPT-5 |
| Anthropic | Claude Opus 4.6、Claude Sonnet 4.6 |
| Google | Gemini 3.1 Pro/Flash |
| 月之暗面 | **Kimi K2.5**（国内首推） |

::: warning 国内模型注意
- **Kimi K2.5**：✅ 支持图片
- **智谱 GLM-5、MiniMax 2.5、DeepSeek、豆包、通义千问**：❌ 不支持图片

如果你用国产模型，建议选择 **Kimi K2.5**。
:::

---

**特殊限制：Anthropic 图片尺寸**

Anthropic (Claude) 模型对图片尺寸有限制：
- **最大 2000 像素**（宽或高）
- 超过此限制会报错：`At least one of the image dimensions exceed max allowed size`

**解决**：截图时选择较小区域，或使用图片压缩工具。

---

**已知问题：Azure GPT-5.2-Codex**

Azure 上的 `gpt-5.2-codex` 模型目前有图片粘贴问题：
- 粘贴后会显示 `[Image 1]`，但发送时提示 "File not found: Image 1"
- 这是模型集成问题，与 OpenCode 无关

**解决**：切换到普通版 `GPT-5.2`（非 Codex）或其他支持图片的模型。

---

### 第 4 关：快捷键冲突检查

**现象**：按 `Ctrl+V` 输入框出现了 `^V` 或其他奇怪字符。

**原因**：终端模拟器或 SSH 客户端拦截了 `Ctrl+V`。

**解决**：
- **Windows Terminal**：设置 → 操作 → 确保 `Ctrl+V` 绑定的是「粘贴」
- **iTerm2 (Mac)**：Preferences → Keys → 检查 `Cmd+V` 绑定
- **JetBrains IDE Terminal (Mac)**：使用 `Ctrl+V` 而不是 `Cmd+V`
- **macOS 某些输入法**（如俄语、中文部分输入法）：切换到英文输入法再试
- **SSH 到远程服务器**：远程服务器也需要安装剪贴板工具，或者使用 OSC52 协议（自动回退）

---

### 第 5 关：终端多路复用器问题

**现象**：在 Zellij、tmux 或 screen 中，复制粘贴不正常。

**原因**：这些多路复用器会拦截 OSC52 剪贴板序列，导致无法与系统剪贴板交互。

**解决**：
- 暂时退出多路复用器，直接在普通终端中使用 OpenCode
- 或在多路复用器外部启动 OpenCode

**受影响的工具**：
- Zellij（已知问题）
- tmux（取决于配置）
- screen（取决于配置）

---

### 第 6 关：WSL 环境特殊问题

**现象**：在 WSL/WSL2 中，复制粘贴行为不一致。

**原因**：WSL 是 Windows 上的 Linux 子系统，剪贴板需要在 Windows 和 Linux 之间桥接。

**解决**：
- **粘贴图片**：WSL 支持图片粘贴，但如果失败，尝试在 Windows Terminal 中直接运行 OpenCode（而不是在 WSL 内）
- **复制内容**：WSL 中复制的文本可以正常粘贴到 Windows，但分享链接等功能可能需要额外配置
- **推荐**：如果主要工作环境是 Windows，建议直接安装 Windows 版 OpenCode

---

## 踩坑提醒

| 现象 | 原因 | 解决 |
|------|------|------|
| Ctrl+V 没反应 | Linux 缺少剪贴板工具 | 安装 `xclip` 或 `wl-clipboard` |
| 粘贴后出现 `^V` | 终端快捷键冲突 | 检查终端设置 |
| 粘贴后 AI 说看不到图 | 模型不支持图片输入 | 切换到 GPT-5.2、Claude 4.6、**Kimi K2.5** 等支持图片的模型 |
| `[Image 1]` 删不掉 | 在只读模式或输入框锁定 | 确保输入框处于编辑状态 |
| 图片太大发送失败 | **Anthropic 模型限制 2000 像素** | 压缩图片或截图时选较小区域 |
| Mac 截图后粘贴没图 | 截图保存到了桌面，没进剪贴板 | 用 `Ctrl + Cmd + Shift + 4` 区域截图 |
| JetBrains IDE 内粘贴失败 | IDE Terminal 快捷键处理不同 | 用 `Ctrl+V` 而不是 `Cmd+V`（Mac）|
| Zellij/tmux 中复制失败 | 多路复用器拦截 OSC52 序列 | 暂时退出多路复用器使用 |
| 某些输入法下粘贴失败 | macOS 输入法切换导致快捷键识别异常 | 切换到英文输入法再试 |
| WSL 中粘贴不稳定 | Windows/Linux 剪贴板桥接问题 | 直接在 Windows Terminal 中运行 OpenCode |

---

## 本课小结

你学会了：
1. **各平台截图快捷键**：Windows/Mac/Linux 的区域/全屏/窗口截图方法
2. **三种给 AI 传图片的方式**：粘贴截图、引用文件、AI 生成
3. **Linux 需要额外安装剪贴板工具**：xclip（X11）或 wl-clipboard（Wayland）
4. **故障排除六步法**：检查剪贴板 → Linux 工具检查 → 模型支持确认 → 快捷键冲突排查 → 多路复用器检查 → WSL 环境检查
5. **模型支持情况**：
   - **国际**：GPT-5.2、Claude 4.6、Gemini 3.1 支持图片
   - **国内**：只有 **Kimi K2.5** 支持，GLM-5、MiniMax 2.5 等不支持
   - Anthropic 限制图片最大 2000 像素
   - Azure GPT-5.2-Codex 目前有图片粘贴问题
6. **特定环境问题**：
   - JetBrains Terminal 要用 `Ctrl+V` 而非 `Cmd+V`
   - Zellij/tmux 等多路复用器可能干扰剪贴板
   - macOS 某些输入法（如俄语、中文部分输入法）可能导致粘贴失败
7. **输入框里的 `[Image N]` 是虚拟标记**：可随时删除

---

## 下一课预告

> 下一课我们学习 **[2.2 管理对话](./02-sessions)**。
>
> 你会学到：
> - 新建、切换多个对话会话
> - 撤销误发的消息
> - 导出对话记录

---

## 附录：源码参考

<details>
<summary><strong>点击展开查看源码位置</strong></summary>

> 更新时间：2026-03-01（v1.2+）

| 功能 | 文件路径 | 关键逻辑 |
|-----|---------|----------|
| 剪贴板图片读取 | [`src/cli/cmd/tui/util/clipboard.ts`](https://github.com/anomalyco/opencode/blob/dev/packages/opencode/src/cli/cmd/tui/util/clipboard.ts) | 跨平台图片读取实现 |
| Windows 图片粘贴 | [`src/cli/cmd/tui/component/prompt/index.tsx`](https://github.com/anomalyco/opencode/blob/dev/packages/opencode/src/cli/cmd/tui/component/prompt/index.tsx#L839-L855) | Ctrl+V 拦截图片粘贴 |
| 粘贴事件处理 | [`src/cli/cmd/tui/component/prompt/index.tsx`](https://github.com/anomalyco/opencode/blob/dev/packages/opencode/src/cli/cmd/tui/component/prompt/index.tsx#L914-L981) | onPaste 事件处理 |
| 图片标记插入 | [`src/cli/cmd/tui/component/prompt/index.tsx`](https://github.com/anomalyco/opencode/blob/dev/packages/opencode/src/cli/cmd/tui/component/prompt/index.tsx#L696-L737) | pasteImage 函数实现 |
| 图片文件引用 | [`src/session/prompt.ts`](https://github.com/anomalyco/opencode/blob/dev/packages/opencode/src/session/prompt.ts#L870-L910) | @ 引用文件处理 |
| 图片发送给 AI | [`src/acp/agent.ts`](https://github.com/anomalyco/opencode/blob/dev/packages/opencode/src/acp/agent.ts#L1015-L1034) | image block 发送逻辑 |
| 快捷键配置 | [`src/config/config.ts`](https://github.com/anomalyco/opencode/blob/dev/packages/opencode/src/config/config.ts#L817) | input_paste 默认 `ctrl+v` |

**关键实现细节**（`clipboard.ts:30-74`）：

```typescript
// 读取剪贴板图片的跨平台实现
if (os === "darwin") {
  // macOS: 使用 osascript 读取剪贴板图片
}
if (os === "win32" || release().includes("WSL")) {
  // Windows: 使用 PowerShell 读取剪贴板
}
if (os === "linux") {
  // Linux Wayland: wl-paste -t image/png
  // Linux X11: xclip -selection clipboard -t image/png -o
}
```

</details>
