---
title: "A3 Short-form Social Content"
subtitle: "Batch Posts, Hashtag Library, Text + Visual Output"
course: "OpenCode Practical Guide"
stage: "Stage 4"
lesson: "A3"
duration: "15 min"
practice: "25 min"
level: "Beginner"
description: "Use OpenCode to batch-generate social media posts, build a hashtag library, and create cohesive text + visual content for Instagram, TikTok, Twitter/X, and more."
tags:
  - social-media
  - content-creation
  - short-form
prerequisite:
  - A1 Writing Workflow
---

# A3 Short-form Social Content

> Use OpenCode to build a social content production line — generate a week's worth of posts in one go, smart hashtag library, and unified text + visual output.

## Course Notes

Key takeaways from this lesson:

<img src="/images/4-scenarios/writer-xiaohongshu-notes.mini.jpeg"
     alt="A3 Short-form Social Content Notes"
     data-zoom-src="/images/4-scenarios/writer-xiaohongshu-notes.jpeg" />

---

## What You'll Be Able to Do

- Generate a week's worth of social posts in one session (7+ posts)
- Build a local hashtag library with smart tag matching
- Output post body + cover text + hashtags in one cohesive package
- Lock in your brand voice for consistent style across all posts

---

## Why OpenCode Instead of Web-based AI?

| Capability | Web-based AI | OpenCode |
|------------|--------------|----------|
| Batch generation | Write one by one, copy-paste | 7+ posts at once, saved to files |
| Hashtag library | Search manually each time | Local library, smart retrieval |
| Brand consistency | Re-describe every time | AGENTS.md locks it in permanently |
| Text + visual | Write body and titles separately | Body + cover + hashtags together |
| Content reuse | Manual copy | @reference to pull past content |

---

## Your Current Pain Points

- Can't keep up with posting frequency, stuck thinking of content
- Don't know which hashtags to use, searching every time
- Inconsistent voice — sometimes casual, sometimes formal

---

## When to Use This Approach

- When you need: High-frequency social posting, batch content production
- And you don't want: Starting from zero every time, low efficiency

---

## Prerequisites

> Make sure you've completed the following:

- [ ] Completed [A1 Writing Workflow](/en/4-scenarios/writer-workflow)
- [ ] Have a social media account (or a clear brand positioning in mind)

---

## Follow Along

### Step 1: Set Up Your Social Content Project

**Why**  
Centralize all content for easy batch operations.

```bash
mkdir ~/my-social-content
cd ~/my-social-content
opencode
```

Let AI help you create the directory structure:

```
Create a social media content management structure:
- hashtags/ (by category: lifestyle, tech, food, etc.)
- assets/ (image descriptions, product info, testimonials)
- posts/ (organized by month)
- hook-templates.md (viral hook templates)
- brand-voice.md (brand persona definition)

Create these directories and placeholder files
```

### Step 2: Lock In Your Brand Voice

**Why**  
Consistent style makes your brand recognizable.

```
Create AGENTS.md defining my social media brand voice:

Brand positioning: Sustainable lifestyle advocate
Persona: 28-year-old urban professional, minimalist, 3 years into zero-waste living
Tone: Friendly peer sharing, authentic, not preachy
Go-to emojis: 
Avoid: "Game changer," "obsessed," "literally dying" (overused)
Hook style: Question / Number / Contrast
Post structure: Pain point hook → Solution → Personal experience → Actionable takeaway
Word count: 150-280 characters (Twitter/X) or 150-300 words (Instagram/TikTok)
```

### Step 3: Build Your Hashtag Library

**Why**  
Hashtags drive discoverability — organize them once, use forever.

```
Create hashtag library files by category:

hashtags/lifestyle.md:
#sustainableliving #minimalism #zerowaste #ecofriendly #consciousconsumer
#slowliving #sustainability #greenliving #ethicalfashion #plasticfree
(mark each with popularity: high/medium/low)

hashtags/tech.md:
#techtips #productivity #digitalminimalism #workfromhome
(continue with relevant tags)
```

### Step 4: Batch Generate a Week's Content

**Why**  
Generate 7 posts in one go — no daily content stress.

```
Generate 7 social media posts for next week on "sustainable lifestyle."

Each post should include:
1. Hook text (under 15 words, scroll-stopping)
2. Body copy (appropriate length for platform)
3. Hashtags (5-10, selected from @hashtags/lifestyle.md)
4. Visual suggestion (what to photograph/create)

Weekly theme distribution:
- Monday: Product swap recommendation
- Tuesday: Quick tip
- Wednesday: Personal story
- Thursday: Myth busting
- Friday: Resource sharing
- Saturday: Behind the scenes
- Sunday: Weekly reflection

Save to posts/2025-Jan-Week2/ with one file per post
```

### Step 5: Collect Viral Hooks

**Why**  
A good hook = higher engagement. Worth collecting systematically.

```
Organize "hook-templates.md" with viral hook patterns:

[Question Hooks]
- Still doing X? Here's why you should stop
- Why your X isn't working (and what actually does)

[Number Hooks]
- 3 products I've repurchased 10+ times
- Day 30 of X: here's what changed

[Contrast Hooks]
- Everyone recommends X, but here's my honest take after a month
- Thought I'd hate it, now I can't live without it

[Pain Point Hooks]
- Finally found a fix for X
- Struggling with X? This changed everything

Save 10 templates per category to hook-templates.md
```

---

## Magic Prompts

