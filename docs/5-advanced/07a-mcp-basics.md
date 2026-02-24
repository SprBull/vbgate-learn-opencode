---
title: 5.7a MCP 基础
subtitle: 连接外部服务入门
course: OpenCode 中文实战课
stage: 第五阶段
lesson: "5.7a"
duration: 15 分钟
practice: 15 分钟
level: 进阶
description: 通过 MCP 连接外部服务，让 AI 调用数据库、搜索引擎、监控平台等任意工具。
tags:
  - MCP
  - 扩展
  - 外部工具
prerequisite:
  - 5.1 配置全解
---

# 5.7a MCP 基础

> 💡 **一句话总结**：通过 MCP（Model Context Protocol）连接外部服务，让 AI 能调用数据库、搜索引擎、监控平台等任意工具。

## 📝 课程笔记

本课核心知识点整理：

<img src="/images/5-advanced/07a-mcp-basics-notes.mini.jpeg" alt="MCP基础学霸笔记" data-zoom-src="/images/5-advanced/07a-mcp-basics-notes.jpeg" />

---

## 学完你能做什么

- 理解 MCP 协议的作用和架构
- 配置本地 MCP 服务器
- 配置远程 MCP 服务器
- 查看 MCP 连接状态

---

## 你现在的困境

- AI 只能操作本地文件，访问不了外部服务
- 想让 AI 查 Sentry 日志、搜索文档、操作数据库
- 听说过 MCP，但不知道怎么配置和使用

---

## 什么是 MCP

MCP（Model Context Protocol）是一种标准协议，让 AI 能调用外部工具和服务。

**核心概念**：

- **MCP 服务器**：提供工具的外部进程或远程服务
- **MCP 工具**：服务器暴露的具体功能（如搜索、查询、操作）
- **MCP 客户端**：OpenCode 内置的连接器

**工作原理**：

```
用户提问 → OpenCode → AI 决定调用 MCP 工具 → MCP 服务器执行 → 返回结果
```

### 注意事项

- MCP 服务器会增加上下文消耗，工具越多 token 消耗越快
- 某些 MCP（如 GitHub）会添加大量 token，容易超出上下文限制
- 建议只启用必要的 MCP 服务器

---

## 配置文件位置

OpenCode 会在多个位置查找配置文件，**后加载的会覆盖先加载的**（优先级从低到高）：

| 加载顺序 | 位置 | 用途 |
|----------|------|------|
| 1（最低） | `~/.config/opencode/opencode.json` | 全局配置，所有项目共享 |
| 2 | `opencode.json` | 项目根目录配置 |
| 3（最高） | `.opencode/opencode.json` | 项目级配置（推荐） |

::: tip 为什么推荐 .opencode/opencode.json？
它有最高优先级，且放在 `.opencode/` 目录下更整洁，方便与其他配置（如 agents、commands）一起管理。
:::

---

## 交互式添加：opencode mcp add

不想手动编辑 JSON？用交互式命令添加 MCP：

```bash
opencode mcp add
```

按提示操作：

```
? Location: (Use arrow keys)
❯ Current project
    /path/to/project/.opencode/opencode.json
  Global
    ~/.config/opencode/opencode.json

? MCP server name: filesystem

? Select MCP server type:
❯ Local
  Remote

? Enter command to run:
opencode x @modelcontextprotocol/server-filesystem /path/to/allowed/dir
```

> ⚠️ **注意**：位置选择仅在 Git 项目中显示。非 Git 项目会直接写入全局配置。

**你应该看到**：

```
✓ MCP server "filesystem" added successfully
```

---

## 本地 MCP 服务器

本地 MCP 服务器运行在你的机器上，通过 stdio 通信。

### 配置方式

在 `opencode.json` 或 `.opencode/opencode.json` 的 `mcp` 下配置：

```jsonc
{
  "$schema": "https://opencode.ai/config.json",
  "mcp": {
    "my-local-mcp": {
      "type": "local",
      "command": ["npx", "-y", "@modelcontextprotocol/server-everything"],
      "enabled": true,
      "environment": {
        "MY_ENV_VAR": "value"
      }
    }
  }
}
```

### 配置选项

<AdInArticle />

