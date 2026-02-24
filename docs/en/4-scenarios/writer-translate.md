---
title: "A5 Multilingual Translation & Refinement"
subtitle: "Batch translation, glossaries, and rewriting"
course: "OpenCode Practical Course"
stage: "Phase 4"
lesson: "A5"
duration: "15 minutes"
practice: "20 minutes"
level: "Advanced"
description: "Use AI for batch translation, refinement, and rewriting across multiple languages. Build glossaries to maintain consistency and boost multilingual content production."
tags:
  - "Translation"
  - "Refinement"
  - "Rewriting"
prerequisite:
  - "A1 Writing Workflow"
---

# A5 Multilingual Translation & Refinement

> 💡 **One-liner**: Use AI for translation, refinement, and rewriting while maintaining terminology consistency.

## 📝 Course Notes

Key takeaways from this lesson:

<img src="/images/4-scenarios/writer-translate-notes.mini.jpeg"
     alt="A5 Translation Notes"
     data-zoom-src="/images/4-scenarios/writer-translate-notes.jpeg" />

---

## What You'll Be Able to Do

- Translate full documents or sections with AI
- Maintain consistency in technical terminology
- Refine text to improve readability
- Rewrite content to reduce similarity

---

## Why OpenCode Instead of Web-based AI?

| Capability | Web-based AI | OpenCode |
|-----|----------|----------|
| Batch Translation | ❌ Copy-paste section by section | ✅ Multi-file batch processing, format preserved |
| Terminology Consistency | ❌ AI may translate differently each time | ✅ @glossary reference, unified across document |
| Long Document Handling | ❌ Easily exceeds context limits | ✅ Section-by-section translation, auto-merge |
| Format Preservation | ❌ Format often lost | ✅ Direct file editing, original format retained |
| Version Comparison | ❌ | ✅ Git tracks translation history |

---

## Your Current Pain Points

- Inconsistent terminology in translated articles
- Unstable quality for long document translations
- Need to reduce similarity but manual rewriting is exhausting

---

## When to Use This Technique

- When you need: High-quality translation or rewriting
- And you don't want to: Spend hours manually adjusting every word

---

## 🎒 Before You Start

> Make sure you've completed the following:

- [ ] Completed [A1 Writing Workflow](./writer-workflow)
- [ ] Have text that needs translation or refinement

---

## Core Concept

### Translation Workflow

```
Glossary Preparation → Section Translation → Terminology Unification → Final Review
```

### Translation vs Refinement vs Rewriting

| Task | Purpose | Typical Scenario |
|-----|------|---------|
| Translation | Cross-language conversion | Translate English paper to Chinese |
| Refinement | Improve expression quality | Enhance article readability |
| Rewriting | Change expression, keep content | Plagiarism check, derivative works |

---

## Follow Along

<AdInArticle />

### Step 1: Prepare a Glossary

**Why**  
Consistent terminology is key to professional translation.

Switch to Build mode:

```
I need to translate a machine learning paper from English.
Help me create a glossary with Chinese translations for these common terms:
- Neural Network
- Deep Learning
- Gradient Descent
- Overfitting
- Regularization

Save as glossary.md
```

### Step 2: Section-by-Section Translation

**Why**  
Breaking long documents into sections maintains quality.

```
@glossary.md

Please translate the following English paragraph with these requirements:
1. Use standard translations from the glossary
2. Maintain academic writing style
3. Ensure natural, flowing sentences

Original text:
{paste English paragraph}
```

### Step 3: Full Document Translation

**Why**  
Smaller files can be translated in one go.

```
@glossary.md @paper.txt

Translate paper.txt into Chinese with these requirements:
1. Use standard glossary translations
2. Preserve original paragraph structure
3. Save as paper_cn.md
```

### Step 4: Refine for Readability

**Why**  
Translations usually need refinement.

```
@paper_cn.md 

Please refine this translation with these requirements:
1. Fix awkward sentences
2. Maintain academic rigor while improving readability
3. Check terminology consistency
4. Edit the file directly
```

### Step 5: Rewrite to Reduce Similarity

**Why**  
Some scenarios require lower similarity scores.

```
Please rewrite the following paragraph to reduce similarity:
1. Keep the original meaning intact
2. Use different expressions
3. Output 3 versions to choose from

Original text:
{paste paragraph needing rewrite}
```

