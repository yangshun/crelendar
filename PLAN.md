# PLAN.md — Content Brief System Strategy

## Mission

Produce one high-quality, factually accurate marketing brief per day for GreatFrontEnd's LinkedIn and Instagram channels. Each brief translates into a carousel post targeting front-end engineers. The system must sustain daily output without sacrificing accuracy — because one wrong version number erodes more trust than one viral post builds.

---

## 1. Content Strategy

### 1.1 Content Pillars

Every post should fall into one of these pillars. The mix ensures variety across a week while serving different engagement and business goals.

| Pillar | Purpose | Engagement Profile | Example |
|---|---|---|---|
| **🔍 Deep Dives** | Teach something non-obvious about a core concept | High saves, moderate likes, strong authority-building | "How JavaScript closures actually cause memory leaks" |
| **⚔️ Comparisons** | Frame a decision the audience faces | High comments (debate), high shares | "Redux vs Zustand — when each actually makes sense" |
| **🏗️ Tech Breakdowns** | Reverse-engineer how top companies build things | Highest impressions, strong likes, aspirational | "How Netflix serves 200M+ users — their front-end stack" |
| **📰 News & Releases** | Be first to explain what matters in a new release | Time-sensitive impressions spike, moderate saves | "Next.js 16 — the 5 changes that actually affect you" |
| **🗺️ Roadmaps & Lists** | Curate and rank tools/skills/paths | High saves, strong for new followers | "Front-end roadmap 2025 — what to learn and in what order" |
| **🎭 Culture & Memes** | Relatable developer humor and shared experiences | Highest raw engagement, broadest reach | "Life as a JavaScript developer" |
| **💼 Career & Craft** | Interview prep, resume tips, career growth | Moderate engagement, highest conversion intent | "The front-end system design questions FAANG actually asks" |

### 1.2 Weekly Content Mix (Recommended)

For daily posting (7 posts/week), the ideal distribution balances reach with depth:

| Day | Pillar | Rationale |
|---|---|---|
| Monday | 🗺️ Roadmaps & Lists | Start the week with actionable, save-worthy content |
| Tuesday | 🔍 Deep Dive | Mid-week learning — audience is in "growth mode" |
| Wednesday | ⚔️ Comparison | Debate content peaks mid-week when engagement is highest |
| Thursday | 🏗️ Tech Breakdown | High-effort content for peak LinkedIn traffic day |
| Friday | 📰 News & Releases | Timely wrap-up of the week's front-end news |
| Saturday | 🎭 Culture & Meme | Lighter weekend content, broadest reach |
| Sunday | 💼 Career & Craft | Career reflection content for weekend browsers |

This is a starting template — it should flex based on what's happening (e.g., a major framework release on Monday bumps News to Monday).

### 1.3 Content Principles

**Insight density over length.** A 7-slide carousel where every slide teaches something beats a 12-slide carousel that pads. The audience is engineers — they respect efficiency.

**Specificity is the hook.** "React 19's `use` hook lets you read promises during render" stops scrolling. "React 19 has exciting new features" does not.

**Opinionated > neutral, but always fair.** Taking a stance ("You probably don't need Redux anymore") drives engagement. But straw-manning alternatives destroys credibility. Always acknowledge when the "losing" option has legitimate strengths.

**Accuracy is brand.** GreatFrontEnd's authority depends on being the account that gets things right. One factual error in a viral post does more brand damage than a week of accurate posts can repair.

**Teach the "why" behind the "what."** Listing features is a changelog. Explaining *why those features matter to the audience's daily work* is content.

---

## 2. Quality Framework

### 2.1 The Accuracy Stack

Briefs are checked at three levels, in order of priority:

| Level | What's Checked | Examples |
|---|---|---|
| **L1: Hard Facts** | Version numbers, API names, syntax, release dates, company attributions | "React 19" not "React 18.3", correct hook signatures |
| **L2: Technical Claims** | Performance comparisons, architectural descriptions, "how it works" explanations | Bundle size claims backed by benchmarks, correct rendering model descriptions |
| **L3: Characterizations** | Opinions, rankings, "best for" claims, trend assertions | "Zustand is gaining momentum" backed by npm trends data, not vibes |

Every brief must pass L1 with zero errors. L2 claims must have sources. L3 claims must be defensible and presented as perspective, not fact.

### 2.2 Engagement Quality Criteria

A brief isn't done until it passes these checks:

