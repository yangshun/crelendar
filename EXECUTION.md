# EXECUTION.md — Brief Creation Pipeline

## Overview

This document defines the **exact pipeline repo Claude follows** to produce a marketing brief from a topic. The pipeline has 5 stages, each with defined inputs, outputs, and quality gates. Stages run sequentially — no stage begins until the previous stage's output is validated.

**Pipeline at a glance:**

```
CLICKUP TASK → [1. Research] → [2. Angle, Format & Hook] → [3. Draft Brief] → [4. Verify & Polish] → [5. Final Output] → GOOGLE DOC + CLOSE SUBTASK
```

**Time budget:** The full pipeline should produce a review-ready brief efficiently. If any stage gets stuck, flag the blocker and move on — don't hallucinate to fill gaps.

---

## Stage 1: Research

### Goal
Gather accurate, current, comprehensive information on the topic. This is the most important stage — everything downstream depends on it.

### Input
- ClickUp "write brief" subtask (primary) — or topic from marketing manager for manual runs
- Content pillar assignment from parent task custom fields (or infer from topic)

### Process

**Step 0: ClickUp Task Intake** (skip if topic was given manually)

0a. **Find the next "write brief" subtask** from the ClickUp "2026 Calender" list (ID: `901814889385`). Use `clickup_search` to find subtasks with status "write brief". For each candidate subtask, fetch its **parent task** using `clickup_get_task` — the parent task's due date is the **post publish date**, which determines priority. **Always pick the subtask whose parent has the earliest publish date.** Skip any tasks whose parent publish date has already passed (overdue posts are handled separately by the marketing team). ClickUp due dates are epoch milliseconds — convert to human dates for comparison (e.g., `1772404200000` ÷ 1000 → Unix timestamp → date).

0b. **Get the parent task** (the topic). Read the parent task's name, description, and custom fields using `clickup_get_task` with the parent task ID.

