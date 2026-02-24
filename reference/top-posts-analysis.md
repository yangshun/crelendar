# Top-Performing Posts Analysis — Brief & Visual Patterns

> **Date:** 2026-02-24
> **Scope:** All 29 briefs + 80+ finished images from `top-linkedin-posts/`
> **Purpose:** Identify what actually works to refine the brief template in `agents.md`

---

## 1. Brand Design System (from finished images)

### Consistent Elements Across ALL Posts
- **GFE logo** (the `<>` mark): bottom-left corner on every slide
- **"Find out more at → greatfrontend.com"**: bottom-right footer bar on every slide
- **Portrait orientation** (4:5 ratio): optimized for LinkedIn/Instagram mobile feeds
- **Bold, large headlines**: always the dominant visual element — readable at thumbnail size
- **Monospace code font**: used for all code snippets, API names, and technical terms
- **Tech logos**: used extensively as visual anchors (React atom, Next.js N, framework icons, etc.)

### Two Distinct Color Themes
| Theme | Used For | Examples |
|---|---|---|
| **Dark mode** (dark navy/black bg) | Tech breakdowns, comparisons, deep dives, roadmaps, data posts | Netflix, Spotify, Redux vs Zustand, React Hooks, Git Skills, State of JS series, Front End Roadmap, Framework Picker |
| **Light mode** (white/cream bg) | News/releases, career content, educational walkthroughs, CTAs | ECMAScript 2025, JS Closures, Next.js 16, Frontend Resume Tips, Uber Interview, Tue Tools |

**~65% of top posts use dark theme.** Dark seems to be the default; light is used when the topic is lighter/educational.

### Per-Topic Accent Colors
- **Yellow/gold**: JS-related (ECMAScript 2025, JS Closures — gold 3D "JS" letters)
- **Blue/purple**: React-related (React Hooks, React UI Libraries, Redux vs Zustand)
- **Green**: tools/ecosystem (Spotify brand green, Electron, Git Skills green accents)
- **Pink/magenta**: State of JS data series (consistent hot pink bars)
- **Blue/white**: Next.js, Uber (clean, corporate feel)
- **Red/black**: Netflix brand colors, Chrome

### Slide Layout Patterns

**Hook slides (Slide 1):**
- Huge bold title (occupies ~60% of slide area)
- One subtitle/tagline underneath
- Relevant tech logo or 3D illustration
- Minimal text — never more than ~15 words total
- Strong visual identity (topic-specific colors/imagery)

**Content slides (mid-carousel):**
- One clear headline at top
- Code snippet OR comparison table OR bullet list — never all three
- Supporting visual (icon, logo, diagram) — always present
- 20-40 words of readable text (code excluded)
- Clear visual hierarchy: headline → main content → supporting detail

**CTA slides (final):**
- "Stay Updated with GreatFrontEnd" or "Join 1M+ engineers who trust GreatFrontEnd"
- One CTA button (styled pill: "Share this post with your network!", "Learn more at greatfrontend.com", "Level Up Your Front End Skills")
- GFE branding prominent
- Matches the color theme of the carousel

### Visual Direction Quality Spectrum (Brief → Output)

| Brief Visual Detail Level | What the designer actually needed | Examples |
|---|---|---|
| **Minimal** ("use yellow/orange palette") | Designer had freedom, produced great work anyway — but required design maturity | ECMAScript 2025 |
| **Layout + icons specified** ("speedometer icon, Rust logo") | Sweet spot — enough guidance without being prescriptive | Next.js 16, Tue Tools |
| **Detailed layout specs** ("60%/40% split, two-column, side-by-side code blocks") | Most designer-ready — output closely matched the brief | JS Closures, Frontend Resume Tips |
| **Reference to previous post** ("use the same format as Netflix post") | Efficient for series posts — leverages existing design language | State of JS series, Spotify |

---

## 2. Brief Structure Patterns (from 29 brief.md files)

### What ALL Top Briefs Actually Have

Every brief, regardless of format, has this two-part structure:

```
PART 1: Caption / Post Content
- Opening hook (first line)
- Educational/contextual body
- Engagement question
- Hashtags

PART 2: Design / Visual Instructions
- Format declaration
- Visual content specification (slides, sections, or layout)
- Designer notes and references
```

