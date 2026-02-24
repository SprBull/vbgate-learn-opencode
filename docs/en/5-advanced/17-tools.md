# Built-in Tools

## Course Notes

Tools allow LLMs to perform operations in your codebase. OpenCode comes with a set of built-in tools, and you can also extend them through [Custom Tools](/en/5-advanced/13-custom-tools.md) or [MCP Servers](/en/5-advanced/07a-mcp-basics.md).

By default, all tools are enabled and run without requiring permissions. However, you can control [Permissions](/en/5-advanced/05-permissions.md) through configuration.

---

## Conditional Activation

Some tools require specific conditions to be enabled:

| Tool | Activation Condition |
|------|---------------------|
| `websearch` | Use OpenCode Zen hosted models OR set `OPENCODE_ENABLE_EXA=true` |
| `codesearch` | Use OpenCode Zen hosted models OR set `OPENCODE_ENABLE_EXA=true` |
| `batch` | Configure `experimental.batch_tool: true` |
| `lsp` | Enable `OPENCODE_EXPERIMENTAL_LSP_TOOL` flag |
| `plan_enter` / `plan_exit` | CLI mode + experimental plan mode flag |

::: tip How to Enable
Configure in `opencode.json`:

```json
{
  "experimental": {
    "batch_tool": true
  }
}
```

Or set environment variables:

```bash
export OPENCODE_ENABLE_EXA=true
export OPENCODE_EXPERIMENTAL_LSP_TOOL=1
```
:::

---

## Configuration

You can configure tools globally or per-agent. Agent configuration overrides global settings.

By default, all tools are set to true. To disable a tool, set it to false.

### Global Configuration

Use the tools option to globally disable or enable tools:

```json
{
  "$schema": "https://opencode.ai/config.json",
  "tools": {
    "write": false,
    "bash": false,
    "webfetch": true
  }
}
```

### Per-Agent Configuration

Use tools in agent definitions to override global settings:

```json
{
  "$schema": "https://opencode.ai/config.json",
  "tools": {
    "write": true,
    "bash": true
  },
  "agent": {
    "plan": {
      "tools": {
        "write": false,
        "bash": false
      }
    }
  }
}
```

## Built-in Tools List

### bash

Execute shell commands in the project environment.

```json
{
  "tools": {
    "bash": true
  }
}
```

Allows LLM to run terminal commands like npm install, git status, etc.

::: details AI Call Parameters

| Parameter | Type | Required | Description |
|------|------|------|------|
| `command` | string | ✅ | Command to execute |
| `description` | string | ✅ | Command description (5-10 words) |
| `workdir` | string | ❌ | Working directory, defaults to project root |
| `timeout` | number | ❌ | Timeout in milliseconds, default 120000 (2 minutes) |

**Safety Mechanisms**:
- Uses tree-sitter-bash to parse command syntax
- Detects commands like `cd`, `rm`, `cp`, `mv`, `mkdir`, `touch`, `chmod`, `chown`, `cat`, etc.
- Requests `external_directory` permission confirmation when involving directories outside the project
- Automatically truncates output exceeding 2000 lines or 50KB, full output saved to file

:::

### edit

Modify existing files using exact string replacement.

```json
{
  "tools": {
    "edit": true
  }
}
```

::: details AI Call Parameters

| Parameter | Type | Required | Description |
|------|------|------|------|
| `filePath` | string | ✅ | Absolute path to the file |
| `oldString` | string | ✅ | Original text to replace |
| `newString` | string | ✅ | Replacement text (must be different from oldString) |
| `replaceAll` | boolean | ❌ | Replace all occurrences (default false) |

**Smart Matching**: edit has 9 matching strategies (SimpleReplacer → LineTrimmedReplacer → BlockAnchorReplacer → WhitespaceNormalizedReplacer → IndentationFlexibleReplacer → EscapeNormalizedReplacer → TrimmedBoundaryReplacer → ContextAwareReplacer → MultiOccurrenceReplacer), trying from strict to loose.

**Prerequisite**: Must read the file first using read, otherwise an error will occur.

**Post-write Check**: Automatically triggers LSP diagnostics to report syntax and type errors.

:::

### write

Create new files or overwrite existing files.

```json
{
  "tools": {
    "write": true
  }
}
```

::: details AI Call Parameters

| Parameter | Type | Required | Description |
|------|------|------|------|
| `filePath` | string | ✅ | Absolute path to the file (must be absolute) |
| `content` | string | ✅ | Content to write |

**Prerequisite**: If the file already exists, must read it first using read, otherwise an error will occur.

**Post-write Check**: Automatically triggers LSP diagnostics to report errors in the current file and other affected files (up to 5 files).

**Diff Preview**: Generates a diff before writing and requests permission confirmation.

:::

### read

Read file or directory contents from the codebase.

```json
{
  "tools": {
    "read": true
  }
}
```

::: details AI Call Parameters