### Batch Post Generation
> Expected outcome: Generate multiple posts with body, hooks, and hashtags

```
## Role
You are a seasoned social media creator who writes viral content. You understand platform algorithms and user psychology.

## Task
Batch generate social media posts, each containing hook text, body copy, hashtags, and visual suggestions.

## Input
### Required
- Brand positioning: [POSITIONING]
- Batch theme: [THEME DIRECTION]
- Quantity: [N] posts

### Optional
- Brand voice reference: @AGENTS.md
- Hashtag library: @hashtags/[CATEGORY].md

## Output Format
Each post includes:

### Post 1: [THEME]
**Hook** (under 15 words, scroll-stopping)
> [HOOK TEXT]

**Body Copy** (platform-appropriate length)
> [CONTENT, matching brand voice]

**Hashtags** (5-10 relevant tags)
> #tag1 #tag2 ...

**Visual Suggestion**
> [Description of image/video to create]

---

## Constraints
- Hooks must be attention-grabbing, under 15 words
- Body copy should feel conversational, like a friend sharing
- Select hashtags from trending/popular categories
- Use appropriate emojis sparingly
- Avoid overused phrases like "game changer," "obsessed"
- Stay authentic, no exaggerated claims
```

### Hashtag Library Update
> Expected outcome: Maintain hashtag library for better discoverability

````
## Role
You are a social media growth specialist, expert in hashtag research and optimization.

## Task
Update hashtag library, analyze popularity, optimize tag strategy.

## Input
### Required
- Category: [TYPE, e.g., lifestyle/tech/food]
- Current library: @hashtags/[TYPE].md

### Optional
- New hashtags to add: [TAGS?]

## Output Format
Updated library structure:

```markdown
# [TYPE] Hashtag Library

## High Popularity (Prioritize)
- #tag1 - Usage notes
- #tag2 - Usage notes

## Medium Popularity (Mix in)
- #tag3 - Usage notes

## Low Popularity (Niche targeting)
- #tag4 - Usage notes

## Outdated (Stop using)
- #oldtag - Reason it's outdated

---
Last updated: [DATE]
```

## Constraints
- Organize by popularity tier for easy selection
- Add usage notes for each hashtag
- Mark outdated tags to avoid mistakes
- Don't add irrelevant hashtags
````

### Hook Optimization
> Expected outcome: Generate multiple hook options for higher engagement

```
## Role
You are a viral hook specialist who understands scroll-stopping content.

## Task
Generate multiple hook options for post content.

## Input
### Required
- Post summary: [BRIEF DESCRIPTION]

### Optional
- Target emotion: [WHAT EMOTION TO EVOKE?]
- Styles to avoid: [WHAT TO AOID?]

## Output Format
Generate 10 hooks across different styles:

### Question Hooks (2-3)
> Spark curiosity, drive clicks
- [HOOK] ⭐⭐⭐⭐⭐
- [HOOK] ⭐⭐⭐⭐

### Number Hooks (2-3)
> Specific and informative
- [HOOK] ⭐⭐⭐⭐
- [HOOK] ⭐⭐⭐

### Contrast Hooks (2-3)
> Create tension, spark discussion
- [HOOK] ⭐⭐⭐⭐⭐
- [HOOK] ⭐⭐⭐⭐

### Pain Point Hooks (2-3)
> Hit the problem, create resonance
- [HOOK] ⭐⭐⭐⭐
- [HOOK] ⭐⭐⭐

**Top Pick**: [HOOK]
**Reason**: [WHY THIS ONE]

## Constraints
- Each hook under 15 words
- Rate each with 1-5 stars
- Cover multiple styles
- Avoid clickbait or exaggerated claims
- Stay aligned with brand voice
```

---

## Checklist

> All items must be complete before moving on

- [ ] Created social content project directory structure
- [ ] Created AGENTS.md with locked-in brand voice
- [ ] Built hashtag library (at least one category)
- [ ] Batch generated at least 3 posts

---

## Common Pitfalls

| Issue | Cause | Solution |
|-------|-------|----------|
| Voice varies each time | No locked persona | Define persona in AGENTS.md |
| Hashtags not precise enough | No hashtag library | Build library by category |
| Hooks don't grab attention | Only wrote one version | Generate 10 alternatives |
| Content feels repetitive | Same prompt every time | Vary themes and angles |

---

## Advanced Tips

### Create Quick Commands

Create `.opencode/command/social.md`:

```markdown
---
description: Quick social post generation
---

Generate a social media post on this topic:

Topic: $ARGUMENTS

Requirements:
1. Follow brand voice in @AGENTS.md
2. Select hashtags from @hashtags/
3. Include hook, body, hashtags, visual suggestion
4. Save to posts/ directory
```

Then just type `/social sustainable coffee tips` for quick generation.

### Asset Library Reuse

Store good content in your asset library:

```
Add the product description from this post to @assets/product-info.md for future reuse
```

---

## Lesson Summary

You learned:

1. Lock in brand voice with AGENTS.md (consistent style)
2. Build hashtag library for smart tag retrieval
3. Batch generate a week's posts (7 posts in one session)
4. Hook + body + hashtags as unified output

**This is what web-based AI can't do — that's the value of OpenCode.**

---

## Next Lesson Preview

> Next up: **[Marketing Copy](./writer-copywriting)** — master the AIDA framework, A/B variant generation, and asset library integration.

---

**More templates**: [Prompt Template Library](/en/appendix/prompts)