This is the actual working structure. The template in `agents.md` has a more complex hierarchy (Review Summary → Visual Content → Core Sections) that none of the real briefs follow.

### Section Labels Used (inconsistent but consistent pattern)

| Part 1 Labels (caption) | Count |
|---|---|
| "Content Brief" | 8 |
| "Post Content" | 5 |
| "Post Caption" | 4 |
| "Post caption" | 1 |
| "LinkedIn" | 2 |
| No label (text starts directly) | 9 |

| Part 2 Labels (visual) | Count |
|---|---|
| "Design Brief" | 10 |
| "Media Brief" | 2 |
| "Graphics Brief" | 3 |
| "Infographic Brief" | 2 |
| No visual section | 4 (text-only or caption-only briefs) |

### Format Distribution in Top Posts

| Format | Count | % |
|---|---|---|
| Carousel (multi-slide) | 11 | 38% |
| Single-image infographic (static) | 11 | 38% |
| Animated GIF / infographic | 4 | 14% |
| Text-only | 2 | 7% |
| Hybrid (GIF + code) | 1 | 3% |

**Key insight:** Carousels and single-image infographics are equally common. The current template is heavily carousel-biased.

### Slide Counts (Carousels Only)

| Post | Slides | Engagement Signal |
|---|---|---|
| ECMAScript 2025 | 10 | High (news + reference) |
| React Hooks | 10 | High (educational + interview) |
| Next.js 16 | 8 | High (news) |
| JS Closures | 8 | High (deep dive) |
| Frontend Resume Tips | 7 | High (career) |
| Uber Interview | 6 | High (interview challenge) |
| React UI Libraries | 6 | High (comparison) |
| Tue Tools | 5 | Moderate (news roundup) |
| Redux vs Zustand | 4 (+ intro) | High (comparison) |
| TS Utility Types | 7 | Moderate (educational) |
| System Design Cheatsheet | 2 | High (reference/save) |

**Median: 7 slides. Range: 2-10.** The 7-10 guideline in agents.md is reasonable for full carousels, but 5-6 slide posts also perform well for focused comparisons.

---

## 3. Caption Patterns

