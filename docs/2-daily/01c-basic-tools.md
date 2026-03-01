---
title: "AI 的基础工具：文件读写、编辑与搜索 | OpenCode 教程"
subtitle: AI 的基础工具
course: OpenCode 中文实战课
stage: 第二阶段
lesson: "2.1c"
duration: 20 分钟
practice: 15 分钟
level: 新手
description: 了解 OpenCode 核心工具 read、write、edit、bash、grep、glob 的用法和分工。学会让 AI 高效读取文件、精确编辑代码、执行命令和搜索代码库。
tags:
  - 工具
  - 文件操作
  - 搜索
  - 命令执行
prerequisite:
  - 2.1 界面与基础操作
---

# AI 的基础工具

## 📝 课程笔记

本课核心知识点整理：

<img src="/images/2-daily/basic-tools-notes.mini.jpeg" 
     alt="AI 的基础工具学霸笔记" 
     data-zoom-src="/images/2-daily/basic-tools-notes.jpeg" />

---

::: warning 📖 这课不需要你动手操作
这课讲的是 **AI 在幕后用什么工具帮你干活**，不是让你学怎么调用这些工具。

你只管用自然语言说"帮我改一下这个文件"、"搜索所有 TODO"，AI 会自动选择合适的工具。

**那为什么要了解？** 因为知道 AI 的能力边界，你才能：
- 写出更好的提示词（比如知道可以让 AI 搜索代码）
- 遇到报错时不慌（比如 AI 说"文件太大"，你知道这是正常的）
- 理解 AI 为什么要先读文件再改（不是它笨，是安全机制）
:::

---

## 学完你能做什么

::: info 🎯 学完你能做什么
- 知道 AI 能帮你做哪些事（读文件、改代码、跑命令、搜索代码库）
- 遇到"文件太大"、"多处匹配"等提示时知道怎么回事
- 理解 AI 为什么有时候要"先读再改"
- 更有信心地指挥 AI 干活
:::

---

## 你现在的困境

你已经会和 AI 对话了，但有时候会冒出一些疑问：

- "AI 读文件时如果文件很大怎么办？会不会漏掉内容？"
- "AI 改代码会不会改错地方？它怎么知道改哪里？"
- "AI 能执行哪些命令？会不会把我的电脑搞坏？"
- "想找某个函数在哪些文件里，怎么让 AI 搜索？"

这些问题的答案都在 AI 的核心工具里。了解它们，你就能更放心地让 AI 帮你干活。

---

## 什么时候读这课

- 好奇 AI 到底是怎么操作你的文件的
- 遇到了"文件太大"、"找不到匹配"等提示，想搞清楚怎么回事
- 想知道 AI 能不能帮你搜索代码、执行命令
- 想写出更精准的提示词，让 AI 更高效

---

## 🎒 开始前的准备

- [ ] 完成了 [2.1 界面与基础操作](./01-interface)
- [ ] 有一个可用的项目目录（随便什么项目都行）
- [ ] OpenCode 能正常和 AI 对话

---

## 核心思路

<AdInArticle />

OpenCode 给 AI 配了 **10 个核心工具**，本课重点讲解其中 6 个最常用的文件操作工具：

| 工具 | 干什么 | 类比 |
|------|--------|------|
| **read** | 读取文件或目录 | 打开文件看内容 |
| **write** | 创建或覆盖文件 | 另存为 |
| **edit** | 精确替换文件中的文本 | 查找替换 |
| **bash** | 执行 Shell 命令 | 在终端敲命令 |
| **grep** | 按内容搜索文件 | 全局搜索 |
| **glob** | 按文件名搜索文件 | 文件管理器里搜文件名 |

你不需要手动调用这些工具。你只管用自然语言描述需求，AI 会自动选择合适的工具。

::: info 还有更多工具
除了这 6 个文件操作工具，OpenCode 还有：

