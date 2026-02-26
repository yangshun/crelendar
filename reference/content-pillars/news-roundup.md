# News Pillar: Biweekly News Format Guide

This guide applies to all **Biweekly News** posts (pillar: News).

## Research & Selection

1. **2-week lookback window.** Only cover updates from the last 2 weeks before the post's publish date.

   **Primary research sources (check all):**
   - **Newsletters in the window:** Pull issues from Bytes (bytes.dev/archives, Mon), JavaScript Weekly (javascriptweekly.com/issues, Fri), This Week in React (thisweekinreact.com/newsletter, Tue/Wed), Frontend Focus (frontendfoc.us/issues, Wed), TypeScript Weekly. Any item featured across 2+ newsletters is a strong signal.
   - **Official channels:** release blogs, GitHub releases, npm updates, browser release notes, TC39 proposals, ecosystem announcements.

2. **Cast a wide net.** Collect 15-20 candidates. Don't filter yet.

2b. **Verify every date.** For each candidate, confirm the exact release date against an official source (official blog post, GitHub release page, or npm page). Use direct web search for each item individually — do not rely on AI recall or research agent summaries for dates. Remove any item whose verified date falls outside the 2-week window. Record the verified date and source URL for each surviving candidate in research notes.

3. **Dedup check.** Cross-reference every candidate against `reference/covered-topics.md`. Any topic already covered in a previous Biweekly News or Tue Tools post is excluded — no exceptions. A major version bump of a previously covered tool (e.g., "Vite 8 GA" after covering "Vite 8 Beta") IS allowed as a new entry.

4. **Rank by importance.** Score each remaining candidate on:
   - **Immediate workflow impact** (highest weight) — does this change what a developer does TODAY? A new formatter they can install now > a browser API that needs cross-browser adoption. Deprioritize browser feature releases (Chrome, Firefox, Safari) unless they immediately change how devs write code.
   - **Audience size** — React update > niche library
   - **Novelty** — first-of-its-kind > incremental patch
   - **Debate potential** — breaking changes, controversial decisions, governance shifts
   - **Code-worthiness** — is there a code snippet or config to show?

5. **Select the top items (target 8-10, but the 2-week window is the hard constraint — if only 4 items qualify, cover 4).** Drop the rest. Never include items outside the 2-week window just to hit the count. Document dropped items and reasoning in research notes.

6. **Assign treatment tier** to each item (see below).

## Treatment Tiers

| Tier | Items | Treatment | Slide allocation |
|---|---|---|---|
| **Tier 1: Headline** | 2-3 items | Dedicated slide per item. Headline + 2-3 bullets + code snippet or visual. Full treatment. | 1 slide each |
| **Tier 2: Quick Hits** | 5-7 items | Grouped onto 1-2 slides. Bold name + 1-line description per item. No code blocks. Compact, scannable. | 3-4 items per slide |

**Tier 1 if:** breaking change, major release, new tool/API, code snippet makes it click, high debate potential.
**Tier 2 if:** incremental update, minor version, noteworthy but no code anchor needed, "good to know."

**When fewer than 8 items qualify:** Adjust tiers proportionally. With 5-7 items: 2-3 Tier 1 + rest as Tier 2 on 1 Quick Hits slide. With 3-4 items: 2-3 Tier 1, rest as Tier 2. No Quick Hits slide needed if only 1-2 Tier 2 items — group them anyway for format consistency, or promote all to Tier 1.

## Slide Structure

Target: **5-10 slides total** (scales with item count)

```
Slide 1: Hook (title + date range + "X updates" count badge)
Slides 2-4: Tier 1 items (1 per slide, full treatment with code/visuals)
Slide 5 (optional): AI Spotlight (front-end AI items, if any exist in the window)
Slides 5-6: Quick Hits (Tier 2 items, 3-4 per slide)
Final Slide: CTA
```

**AI Spotlight:** Front-end AI updates get their own treatment when available - client-side AI APIs (WebNN, WebGPU ML), AI-assisted dev tools, AI-built projects, coding agent news. If a substantial AI item exists in the window, give it a dedicated slide. If minor, fold into Quick Hits with an "AI" tag.

### Quick Hits slide format:
- Headline: "Quick Hits" or "Also This Fortnight"
- List of 3-4 items, each as:
  **[Tool/Topic vX.X]** — one-line description of what shipped/changed
- No code blocks. Compact text. Scannable at mobile size.

## Post-Brief: Update Dedup Tracker

After finalizing the brief, append all covered topics (both Tier 1 and Tier 2) to `reference/covered-topics.md`.