- **Hook test:** Could the first slide work as a standalone post? If it doesn't stop the scroll alone, it fails.
- **Swipe motivation:** Does each slide create a reason to see the next one? (curiosity gap, building sequence, "wait, there's more")
- **Screenshot test:** Would someone screenshot any individual slide to share or save? At least 2-3 slides should pass this.
- **Comment bait:** Does the post naturally invite opinions? ("Do you agree?" is lazy — a genuinely debatable framing is better.)
- **Save trigger:** Does it contain reference-worthy information the audience will want to come back to?

### 2.3 The GFE Tie-In Spectrum

Product mentions should feel earned, not inserted. Here's the spectrum from most organic to most forced:

| ✅ Organic | ⚠️ Acceptable | ❌ Forced |
|---|---|---|
| GFE cited as the source of the data/insight | "Practice this on GreatFrontEnd" in caption | Mid-carousel "brought to you by GFE" slide |
| Post topic naturally aligns with a GFE feature | GFE mentioned in final slide as a resource | Shoehorning GFE into an unrelated topic |
| Author byline establishes GFE credibility | Carousel branded with GFE design language | Multiple GFE mentions throughout carousel |

**Rule of thumb:** The audience should get full value from the post even if they ignore every GFE mention. The product tie-in is a bonus, not a tax.

---

## 3. Format Best Practices

### 3.1 Supported Formats

| Format | Best For | Engagement Profile | Share of Top Posts |
|---|---|---|---|
| **Carousel** | Multi-point explainers (5+ points), step-by-step | Highest saves, strong swipe-through | 38% |
| **Single Image** | Cheatsheets, "how X works", roadmaps, comparison tables | High saves, high shares | 38% |
| **Animated GIF** | Architecture reveals, process flows, annotated screenshots | High watch time, "wow" factor | 14% |
| **Data Visualization** | Survey rankings, adoption trends, framework comparisons | High saves, strong authority | (subset of Single Image) |
| **Meme / Culture** | Relatable developer humor, shared experiences, hot takes | Highest raw likes, broadest reach | — |
| **Text-Only** | Personal takes, stories, hot opinions, breaking news | Authenticity signal, strong comments | 7% |

> **Important:** Carousels and single images are equally common in top-performing posts.
> Do not default to carousel — always consider whether a single image or GIF would be stronger.

### 3.2 Carousel Best Practices

| Element | Guideline |
|---|---|
| **Slide count** | 7–10 slides. Under 7 feels thin. Over 10, swipe fatigue sets in. |
| **Text per slide** | 30–50 words max. Carousel slides are visual — if it reads like a blog paragraph, it's too dense. |
| **Hierarchy per slide** | One headline idea + 2–3 supporting points. Never more than one key concept per slide. |
| **Visual elements** | Code snippets, diagrams, comparison tables, icons. Pure text slides should be the minority. |
| **Font size** | Must be readable without zooming on mobile. If a slide needs small text to fit, it has too much content. |

### 3.3 Slide-by-Slide Anatomy

| Slide | Role | Tips |
|---|---|---|
| **Slide 1 (Hook)** | Stop the scroll | Bold claim, surprising stat, provocative question, or visual pattern interrupt. No preamble. |
| **Slides 2–3** | Establish context | Set up the "why this matters" or "here's the situation" |
| **Slides 4–7** | Core content | The meat — each slide delivers one clear insight |
| **Slide 8–9** | Climax / synthesis | The "so what" — tie it together, deliver the punchline or key takeaway |
| **Final slide** | CTA + brand | Follow prompt, save prompt, GFE mention, or memorable closer |

### 3.4 Hook Patterns That Work

Based on top-performing posts and LinkedIn/Instagram best practices:

1. **The Ranking:** "Top 7 JavaScript frameworks in 2025" — lists promise structured value
2. **The Breakdown:** "How Netflix's front end actually works" — specificity + aspirational brand
3. **The Versus:** "Redux vs Zustand — which should you use?" — binary choice creates urgency
4. **The Myth-Bust:** "You don't actually understand JavaScript hoisting" — challenges ego (carefully)
5. **The Timely:** "Next.js 16 just dropped — here's what changed" — urgency + FOMO
6. **The Relatable:** "Every front-end developer has made at least one of these confessions" — belonging

### 3.5 Single Image Best Practices

Single images are **38% of our top-performing posts** — they deserve as much attention as carousels. They work because they're information-dense, screenshot-friendly, and save-worthy.

**Content structure:**
- Organize content into **4-7 distinct zones** (sections, quadrants, columns)
- Each zone has: a bold section title + 2-4 supporting points or a code snippet
- The brief defines the content for each zone; the design team handles layout
- Top performers: JS Hoisting (3 zones: What/Comparison Table/Why It Matters), localStorage (7 zones), Git Skills (4 progression levels)