| 工具 | 作用 | 教程位置 |
|------|------|---------|
| **Task** | 创建子 Agent 处理复杂任务 | [Agent 权限与安全](/5-advanced/02c-agent-permissions) |
| **WebFetch** | 获取网页内容 | [联网搜索](/5-advanced/23-web-search) |
| **TodoWrite** | 任务清单管理（AI 自动使用） | — |
| **Skill** | 加载专业知识包 | [Skill 系列](/5-advanced/03a-skills-basics) |

**TodoWrite 是什么？**

当你给 AI 一个复杂任务时，可能会看到它自动列出这样的计划：

```
1. [ ] 分析代码结构
2. [x] 读取配置文件
3. [ ] 修改入口文件
4. [ ] 运行测试验证
```

这就是 TodoWrite 工具在工作。它会创建一个任务清单，做完一项勾选一项，防止 AI "忘事"或"走偏"。你不需要手动调用，AI 会在需要时自动使用。
:::

但了解它们的能力和限制，能帮你写出更好的提示词，也能在出问题时快速定位原因。

::: tip 核心原则：工具各司其职
不要让 AI 用 bash 命令（`cat`、`sed`、`grep`）来做文件操作。专用工具有权限检查、智能容错、性能优化，bash 命令没有这些保护。
:::

---

## 跟我做

### 第 1 步：让 AI 读取文件

**为什么**
read 是最基础的工具，AI 需要先"看到"文件内容才能帮你分析或修改。

在 OpenCode 中输入：

```
帮我看看 package.json 里有什么
```

**你应该看到**：AI 调用 read 工具读取文件，然后给你分析内容。

::: details 📦 read 工具的能力
**基本参数**：
- `filePath`：文件的绝对路径
- `offset`：从第几行开始读（默认第 1 行）
- `limit`：最多读多少行（默认 2000 行）

**大文件处理**：如果文件超过 2000 行，read 会自动截断，并提示"Use offset parameter to read beyond line 2001"。AI 会自动用 offset 参数继续读取后面的内容。

**特殊文件**：read 还能读取图片（PNG、JPG、GIF）和 PDF，会转成 base64 发给 AI 模型分析。但不支持 SVG 和二进制文件（.zip、.exe 等）。

**智能纠错**：如果你拼错了文件名，read 会提示相似的文件名。比如你说 `packge.json`，它会建议 `package.json`。

**读取目录**：read 不仅能读文件，还能读目录。在对话中用 `@目录名` 提及一个目录，AI 会用 read 工具获取目录内容（列出子目录和文件），输出格式友好易读。这在你想让 AI 了解项目结构时很有用。
:::

### 第 2 步：让 AI 创建文件

**为什么**
write 工具用来创建新文件或完全覆盖已有文件。

```
帮我创建一个 hello.txt，内容写 "Hello OpenCode"
```

**你应该看到**：AI 调用 write 工具创建文件，并显示写入成功。

::: warning ⚠️ "先读后写"规则
如果文件已经存在，AI 必须先用 read 读取文件，然后才能用 write 覆盖。这是为了防止 AI 在不知道文件当前内容的情况下误覆盖。

如果 AI 跳过了读取直接写入已有文件，OpenCode 会报错。
:::

**写入后的自动检查**：write 完成后会自动触发 LSP 诊断。如果写入的代码有语法错误或类型问题，AI 会立刻看到并尝试修复。

### 第 3 步：让 AI 编辑文件

**为什么**
edit 是 OpenCode 最聪明的工具。它不是简单地"改第几行"，而是用字符串匹配来精确定位要修改的位置。

```
把 hello.txt 里的 "Hello OpenCode" 改成 "Hello World"
```

**你应该看到**：AI 调用 edit 工具，用 `oldString: "Hello OpenCode"` 和 `newString: "Hello World"` 完成替换。

::: details 📦 edit 的智能匹配
edit 工具有 9 层匹配策略，从严格到宽松逐层尝试：

