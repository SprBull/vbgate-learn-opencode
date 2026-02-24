---
title: "A6 Novel Writing (Advanced)"
subtitle: "Multi-file management, character cards, character consistency"
course: "OpenCode Practical Course"
stage: "Stage 4"
lesson: "A6"
duration: "25 minutes"
practice: "30 minutes"
level: "Advanced"
description: "Use OpenCode to manage novel multi-file chapters, maintain character cards, and keep character consistency to improve novel writing efficiency."
tags:
  - novel
  - character
  - plot
  - dialogue
prerequisite:
  - A1 Writing Workflow
---

# A6 Novel Writing (Advanced)

> 💡 **One-sentence summary**: Use AI to help conceptualize world-building, design characters, develop plots, and write dialogue.

## 📝 Course Notes

Key takeaways from this lesson:

<img src="/images/4-scenarios/writer-novel-notes.mini.jpeg"
     alt="A6 Novel Writing (Advanced) Course Notes"
     data-zoom-src="/images/4-scenarios/writer-novel-notes.jpeg" />

<!-- 📹 Demo placeholder: Novel writing demo -->
<!-- TODO: Record demo GIF -->
<!-- ![Novel writing demo](/images/4-scenarios/writer-novel-demo.gif) -->

---

## What You'll Be Able to Do

- Use AI to conceptualize story outlines and world-building
- Design three-dimensional characters using character card templates
- Use AI to help develop plots and design conflicts
- Write dialogue with distinctive styles

---

## Why Use OpenCode Instead of Web-based AI?

| Capability | Web-based AI | OpenCode |
|-----|----------|----------|
| Multi-file management | ❌ Only in one conversation | ✅ Outlines, character cards, chapters stored separately |
| Character consistency | ❌ Easy to forget settings in long works | ✅ Reference with @character-card, AI always remembers |
| World-building management | ❌ Redescribe every time | ✅ AGENTS.md solidifies settings |
| Chapter versioning | ❌ | ✅ Git tracks modification history of each chapter |
| Cross-chapter search | ❌ | ✅ Full project search for characters/plots |

---

## Your Current Struggle

- Have story ideas but don't know how to develop them into complete plots
- Characters experience "personality collapse" as you write
- Dialogue is too flat, lacking character distinctiveness

---

## When to Use This Technique

- When you need to: Create a novel with complete world-building and three-dimensional characters
- And don't want to: Discover plot logic holes halfway through writing

---

## 🎒 Before You Start

> Make sure you have completed the following:

- [ ] Completed [A1 Writing Workflow](./writer-workflow)
- [ ] Have a preliminary idea for a novel

---

## Core Concept

### Novel Writing Quartet

| Stage | Content | AI Assistance Method |
|-----|------|-----------|
| Conceptualize | World-building, timeline, core conflict | Discuss in Plan mode |
| Character | Character cards, relationship maps, character arcs | Generate with templates |
| Plot | Chapter outlines, scene design, foreshadowing | Plan chapter by chapter |
| Execute | Write dialogue, describe scenes | Output in Build mode |

---

## Follow Along

### Step 1: Conceptualize the Story Outline

**Why**  
Build the skeleton first, then add flesh and blood.

Switch to Plan mode and enter:

```
I want to write an urban suspense novel:
- Background: A series of disappearances at a tech company
- Protagonist: A programmer with social anxiety
- Core mystery: All missing persons were using the same APP

Please help me design:
1. The three-act structure of the story
2. Core conflicts and turning points
3. Several possibilities for the ending
```

### Step 2: Design Main Characters

**Why**  
Three-dimensional characters give the story life.

Enter:

```
Based on the story above, help me design the protagonist's character card, including:
- Basic info (name, age, occupation)
- Physical appearance
- Personality traits (at least 3 positive, 2 negative)
- Backstory
- Core motivation
- Character arc (from what state to what state)
```

::: tip 💡 Save Character Card
Switch to Build mode and have AI save the character card as `characters/protagonist.md` for easy reference later.
:::

### Step 3: Design Chapter Outline

<AdInArticle />

**Why**  
Having an outline maintains plot coherence.

Enter:

```
Based on the three-act structure, help me design an outline for the first 5 chapters, each containing:
- Chapter title
- Main scenes
- Chapter objective (what plot to advance/what information to reveal)
- End-of-chapter suspense
```

### Step 4: Write Chapter One

**Why**  
Start actual creation.

Switch to Build mode:

```
@characters/protagonist.md Based on the character settings and chapter one outline, write the complete first chapter.
Requirements:
- First-person perspective
- Start with an engaging scene
- Around 3000 words
- Save as chapters/chapter-one.md
```

### Step 5: Write Character Dialogue

**Why**  
Dialogue is key to revealing character personality.

```
@characters/protagonist.md @characters/supporting-character.md Write a dialogue scene between the protagonist and supporting character:
- Scene: First meeting in the company corridor
- Purpose: Hint that the supporting character knows some secrets
- Style: Protagonist stutters nervously, supporting character acts casual
```

---

## 📋 Magic Prompts

### 👤 Character Card Generation
> Expected effect: Generate complete character cards with personality, background, and motivation