| 选项 | 类型 | 必填 | 描述 |
|------|------|------|------|
| `type` | String | ✓ | 必须是 `"local"` |
| `command` | Array | ✓ | 命令数组，如 `["npx", "-y", "xxx"]` 或 `["bun", "x", "xxx"]` |
| `environment` | Object | | 环境变量键值对 |
| `enabled` | Boolean | | 是否启用，默认 `true` |
| `timeout` | Number | | 连接超时（毫秒），默认 30000 |

> ⚠️ **注意**：官方文档描述 timeout 默认值为 2000+ms，但源码实际默认值为 30000ms（30秒）。来源：`mcp/index.ts:29`

### 使用方式

配置完成后，在对话中添加提示词引导 AI 使用：

```
use the my-local-mcp tool to do something
```

---

## 远程 MCP 服务器

远程 MCP 服务器通过 HTTP/SSE 协议连接。

### 配置方式

```jsonc
{
  "$schema": "https://opencode.ai/config.json",
  "mcp": {
    "my-remote-mcp": {
      "type": "remote",
      "url": "https://mcp.example.com/mcp",
      "enabled": true,
      "headers": {
        "Authorization": "Bearer {env:MY_API_KEY}"
      }
    }
  }
}
```

### 配置选项

| 选项 | 类型 | 必填 | 描述 |
|------|------|------|------|
| `type` | String | ✓ | 必须是 `"remote"` |
| `url` | String | ✓ | 远程 MCP 服务器 URL |
| `enabled` | Boolean | | 是否启用，默认 `true` |
| `headers` | Object | | 自定义请求头 |
| `oauth` | Object/false | | OAuth 配置或禁用 OAuth |
| `timeout` | Number | | 连接超时（毫秒），默认 30000 |

---

## 连接状态

MCP 连接有 5 种状态：

| 状态 | 说明 |
|------|------|
| `connected` | 已连接，工具可用 |
| `disabled` | 配置中 `enabled: false`，未连接 |
| `failed` | 连接失败，查看错误信息 |
| `needs_auth` | 需要 OAuth 认证 |
| `needs_client_registration` | 需要预注册客户端 ID |

查看当前状态：

```bash
opencode mcp list
```

---

## 快速开始示例

### 示例 1：本地测试服务器

```jsonc
{
  "$schema": "https://opencode.ai/config.json",
  "mcp": {
    "everything": {
      "type": "local",
      "command": ["npx", "-y", "@modelcontextprotocol/server-everything"]
    }
  }
}
```

测试使用：

```
use the everything tool to add 3 and 4
```

### 示例 2：Context7 文档搜索

```jsonc
{
  "$schema": "https://opencode.ai/config.json",
  "mcp": {
    "context7": {
      "type": "remote",
      "url": "https://mcp.context7.com/mcp"
    }
  }
}
```

测试使用：

```
use context7 查询 React hooks 最佳实践
```

### 示例 3：Grep 代码搜索

```jsonc
{
  "$schema": "https://opencode.ai/config.json",
  "mcp": {
    "gh_grep": {
      "type": "remote",
      "url": "https://mcp.grep.app"
    }
  }
}
```

测试使用：

```
use the gh_grep tool 搜索如何在 Node.js 中实现 JWT 验证
```

---

## 踩坑提醒

| 现象 | 原因 | 解决 |
|-----|-----|-----|
| MCP 连接超时 | timeout 设置过短或网络慢 | 增大 `timeout` 值，默认 30000ms |
| 本地 MCP 启动失败 | 命令不存在或路径错误 | 确认 `command` 数组正确，检查 PATH |
| 远程 MCP 连接失败 | URL 错误或服务器不可用 | 验证 URL 是否正确，检查网络 |

---

## 本课小结

你学会了：

1. **MCP 协议**：让 AI 连接外部服务的标准协议
2. **配置位置**：项目级 vs 全局级，团队共享 vs 个人偏好
3. **交互式添加**：`opencode mcp add` 命令
4. **本地 MCP**：`type: "local"` + `command` 数组
5. **远程 MCP**：`type: "remote"` + `url`
6. **连接状态**：5 种状态及查看方法

---

## 下一步

- [5.7b MCP 进阶](./07b-mcp-advanced) - OAuth 认证、权限管理、更多 MCP 示例

::: tip 遇到问题？
MCP 配置卡住了？[加入社群](/community)，和 2000+ 同路人一起交流，实时答疑。
:::
