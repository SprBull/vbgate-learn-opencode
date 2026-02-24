---
title: "B2 Refactoring & Testing"
subtitle: "Identify code smells, safe refactoring, test generation"
course: "OpenCode Practical Course"
stage: "Stage 4"
lesson: "B2"
duration: "20 min"
practice: "25 min"
level: "Advanced"
description: "Use AI to identify code smells, safely refactor code structure, and automatically generate test cases to improve code quality."
tags:
  - "Refactoring"
  - "Testing"
  - "Code Quality"
prerequisite:
  - "B1 Daily Development"
---

# B2 Refactoring & Testing

> 💡 **One-liner**: Use AI to identify code smells, refactor safely, and automatically generate test cases.

## 📝 Course Notes

Key takeaways from this lesson:

<img src="/images/4-scenarios/coder-refactor-notes.mini.jpeg"
     alt="B2 Refactoring & Testing Notes"
     data-zoom-src="/images/4-scenarios/coder-refactor-notes.jpeg" />

---

## What You'll Be Able to Do

- Let AI identify "code smells" in your code
- Safely refactor code
- Automatically generate unit tests
- Analyze edge cases and supplement tests

---

## Your Current Struggles

- Code gets messier over time, but you're afraid to change it
- Want to refactor but lack test coverage
- Too few test cases, can't improve coverage

---

## When to Use This Technique

- When you need to: Improve code quality and test coverage
- And don't want to: Manually write numerous test cases

---

## 🎒 Before You Start

> Make sure you've completed the following:

- [ ] Completed [B1 Daily Development](./coder-daily)
- [ ] Have a code file that needs refactoring or testing

---

## Core Concepts

### Safe Refactoring in Three Steps

```
1. Tests first → 2. Small refactoring steps → 3. Tests pass
```

### Code Smells Overview

| Code Smell | Symptoms (Experience Signals) | Refactoring Direction |
|-------|----------------|---------|
| Long Function | Can't see the whole thing at a glance, mixing multiple concerns | Extract function / Split responsibilities |
| Too Many Parameters | Callers struggle to remember what each parameter means | Introduce Parameter Object / Split function |
| Duplicated Code | Similar logic appears in multiple places | Extract common function |
| Deep Nesting | Reading code requires repeatedly tracing back through conditions | Early return / Extract conditional logic |
| Unclear Naming | Can't tell purpose from the name | Rename |

---

## Follow Along

<AdInArticle />

### Step 1: Identify Code Smells

**Why**
Diagnose first, then treat.

Switch to Plan Agent:

```
@src/utils/data.ts Please analyze the code quality of this file:
1. List discovered "code smells"
2. Severity of each issue (High/Medium/Low)
3. Recommended refactoring approaches
4. Priority suggestions for refactoring
```

### Step 2: Generate Tests First

**Why**
Tests enable safe refactoring.

Switch to Build Agent:

```
@src/utils/data.ts Generate unit tests for this file:
1. Use Vitest framework
2. Cover all exported functions
3. Include normal cases and edge cases
4. Save as src/utils/data.test.ts
```

### Step 3: Safe Refactoring

**Why**
Small steps, verify each step.

```
@src/utils/data.ts Please refactor the parseUserData function:
- Issue: Function is too long (50 lines), single responsibility violation
- Requirements: Split into 3 smaller functions
- Keep the public interface unchanged
- Run tests after refactoring to confirm
```

### Step 4: Supplement Edge Case Tests

**Why**
Edge cases are often bug-prone areas.

```
@src/utils/data.ts @src/utils/data.test.ts

Analyze the code's edge cases and supplement the following tests:
1. Empty inputs (null, undefined, empty arrays)
2. Extreme values (very large numbers, very long strings)
3. Type errors (passing wrong types)
4. Concurrency scenarios (if async operations exist)
```

### Step 5: Run Tests to Verify

**Why**
Confirm refactoring didn't break functionality.

> In OpenCode TUI, messages starting with `!` execute shell commands and bring output into the conversation: https://opencode.ai/docs/tui

```
!npm test src/utils/data.test.ts
```

**You should see**: All tests pass

---

## 📋 Magic Prompts

### ✅ Code Review
> Expected outcome: Comprehensive analysis of code quality issues with improvement suggestions

