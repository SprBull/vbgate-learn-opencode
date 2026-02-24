---
title: "Prompt Engineering Guidelines"
description: "Principles and best practices for writing high-quality prompts"
---

# Prompt Engineering Guidelines

> This document defines the prompt writing standards for OpenCode tutorials, ensuring all templates maintain consistent high quality.

---

## 🎯 Core Principles

### 1. Structure First

Every template must include clear structural hierarchy:

<!-- @click-to-copy -->
```
Role Definition → Task Description → Input Specification → Output Specification → Examples → Constraints
```

### 2. Few-shot Required (Example-Driven)

Complex tasks must provide 1-2 concrete examples to help the model understand the expected input/output format.

### 3. Explicit Chain of Thought

For reasoning tasks, explicitly guide step-by-step thinking: "analyze first, then output."

### 4. Quantified Criteria

Any scoring/evaluation must have clear scoring dimensions and definitions for each score range.

### 5. Graceful Degradation

Templates should include: how to handle incomplete input, how to clarify ambiguities, how to respond when beyond capability scope.

### 6. Self-Verification

Complex tasks should perform self-check before output to ensure requirements are met.

### 7. Consistent Placeholders

Use unified placeholder syntax throughout the document, clearly distinguishing required and optional fields.

---

## 📋 Standard Template Structure

<!-- @click-to-copy -->
```markdown
## Role
You are [professional identity], expert in [core capabilities]. [Additional identity anchoring description]

## Task
[Clear description of the task to complete]

## Input Information
### Required
- Variable Name: [Variable Description]

### Optional
- Variable Name: [Variable Description?] (Default: xxx)

## Output Specification
Output in the following structure:
1. [Output Item 1]
2. [Output Item 2]
...

## Example

### Input
[Specific input example]

### Output
[Corresponding ideal output]

## Constraints
- ✅ Should: [Positive behavior]
- ❌ Avoid: [Negative behavior]

## Self-Check List
Confirm before completion:
- [ ] [Check Item 1]
- [ ] [Check Item 2]

## Error Handling
- If missing key information, ask the user first
- If task is out of scope, explain why and suggest alternatives
```

---

## 🏷️ Placeholder Specification
<AdInArticle />

### Syntax

| Type | Syntax | Example |
|------|------|------|
| **Required Variable** | `[Variable Name]` | `[Programming Language]` |
| **Optional Variable** | `[Variable Name?]` | `[Framework?]` |
| **With Default Value** | `[Variable Name=Default]` | `[Style=Casual]` |
| **Choose One** | `[Option1/Option2/Option3]` | `[Fantasy/Urban/Romance]` |
| **Text Block** | `[Paste Area Description]` | `[Paste Code]` |

### Example Comparison

**❌ Poor Writing**:
```
Type: Fantasy/Urban/Romance
Language: Language
Paste code
```

**✅ Good Writing**:
```
Type: [Fantasy/Urban/Romance/Mystery/Sci-Fi]
Language: [Programming Language]

[Paste Code]
```

---

## 📊 Scoring Criteria Specification

Any template using scoring must define scoring criteria:

### Example: Code Quality Scoring

| Score | Readability | Performance | Security | Test Coverage |
|------|--------|------|--------|---------|
| 9-10 | Clear naming, complete comments | O(n) or better | No vulnerabilities | >90% |
| 7-8 | Reasonable naming, key comments | O(n log n) | Low risk | 70-90% |
| 5-6 | Basically readable | O(n²) | Medium risk | 50-70% |
| <5 | Hard to understand | O(n³)+ | High risk | <50% |

**Composite Score Calculation**: Readability×0.3 + Performance×0.3 + Security×0.25 + Test Coverage×0.15

---

## 👤 Role Definition Specification

### Elements

1. **Professional Identity**: Who you are
2. **Core Capabilities**: What you're expert at
3. **Service Target**: Who you serve (optional)
4. **Style Characteristics**: Working style (optional)

### Example

**❌ Poor Writing**:
```
You are an assistant.
```

**✅ Good Writing**:
```
You are a senior technical documentation engineer, expert at explaining complex code in easy-to-understand terms.
Your explanations have been praised by beginners as "finally understood."
```

---

## ⚖️ Constraints Specification

Use ✅ and ❌ to clearly distinguish positive and negative behaviors:

```markdown
## Constraints
- ✅ Questions should be specific to line numbers
- ✅ Every issue should have a fix suggestion
- ✅ Acknowledge what was done well
- ❌ Avoid substituting subjective preferences for objective standards
- ❌ Avoid criticizing without providing solutions
```

---

## 🔧 Error Handling Specification

Every template should include an error handling section:

<!-- @click-to-copy -->
```markdown
## Error Handling
- If information is insufficient, list what needs to be added and explain why
- If the problem is beyond capability scope, explain and suggest help channels
- If there are multiple independent issues, suggest handling them one by one
```

---

## ✅ Self-Check List Specification

Complex tasks should include a self-check list:

<!-- @click-to-copy -->
```markdown
## Self-Check List
Confirm before completion:
- [ ] Every protagonist has a clear arc
- [ ] The pacing of introduction, development, climax, and resolution is reasonable
- [ ] The core conflict runs through the entire text
- [ ] The highlights are enough to attract target readers
```

---

## 🤖 Agent/Skill Description Specification

### Structure Template

<!-- @click-to-copy -->
```yaml
description: |
  [One sentence explaining core capability]
  Provides: [Resources included in this Skill]
  Suitable for: [Trigger scenario 1], [Trigger scenario 2]
  Not suitable for: [Boundary scenario 1], [Boundary scenario 2]
```

### Example

**❌ Poor Writing**:
```yaml
description: Code review expert
```

**✅ Good Writing**:
```yaml
description: |
  Code review expert, focused on security vulnerabilities, performance issues, code quality.
  Suitable for: PR review, code health check, security audit.
  Not suitable for: code generation, feature implementation, test writing.
```

---

## 📝 Checklist

Before publishing a template, confirm the following:

- [ ] Has clear role definition
- [ ] Input information distinguishes required/optional
- [ ] Has complete output specification
- [ ] Complex tasks have Few-shot examples
- [ ] Scoring types have quantified criteria
- [ ] Has constraints (✅/❌)
- [ ] Has error handling mechanism
- [ ] Placeholder syntax is unified
- [ ] No format errors

---

## Related Resources

- [Prompt Template Library](/en/appendix/prompts) - Ready-to-use templates
- [Agent Quick Start](/en/5-advanced/02a-agent-quickstart) - Create Agents
- [Skill Basics](/en/5-advanced/03a-skills-basics) - Create Skills
