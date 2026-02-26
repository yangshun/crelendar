# agents.md — GreatFrontEnd Marketing Brief Generator

> **This is the entry point.** Read this file first, then follow the pipeline in `EXECUTION.md`. Strategy rationale lives in `PLAN.md`.

---

## Mission

Produce one factually accurate, high-engagement marketing brief per day for GreatFrontEnd's LinkedIn and Instagram. Each brief → post → engagement → sales. **Accuracy is the brand. Engagement is the goal. Briefs are the system.**

---

## Key Documents

| Document | Purpose | When to Read |
|---|---|---|
| `agents.md` (this file) | Repo rules, audience, template, standards | Every session start |
| `PLAN.md` | Content strategy, pillars, quality framework, format best practices | When choosing angles or evaluating brief quality |
| `EXECUTION.md` | 5-stage pipeline with quality gates | When producing a brief (follow stage by stage) |

---

## Target Audience

Front-end engineers (junior → senior), front-end AI engineers, and full-stack engineers. These are practitioners — they value accuracy, depth, and insight over fluff. They stop scrolling for content that makes them feel smarter or validates something they've experienced.

---

## Repo Structure

```
/
├── agents.md                  # Entry point — repo rules and standards
├── PLAN.md                    # Content strategy and quality framework
├── EXECUTION.md               # 5-stage brief creation pipeline
├── top-linkedin-posts/        # Reference data: 29 top-performing posts (briefs + images)
├── briefs/                    # Output directory for new briefs
│   ├── drafts/                # WIP briefs awaiting marketing manager review
│   └── approved/              # Reviewed and approved briefs
├── reference/                 # Supporting research & source material
│   ├── greatfrontend-info/    # Product facts, features, pricing, positioning
│   ├── topic-research/        # Per-topic research notes (saved during Stage 1)
│   ├── content-pillars/        # Per-pillar format guides (e.g., news-roundup.md)
│   ├── covered-topics.md       # Dedup tracker for news/tools roundups
│   └── top-posts-analysis.md  # Analysis of top-performing posts (patterns & insights)
└── templates/                 # Brief templates and format specs
```

---

## ClickUp Workflow

This section documents the ClickUp workspace structure and task conventions so that any session can operate without rediscovery.

### Workspace Hierarchy

```
Workspace: 90182221284
  └── Space: "GFE Content Marketing" (ID: 90189131238)
       └── List: "2026 Calender" (ID: 901814889385)
            └── Parent tasks = topics (one per post)
                 └── Subtasks = pipeline steps per topic
```

### Task Structure

Each **parent task** represents a content topic. It holds all metadata in its name, description, and custom fields. Each parent has **subtasks** representing pipeline steps:

| Subtask Name | Role |
|---|---|
| write brief | Produce the marketing brief (our primary task) |
| create design | Designer creates visual assets |
| review design | Design reviewer checks assets |
| write caption | Caption writer drafts social copy |
| final check | Coordinator does final approval |

### Brief Output — ClickUp Docs

1. Open the "write brief" subtask assigned to you
2. Navigate to the **parent task** (the topic)
3. Create a **ClickUp Doc** in the "2026 Calender" list with the brief content
4. Set the **"ClickUp Brief"** custom field (field ID: `68e015f7-6830-44ea-ab09-6280bdd0d00e`) on the parent task to the ClickUp Doc URL

**Do NOT overwrite the "Brief link" field** — that contains the original Google Doc link. Use the separate "ClickUp Brief" field for the ClickUp Doc output.

### Parent Task Custom Fields

| Field | Purpose |
|---|---|
| **ClickUp Brief** | ClickUp Doc URL where the brief is written (our output) |
| Brief link | Original Google Doc link (do not overwrite) |
| Content Pillars | Which pillar this topic belongs to |
| Post format | Carousel, single image, etc. (may already be decided) |
| Topic Category | Topic classification |
| Platform to post on | LinkedIn, Instagram, etc. |
| Post reference | Reference post URLs |
| Design link | Link to design assets |
| Video Link | Link to video assets |