```
## Role
You are a senior novel editor skilled at creating three-dimensional, deep character images.

## Task
Generate a complete character card based on the basic information provided by the user.

## Input Information
### Required Fields
- Name: [Character Name]
- Identity: [Occupation/Identity]

### Optional Fields
- Age: [Age?]
- Story Type: [Fantasy/Urban/Romance/Suspense?]
- Character Position: [Protagonist/Antagonist/Supporting?]
- Special Requirements: [Other requirements?]

## Output Specification
### 1. Physical Description (around 100 words)
> Focus on the most distinctive features

### 2. Personality Spectrum
| Positive Traits | Negative Traits |
|---------|---------|
| Trait 1 + Specific manifestation | Flaw 1 + Specific manifestation |
| Trait 2 + Specific manifestation | Flaw 2 + Specific manifestation |
| Trait 3 + Specific manifestation | |

### 3. Backstory (around 200 words)
> Core experiences that shape character motivation

### 4. Core Motivation
- **External Goal**: What he/she wants
- **Internal Need**: What he/she truly lacks

### 5. Fatal Weakness
> What makes him/her vulnerable

### 6. Signature Traits
- Catchphrase:
- Signature gesture:

### 7. Character Arc
> From [starting state] → to [ending state]

## Constraints
- ✅ Physical description should be vivid
- ✅ Personality traits should have contradictions (not a perfect person)
- ✅ Backstory should explain the origin of personality
- ❌ Avoid stereotypes (all good or all bad)
- ❌ Avoid being too similar to mainstream characters
```

### 📖 Chapter Outline Generation
> Expected effect: Generate chapter outlines with scenes, conflicts, and suspense

```
## Role
You are a senior novel editor skilled at structural design and pacing control.

## Task
Generate detailed outlines for specified chapters based on the story background.

## Input Information
### Required Fields
- Story Synopsis: [Story Synopsis]
- Chapter Number: Chapter [N]

### Optional Fields
- Previous Chapter Summary: [What happened in the previous chapter?]
- Chapter Objective: [What plot needs to be advanced?]
- Involved Characters: @[Character card file?]

## Output Specification
### Chapter Title
> [Attractive title]

### Opening Scene
- Time:
- Location:
- Atmosphere:

### Main Events in This Chapter (3-5)
1. Event 1: [Description]
2. Event 2: [Description]
3. ...

### Chapter Conflict Points
- **External Conflict**: [Description]
- **Internal Conflict**: [Description]

### Character Emotional Changes
| Character | Starting State | Ending State |
|------|---------|---------|

### End-of-Chapter Suspense/Hook
> [Design that makes readers want to read the next chapter]

### Connection to Main Plot
> How this chapter advances the main storyline

## Constraints
- ✅ Each chapter should have an independent mini-climax
- ✅ Must have suspense at the end of the chapter
- ✅ Logical coherence with preceding and following chapters
- ❌ Avoid piling up events without focus
- ❌ Avoid disconnecting from the main plot
```

### 💬 Dialogue Polishing
> Expected effect: Polish dialogue to better fit character personality and have more tension

```
## Role
You are a professional novel dialogue editor skilled at making dialogue vivid, layered, and full of subtext.

## Task
Polish the dialogue provided by the user to make it more literary and dramatically tense.

## Input Information
### Required Fields
- Character Settings: @[Character card file] (or describe character personality)
- Scene Background: [Description]
- Original Dialogue:

[Paste dialogue]

### Optional Fields
- Dialogue Purpose: [What to achieve?]
- Emotional Tone: [Tense/Warm/Oppressive?]

## Polishing Dimensions
1. **Character Distinctiveness**: Each character speaks differently
2. **Subtext**: Saying one thing on the surface, thinking another inside
3. **Action Description**: Small gestures, expressions while speaking
4. **Rhythm Control**: Fast and slow, long and short
5. **Emotional Layers**: Ups and downs of emotions

## Output Specification
### Polished Dialogue
[Complete polished dialogue]

### Polishing Notes
| Change Point | Original | After Change | Reason |
|--------|------|--------|------|

## Constraints
- ✅ Keep original meaning unchanged
- ✅ Each character's speaking style should be distinct
- ✅ Add necessary action/expression descriptions
- ❌ Avoid being overly formal
- ❌ Avoid dialogue that's too long (3-5 sentences per exchange is ideal)
```


---

## Checklist ✅

> Must pass all items to continue

- [ ] Completed the story's three-act structure design
- [ ] Created at least one character card file
- [ ] Wrote the first chapter content
- [ ] Can use @ to reference character cards when writing dialogue

---

## Common Pitfalls

| Phenomenon | Cause | Solution |
|-----|-----|-----|
| Character personality collapsed | Didn't use character card | Create character card files, use @ reference every time you write dialogue |
| Plot contradictions | No overall outline | Design three-act structure and chapter outline first |
| Dialogue too formal | Style instructions unclear | Add style requirements in the prompt |

---

## Lesson Summary

You learned:

1. Novel writing quartet (Conceptualize → Character → Plot → Execute)
2. Design three-dimensional characters using character card templates
3. Use @ to reference character cards to maintain consistency
4. Write distinctive dialogue using the dialogue polishing prompt

---

## Next Lesson Preview

> In the next lesson, we'll learn script writing, mastering scene library management and format automation techniques.

---

📚 **More Complete Templates**: [Prompt Template Library](../appendix/prompts)