| Parameter | Type | Required | Description |
|------|------|------|------|
| `filePath` | string | ✅ | Absolute path to file or directory |
| `offset` | number | ❌ | Line/entry to start reading from (**1-indexed**, counting from 1) |
| `limit` | number | ❌ | Maximum lines/entries to read (default 2000) |

**File Read Limits**:
- Default reads 2000 lines (`DEFAULT_READ_LIMIT`)
- Single lines exceeding 2000 characters are truncated (`MAX_LINE_LENGTH`)
- Total output limit 50KB (`MAX_BYTES`)

**Directory Reading** (v1.1.60+):
- Returns list of entries when reading directories, subdirectories end with `/`
- Entries sorted alphabetically
- Supports `offset` and `limit` pagination (same as file reading, 1-indexed)

**Directory Reading Output Example**:

```xml
<path>/Users/xxx/project/src</path>
<type>directory</type>
<entries>
components/
utils/
index.ts
(3 entries)
</entries>
```

**Special Files**: Supports reading images (PNG, JPG, GIF, excluding SVG) and PDFs, converted to base64 attachments. Binary files (.zip, .exe, etc.) will error.

**Smart Correction**: When file doesn't exist, searches for similar filenames in the same directory and suggests.

:::

### grep

Search file contents using regular expressions.

```json
{
  "tools": {
    "grep": true
  }
}
```

::: details AI Call Parameters

| Parameter | Type | Required | Description |
|------|------|------|------|
| `pattern` | string | ✅ | Regular expression pattern |
| `path` | string | ❌ | Search path, defaults to current directory |
| `include` | string | ❌ | File filter pattern, e.g., `"*.ts"` |

**Result Limits**:
- Returns maximum 100 matches, truncated if exceeded
- Single lines exceeding 2000 characters will be truncated

:::

### glob

Find files through pattern matching.

```json
{
  "tools": {
    "glob": true
  }
}
```

::: details glob Pattern Syntax

| Pattern | Description | Example |
|------|------|------|
| `*` | Match any characters (excluding `/`) | `*.ts` |
| `**` | Match any directory level | `src/**/*.ts` |
| `?` | Match single character | `file?.ts` |
| `[abc]` | Match specified characters | `file[123].ts` |
| `{a,b}` | Match multiple patterns | `*.{ts,tsx}` |

**Result Limit**: Returns maximum 100 files, truncated if exceeded.

:::

### list

List files and directories under a given path.

```json
{
  "tools": {
    "list": true
  }
}
```

### lsp (Experimental)

Interact with configured LSP servers to get code intelligence features like definitions, references, hover information, and call hierarchy.

### patch

Apply patches to files.

```json
{
  "tools": {
    "patch": true
  }
}
```

### multiedit

Batch modify multiple locations in the same file.

```json
{
  "tools": {
    "multiedit": true
  }
}
```

### skill

Load SKILL.md files and return their content in the conversation.

```json
{
  "tools": {
    "skill": true
  }
}
```

### todowrite

Manage todo lists during coding sessions.

```json
{
  "tools": {
    "todowrite": true
  }
}
```

### todoread

Read existing todo lists.

```json
{
  "tools": {
    "todoread": true
  }
}
```

### question

Allows AI to ask you questions while performing tasks.

```json
{
  "tools": {
    "question": true
  }
}
```

This tool enables AI to:

- Collect your preferences or requirements
- Clarify ambiguous instructions
- Get decisions on implementation choices
- Provide multiple directions for you to choose

Each question includes a title, question text, and list of options. You can select from options or enter a custom answer. When there are multiple questions, you can navigate between them before submitting.

**Usage Example**:

```
You: Help me refactor this module

AI: I noticed several refactoring approaches, which do you prefer?
    ○ Extract into independent functions
    ○ Split into multiple classes
    ○ Keep structure, only optimize naming
    [Enter custom answer]
```

**Note**: `todowrite` and `todoread` tools are disabled by default in subagents, but `question` tool is enabled by default.

### webfetch

Fetch web page content, supporting HTML, Markdown, plain text, and images.

```json
{
  "tools": {
    "webfetch": true
  }
}
```

::: details AI Call Parameters

