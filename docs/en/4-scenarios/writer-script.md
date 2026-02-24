---
title: "A7 Script Writing (Advanced)"
subtitle: "Scene Library Management, Format Automation"
course: "OpenCode Chinese Practical Course"
stage: "Stage 4"
lesson: "A7"
duration: "20 minutes"
practice: "25 minutes"
level: "Advanced"
description: "Use AI to assist in writing standard format scripts, from story synopsis to scene breakdown to detailed scene writing, build a scene library for quick reuse."
tags:
  - "Script"
  - "Dialogue"
  - "Scene"
prerequisite:
  - "A1 Creative Workflow"
---

# A7 Script Writing (Advanced)

> 💡 **One-line Summary**: Use AI to assist in writing standard format scripts, from story synopsis to scene breakdown to detailed scene writing.

## 📝 Course Notes

Key concepts from this lesson:

<img src="/images/4-scenarios/writer-script-notes.mini.jpeg"
     alt="A7 Script Writing (Advanced) Study Notes"
     data-zoom-src="/images/4-scenarios/writer-script-notes.jpeg" />

<!-- 📹 Demo slot: Script writing demo -->
<!-- TODO: Demo GIF to be recorded -->
<!-- ![Script Writing Demo](/images/4-scenarios/writer-script-demo.gif) -->

---

## What You Can Do After This Lesson

- Understand standard script format
- Use AI to generate scene breakdowns
- Write properly formatted scene descriptions and dialogue
- Complete a 10-minute short film script

---

## Why Use OpenCode Instead of Web AI?

| Capability | Web AI | OpenCode |
|-----|----------|----------|
| Scene Library Management | ❌ Re-describe scenes each time | ✅ Scene template files, @reference reuse |
| Format Automation | ❌ Format often gets messy | ✅固化script format in AGENTS.md |
| Scene Management | ❌ Only in one file | ✅ One file per scene, independent editing |
| Character Voice | ❌ Dialogue easily mixed up | ✅ @character-voice.md maintains distinction |
| Version Comparison | ❌ | ✅ Git tracks every revision |

---

## Your Current Struggle

- Don't know what standard script format looks like
- Dialogue reads like a novel, not like real speech
- Scene transitions are abrupt, pacing is off

---

## When to Use This Technique

- When you need to: Write a professionally formatted script
- And you don't want to: Produce something that doesn't look like a script

---

## 🎒 Before You Start

> Make sure you've completed the following:

- [ ] Completed [A1 Creative Workflow](./writer-workflow)
- [ ] Have a short film story idea

---

## Core Concept

### Script Writing Process

```
Story Synopsis → Scene Breakdown → Detailed Scene Writing → Dialogue Polish
```

### Standard Script Format

```
Scene 1: INT. COFFEE SHOP - DAY

    A quiet afternoon, sunlight streams through the glass windows.
    ZHANG SAN (30s, casual suit) sits in the corner,
    staring blankly at his phone screen.

                    ZHANG SAN
                (muttering to himself)
        Why isn't she here yet...

    The door bell rings. LI SI (28, sharp short hair) pushes open the door.

                    LI SI
        Been waiting long?

                    ZHANG SAN
                (standing up)
        No, I just got here too.
```

---

## Follow Along

<AdInArticle />

### Step 1: Write the Story Synopsis

**Why**  
Scripts start with a synopsis, one sentence that captures the story.

Switch to Plan mode:

```
Help me brainstorm a 10-minute short film synopsis:
- Genre: Urban romance
- Characters: Two old classmates reuniting after years
- Core conflict: A misunderstanding from the past
- Resolution: Letting go and reconciliation

Summarize the entire story in one paragraph
```

### Step 2: Generate Scene Breakdown

**Why**  
Break the story into scenes, determine each scene's function.

```
Break down the above story into 5-7 scenes, each containing:
1. Scene number and location
2. Characters appearing
3. Scene purpose (what plot point to advance / what to reveal)
4. Emotional tone
```

### Step 3: Write the First Scene

**Why**  
The opening scene determines whether viewers keep watching.

Switch to Build mode:

```
Based on the scene breakdown, write Scene 1 in standard script format:
1. Scene descriptions should be concise and visual
2. Dialogue should be conversational with subtext
3. Add necessary action directions
4. Save as scripts/scene01.md
```