### Subtask Description Resources

The "write brief" subtask description typically contains useful reference links:
- Old briefs Google Drive folder (examples of prior briefs)
- Content pillar strategy document
- Design kit guidelines document

Read these on first encounter to understand conventions.

### Design Approach Options

ClickUp tasks may specify one of two design approaches:

| Approach | Details |
|---|---|
| **Option 1: Marketing Design Kit** | Character limits apply — Cover Slide Title: 40-48 chars, Subtitle: 120-140 chars |
| **Option 2: Custom Design** | No fixed character limits |

When the parent task indicates "Marketing Design Kit," the brief must respect these character limits.

### Status Flow

The "write brief" subtask starts with status **"write brief"**. When the brief is complete and written to the Google Doc, close the subtask by setting its status to **"subtask closed"**.

### Team

| Person | Role |
|---|---|
| Yangshun Tay | Brief writer |
| Damian Ng | Brief writer |
| Pascal Esatama | Designer |
| Jyoti | Caption writer |
| Avinash Singh | Coordinator / final check |
| Nitesh Seram | Design reviewer |

### MCP Tools

| Tool | Transport | Purpose |
|---|---|---|
| ClickUp MCP | HTTP (`https://mcp.clickup.com/mcp`) | Read tasks, custom fields, update status |
| Google Docs MCP | stdio (`npx -y google-docs-mcp`) | Write brief content into linked Google Docs |

---

## Brief Template

One flexible template for all formats. The brief focuses on **content and structure** — the design team handles visual execution. Every brief has three parts: **Brief Info** → **Caption** → **Content Brief** (format-specific). Include only the format section that applies.

