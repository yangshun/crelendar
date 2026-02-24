# Refined Brief Template — Proposal

> **Based on:** Analysis of all 29 top-performing briefs + 80+ finished slide images
> **Changes driven by:** What actual high-performing briefs do vs. what the current template prescribes

---

## Summary of Changes

### Structural Changes
1. **Reordered to Caption → Design Brief** (all 29 top briefs use this order)
2. **Replaced Review Summary** with a leaner metadata block (removed Confidence, Similar Past Post, Date, Platform — never used)
3. **Moved GFE Tie-in and Sources inline** instead of standalone sections (matching real practice)
4. **Added Design Reference field** (previous post / visual inspiration — used in ~40% of briefs)
5. **Added Color Theme field** (critical — dark vs light theme determines the entire look)

### Format-Specific Changes
6. **Expanded Single Image section** significantly — it's 38% of top posts but had the thinnest template section. Added spatial layout zones, data table structure, code snippet handling
7. **Added per-slide layout field** to Carousel (real briefs specify "two-column", "grid of 4 cards", "side-by-side code blocks")
8. **Added standard CTA slide options** based on actual CTA copy from finished posts
9. **Added Data Visualization sub-format** for State of JS / ranking posts (4 of the top posts use this)

### Removed
10. **Removed standalone Designer Notes** — notes are inline per slide/section (matching practice)
11. **Removed standalone GFE Tie-in section** — integrated into Caption and CTA slide
12. **Simplified Sources** — inline with content + optional "planned first comment" field

---

## Proposed Template

```markdown
# ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
# METADATA (required for all formats)
# ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

## Brief Info
- **Topic:** [topic]
- **Date:** YYYY-MM-DD
- **Pillar:** [🔍 Deep Dive | ⚔️ Comparison | 🏗️ Tech Breakdown | 📰 News | 🗺️ Roadmap/List | 🎭 Culture | 💼 Career]
- **Format:** [Carousel | Single Image (Static) | Single Image (Animated) | Data Visualization | Text-Only | Meme]
- **Key angle:** [one sentence]
- **GFE tie-in:** [CTA slide + caption link | Caption link only | Hashtag only | None]

---

# ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
# CAPTION (required for all formats — write this first)
# ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

## LinkedIn Caption
[Line 1 = hook. This is the only line visible before "see more." Make it count.]

[2-4 sentences of context, insight, or a bulleted summary of what the visual covers. Add value beyond what's in the image — don't just repeat slide headlines.]

[Engagement prompt — a genuine question that invites opinions, not "What do you think?" but something specific: "Which one are you using in production?" / "Where are you on this roadmap?"]

[5-9 hashtags — mix of broad (#JavaScript #WebDevelopment) and specific (#ECMAScript2025 #ReactServerComponents). Include #GreatFrontEnd when appropriate.]

[GFE link with UTM: https://www.greatfrontend.com/?utm_source=linkedin&utm_medium=social&utm_campaign=TOPIC_MONTH+YEAR]

## Instagram Caption (if different)
[Shorter version. Replace "link below" with "link in bio." Adjust tone for Instagram audience if needed. Skip if identical to LinkedIn.]

---

# ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
# DESIGN BRIEF (include the section matching your format)
# ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

**Format:** [Carousel (N slides) | Single-page static infographic | Single-page animated GIF | Bar chart / ranking | Text-only (no graphic)]
**Color theme:** [Dark (dark navy/black bg) | Light (white/cream bg)]
**Accent color:** [topic-specific — e.g., "gold/yellow for JS", "blue/purple for React", "brand colors for [company]"]
**Design reference:** [Link to a previous GFE post to match, or "New design" | Pinterest/external reference URL]


# ── Format A: Carousel ────────────────────────────

## Slide 1 — Hook
**Title:** [under 10 words — large, bold, the dominant element]
**Subtitle:** [one-line supporting context or tagline]
**Visual:** [relevant tech logo, 3D illustration, or visual metaphor]
**Layout:** [e.g., "centered title, logo top-right, subtitle below with arrow"]

## Slide 2 — [Slide Title]
**Headline:** [the point of this slide — bold, top of slide]
**Content:**
- [Point 1]
- [Point 2]
**Code snippet:** [if applicable — keep under 6 lines]
**Layout:** [e.g., "headline top, code block center, bullet points below" or "two-column: code left, explanation right"]
**Visual elements:** [icons, logos, diagrams — be specific]

[Repeat for each content slide. One idea per slide. 30-50 words max per slide (excluding code).]

## Slide N — CTA
**Headline:** [Choose from proven options below or write custom]
**CTA button text:** [e.g., "Share this post with your network!", "Level Up Your Front End Skills"]
**GFE copy:** [e.g., "Follow us for the latest front end tools, news, and interview preparation tips." or "greatfrontend.com/interviews"]

> **Proven CTA headlines from top posts:**
> - "Stay Updated with GreatFrontEnd"
> - "Join 1M+ engineers who trust GreatFrontEnd"
> - "Ready to Ace the Interview?"
> - "Follow for more" (simple, low-friction)

**Target slide count:** 7-10 for full explainers. 5-6 acceptable for focused comparisons or tool roundups. Under 5 → consider single image instead.


# ── Format B: Single Image (Static Infographic) ──

## Layout
**Layout type:** [grid | split-panel (left/right) | flowchart | vertical list with icons | comparison table | quadrant grid]
**Spatial zones:** [describe what goes where — e.g., "Title top-left. Comparison table fills center. 'Why it matters' box at bottom."]

## Title Block
**Main title:** [bold, top of image — the hook]
**Subtitle:** [optional — one line of context]

## Content Sections
[For each section/zone of the infographic:]

### Section 1: [Name]
**Content:** [text, bullets, or data]
**Visual element:** [icon, logo, code snippet, diagram]
**Position:** [where in the layout — e.g., "top-left quadrant"]

### Section 2: [Name]
...

[Repeat for all sections. Single images can be information-dense — aim for 4-7 distinct content zones.]

## Data Table (if applicable)
| Item | Description | Logo/Icon | Source |
|---|---|---|---|
| [Name] | [one-line description] | [logo URL or "use official logo"] | [source URL] |

**Designer notes:** [any specific instructions — e.g., "Use tech logos as visual anchors", "Reference image: [URL]", "Match the layout of our [previous post name]"]


# ── Format C: Single Image (Animated GIF) ─────────

## Hook Frame (what viewers see at rest / first glance in feed)
**Static layout:** [describe — this must work as a standalone image too]

## Animation Sequence
1. [What appears/moves first]
2. [What appears/moves next]
3. [Continue...]

**Final state:** [what the viewer sees when animation completes — must be readable and complete]
**Animation style:** [e.g., "sequential reveal, items appear one by one", "arrows animate to connect elements", "code types out line by line"]
**Duration:** [target seconds — keep under 15s for social]
**Fallback:** [if animation isn't feasible, describe the static alternative]

**Source assets:** [video URL, screenshot to annotate, or reference image]
**Designer notes:** [additional context]


# ── Format D: Data Visualization (Rankings/Charts) ─

## Chart Type
**Visualization:** [horizontal bar chart | vertical bar chart | ranking list with trend lines | pie chart]
**Data source:** [e.g., "State of JS 2024 — https://2024.stateofjs.com/..."]

## Data
| Rank | Item | Value | Logo |
|---|---|---|---|
| #1 | [Name] | [percentage or metric] | [logo URL or "use official logo"] |
| #2 | ... | ... | ... |

**Description per item:** [optional — one-line description next to each item, like "A battle-tested framework for reactive apps."]
**Disclaimer text:** [e.g., "Usage percentages sourced from State of JS 2024 survey" — include at bottom of image]
**Designer notes:** [e.g., "Match the pink/magenta theme of our previous State of JS posts but change hue to differentiate"]


# ── Format E: Text-Only (LinkedIn Native) ─────────

## Post Body
[Full text of the LinkedIn post. This IS the content — there is no visual.]

[Write in first person / author voice. One-liner paragraphs with line breaks for readability. First line is everything — it's the "see more" preview.]

**Formatting notes:** [line break style, emoji usage, structural choices]

> No Design Brief needed for text-only posts. The LinkedIn Caption section above becomes the primary engagement prompt instead.


# ── Format F: Meme / Culture ──────────────────────

## Meme Concept
**Format/template:** [named meme format or "original"]
**Visual:** [what the image shows]
**Text:** [exact text overlays / captions — precision matters for memes]
**Why it works:** [one line on audience resonance]

**Designer notes:** [style references, tone guidance]


# ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
# SOURCES (required for factual posts, skip for memes/culture)
# ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

## Sources
- [Fact/claim] — [Source URL]
- [Fact/claim] — [Source URL]

**Planned first comment:** [optional — source links to post as first LinkedIn comment, e.g., "Read more here: [URL1], [URL2]"]

> For memes/culture posts: "No factual claims — culture/humor post."
> For data posts: include the survey/data source URL and any disclaimer text that should appear on the image.
```