| 策略 | 说明 | 例子 |
|------|------|------|
| 精确匹配 | 完全一致 | `foo` 匹配 `foo` |
| 行首尾空白忽略 | 忽略每行开头结尾的空格 | `  foo  ` 匹配 `foo` |
| 首尾行锚点 | 用第一行和最后一行定位代码块 | 函数开头和结尾匹配 |
| 空白规范化 | 多个空格当一个 | `a  b` 匹配 `a b` |
| 缩进容错 | 忽略整体缩进差异 | 2 空格缩进匹配 4 空格 |
| 转义字符处理 | 处理 `\n`、`\t` 等 | `a\nb` 匹配实际换行 |
| 边界修剪 | 去掉首尾空白后匹配 | 前后有空行也能匹配 |
| 上下文感知 | 用首尾行 + 中间内容相似度 | 代码块略有变化也能匹配 |
| 多处匹配 | 找到所有精确匹配 | 配合 replaceAll 使用 |

简单说：你给 AI 的代码片段不需要和文件里的完全一致，有点缩进差异、空格差异都没关系。
:::

**多处匹配怎么办？**

如果 `oldString` 在文件中出现了多次，edit 会报错：

```
Found multiple matches for oldString.
Provide more surrounding lines in oldString to identify the correct match.
```

解决方法：
- 让 AI 提供更多上下文（多包含几行代码），确保唯一匹配
- 或者用 `replaceAll` 参数一次性替换所有匹配

### 第 4 步：让 AI 执行命令

**为什么**
bash 工具让 AI 能执行 Shell 命令，比如跑测试、装依赖、查看 Git 状态。

```
帮我运行一下 git status
```

**你应该看到**：AI 调用 bash 工具执行命令，返回 Git 状态信息。

::: danger 🚫 不要用 bash 做文件操作
这是新手最容易犯的错误。bash 工具是用来执行命令的，不是用来操作文件的。

| ❌ 不要这样 | ✅ 应该这样 |
|------------|-----------|
| 用 `cat` 读文件 | 用 read 工具 |
| 用 `echo > file` 写文件 | 用 write 工具 |
| 用 `sed` 编辑文件 | 用 edit 工具 |
| 用 `find` 搜文件 | 用 glob 工具 |
| 用 `grep` 搜内容 | 用 grep 工具 |

为什么？专用工具有权限检查、智能容错、LSP 诊断，bash 命令没有这些保护。
:::

**bash 的安全机制**：
- 默认超时 2 分钟，防止命令卡住
- 用 tree-sitter 解析命令语法，对 `rm`、`cp`、`mv` 等文件操作命令检查路径是否在项目目录内
- 所有命令都会请求权限确认（可设置自动批准规则）
- 输出超过 2000 行或 50KB 会自动截断

### 第 5 步：让 AI 搜索代码

**为什么**
grep 和 glob 是两个搜索工具，一个搜内容，一个搜文件名。

**搜索文件内容**（grep）：

```
帮我找出项目里所有用到 console.log 的地方
```

**你应该看到**：AI 调用 grep 工具，返回匹配的文件和行号。

**搜索文件名**（glob）：

```
帮我找出所有的测试文件
```

**你应该看到**：AI 调用 glob 工具，用 `**/*.test.ts` 之类的模式搜索。

| 你想做什么 | AI 会用什么 | 示例提示词 |
|-----------|-----------|-----------|
| 找某个函数在哪里用了 | grep | "搜索所有调用 getUserData 的地方" |
| 找某个文件在哪 | glob | "找到所有配置文件" |
| 找某个字符串 | grep | "搜索所有 TODO 注释" |
| 列出某类文件 | glob | "列出 src 下所有 .tsx 文件" |

::: tip 搜索结果限制
grep 和 glob 都最多返回 100 条结果。如果结果被截断，可以：
- 缩小搜索目录（"只在 src 目录下搜索"）
- 用更精确的关键词
- 过滤文件类型（"只搜索 .ts 文件"）
:::

---

## 工具协作：AI 怎么组合使用

实际工作中，AI 很少只用一个工具。看几个典型场景：

**场景 1：重命名函数**

```
你：把所有 getUserData 改成 fetchUserInfo

AI 的操作流程：
1. grep 搜索 "getUserData" → 找到 20 个文件
2. 逐个文件 read 读取
3. edit + replaceAll 替换
4. bash 运行测试验证
```

