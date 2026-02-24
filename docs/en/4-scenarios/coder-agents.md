---
title: "B5 Dedicated Development Agents"
subtitle: "Create Code Reviewer, Security Auditor"
course: "OpenCode Practical Course"
stage: "Phase 4"
lesson: "B5"
duration: "25 minutes"
practice: "30 minutes"
level: "Advanced"
description: "Create dedicated Code Reviewer and Security Auditor agents to automate code review and security checks."
tags:
  - Agent
  - Code Review
  - Security Audit
prerequisite:
  - "B1 Development Daily"
  - "3.2 Understanding Agents"
---

# B5 Dedicated Development Agents

> 💡 **One-line summary**: Create dedicated development agents like Code Reviewer, Security Auditor, and Test Writer.

## 📝 Course Notes

Key takeaways from this lesson:

<img src="/images/4-scenarios/coder-agents-notes.mini.jpeg"
     alt="B5 Dedicated Development Agents - Course Notes"
     data-zoom-src="/images/4-scenarios/coder-agents-notes.jpeg" />

---

## What You'll Be Able to Do

- Create a Code Reviewer Agent
- Create a Security Auditor Agent
- Create a Test Writer Agent
- Combine multiple agents into a development workflow

---

## Your Current Pain Points

- You have to do code review, security checks, and test generation yourself
- You need to tell the AI what standards to use for review every time
- You want multiple "experts" to collaborate but don't know how to implement it

---

## When to Use This Technique

- When you need: Use specialized agents to improve development quality
- And you don't want: Repeatedly input review standards every time

---

## 🎒 Prerequisites

> Make sure you've completed the following:

- [ ] Completed [B1 Development Daily](./coder-daily)
- [ ] Completed [3.2 Understanding Agents](../3-workflow/02-agents)

---

## Core Concept

### Development Agent Matrix

| Agent | Responsibility | Use Case |
|-------|---------------|----------|
| Code Reviewer | Code review | PR review, self-check |
| Security Auditor | Security audit | Pre-release check |
| Test Writer | Test generation | Test coverage supplement |
| Doc Writer | Documentation | Comments, README |

---

## Follow Along

### Step 1: Create Code Reviewer Agent

**Why**  
A professional code review agent can discover more issues.

```bash
mkdir -p ~/.config/opencode/agent
```

> Agent configuration file locations:
> - Global: `~/.config/opencode/agent/`
> - Project-level: `.opencode/agent/`
>
> The agent's invocation name defaults to the filename: for example, `code-reviewer.md` corresponds to `@code-reviewer`.

Create the configuration:

```
Help me create a Code Reviewer Agent, save to ~/.config/opencode/agent/code-reviewer.md:

---
description: Strict code review expert
mode: subagent
model: anthropic/claude-opus-4-5-thinking
temperature: 0.3
permission:
  edit: deny
  bash: deny
---


# Code Reviewer Agent

You are an experienced senior engineer specializing in code review.

## Review Checklist

### Code Quality
- [ ] Single responsibility per function
- [ ] Clear and accurate naming
- [ ] No duplicate code
- [ ] Appropriate comments

### Potential Issues
- [ ] Boundary condition handling
- [ ] Complete error handling
- [ ] No memory leak risks
- [ ] No race conditions

### Maintainability
- [ ] Code is easy to understand
- [ ] Good testability
- [ ] Follows project conventions

## Output Format

For each issue, output in the following format:
- **Location**: filename:line_number
- **Issue**: description of the problem
- **Severity**: High / Medium / Low
- **Suggestion**: fix recommendation
```

Sources (Agent Markdown field and tools syntax examples):
- `opencode/packages/web/src/content/docs/agents.mdx:163`
- `opencode/packages/web/src/content/docs/agents.mdx:167`
- `opencode/packages/web/src/content/docs/agents.mdx:169`

### Step 2: Create Security Auditor Agent
<AdInArticle />

**Why**  
Security audits require a specialized perspective.