```markdown
# ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
# BRIEF INFO (required for all formats)
# ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

# [Post Title]

- **Date:** YYYY-MM-DD
- **Topic:** [topic]
- **Pillar:** [🔍 Deep Dive | ⚔️ Comparison | 🏗️ Tech Breakdown | 📰 News | 🗺️ Roadmap/List | 🎭 Culture | 💼 Career]
  > For pillar-specific format guides, check `reference/content-pillars/`. Currently available: `news-roundup.md` (Biweekly News), `ai-coding-tips.md` (Ship with AI).
- **Format:** [Carousel | Single Image | Animated GIF | Data Visualization | Meme | Text-Only]
- **Format rationale:** [why this format and not another — required]
- **Key angle:** [one sentence]
- **GFE tie-in:** [CTA slide + caption link | Caption link only | Hashtag only | None]
- **Design inspiration:** [optional — e.g., "ByteByteGo system design style" or "NeetCode explainer format"]
- **Color theme:** [Dark (navy/black bg) | Light (white/cream bg)]
- **Accent color:** [topic-specific — e.g., "gold/yellow for JS", "blue for React", "red #e50914 for Netflix"]


# ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
# CAPTION (required for all formats — write this first)
# ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

## LinkedIn Caption
[Line 1 = hook. This is the only line visible before "see more." Make it count.]

[2-4 sentences of context or insight that adds value beyond the visual content.]

[Engagement prompt — a specific question that invites opinions. Not "What do you think?" but "Which one are you using in production?" or "Where are you on this roadmap?"]

[5-9 hashtags — mix of broad (#JavaScript #WebDevelopment) and specific (#ECMAScript2025). Include #GreatFrontEnd when appropriate. **ClickUp doc version only:** prefix each hashtag with backslash (\#) to prevent ClickUp's markdown parser from rendering the hashtag line as a heading, which cascades to the CTA line below.]

[GFE link with UTM: https://www.greatfrontend.com/?utm_source=linkedin&utm_medium=social&utm_campaign=TOPIC_MONTH+YEAR]

## Instagram Caption (if different from LinkedIn)
[Shorter version. Replace "link below" with "link in bio." Skip this section if identical to LinkedIn.]

> **Note:** For text-only posts, this Caption section becomes the secondary
> engagement prompt (e.g., "Drop your take below.") rather than a full caption.


# ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
# CONTENT BRIEF (include the section matching your format)
# ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

# ── Format A: Carousel ────────────────────────────

## Slide 1 — Hook
**Title:** [under 10 words — bold, the dominant visual element]
**Subtitle:** [one-line supporting context or tagline]
**Visual direction:**
- Layout: [e.g., "centered title, tech logo bottom-right"]
- Key elements: [e.g., "React atom logo", "3D JS letters", "code snippet preview"]
- Style notes: [e.g., "dark bg, blue accent", "bold sans-serif title"]

## Slide 2 — [Slide Title]
**Headline:** [the point of this slide]
- [Supporting point 1]
- [Supporting point 2]
**Visual direction:**
- Layout: [e.g., "headline top, code block center, bullet list below"]
- Key elements: [e.g., "code snippet in monospace", "comparison table", "diagram showing X"]
- Style notes: [e.g., "consistent with slide 1 theme"]

[Repeat for each content slide. One idea per slide. 30-50 words max (excluding code).]

## Final Slide — CTA
**Headline:** [choose from proven options or write custom]
**GFE copy:** [e.g., "Follow us for the latest front end tools, news, and interview prep."]
**CTA button text:** [e.g., "Share this post with your network!"]

> **Proven CTA headlines from top-performing posts:**
> - "Stay Updated with GreatFrontEnd"
> - "Join 1M+ engineers who trust GreatFrontEnd"
> - "Ready to Ace the Interview?"

**Target:** 7-10 slides for full explainers and tiered news roundups. 5-6 for focused comparisons. Under 5 → consider single image instead.


# ── Format B: Single Image (Static Infographic) ──

## Title
**Main title:** [bold, top of image — this is the hook]
**Subtitle:** [optional — one line of context]

## Content Sections
[Define 4-7 content zones. For each:]

### Section 1: [Name]
**Content:** [text, bullets, or data points]
**Visual direction:**
- Layout: [e.g., "6-row grid with icon + title + bullets per row", "2-column comparison"]
- Key elements: [e.g., "⚠️ accent highlight on rows 5-6 to signal 'overlooked'", "code snippet in monospace"]
- Style notes: [e.g., "dark theme, gold accent", "use ❌/✅ contrast markers"]

### Section 2: [Name]
**Content:** [...]
**Visual direction:**
- Layout: [...]
- Key elements: [...]
- Style notes: [...]

[Repeat for all sections.]

## Data Table (if applicable — for tech stacks, tool comparisons, etc.)
| Item | Description | Logo | Source |
|---|---|---|---|
| [Name] | [one-line description] | [official logo] | [source URL] |

> **When to use this format:** Single concepts, cheatsheets, "how X works" explainers,
> roadmaps, comparison tables, anything with fewer than 5 distinct points.
> Top-performing examples: JS Hoisting, localStorage, Git Skills, Framework Picker.


# ── Format C: Animated GIF ────────────────────────

## Hook Frame
[What the viewer sees at rest / first glance in the feed. Must work as a standalone static image too.]

## Animation Sequence
1. [What appears or changes first]
2. [What appears or changes next]
3. [Continue...]

**Final state:** [what the viewer sees when animation completes — must be readable and complete]
**Key message:** [the one thing the audience should take away]
**Fallback:** [if animation isn't feasible, describe the static alternative]

> **When to use this format:** Process flows, architecture reveals, tech stack breakdowns
> with relationships, annotated screenshots, UI component showcases.
> Top-performing examples: Figma breakdown, Microfrontends, localStorage, Chrome 135.


# ── Format D: Data Visualization ──────────────────

## Chart Concept
**Visualization type:** [horizontal bar chart | ranking list | trend lines | comparison grid]
**Data source:** [e.g., "State of JS 2024 — https://2024.stateofjs.com/..."]

## Data
| Rank | Item | Value | Description |
|---|---|---|---|
| #1 | [Name] | [percentage or metric] | [one-line description] |
| #2 | ... | ... | ... |

**Disclaimer text:** [e.g., "Usage percentages sourced from State of JS 2024 survey"]

> **When to use this format:** Survey results, framework rankings, adoption trends,
> any data-backed content with 5+ items to rank or compare.
> Top-performing examples: State of JS series (FE frameworks, meta frameworks, testing, backend).


# ── Format E: Text-Only (LinkedIn Native) ─────────

## Post Body
[Full text of the LinkedIn post. This IS the content — there is no visual.]

[First person / author voice. One-liner paragraphs with line breaks. First line is everything.]

**Formatting notes:** [line breaks, emoji usage, structural choices]

> **When to use this format:** Hot takes, personal stories, opinions, breaking news
> (speed > production quality). No design needed.
> Top-performing example: "Is Modern Front End Development Really Better?"


# ── Format F: Meme / Culture ──────────────────────

## Meme Concept
**Format/template:** [named meme format or "original concept"]
**Text:** [exact text overlays / captions — precision matters]
**Why it works:** [one line on audience resonance]

> **When to use this format:** Relatable developer humor, shared frustrations,
> tech culture moments. Minimal text, maximum relatability.


# ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
# SOURCES (required for factual posts)
# ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

## Sources
- [Fact/claim] — [Source URL]
- [Fact/claim] — [Source URL]

**Planned first comment:** [Required — choose one strategy:]
- Source/resource links (for data or tech stack posts)
- Deeper GFE link with context (for interview/learning posts)
- Conversation starter question (for opinion/culture posts)
- "Read more at [URL]" (for news/release posts)

> For memes/culture posts: "No factual claims — culture/humor post."
```