**场景 2：添加新功能**

```
你：给 User 组件添加 email 字段

AI 的操作流程：
1. glob 搜索 "User.tsx" → 找到文件
2. read 读取文件内容
3. edit 修改接口定义和组件代码
4. 自动 LSP 检查类型错误
```

**场景 3：定位 Bug**

```
你：登录后没有跳转到首页，帮我查一下

AI 的操作流程：
1. grep 搜索 "login" 相关代码
2. read 读取登录逻辑
3. grep 搜索 "redirect" 或 "navigate"
4. 分析代码逻辑，找到问题
```

---

## 检查点 ✅

> 全部通过才能继续

- [ ] 知道 AI 有 10 个核心工具，本课重点学了 6 个文件操作工具
- [ ] 理解"先读后写"规则
- [ ] 知道 edit 工具用字符串匹配而不是行号定位
- [ ] 知道不应该让 AI 用 bash 做文件操作
- [ ] 知道 grep 搜内容、glob 搜文件名

---

## 踩坑提醒

| 现象 | 原因 | 解决 |
|-----|-----|-----|
| AI 说"File not found" | 文件路径错误或拼写错误 | read 会提示相似文件名，按提示修正 |
| AI 说"Found multiple matches" | edit 的 oldString 在文件中出现了多次 | 让 AI 提供更多上下文，或用 replaceAll |
| AI 说"Output truncated" | 文件或命令输出太大 | 正常现象，AI 会自动分段读取 |
| AI 用 `cat` 读文件 | AI 没有遵守工具分工 | 提醒它"用 read 工具读取" |
| bash 命令超时 | 默认 2 分钟超时 | 告诉 AI "这个命令可能需要 10 分钟" |
| write 报错"must read first" | 覆盖已有文件前没有先读取 | AI 会自动先 read 再 write，如果报错可以提醒它 |

---

## 本课小结

OpenCode 有 **10 个核心工具**，本课重点讲了 **6 个文件操作工具**：

| 工具 | 作用 | 记忆点 |
|------|------|--------|
| read | 读取文件/目录 | 大文件自动分段，支持图片和 PDF，可用 @ 提及目录 |
| write | 创建/覆盖文件 | 必须先读后写，写完自动 LSP 检查 |
| edit | 精确字符串替换 | 9 层智能匹配，不怕缩进差异 |
| bash | 执行 Shell 命令 | 有超时和安全检查，别用它操作文件 |
| grep | 搜索文件内容 | 正则表达式，最多 100 条结果 |
| glob | 搜索文件名 | glob 模式，最多 100 条结果 |

记住三条规则：
1. 专用工具 > bash 命令
2. 先读取再写入
3. 搜索结果有上限，必要时缩小范围

---

## 下一课预告

> 下一课我们学习 **[使用图片与 AI 对话](./01d-images)**。
>
> 你会学到：
> - 如何把截图直接粘贴给 AI
> - Linux 上配置图片粘贴支持
> - 引用本地图片文件让 AI 分析

---

## 附录：源码参考

<details>
<summary><strong>点击展开查看源码位置</strong></summary>

> 更新时间：2026-02-14