**Brief writing tips for single images:**
- Define each content section clearly — the designer should not have to interpret ambiguous groupings
- Include a data table when the content is structured (tech stacks, tool comparisons, rankings)
- Suggest visual elements per section: "code snippet", "comparison table", "icon grid", "tech logos"
- The main title/headline is the hook — it must stop the scroll at thumbnail size

**What works in practice:**
- "How X Works" explainers with labeled sections
- Skill level progressions (beginner → advanced)
- Cheatsheets and comparison tables
- Flowcharts with decision points
- "What / How / Why" three-section structure

### 3.5.1 Data Visualization Best Practices

A subset of single images — used for survey data, framework rankings, and adoption trends. Four of our top posts use this format (State of JS series).

- Include a **data table** in the brief with exact values — the designer translates to a chart
- Always include **data source URL** and **disclaimer text** (e.g., "Usage percentages sourced from...")
- Suggest chart type (horizontal bar chart, ranking list with trend lines, etc.) but leave visual execution to design
- Tech logos next to each item are essential visual anchors
- These posts are highly save-worthy — accuracy is critical

### 3.6 Animated GIF Best Practices

Animated GIFs are **14% of our top-performing posts** and deliver the strongest "wow" factor. Top performers: Figma breakdown, Microfrontends, localStorage, Chrome 135.

- The hook frame (what's visible before play / at rest) must work as a static image too — most users see it paused in-feed first
- Keep total animation under 15 seconds — shorter is better for social feeds
- Sequential reveal (items appearing one by one) is the most reliable animation pattern for technical content
- Build from simple → complex: start with a familiar concept, then layer on new information
- Always ensure the final resting state is a complete, readable graphic — some platforms auto-pause or users re-watch
- **Always include a fallback** in the brief — describe the static alternative if animation isn't feasible
- Best for: architecture diagrams, process flows, annotated screenshots, UI component showcases

### 3.7 Meme / Culture Best Practices

- Relatability > cleverness. The best memes make people think "this is literally me"
- Use well-known meme templates when the joke fits — format recognition is half the engagement
- Developer-specific humor works because it signals "this is for us" — niche > broad
- Keep text minimal and punchy. If the joke needs explaining, it's not working
- Memes can afford to be slightly edgy or opinionated in ways that technical content can't

### 3.8 Text-Only (LinkedIn Native) Best Practices

- First line is everything — it's the only thing visible before "see more"
- One-liner paragraphs with line breaks perform best on LinkedIn (wall of text kills engagement)
- Personal voice and mild vulnerability outperform polished corporate tone
- Best for: hot takes after a release, "unpopular opinion" framings, career advice, personal stories
- Speed advantage: text-only posts can be published within minutes of a news event

---

## 4. System Design Principles

### 4.1 Pipeline Over Monolith

Brief creation should be a multi-stage pipeline, not a single prompt. Each stage has a clear input, output, and quality gate. This lets us:
- Isolate failures (a research error doesn't corrupt the whole brief)
- Parallelize where possible
- Insert human review at the right moment
- Improve individual stages independently

### 4.2 Research-First, Write-Second

The pipeline must separate research from writing. A common failure mode for AI-generated technical content is "confidently wrong" — the model generates plausible-sounding but inaccurate claims. The fix is to force research as an explicit, verifiable stage *before* any writing begins.

### 4.3 Reference Data is Guardrail, Not Gospel

Top-performing historical posts are used to calibrate quality and identify patterns — not as templates to copy. The content landscape evolves. What worked 6 months ago may feel stale now. The system should learn from patterns (specificity wins, comparisons drive comments) while leaving room for experimentation.

### 4.4 Designer-Ready Output

The brief is the handoff artifact. A designer should be able to produce the carousel from the brief alone. This means: explicit slide-by-slide structure, suggested visual treatments, all text finalized, and sources available for fact-checking if the designer wants to verify something.

---

## 5. Roadmap

### Phase 1: Foundation (Now)
- ✅ Repo structure and agents.md
- ✅ Plan and execution documents
- 🔲 Brief template finalized with sample briefs
- 🔲 Automated pipeline (research → draft → verify → final)
- 🔲 Reference data loaded (top posts + sample briefs)

### Phase 2: Optimization
- 🔲 Feedback loop: post performance data flows back into the system
- 🔲 Hook library: catalog of proven hook patterns with performance data
- 🔲 Accuracy checklist automation: automated fact-check stage

### Phase 3: Content Intelligence
- 🔲 Topic generation: system proposes topics based on content mix, trends, and gaps
- 🔲 Performance prediction: estimate engagement potential before publishing
- 🔲 Content calendar: automated weekly planning with pillar balance