```
## Role
You are a Tech Lead responsible for code quality. Your review style is strict but constructive.

## Task
Perform a comprehensive review of submitted code, identify issues, and provide improvement suggestions.

## Input
### Required
- Programming Language: [Language]
- Code: @[File Path] or [Paste Code]

### Optional
- Review Focus: [What aspects to focus on?]
- Project Context: [What is the code's context?]

## Review Dimensions
1. **Code Quality**: Naming conventions, code structure, readability, duplicated code
2. **Potential Issues**: Bug risks, edge cases, error handling, performance issues
3. **Security Concerns**: Input validation, sensitive information, injection risks
4. **Best Practices**: Design patterns, SOLID principles, test coverage

## Output Format
### Review Summary
- **Code Rating**: A(Excellent)/B(Good)/C(Average)/D(Needs Refactoring)
- **One-liner Comment**
- **Must Fix Before Merge**: Yes/No

### Issues List
- 🔴 **Critical Issues**: `[File:Line]` Issue + Risk + Suggestion
- 🟡 **Suggested Improvements**: Issues recommended to fix
- 🟢 **Strengths**: Things worth keeping

## Constraints
- ✅ Issues should be specific to line numbers
- ✅ Every issue should have a fix suggestion
- ✅ Acknowledge what's done well
- ❌ Avoid replacing objective standards with subjective preferences
- ❌ Avoid criticism without solutions
```

### 🧪 Test Generation
> Expected outcome: Generate comprehensive unit tests covering edge cases

```
## Role
You are a QA Engineer skilled at designing comprehensive test cases covering normal flows and edge cases.

## Task
Generate unit tests for the function or module provided by the user.

## Input
### Required
- Programming Language: [Language]
- Code: @[File Path] or [Paste Code]

### Optional
- Test Framework: [Jest/Vitest/Pytest/JUnit?] (Default: auto-detect)
- Test Style: [BDD describe/it style?]

## Output Format
Use AAA Pattern (Arrange-Act-Assert), covering:
1. **Happy Path** (Normal flow)
2. **Edge Cases** (Null values, extremes, boundary points)
3. **Exception Cases** (Invalid input, thrown exceptions)
4. **Async Operations** (If Promise/async exists)

Each test case should include:
- Clear naming (describing test intent)
- Necessary comments (explaining test scenario)

## Constraints
- ✅ Test case names should clearly express test intent
- ✅ Cover main edge cases
- ✅ Test code should be directly runnable
- ❌ Avoid testing implementation details
- ❌ Avoid dependencies between test cases
```

### 🔧 Refactoring Suggestions
> Expected outcome: Provide safe refactoring plan to reduce change risk

```
## Role
You are a Refactoring Expert skilled at identifying code smells and providing safe refactoring plans.

## Task
Analyze code issues and provide safe refactoring steps and suggestions.

## Input
### Required
- Code: @[File Path] or [Paste Code]

### Optional
- Known Issues: [What problems have you noticed?]
- Refactoring Goal: [What effect do you want to achieve?]

## Output Format
1. **Current Problem Analysis**
   - Discovered code smells (Long Function/Too Many Parameters/Deep Nesting/Duplicated Code/Unclear Naming)
   - Severity of each issue (High/Medium/Low)

2. **Recommended Refactoring Steps** (in order)
   - What to do in each step
   - Risk assessment for each step
   - How to verify step success

3. **Tests to Add**
   - Tests that should exist before refactoring
   - Tests to add after refactoring

4. **Expected Results After Refactoring**
   - Code quality improvements
   - Maintainability improvements

## Constraints
- ✅ Small refactoring steps, each verifiable
- ✅ Keep public interface unchanged
- ✅ Tests before refactoring
- ❌ Avoid changing too much at once
- ❌ Avoid changing business logic
```


---

## Checklist ✅

> All items must pass to continue

- [ ] Identified code smells using AI
- [ ] Generated unit tests
- [ ] Completed safe refactoring
- [ ] All tests pass

---

## Common Pitfalls

| Symptom | Cause | Solution |
|-----|-----|-----|
| Functionality broken after refactoring | No tests written first | Generate tests before refactoring |
| Low test coverage | Only testing normal cases | Add edge case and exception tests |
| Inaccurate smell detection | Code snippet too small | Give AI complete file context |

---

## Lesson Summary

You learned:

1. Using AI to identify code smells
2. Safe refactoring flow with tests first
3. Automatically generating unit tests
4. Analyzing and supplementing edge case tests

---

## Next Lesson Preview

> Next lesson we'll learn about documentation automation and Git collaboration techniques.

---

📚 **More Complete Templates**: [Prompt Template Library](../appendix/prompts)