| 功能 | 文件路径 | 行号 |
|------|---------|------|
| **工具注册表（完整列表）** | [`src/tool/registry.ts`](https://github.com/anomalyco/opencode/blob/dev/packages/opencode/src/tool/registry.ts#L98-L119) | 98-119 |
| read 工具定义和参数 | [`src/tool/read.ts`](https://github.com/anomalyco/opencode/blob/dev/packages/opencode/src/tool/read.ts#L17-L204) | 17-204 |
| read 默认限制常量 | [`src/tool/read.ts`](https://github.com/anomalyco/opencode/blob/dev/packages/opencode/src/tool/read.ts#L13-L15) | 13-15 |
| read 二进制文件检测 | [`src/tool/read.ts`](https://github.com/anomalyco/opencode/blob/dev/packages/opencode/src/tool/read.ts#L206-L261) | 206-261 |
| read 图片/PDF 处理 | [`src/tool/read.ts`](https://github.com/anomalyco/opencode/blob/dev/packages/opencode/src/tool/read.ts#L113-L139) | 113-139 |
| read 文件名建议 | [`src/tool/read.ts`](https://github.com/anomalyco/opencode/blob/dev/packages/opencode/src/tool/read.ts#L49-L67) | 49-67 |
| write 工具定义 | [`src/tool/write.ts`](https://github.com/anomalyco/opencode/blob/dev/packages/opencode/src/tool/write.ts#L19-L85) | 19-85 |
| write LSP 诊断 | [`src/tool/write.ts`](https://github.com/anomalyco/opencode/blob/dev/packages/opencode/src/tool/write.ts#L56-L73) | 56-73 |
| edit 工具定义和参数 | [`src/tool/edit.ts`](https://github.com/anomalyco/opencode/blob/dev/packages/opencode/src/tool/edit.ts#L27-L155) | 27-155 |
| edit 9 层匹配策略 | [`src/tool/edit.ts`](https://github.com/anomalyco/opencode/blob/dev/packages/opencode/src/tool/edit.ts#L184-L580) | 184-580 |
| edit replace 核心函数 | [`src/tool/edit.ts`](https://github.com/anomalyco/opencode/blob/dev/packages/opencode/src/tool/edit.ts#L618-L655) | 618-655 |
| bash 工具定义 | [`src/tool/bash.ts`](https://github.com/anomalyco/opencode/blob/dev/packages/opencode/src/tool/bash.ts#L55-L269) | 55-269 |
| bash 默认超时 | [`src/tool/bash.ts`](https://github.com/anomalyco/opencode/blob/dev/packages/opencode/src/tool/bash.ts#L22) | 22 |
| bash 命令解析 | [`src/tool/bash.ts`](https://github.com/anomalyco/opencode/blob/dev/packages/opencode/src/tool/bash.ts#L93-L145) | 93-145 |
| bash 输出截断常量 | [`src/tool/truncation.ts`](https://github.com/anomalyco/opencode/blob/dev/packages/opencode/src/tool/truncation.ts#L10-L11) | 10-11 |
| bash 输出截断逻辑 | [`src/tool/truncation.ts`](https://github.com/anomalyco/opencode/blob/dev/packages/opencode/src/tool/truncation.ts#L50-L105) | 50-105 |
| grep 工具定义 | [`src/tool/grep.ts`](https://github.com/anomalyco/opencode/blob/dev/packages/opencode/src/tool/grep.ts#L12-L150) | 12-150 |
| grep 结果限制 | [`src/tool/grep.ts`](https://github.com/anomalyco/opencode/blob/dev/packages/opencode/src/tool/grep.ts#L100-L101) | 100-101 |
| glob 工具定义 | [`src/tool/glob.ts`](https://github.com/anomalyco/opencode/blob/dev/packages/opencode/src/tool/glob.ts#L9-L80) | 9-80 |
| glob 结果限制 | [`src/tool/glob.ts`](https://github.com/anomalyco/opencode/blob/dev/packages/opencode/src/tool/glob.ts#L35) | 35 |

**关键常量**：
- `DEFAULT_READ_LIMIT = 2000`：read 工具默认读取行数
- `MAX_LINE_LENGTH = 2000`：单行最大字符数
- `MAX_BYTES = 50 * 1024`：read 工具和通用输出截断的最大字节数 50KB
- `DEFAULT_TIMEOUT = 2 * 60 * 1000`：bash 工具默认超时 2 分钟
- `MAX_METADATA_LENGTH = 30_000`：bash 工具元数据最大长度
- `limit = 100`：grep/glob 工具结果上限

**关键函数**：
- `replace()`：edit 工具的核心替换逻辑，依次尝试 9 种 Replacer
- `isBinaryFile()`：检测文件是否为二进制（扩展名 + 字节分析）
- `Ripgrep.files()`：glob 工具底层使用 ripgrep 搜索文件
- `Truncate.output()`：bash 输出截断逻辑，超限后保存完整输出到文件

</details>