### Step 4: Design Character Voices

**Why**  
Each character should have a distinct way of speaking.

```
Design "voices" for both protagonists:
- Character A: Speaking style, catchphrases, rhythm patterns
- Character B: Speaking style, catchphrases, rhythm patterns

Save as scripts/character-voice.md
```

### Step 5: Complete the Entire Script

**Why**  
Complete scene by scene.

```
@scripts/character-voice.md Based on the scene breakdown and character voice settings, continue writing scenes 2-5, save as corresponding files
```

---

## 📋 Magic Prompts

### 📝 Script Format Conversion
> Expected result: Convert dialogue to standard script format

````
## Role
You are a professional screenwriter, expert in standard script format specifications.

## Task
Convert user-provided dialogue or story segments to standard script format.

## Input Information
### Required Fields
- Content: [paste dialogue or story segment]

### Optional Fields
- Scene info: [time/location?]
- Character info: [character age/appearance?]

## Output Specification
Output in standard script format:

```
Scene N: [INT./EXT.] - [LOCATION] - [TIME]

    [Scene description: environment, atmosphere, visual elements]
    [First character appearance: brief age and appearance description]

                    [CHARACTER NAME (CENTERED, UPPERCASE)]
                (action/expression direction)
        [Dialogue content, indented]

                    [ANOTHER CHARACTER]
        [Dialogue content]
```

### Format Specifications
1. **Scene Heading**: Indicates INT./EXT., location, time
2. **Scene Description**: Bold, describing environment
3. **Character Name**: Centered, uppercase
4. **Action Direction**: In parentheses, below character name
5. **Dialogue**: Below action direction, indented

## Constraints
- ✅ Strictly follow standard script format
- ✅ Add appearance description for first character appearance
- ✅ Scene descriptions should be concise and visual
- ❌ Avoid novel-style narration
- ❌ Avoid overly long dialogue (no more than 3-5 lines per turn)
````

### 💬 Dialogue Generation
> Expected result: Generate dialogue consistent with character personality

````
## Role
You are a veteran screenwriter, skilled at writing dialogue with tension and subtext.

## Task
Based on scene and character settings, generate dialogue consistent with character personalities.

## Input Information
### Required Fields
- Scene background: [scene description]
- Character A: [name] - [personality traits]
- Character B: [name] - [personality traits]
- Dialogue purpose: [what to achieve / what to reveal]

### Optional Fields
- Emotional tone: [tense/warm/oppressive?]
- Character voice: @[character voice file?]

## Output Specification
Output in standard script dialogue format:

```
                    [CHARACTER A]
                (action/expression)
        [Dialogue]

                    [CHARACTER B]
                (action/expression)
        [Dialogue]
```

### Dialogue Requirements
1. **Character Distinction**: Each character speaks differently
2. **Subtext**: Surface meaning vs. inner thoughts
3. **Rhythm Variation**: Fast and slow, long and short
4. **Action Integration**: Small gestures and expressions while speaking
5. **Conflict Tension**: Advance conflict through dialogue

## Constraints
- ✅ Consistent with each character's personality and speaking style
- ✅ Keep each dialogue turn to 3-5 lines
- ✅ Include necessary action/expression directions
- ❌ Avoid overly formal dialogue
- ❌ Avoid characters sounding the same
````


---

## Checkpoints ✅

> Must pass all to continue

- [ ] Completed the story synopsis
- [ ] Generated the scene breakdown
- [ ] Wrote at least one scene in standard format
- [ ] Dialogue has character distinction

---

## Common Pitfalls

| Issue | Cause | Solution |
|-----|-----|-----|
| Wrong format | AI used novel format | Explicitly request "standard script format" |
| Dialogue too long | No limit on dialogue length | Request "3-5 lines per character per turn" |
| Characters sound the same | No character voice design | Define each character's speaking characteristics first |

---

## Lesson Summary

You learned:

1. Script writing process (synopsis → breakdown → detailed writing → polish)
2. Standard script format specifications
3. How to design character "voices"
4. Using AI to batch generate scenes

---

## Next Lesson Preview

> In the next lesson, we'll learn web novel writing, mastering daily update workflows and batch drafting techniques.

---

📚 **More Complete Templates**: [Prompt Template Library](../appendix/prompts)