| Parameter | Type | Required | Description |
|------|------|------|------|
| `url` | string | ✅ | URL to fetch (must start with http:// or https://) |
| `format` | string | ❌ | Return format: `markdown` (default), `text`, `html` |
| `timeout` | number | ❌ | Timeout in seconds (max 120, default 30) |

**Image Support** (v1.1.62+):
- When URL points to an image (image/*), automatically converted to base64 attachment
- SVG (image/svg+xml) and FastBidSheet (image/vnd.fastbidsheet) not supported

**HTML Conversion**:
- `format: "markdown"` - HTML automatically converted to Markdown
- `format: "text"` - Extracts plain text, removes script/style tags
- `format: "html"` - Returns raw HTML

**Limit**: Response size limit 5MB.

:::

### websearch (Experimental)

Search web content using OpenCode Exa AI service.

```json
{
  "tools": {
    "websearch": true
  }
}
```

> Requires setting environment variable OPENCODE_ENABLE_EXA=true or using OpenCode Zen hosted models.

### codesearch (Experimental)

Search codebases and online resources to find relevant APIs, libraries, and documentation.

```json
{
  "tools": {
    "codesearch": true
  }
}
```

> Requires setting environment variable OPENCODE_ENABLE_EXA=true or using OpenCode Zen hosted models.

::: details AI Call Parameters

| Parameter | Type | Default | Description |
|------|------|--------|------|
| `query` | string | Required | Search query, e.g., `"React useState hook examples"` |
| `tokensNum` | number | 2000+ | Number of tokens to return (1000-2000+) |

**tokensNum Selection Guide**:

| Value | Use Case |
|-----|---------|
| 1000-2000 | Precise queries, need only brief examples |
| 2000+ | Regular queries (default) |
| 10000-20000 | Need complete documentation |
| 30000-2000+ | Need comprehensive reference materials |

**Other Limits**: Request timeout 30 seconds.

:::

### batch (Experimental)

Execute multiple tool calls in parallel, reducing wait time. When AI needs to simultaneously read multiple files, execute multiple search commands, or other independent operations, batch can complete them all at once, 2-5x faster than sequential execution.

**How to Enable**:

```json
{
  "experimental": {
    "batch_tool": true
  }
}
```

::: details AI Call Parameters

**Parameter Structure**:

```typescript
{
  tool_calls: [
    { tool: "tool_name", parameters: { /* params */ } },
    { tool: "tool_name", parameters: { /* params */ } },
    // ... up to 25
  ]
}
```

**Actual Call Example**:

```json
[
  {"tool": "read", "parameters": {"filePath": "src/index.ts", "limit": 350}},
  {"tool": "grep", "parameters": {"pattern": "Session\\.updatePart", "include": "src/**/*.ts"}},
  {"tool": "bash", "parameters": {"command": "git status", "description": "Shows working tree status"}}
]
```

**Return Format**:

```json
{
  "title": "Batch execution (3/3 successful)",
  "output": "All 3 tools executed successfully.\n\nKeep using the batch tool for optimal performance in your next response!",
  "metadata": {
    "totalCalls": 3,
    "successful": 3,
    "failed": 0,
    "tools": ["read", "grep", "bash"],
    "details": [
      {"tool": "read", "success": true},
      {"tool": "grep", "success": true},
      {"tool": "bash", "success": true}
    ]
  }
}
```

:::

**Suitable for batch**:

| Scenario | Description |
|------|------|
| Reading multiple files simultaneously | Read package.json, tsconfig.json, .eslintrc.json at once |
| grep + glob + read combination | Search first then read, parallelize independent parts |
| Multiple bash commands | Execute git status, npm test simultaneously |
| Multiple edits | Modify different locations in multiple files simultaneously |

**Not suitable for batch**:

| Scenario | Reason |
|------|------|
| Operations with dependencies | Create file then read it, order not guaranteed |
| Stateful sequential operations | git add then git commit |

**Limits**:

| Limit Item | Value | Description |
|--------|-----|------|
| Max calls | 25 | Exceeded calls discarded with error |
| No nesting | batch | Cannot call batch within batch |
| External tools | Not supported | MCP tools cannot be executed through batch, need separate calls |
| Partial failure | Doesn't affect others | One call failing won't interrupt other parallel calls |

## Internal Implementation

Tools like grep, glob, and list use ripgrep under the hood. By default, ripgrep respects .gitignore patterns, so files and directories listed in .gitignore are excluded from searches and listings.

### Ignore Patterns

To include files that would normally be ignored, create a .ignore file in the project root:

```text
!node_modules/
!dist/
!build/
```

## Search Tool Usage Tips

These tips can help you write more precise prompts, enabling AI to find target code more efficiently.

### Differences Between Three Search Tools

| Scenario | Tool AI Will Use |
|------|---------------|
| Find usage examples for an API | codesearch (search online docs and examples) |
| Search for specific strings in local code | grep (regex match file contents) |
| Find files by filename | glob (pattern match file paths) |

### Combined Usage

Common combination strategies AI uses:

1. **First glob to find files, then grep to search content**
   ```
   You: Help me find where interface User is defined in all TypeScript files
   AI: First use glob to find *.ts files, then use grep to search "interface User"
   ```

2. **codesearch for examples, grep for local implementation**
   ```
   You: I want to know how to properly clean up React useEffect, then check if our project uses it correctly
   AI: First use codesearch to check docs, then use grep to search useEffect locally
   ```

### Pay Attention to Result Limits

**grep** and **glob** tools have a 100 result limit. If you notice AI saying "results truncated", you can:

- Ask AI to use more specific search conditions
- Specify a smaller directory scope
- Use more precise regular expressions

**codesearch** has no result count limit, but has a 30-second timeout.

## Related Resources

- [Custom Tools](/en/5-advanced/13-custom-tools.md) - Create custom tools
- [MCP Servers](/en/5-advanced/07a-mcp-basics.md) - Integrate external tools
- [Permissions](/en/5-advanced/05-permissions.md) - Control tool permissions