### Structure (consistent across all posts)
1. **Hook line** (the "see more" preview): Bold statement, question, or claim
2. **Body** (2-6 sentences): Context, key points, or a bulleted list mirroring the visual content
3. **Engagement prompt**: Question inviting comments ("Which one are you using?", "What level are you at?")
4. **Hashtags**: 5-9 tags, mix of broad (#JavaScript) and specific (#ECMAScript2025)
5. **GFE link** (when present): UTM-tagged URL at the very end

### Average caption length: ~140 words (excluding hashtags)

### Hook Patterns That Appear in Top Posts

| Pattern | Example | Frequency |
|---|---|---|
| **Provocative question** | "Is Modern Front End Development Really Better?" | 5 posts |
| **Bold declarative** | "Chrome 135 introduces a fully customizable `<select>`" | 6 posts |
| **Problem/pain point** | "Tired of your frontend repo turning into a spaghetti mess?" | 3 posts |
| **News announcement** | "JavaScript Just Got a Major Upgrade" | 4 posts |
| **List/ranking promise** | "Top 10 JavaScript Front End Frameworks from 2024" | 5 posts |
| **Challenge to reader** | "Can you solve this Uber front end interview question?" | 2 posts |
| **Skill gap** | "Git Skills That Separate Junior Developers from Senior Ones" | 3 posts |

---

## 4. GFE Tie-In Patterns (from actual posts)

### How GFE appears in finished designs
- **Every slide** has the "Find out more at → greatfrontend.com" footer
- **Hook slides** sometimes include GFE logo
- **CTA slides** always feature GFE prominently

### GFE tie-in spectrum (actual practice)

| Level | Description | Count |
|---|---|---|
| **Full CTA slide** | Dedicated final slide with GFE branding and CTA | 15 posts |
| **Caption link only** | UTM-tagged URL in caption, no visual GFE reference beyond footer | 8 posts |
| **Hashtag only** | Just #GreatFrontEnd in tags | 4 posts |
| **None** | No GFE mention at all (beyond the standard footer) | 2 posts |

### CTA Copy That Appears on Final Slides (actual text from images)
- "Stay Updated with GreatFrontEnd — Follow us for the latest front end tools, news, and interview preparation tips."
- "Join 1M+ engineers who trust GreatFrontEnd — greatfrontend.com/interviews"
- "Ready to Ace the Interview? GreatFrontEnd has resources to master front end interviews."
- "Share this post with your network!"
- "Level Up Your Front End Skills"
- "Learn more at greatfrontend.com"

---

## 5. Sources & Verification Patterns

| Approach | Count | Examples |
|---|---|---|
| No sources at all | 18 posts | Most educational and career posts |
| Source URL in caption disclaimer | 4 posts | State of JS series ("sourced from https://...") |
| Sources in brief but not in post | 3 posts | Netflix (engineering blog URLs in brief), Redux vs Zustand |
| Sources as planned first comment | 1 post | Tue Tools ("Comments section: Read more here...") |
| Inline per-item sources | 2 posts | Netflix tech stack table, Spotify tech stack table |

**Key insight:** Formal source documentation is rare in the actual briefs. When present, it's usually data-backed posts (State of JS) or tech stack posts (engineering blog citations). The template's "Sources & Verification" section with `[Claim] — [Source URL]` format doesn't match how sources actually appear.

---

## 6. Template vs Reality — Gap Analysis

### What the current template prescribes but NO top brief actually uses:

| Template Element | Used in Practice? |
|---|---|
| Review Summary (Topic, Pillar, Format, Key angle, GFE tie-in, Confidence, Similar past post) | **NEVER** — 0 of 29 briefs |
| Date field | **NEVER** |
| Platform field | **NEVER** |
| Confidence rating | **NEVER** |
| Similar past post reference | **NEVER** (though some reference previous posts for design) |
| Standalone GFE Tie-in section (What/Where/Copy) | **NEVER** — always inline |
| Standalone Sources & Verification section | **1 of 29** (Redux vs Zustand) |
| Standalone Designer Notes section | **NEVER** — always inline per slide/section |
| `## Slide N — [Title]` markdown heading format | **NEVER** — plain text labels like "Slide 1:" |

### What top briefs actually do that the template DOESN'T account for:

| Real-World Pattern | Template Coverage |
|---|---|
| Caption-first ordering (caption → design) | Template puts visuals first, caption after |
| "Content Brief" / "Design Brief" two-part structure | Not in template |
| Format declaration at the top of design section | Not in template |
| Reference to previous post's design | Not in template |
| Reference images/URLs for visual inspiration | Not in template |
| Per-slide layout specs (columns, grids, percentages) | "Visual direction" is a single line in template |
| Multi-platform captions (LinkedIn + Instagram) | Not in template |
| Data tables for tech stacks and rankings | Not in template |
| UTM-tagged links for tracking | Not in template |
| "Comments section" for source links | Not in template |
| Animation sequence and fallback notes | Partially covered in Option C |
| Color theme specification | Not in template |
| Per-slide accent/thematic styling | Not in template |

---

## 7. Key Recommendations for Template Refinement

### High Priority
1. **Restructure brief order to Caption → Design** (matching real workflow)
2. **Add format declaration as a required first field** in the design section
3. **Replace the Review Summary with a simpler metadata block** (just topic, pillar, format, GFE tie-in yes/no)
4. **Expand visual direction into structured sub-fields**: layout type, color theme, reference images, per-slide layout specs
5. **Add "Design Reference" field** for referencing previous successful posts
6. **Add single-image infographic template section** (spatial layout zones, not slide-by-slide)
7. **Add data table structure** for tech stack and ranking posts

### Medium Priority
8. **Standardize section labels** ("Caption" and "Design Brief" — pick one term each)
9. **Add multi-platform caption support** (LinkedIn + Instagram variants)
10. **Add UTM tracking link field** for GFE links
11. **Simplify Sources to match reality**: inline per-item + optional "planned first comment" field
12. **Add color theme/accent specification** to design section
13. **Make CTA slide a standard component** with proven copy options

### Low Priority
14. **Add animation fallback notes** for animated infographic format
15. **Add versioning support** (draft/revision tracking)
16. **Document the brand design system** (dark/light themes, GFE footer, logo placement) as a reference