---

## 📋 Magic Prompts

### 🌐 Professional Multilingual Translation
> Expected result: High-quality translation with consistent terminology

```
## Role
You are a professional translator skilled in making translations natural and fluent while preserving original meaning.

## Task
Translate the user-provided text into the target language.

## Input Information
### Required
- Target language: 【Simplified Chinese / English / Japanese / Spanish / French / German / ...】
- Original text:

[Paste original text]

### Optional
- Glossary: @【glossary file?】
- Domain: 【Technical / Legal / Medical / Literary?】
- Tone style: 【Formal / Casual / Professional?】

## Translation Requirements
1. **Terminology Consistency**: Use standard translations from the glossary
2. **Format Preservation**: Maintain original paragraphs, headings, and list structure
3. **Natural Flow**: Don't translate word-by-word; make the translation read naturally
4. **Proper Nouns**: Add original text in parentheses on first occurrence (e.g., Machine Learning 机器学习)

## Output Format
### Translation
[Translation result]

### Translation Notes (if any)
- Polysemy handling: 【word】translated as【translation】, because【reason】
- Terminology confirmation: 【term】uses【translation】, per glossary

## Constraints
- ✅ Terminology consistency throughout (same term = same translation)
- ✅ Readability over word-for-word faithfulness
- ✅ Use domain-standard translations for technical terms
- ❌ Avoid translationese (awkward phrasing from literal translation)
- ❌ Don't omit original content

## Error Handling
- If target language not provided, ask the user first
- If encountering polysemous words, note possible translations for user to choose
- If a term isn't in the glossary, use common translation and flag it
```

### ✏️ Rewriting for Similarity Reduction
> Expected result: Multiple rewritten versions maintaining original meaning

```
## Role
You are a professional editor skilled at changing expressions while preserving meaning.

## Task
Rewrite the user-provided text to reduce similarity with the original.

## Input Information
### Required
- Rewrite level: 【Light (30%) / Medium (50%) / Heavy (70%)】
- Original text:

[Paste original text]

### Optional
- Keywords to preserve: 【terms that must stay?】
- Style requirement: 【Academic / Casual / Formal?】

## Rewrite Strategies
### Light Rewrite (~30%)
- Synonym replacement
- Minor word order adjustments
- Keep core expressions

### Medium Rewrite (~50%)
- Sentence structure changes
- Active/passive voice conversion
- Merge/split sentences

### Heavy Rewrite (~70%)
- Reorganize paragraph logic
- Express same meaning differently
- Add/remove descriptive details

## Output Format
### Version 1
[Rewritten text]

### Version 2
[Alternative rewrite]

### Version 3
[Third rewrite approach]

---

### Rewrite Statistics
| Version | Estimated Change | Main Techniques Used |
|---------|-----------------|---------------------|
| Version 1 | X% | 【technique】 |
| Version 2 | X% | 【technique】 |
| Version 3 | X% | 【technique】 |

**Recommended Version**: Version【N】
**Reason**: 【reason】

## Constraints
- ✅ Preserve original meaning
- ✅ Keep technical terms accurate
- ✅ Make each version distinctly different
- ❌ Don't change core viewpoints
- ❌ Don't introduce information not in the original
```

---

## Checklist ✅

> Must complete all before moving on

- [ ] Created a glossary
- [ ] Used @ to reference glossary during translation
- [ ] Completed refinement edits
- [ ] Can generate rewritten versions

---

## Common Pitfalls

| Issue | Cause | Solution |
|-----|-----|-----|
| Inconsistent terminology | No glossary | Create glossary first, @ reference during translation |
| Quality drops in long texts | Too much at once | Translate section by section, ~2000+ words each |
| Meaning changed after rewrite | Too aggressive | Specify "preserve original meaning" |

---

## Lesson Summary

You learned:

1. Translation workflow (glossary → section translation → unification → refinement)
2. Using @ to reference glossaries for consistency
3. Refinement and rewriting techniques

---

## Next Lesson Preview

> Next, we'll dive into advanced content — Fiction Writing, learning multi-file management, character card design, and maintaining character consistency.

---

📚 **More Complete Templates**: [Prompt Template Library](../appendix/prompts)