### Format Selection Guide

**Default rule: do NOT default to carousel.** Before selecting carousel, ask: "Could this work as a single image or animated GIF?" If the topic has fewer than 5 distinct points, it probably should.

| If the topic is... | Recommended format | Why |
|---|---|---|
| Single concept, cheatsheet, or "how X works" | **Single Image** | One dense, save-worthy visual. Top performers: Hoisting, localStorage, Git Skills |
| Process flow, architecture, or tech stack with relationships | **Animated GIF** | Motion reveals complexity. Top performers: Figma, Microfrontends |
| Survey data, rankings, or adoption stats | **Data Visualization** | Bar charts with logos and percentages. Top performers: State of JS series |
| Technical explainer with 5+ distinct points | **Carousel** | Each point gets a slide. Top performers: ECMAScript 2025, React Hooks |
| Side-by-side comparison (X vs Y) | **Carousel** (short, 5-6 slides) | Comparison table + scenario slides. Top performer: Redux vs Zustand |
| Relatable developer humor or culture | **Meme** | Low production, high relatability |
| Personal take, story, or hot opinion | **Text-Only** | Authenticity > polish. Top performer: "Is Modern FE Really Better?" |
| Breaking news (first 2 hours) | **Text-Only** | Speed matters; upgrade to another format later if warranted |

**Format variety check:** Before finalizing, check `briefs/drafts/` and `briefs/approved/` for the last 5 posts. Avoid using the same format 3+ times in a row. Rotate between carousels, single images, GIFs, and data visualizations.

The marketing manager makes the final format call.

---

## Accuracy Standards

### The Accuracy Stack (in priority order)

| Level | What | Standard |
|---|---|---|
| **L1: Hard Facts** | Version numbers, API names, syntax, dates, company attributions | Zero errors. Verified against official sources. |
| **L2: Technical Claims** | Performance comparisons, architecture descriptions, "how it works" | Must have source. Hedged if source is indirect. |
| **L3: Characterizations** | Opinions, rankings, trend claims | Presented as perspective, not fact. Backed by data where possible. |

### Non-negotiable Rules
- Every technical claim must trace to an authoritative source
- When comparing technologies, use consistent evaluation criteria and acknowledge tradeoffs
- Flag anything below 95% confidence with `[VERIFY]` — never silently guess
- Outdated information must never be presented as current

---

## Writing Style