```
Help me create a Security Auditor Agent, save to ~/.config/opencode/agent/security-auditor.md:

---
description: Security vulnerability hunter
mode: subagent
model: anthropic/claude-opus-4-5-thinking
temperature: 0.2
permission:
  edit: deny
  bash: deny
---

# Security Auditor Agent

You are a security expert specializing in discovering security vulnerabilities in code.

## Check Items

### Input Validation
- SQL injection
- XSS attacks
- Command injection
- Path traversal

### Authentication & Authorization
- Authentication bypass
- Privilege escalation
- Session management

### Sensitive Data
- Hardcoded secrets
- Sensitive information leakage
- Insecure storage

### Dependency Security
- Known vulnerable dependencies
- Outdated package versions

## Output Format

For each security issue:
- **Vulnerability Type**: OWASP classification
- **Location**: filename:line_number
- **Risk Level**: Critical/High/Medium/Low
- **Description**: vulnerability description
- **Fix Suggestion**: how to fix
- **Reference**: relevant CWE/CVE
```

### Step 3: Create Test Writer Agent

**Why**  
A dedicated test agent can generate more comprehensive tests.

```
Help me create a Test Writer Agent, save to ~/.config/opencode/agent/test-writer.md:

---
description: Test case expert
mode: subagent
model: anthropic/claude-opus-4-5-thinking
temperature: 0.4
permission:
  edit: deny
  bash: deny
---

# Test Writer Agent

You are a testing expert skilled at designing and writing test cases.

## Test Strategy

1. **Unit Tests**: Isolate and test each function
2. **Integration Tests**: Test module interactions
3. **Boundary Tests**: Test boundary conditions
4. **Exception Tests**: Test error handling

## Test Coverage

Each function must cover:
- Normal inputs
- Boundary values (max, min, threshold)
- Invalid inputs (null, undefined, wrong type)
- Exception cases (network errors, timeouts)

## Output Format

Use the project's test framework to generate runnable test code.
```

### Step 4: Use Dedicated Agents

**Why**  
Invoke dedicated agents to complete tasks.

Restart OpenCode:

```bash
opencode
```

Invoke Code Reviewer:

```
@code-reviewer @src/services/auth.ts Please review this authentication module
```

Invoke Security Auditor:

```
@security-auditor @src/controllers/ Perform a security audit on this directory
```

Invoke Test Writer:

```
@test-writer @src/utils/validate.ts Generate complete test cases for this file
```

### Step 5: Combine into a Workflow

**Why**  
Multiple agents working together is more efficient.

Create a comprehensive review command `.opencode/command/comprehensive-review.md`:

```
---
description: Comprehensive code review
---

Please execute in order:
1. @code-reviewer review code quality
2. @security-auditor check security risks
3. @test-writer analyze test coverage

Target file: $ARGUMENTS

Finally, summarize all issues and sort by priority.
```

Sources (custom command directory and parameter placeholder):
- `opencode/packages/web/src/content/docs/commands.mdx:20`
- `opencode/packages/web/src/content/docs/commands.mdx:113`
- `opencode/packages/opencode/src/config/config.ts:191`
- `opencode/packages/opencode/src/command/index.ts:49`

Usage:

```
/comprehensive-review src/services/payment.ts
```

---

## Checkpoint ✅

> Must pass all items to continue

- [ ] Created Code Reviewer Agent
- [ ] Created Security Auditor Agent
- [ ] Created Test Writer Agent
- [ ] Can invoke with @agent-name

---

## Common Pitfalls

| Symptom | Cause | Solution |
|---------|-------|----------|
| @agent-name doesn't respond | Invocation name doesn't match filename (or typo) | Confirm filename (without .md) is the invocation name, e.g., `code-reviewer.md` → `@code-reviewer` |
| Agent configuration doesn't take effect | Config file not in agent directory | Put in `~/.config/opencode/agent/` (global) or `.opencode/agent/` (project-level) |
| Multiple agents give inconsistent results | Each executes independently | Chain with command and summarize together |

---

## Lesson Summary

You learned:

1. Create Code Reviewer Agent
2. Create Security Auditor Agent
3. Create Test Writer Agent
4. Combine multiple agents into a workflow

---

## Next Lesson Preview

> Next lesson we'll learn **[B6 Intranet/Offline Deployment](./coder-intranet)**.
>
> You'll learn:
> - Run OpenCode in enterprise intranet environment
> - Disable all external network requests
> - Configure internal AI gateway