0b-ii. **Extract and evaluate manager requirements from the description.** The parent task's description may contain additional requirements from the marketing manager - specific angles, mandatory talking points, visual preferences, tone notes, links to include, or constraints (e.g., "must mention X feature", "don't compare to Y", "use this specific CTA link"). List these as explicit constraints. Then **sanity-check each requirement:**
   - Does it conflict with something the research will likely surface? (e.g., manager says "focus on performance" but the topic's real insight is about DX)
   - Does it make sense for the chosen format? (e.g., "include 10 talking points" on a single-image post)
   - Is a requested claim actually accurate? (e.g., manager says "fastest framework" - verify before including)
   - Does it conflict with pipeline best practices (tone rules, engagement patterns, format guidelines)?
   If a requirement looks off, **flag it with a `[MANAGER-CHECK]` tag** in the research notes and proceed with a suggested alternative - don't silently ignore it, but don't blindly follow it either. Requirements that check out become hard constraints for Stages 2-4. If the description is empty or contains only the topic name, note "no additional requirements" and proceed.

0c. **Note the "ClickUp Brief" custom field** on the parent task (field ID: `68e015f7-6830-44ea-ab09-6280bdd0d00e`). This is where you'll set the ClickUp Doc URL after writing the brief in Stage 5.

0d. **Note the content pillar, post format, and topic category** from the parent task's custom fields. These inform Stage 2 decisions (some may already be decided by the marketing manager).

0e. **Read reference links from the subtask description.** The "write brief" subtask description typically contains links to: an old briefs Google Drive folder, the content pillar strategy doc, and the design kit guidelines doc.

1. **Check prior art.** Search `top-linkedin-posts/` and `briefs/approved/` for any previous posts on the same or adjacent topics. Note what angles were covered and how they performed.

2. **Primary research.** Gather facts from authoritative sources:
   - Official documentation and release notes
   - Official tech blogs (company engineering blogs for breakdowns)
   - GitHub repos (stars, recent commits, contributor activity)
   - npm trends / bundlephobia for adoption and size data
   - Reputable tech publications (not random Medium posts)
   - Conference talks and official announcements

3. **Mine for insights.** Separate what's common knowledge from what's genuinely new or surprising. For each major fact or claim, ask:
   - **Would a mid-level engineer already know this?** If yes, it's context — not the headline.
   - **What's the non-obvious layer?** Every topic has a surface understanding and a deeper truth. Dig for the deeper truth. Examples:
     - Surface: "React uses a virtual DOM" → Insight: "React 19's compiler eliminates the need for useMemo/useCallback in most cases"
     - Surface: "Use debounce for search inputs" → Insight: "300ms is the sweet spot — under 200ms wastes API calls, over 500ms feels laggy"
     - Surface: "System design interviews test architecture" → Insight: "Interviewers score on 6 axes, and the 2 most overlooked ones are what flip no-hire to hire"
   - **Is there authoritative data that contradicts popular belief?** Myth-busting backed by official sources is the highest-engagement content pattern.
   - **Can I cite a specific source that gives this credibility?** Insights from official engineering blogs, core team members, or verified benchmarks carry more weight than generic best practices.

4. **Compile research notes.** Save to `reference/topic-research/YYYY-MM-DD-topic-slug.md` with:
   - Key facts and data points
   - Source URLs for every claim
   - **Insight map:** What the audience likely already knows (common understanding) vs. what would be new/surprising (the insight). This map directly feeds Stage 2 angle selection and Stage 3 content.
   - Potential inaccuracies or common misconceptions to avoid (or bust)

### Output
A research document with sourced facts and a clear insight map, ready for the next stage.

### Quality Gate
- ❏ Minimum 3 authoritative sources consulted
- ❏ All version numbers and release dates verified against official sources
- ❏ No claim exists without a source URL
- ❏ Prior art checked — not duplicating a recent post
- ❏ Insight map present — at least 2-3 facts/angles identified that go beyond common understanding

---

## Stage 2: Angle, Format & Hook

### Goal
Choose the most engaging angle for the topic and craft a hook that stops the scroll. This stage is strategic — the same topic can be a 100-like post or a 1,000-like post depending on the angle.

### Input
- Research notes from Stage 1
- Content pillar (determines the framing approach)
- Manager requirements from task description (extracted in Step 0b-ii) - validated requirements are hard constraints; any flagged with `[MANAGER-CHECK]` should be raised before proceeding
- Historical performance data for similar topics

### Process

1. **Generate 3 candidate angles.** Each angle should be a different framing of the same topic. For example, "JavaScript closures" could be:
   - Deep Dive: "The 3 memory leak patterns closures create (and how to fix them)"
   - Myth-Bust: "You've been explaining closures wrong in interviews"
   - Practical: "Closures in 60 seconds — the only explanation you need"

2. **Score each angle** against these criteria:
   - **Insight depth:** Does this angle reveal something the audience doesn't already know? Apply the "top 3 Google results" test — if the insight appears in the first 3 search results for the topic, it's common knowledge, not an insight. The angle should be built around findings from the insight map (Stage 1, step 3), not around surface-level facts.
   - **Novelty:** Has this angle been done to death, or is it fresh?
   - **Specificity:** Is it concrete enough to stop scrolling?
   - **Debate potential:** Will people comment to agree/disagree?
   - **Save-worthiness:** Will people bookmark this for reference?
   - **GFE alignment:** Does it naturally connect to something GFE offers?

3. **Select the best format** for the chosen angle using the Format Selection Guide in `agents.md`. **Do not default to carousel.** Before selecting carousel, ask: "Could this work as a single image, animated GIF, or data visualization?"

   Decision checklist:
   - How many distinct points does the content have? (<5 → single image or data viz, 5+ → carousel)
   - Is the content a single concept, cheatsheet, or "how X works"? (→ single image)
   - Is it a process/flow or architecture with relationships? (→ animated GIF)
   - Is it survey data, rankings, or adoption stats? (→ data visualization)
   - Is it humor or relatable culture? (→ meme)
   - Is it a hot take, story, or opinion? (→ text-only)
   - Is it time-sensitive news? (→ text-only for speed, upgrade format later if warranted)

   **Format variety check:** Review the last 5 posts in `briefs/drafts/` and `briefs/approved/`. Avoid using the same format 3+ times in a row. Rotate between formats.

   **Format rationale is required** — explain in the Brief Info why this format was chosen over alternatives. The marketing manager makes the final call.

   Optionally suggest a **design inspiration** reference from the list in `agents.md` (ByteByteGo, Nikki Siapno, Design Gurus, Codemia, NeetCode, Pragmatic Engineer) if a style match is clear.

4. **Draft 2-3 hook variations.** Each hook should use a different pattern:
   - Ranking/list ("Top 7...")
   - Surprising claim ("You don't need X anymore")
   - Specific question ("Why does Netflix use X instead of Y?")
   - Timely trigger ("X just released — here's what changed")

5. **Pressure-test the visual hook.** The hook is the headline on Slide 1 (carousel) or the main title (single image) — it's the thing that stops the scroll in the feed. For each candidate hook, check:

   - **Does it contain a specific number, name, or claim?** "6 things interviewers score you on" > "What interviewers look for." "Why Netflix uses React" > "How companies choose frameworks."
   - **Does it use contrast or surprise?** "You can nail the architecture and still get rejected" > "Tips for system design interviews."
   - **Would someone screenshot JUST this headline?** If the hook alone wouldn't get engagement, it's too generic.
   - **Is it under 15 words?** Visual hooks must be instantly readable at mobile thumbnail size.

   Top hook patterns from our best-performing posts:
   - Surprising specific: "Up to 10x faster Fast Refresh" (Next.js 16)
   - Ego challenge: "You've been explaining closures wrong in interviews"
   - Named entity + mystery: "How Netflix serves 200M+ users — their front-end stack"
   - Quantified list: "The 6 evaluation axes behind every hire/no-hire decision"
   - Binary tension: "Redux vs Zustand — which should you use in 2025?"

   Select the hook with the best combination of specificity, curiosity, and clarity.

### Output
- Chosen angle with rationale
- Recommended format with rationale (why this format, not another)
- Final hook (Slide 1 text for carousels, headline/opener for other formats)
- Rough content arc outline
- Design inspiration reference (if applicable)

### Quality Gate
- ❏ Angle is specific, not generic
- ❏ Format is chosen with explicit justification (not just "carousel because it's default")
- ❏ Format variety checked against recent posts
- ❏ Hook works as a standalone piece of content (would it get engagement on its own?)
- ❏ Content arc has a clear structure appropriate to the chosen format

---

## Stage 3: Draft Brief

### Goal
Produce the complete slide-by-slide brief following the standard template.

### Input
- Research notes (Stage 1)
- Chosen angle, format, hook, and arc (Stage 2)

### Process

Follow the flexible brief template in `agents.md`. Use the **Header** and **Core Sections** for every brief, then fill in the **Visual Content** section matching your chosen format.

**Content quality rules (apply to ALL formats):**

Every content section/slide must include at least ONE of:
- A **concrete example** (named tool, framework, company, or scenario)
- A **code snippet** or technical artifact (API call, component structure, config)
- A **specific number** (percentage, metric, count, version)
- A **contrast pattern** (common mistake vs correct approach, or before/after)

**Avoid abstract-only sections.** "Define clear responsibilities for each component" is a principle. "Your Autocomplete needs 3 layers: UI Component → Debounce Logic → API Client" is actionable content. Readers save and share the second, scroll past the first.

**Example domain-matching.** All BAD/GOOD examples and code anchors must match the abstraction level of the topic. System design briefs use architectural examples (SSR vs CSR, polling vs WebSocket, client-side vs server-side filtering). Machine coding briefs use component-level examples (state management, event handlers, ARIA attributes). Don't use library-choice examples (Redux vs Zustand) in a system design context, or architectural examples in a machine coding context. Match the abstraction level to the interview type.

**Lead with insights, not common knowledge.** Each content section should teach the audience something they didn't already know — or reframe something they thought they knew. Use the insight map from Stage 1 to identify which facts are genuinely new vs. context. Common knowledge can appear as setup/context, but the core point of each section must go deeper. Ask: "Would a mid-level engineer with 3 years of experience already know this?" If yes, either cut it, use it as a brief setup for the real insight, or find the non-obvious layer underneath it.

**Include at least one "what goes wrong" element.** Top-performing posts show mistakes alongside correct approaches. This creates recognition ("I've done that!") and drives comments. Examples:
- ❌ "Fetching on every keystroke" → ✅ "Debounce with 300ms delay"
- ❌ "One giant component with all state" → ✅ "Split by responsibility"

**Use progressive structure when possible.** Don't give all sections equal weight. Options:
- Skill progression: Basic → Intermediate → Advanced
- Layered reveal: Simple concept → Real-world complexity → Edge cases
- Familiar → Surprising: Start with what audience knows, build to what they don't
- Common → Overlooked: Cover the obvious first, then reveal the hidden factors

**Format-specific guidance:**

#### For Carousels:
1. **Write the hook slide.** Under 15 words for the headline. Instantly understandable. Include visual direction.
2. **Write slides 2 through N-1.** One idea per slide. Headline + 2-3 supporting points. 30-50 words max. Include visual direction for each.
3. **Each content slide needs a concrete anchor.** A code snippet, a named example, a number, or a contrast. If a slide is pure text bullets with no concrete anchor, rewrite it or merge it with another slide.
4. **Write the closer slide.** Summary/cheatsheet (high saves), strong takeaway (high comments), or CTA + GFE mention.
5. **Target 7-10 slides total.** Under 7 feels thin. Over 10, swipe fatigue sets in.
6. **Maintain swipe motivation.** Each slide should create a reason to see the next one.

#### For Single Images:
1. **Nail the headline/text overlay.** This is your entire visual real estate — every word matters.
2. **Each content zone needs specificity.** For technical topics: include example questions, tool names, or code fragments. For career topics: include specific phrases, metrics, or before/after examples. If a zone reads like a generic tip ("be a good communicator"), add a concrete "what this looks like" example.
3. **Describe the visual clearly.** The designer needs to know exactly what to create.
4. **Ensure the image works at thumbnail size.** Mobile feeds are small — test visual hierarchy mentally.

#### For Animated Infographics:
1. **Define the hook frame.** What does the viewer see before animation plays or at first glance in the feed?
2. **Map the animation sequence.** Number each stage of what appears, moves, or transforms.
3. **Describe the final state.** What's the complete picture when the animation finishes?
4. **Include motion notes.** Timing, easing, style cues — the animator needs direction, not just frames.

#### For Memes / Culture:
1. **Specify the format/template.** Name the meme format or describe the original concept.
2. **Write exact text.** Meme copy must be precise — a single word change can kill the joke.
3. **Explain why it works.** This helps the reviewer and future briefs understand the humor mechanics.

#### For Text-Only (LinkedIn Native):
1. **Write the full post text.** First line is critical — it's the "see more" preview. Write in the author's voice.
2. **Include formatting notes.** Line breaks, emoji usage, structural choices that affect readability.
3. **Prioritize speed for news.** Text-only is the fast format — don't over-produce when timeliness matters.

**For all formats:**

4. **Write the caption.** (For text-only posts, this becomes the engagement prompt instead.)
   - First line hooks — it's the "see more" preview on LinkedIn
   - 2-4 sentences of context or additional insight not in the visual content
   - 3-5 relevant hashtags (mix of broad and specific)
   - Single CTA: follow, save, share, or check out GFE (pick one, not all)

5. **Consider a CTA slide/element.** 15 of 29 top-performing posts include a dedicated CTA slide or footer zone. For carousels: add a final slide with proven GFE copy. For single images: include a footer zone. For text-only or memes: skip. Proven options from top posts:
   - "Stay Updated with GreatFrontEnd"
   - "Join 1M+ engineers who trust GreatFrontEnd"
   - "Ready to Ace the Interview?"

6. **Write the GFE tie-in section** (if applicable — skip for pure memes/culture posts).
   - What specific GFE feature/content is relevant?
   - Where should the mention appear?
   - Draft the exact GFE mention text

7. **Compile sources.** List every source URL used. For memes/culture posts with no factual claims, note "No factual claims — culture/humor post."

### Output
A complete brief following the template in `agents.md`.

### Quality Gate
- ❏ Brief follows the correct format section from the template
- ❏ Hook/headline is strong enough to stop the scroll on its own
- ❏ Content density is appropriate for the format (no carousel slides over 50 words; no overloaded single images)
- ❏ Visual direction / creator notes are clear enough for handoff
- ❏ Caption is written and includes hashtags + CTA
- ❏ GFE tie-in is documented and feels organic (or explicitly skipped with reason)
- ❏ Sources section is complete

---

## Stage 4: Verify & Polish

### Goal
Catch every factual error, tighten the writing, and pressure-test engagement potential.

### Input
- Complete draft brief (Stage 3)
- Original research notes (Stage 1)

### Process

**Accuracy pass:**

1. **Re-verify every hard fact** in the brief against its source:
   - Version numbers match current releases
   - API names and syntax are correct
   - Company attributions are verified (e.g., "Netflix uses React" — confirmed via their tech blog)
   - Statistics have sources and dates
   - No outdated information presented as current

2. **Flag anything uncertain** with `[VERIFY]` tag and a note explaining what needs checking.

3. **Check for common AI-generated errors:**
   - Libraries/tools described with features they don't actually have
   - Conflating similar but different technologies
   - Outdated syntax or deprecated APIs presented as current
   - Overly confident claims that should be hedged

**Engagement pass:**

4. **Re-read the hook** fresh. Does it still stop the scroll after you've been deep in the content? If not, rewrite it.

5. **Check slide flow.** Read just the headlines of slides 1 through N in sequence. Do they tell a coherent, compelling story on their own? If not, reorder or rewrite headlines.

6. **Kill weak slides.** Any slide that doesn't teach, surprise, or advance the narrative gets cut or merged. 7 strong slides > 10 padded slides.

7. **Check for comment triggers.** Is there at least one moment in the carousel that will make someone think "wait, I disagree" or "yes, this is so true" or "I've experienced this"? If not, sharpen an opinion or add a relatable example.

8. **Verify CTA numbers against live product.** Any product count in the CTA, footer, or first comment (e.g., "15 system design questions", "91 React questions") must be verified against the live GFE page, not just research notes. Research notes can go stale between when you gathered them and when the brief is finalized. Check the actual URL you're linking to and confirm the number matches what's on the page.

9. **Insight freshness check.** Re-read each content section and ask: "Would an engineer with 3 years of experience already know this?" Flag any section where the answer is "yes" for the core point (not just the setup). For flagged sections, either:
   - Replace the common-knowledge point with the deeper insight from the research notes
   - Add a "but here's what most people get wrong" twist that reframes the familiar
   - Cut the section and redistribute its space to sections with genuine insights
   Every section's core point must be something the reader is unlikely to already know, sourced from authoritative references — not generic best-practice advice repackaged.

9. **Check content progression.** Read the content sections/slides in order. Do they build on each other, or could they be shuffled randomly without losing anything? If the order doesn't matter, restructure into one of these arcs:
   - Familiar → Surprising (what you know → what you're missing)
   - Easy → Hard (progressive difficulty)
   - Problem → Solution (pain point → fix)
   - Common → Overlooked (obvious stuff → hidden factors that actually matter)

10. **Check for concrete anchors.** Count the number of content sections/slides that contain at least one concrete example, code snippet, specific number, or contrast pattern. If fewer than 60% of sections have a concrete anchor, add them. Abstract-only sections are the #1 quality gap between our briefs and top performers.

**Writing pass:**

11. **Cut filler words.** Remove "basically", "essentially", "actually" (unless genuinely needed for contrast), "really", "very", "just".

12. **Activate passive voice.** "The DOM is updated by React" → "React updates the DOM."

13. **Check jargon calibration.** The audience is engineers - don't over-explain basics. But don't assume familiarity with niche tools without context.

14. **Tone check.** Re-read the caption and slide headlines out loud. Do they sound like something you'd post on Reddit, or something a corporate social media manager wrote? Specific red flags:
    - Inspirational closers ("keep learning!", "you've got this!")
    - AI-speak ("it's worth noting", "let's delve", "comprehensive guide")
    - LinkedIn cringe ("thought leaders", "level up", "let's explore")
    - Over-hedging ("it could be argued that", "one might consider")
    If any section fails the vibe check, rewrite it blunter and more direct.

### Output
A polished, verified brief ready for review.

### Quality Gate
- ❏ Zero `[VERIFY]` tags remaining (all resolved or explicitly flagged for human review)
- ❏ Every fact cross-checked against source
- ❏ Headline-only read-through tells a clear story
- ❏ No slide exceeds word limit after edits
- ❏ At least one strong engagement trigger present
- ❏ Content sections have a clear progression (not randomly orderable)
- ❏ 60%+ of content sections have a concrete anchor (example, code, number, or contrast)
- ❏ Every section's core point goes beyond common knowledge (insight freshness check passed)
- ❏ Writing is tight — no filler

---

## Stage 5: Final Output

### Goal
Package the brief in its final format, ready for the marketing manager's review.

### Input
- Polished brief (Stage 4)

### Process

1. **Format the brief** using the standard template from `agents.md`.
2. **Save to** `briefs/drafts/YYYY-MM-DD-topic-slug.md` (local backup).
3. **Humanize the text.** Before writing to ClickUp, clean the brief text of common AI artifacts:
   - Replace em dashes (—) with regular dashes (-)
   - Replace en dashes (–) with regular dashes (-)
   - Replace curly/smart quotes (" " ' ') with straight quotes (" ')
   - Strip invisible Unicode characters: zero-width spaces (U+200B), zero-width joiners (U+200D), zero-width non-joiners (U+200C), byte order marks (U+FEFF), word joiners (U+2060), and soft hyphens (U+00AD)
   - Replace horizontal ellipsis (…) with three dots (...)

   Run this as a text replacement pass on the full brief content string before passing it to `clickup_update_document_page`. The local backup in `briefs/drafts/` is NOT cleaned - keep the original there for diff visibility.
4. **Write brief to ClickUp Doc.** Create a ClickUp Doc in the "2026 Calender" list (ID: `901814889385`) using `clickup_create_document`. Write the brief content into it using `clickup_create_document_page`. Then set the parent task's "ClickUp Brief" custom field (field ID: `68e015f7-6830-44ea-ab09-6280bdd0d00e`) to the ClickUp Doc URL using `clickup_update_task`. (Skip if this was a manual run without a ClickUp task.)
5. **Save research notes** (if not already saved) to `reference/topic-research/`.
6. **Generate a review summary** - a short block at the top of the brief for the marketing manager:

```markdown
## Review Summary
- **Topic:** [topic]
- **Pillar:** [content pillar]
- **Slide count:** [N]
- **Key angle:** [one sentence describing the angle]
- **GFE tie-in:** [where and how GFE is mentioned]
- **Confidence:** [High / Medium - with notes on any areas needing human verification]
- **Similar past post:** [link to any prior post on same topic, or "None"]
```

7. **Close the ClickUp subtask.** Set the "write brief" subtask status to **"subtask closed"** using the ClickUp MCP `clickup_update_task` tool. (Skip if this was a manual run without a ClickUp task.)

### Output
- Final brief at `briefs/drafts/YYYY-MM-DD-topic-slug.md` (local backup)
- Brief written to a ClickUp Doc, URL set in parent task's "ClickUp Brief" custom field
- Research notes at `reference/topic-research/YYYY-MM-DD-topic-slug.md`
- ClickUp "write brief" subtask closed (status: "subtask closed")

### Quality Gate
- ❏ File naming convention followed
- ❏ Review summary is present and complete
- ❏ All sections of the template are filled in
- ❏ Brief is self-contained (designer could work from it alone)
- ❏ ClickUp Doc text is humanized (no em dashes, no invisible Unicode, no smart quotes)
- ❏ ClickUp Doc created and URL set in "ClickUp Brief" field (or skipped for manual runs)
- ❏ ClickUp "write brief" subtask closed (or skipped for manual runs)

---

## Post-Review Flow

After the marketing manager reviews:

- **Approved:** Move from `briefs/drafts/` to `briefs/approved/`. Hand off to design.
- **Needs revision:** Marketing manager leaves notes. Repo Claude revises, re-runs Stage 4 verification, and resubmits.
- **Rejected:** Brief stays in drafts with a `REJECTED` prefix and a note explaining why. This becomes learning data for future briefs.

---

## Error Handling

| Situation | Action |
|---|---|
| Cannot find authoritative source for a claim | Do not include the claim. Note the gap in the research doc. |
| Topic is too broad for a single carousel | Propose splitting into a series. Recommend the strongest sub-topic for the first post. |
| Topic has been covered in a recent post | Flag the overlap. Propose a fresh angle or suggest an alternative topic. |
| Unsure about a technical detail | Mark with `[VERIFY]` and include what you *think* is correct plus why you're uncertain. Never silently guess. |
| Topic is too niche for broad engagement | Flag the concern with estimated engagement potential. Suggest ways to broaden the hook while keeping the content specific. |
| Conflicting information across sources | Note the conflict, cite both sources, and recommend which to trust based on authority and recency. |

---

## File Naming Conventions

| Type | Pattern | Example |
|---|---|---|
| Draft brief | `briefs/drafts/YYYY-MM-DD-topic-slug.md` | `briefs/drafts/2025-07-15-react-vs-svelte.md` |
| Approved brief | `briefs/approved/YYYY-MM-DD-topic-slug.md` | `briefs/approved/2025-07-15-react-vs-svelte.md` |
| Research notes | `reference/topic-research/YYYY-MM-DD-topic-slug.md` | `reference/topic-research/2025-07-15-react-vs-svelte.md` |
| Rejected brief | `briefs/drafts/REJECTED-YYYY-MM-DD-topic-slug.md` | `briefs/drafts/REJECTED-2025-07-15-react-vs-svelte.md` |

---

## Quick Reference: Repo Claude Checklist

Before submitting any brief, confirm:

```
[ ] agents.md read at session start
[ ] ClickUp "write brief" subtask opened and parent task metadata read
[ ] Brief link (Google Doc URL) extracted from parent task custom fields
[ ] Content pillar, post format, topic category noted from custom fields
[ ] Reference links from subtask description read
[ ] Prior art checked in top-linkedin-posts/ and briefs/approved/
[ ] Stage 1: Research saved with sourced facts
[ ] Stage 2: 3 angles considered, format selected, strongest hook crafted
[ ] Stage 3: Full brief drafted using correct format template section
[ ] Stage 4: Every fact re-verified, writing tightened, engagement-tested
[ ] Stage 5: Final format, review summary, files saved correctly
[ ] Brief written to ClickUp Doc, URL set in parent task "ClickUp Brief" field
[ ] Local backup saved to briefs/drafts/
[ ] ClickUp "write brief" subtask closed (status: "subtask closed")
[ ] No [VERIFY] tags remaining unresolved
[ ] Brief is self-contained for designer/creator handoff
```