**Voice:** A dev who's mass-commenting on Reddit at midnight - direct, a little unfiltered, but clearly knows their stuff. Not a conference speaker. Not a LinkedIn thought leader. Just someone who's been in the trenches and is telling you how it actually is.

**Tone rules:**
- **Sound like a person, not a brand.** First-person, casual phrasing, contractions always. "Here's the thing" > "It is important to note that"
- **Be blunt.** "Most people get this wrong" > "This is a commonly misunderstood topic." Don't hedge when you're right.
- **Drop the inspirational closer.** No "keep learning!" or "you've got this!" endings. End with a sharp question or a provocative claim. Reddit energy, not LinkedIn energy.
- **Keep it natural.** Short sentences. Sentence fragments are fine. If a phrase sounds like something you'd actually say out loud to a coworker, it works. If it sounds like a caption template, cut it.
- **No corporate speak.** Ban list: "leverage", "utilize", "cutting-edge", "revolutionary", "empower", "drive results", "deep dive into", "unpack", "let's explore", "in today's landscape"
- **No AI-speak.** Ban list: "it's worth noting", "interestingly", "let's delve", "crucial", "comprehensive", "game-changer", "navigate the complexities", "at the end of the day"
- **Specificity > generality.** "React 19's compiler eliminates useMemo in most cases" beats "React 19 has exciting performance improvements"
- **Opinionated when defensible.** Take stances, but don't strawman the other side. "You probably don't need Redux anymore - here's why" > "Redux is bad"

**Caption voice specifically:**
- First line is a hook - punchy, no preamble, could be a Reddit post title
- Body reads like a top Reddit comment: real talk, specific examples, zero fluff
- Engagement prompt should feel like a genuine question you'd ask on r/webdev, not a "tell me in the comments!" CTA
- Hashtags are a necessary evil - keep them at the end, don't let them infect the tone

**What good tone sounds like:**
- "Sounds easy - until the interviewer keeps adding requirements."
- "Most candidates plateau at level 2. Be honest - where would you stop?"
- "Level 4 - accessibility - is what separates senior hires from everyone else, and almost nobody even practices it."

**What bad tone sounds like:**
- "In this comprehensive guide, we'll explore the key evaluation criteria..."
- "Ready to level up your interview game? Let's dive in!"
- "Understanding these concepts is crucial for any aspiring front-end engineer."

### Design Inspiration References

When suggesting visual treatment in the **Design inspiration** field, reference these accounts whose styles resonate with our audience:

| Account | Known For | Good Reference When |
|---|---|---|
| **Alex Xu / ByteByteGo** | System design diagrams, architecture breakdowns | Tech breakdowns, "how X works" posts |
| **Nikki Siapno** | Career content, clean infographics | Career & craft posts, resume/interview tips |
| **Design Gurus (Arslan Ahmad)** | Interview prep visuals, DSA explainers | Deep dives, algorithm content |
| **Codemia** | Coding concept visualizations | Educational explainers, concept breakdowns |
| **NeetCode** | Algorithm/DSA content, clean explanations | Technical deep dives, coding challenges |
| **The Pragmatic Engineer** | Industry news, engineering culture commentary | News & releases, industry takes |

These are suggestions for the design team — include them when a style match is clear, skip when it's not.

---

## GFE Product Context

The audience is allergic to hard sells. GFE mentions must feel earned, not inserted. The post should deliver full value even if the reader ignores every GFE reference.

**Always verify** current GFE product details before referencing them - check `reference/greatfrontend-info/` or the live site. Never assume features or pricing.

**Specifically for CTAs:** Any product count (number of questions, number of topics, etc.) referenced in the CTA, footer zone, or planned first comment must be verified against the live GFE page you're linking to. Don't rely on research notes alone - check the actual page. Numbers change as GFE adds/removes content.

**Never hardcode GFE question counts.** Don't write "90+ React questions" or "15 system design questions" in CTAs, slides, or first comments. These numbers change as GFE adds content, and a stale number undermines trust. Instead write "React interview questions with detailed solutions" or "system design questions with solutions." The value prop is the quality and solutions, not the count.