---

## What Changed and Why

| Change | Reason (from analysis) |
|---|---|
| Caption moved before Design Brief | All 29 top briefs write captions first, design second |
| Review Summary → Brief Info (leaner) | Confidence, Similar Past Post, Date, Platform fields were never used in any real brief |
| Added Instagram Caption variant | 1 of 29 briefs (Uber) had platform-specific captions; marketing manager confirmed dual-platform |
| Added Color Theme + Accent Color | ~65% of top posts use dark theme; accent colors are topic-specific and critical to visual identity |
| Added Design Reference field | ~40% of briefs reference a previous post or external URL for design direction |
| Added per-slide Layout field to Carousel | Top briefs specify "two-column", "grid of 4 cards", "side-by-side code" — single "Visual direction" line was insufficient |
| Added proven CTA headline options | CTA slides are highly consistent — providing proven options saves time and maintains brand consistency |
| Expanded Single Image to full section | 38% of top posts are single-image infographics but the old template had just 3 fields for them |
| Added Data Visualization format | 4 top posts (State of JS series) use this format — needs its own data table structure |
| Added Animated GIF fallback field | localStorage brief explicitly handles "if animation isn't feasible" — good practice |
| Removed standalone GFE Tie-in section | Never used as a standalone section in any real brief — integrated into Caption and CTA slide |
| Removed standalone Designer Notes section | Never used — designer notes are always inline per slide/section |
| Added UTM link template | Top briefs with GFE links use UTM tracking — standardizing this saves time |
| Simplified Sources | Only 1 of 29 briefs had formal sources; added "planned first comment" for the Tue Tools pattern |