**GFE is an interview practice platform, not a course platform.** Never use "course," "courses," "curriculum," or "lessons" when describing GFE. Words like "learn," "study," and "prepare" are fine in interview prep context.

**Use the correct messaging per GFE product:**
- **Interview Prep** (Questions, System Design, Playbook — `/prepare`, `/system-design`, `/front-end-interview-guidebook`): Frame as interview practice. Use "practice," "prepare," "ace," "interview questions," "solutions by ex-interviewers."
- **Projects** (`/projects`): Frame as skill building and portfolio. Use "build," "showcase," "portfolio-ready," "real-world projects," "professional designs," "community code reviews." Projects is NOT interview prep — it's about building skills and creating impressive portfolio pieces.
- **Blog** (`/blog/*`): Frame as practical tips and real-world techniques. Can mention interview relevance as a secondary angle, not the primary framing.

---

## Rules for Repo Claude

1. **Read this file first** at the start of every session.
2. **Follow the 5-stage pipeline** in `EXECUTION.md` for every brief — no skipping stages.
3. **Consult `PLAN.md`** for content pillar selection, hook patterns, and engagement criteria.
4. **Check prior art** in `top-linkedin-posts/` and `briefs/approved/` before starting any topic.
5. **Never fabricate technical details.** If unsure, flag with `[VERIFY]` — never guess silently.
6. **Save research notes** to `reference/topic-research/` during Stage 1 — build institutional knowledge.
7. **Think in the chosen format:** Carousels = 7-10 slides, one idea per slide, 30-50 words. Single images = 4-7 content zones, information-dense. Animated GIFs = hook frame + sequence. Data viz = chart type + data table. Memes = minimal text, maximum relatability. Text-only = first line is everything.
8. **Optimize the hook** — the first slide/headline determines everything. Spend disproportionate effort here.
9. **Keep briefs self-contained** — the content brief provides all text, data, and structure. Include light visual suggestions but leave design decisions to the design team.
10. **Date-stamp everything** — front-end moves fast; "latest" is stale in 3 months.
11. **Pull tasks from ClickUp** — check the "2026 Calender" list (ID: `901814889385`) in Space "GFE Content Marketing" for "write brief" subtasks. These are your assignments. **Prioritize by the parent task's due date (the post publish date), NOT the subtask's due date (the brief deadline).** This is the ONLY valid sort key — always fetch ALL open subtasks, retrieve each parent's due date, sort ascending, and pick the earliest. Never use subtask due date for ordering. Skip tasks whose parent publish date has already passed — those are handled separately.
12. **Write output to a ClickUp Doc** — create a ClickUp Doc in the "2026 Calender" list, then set the parent task's "ClickUp Brief" custom field (field ID: `68e015f7-6830-44ea-ab09-6280bdd0d00e`) to the doc URL. Do NOT overwrite the "Brief link" field.
13. **Close the subtask when done** — after writing the brief to a ClickUp Doc and saving a local backup, set the "write brief" subtask status to "subtask closed" in ClickUp.
14. **Save a local backup** to `briefs/drafts/` following the naming convention (`YYYY-MM-DD-topic-slug.md`), in addition to writing to the ClickUp Doc.
15. **Respect task description requirements - but verify them.** If the marketing manager added requirements in the parent task's description (specific angles, talking points, constraints, links), extract and sanity-check each one. Validated requirements are hard constraints the brief must satisfy. But if a requirement contains an inaccurate claim, conflicts with pipeline best practices, or doesn't fit the format/angle, flag it with `[MANAGER-CHECK]` and suggest an alternative rather than blindly following it. The manager is human too - catch mistakes before they make it into the brief.
16. **Never repeat topics in news roundups or AI tips.** Before researching a Biweekly News or Ship with AI brief, check `reference/covered-topics.md` and the relevant pillar guide in `reference/content-pillars/` (`news-roundup.md` for Biweekly News, `ai-coding-tips.md` for Ship with AI). After completing one, update the tracker with all topics covered.
