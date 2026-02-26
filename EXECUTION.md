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

0a. **Find the next "write brief" subtask** from the ClickUp "2026 Calender" list (ID: `901814889385`). Use `clickup_search` to find subtasks with status "write brief". For each candidate subtask, fetch its **parent task** using `clickup_get_task` — the parent task's due date is the **post publish date**, which determines priority.

   **CRITICAL: Sort ALL candidates by parent task due date (publish date), NOT by subtask due date (brief deadline).** The subtask due date is the brief-writing deadline — it does NOT determine execution order. The parent due date is the actual post publish date and is the ONLY valid sort key for priority.

   To determine correct order:
   1. Fetch ALL open "write brief" subtasks (not just the first few results)
   2. For each, retrieve the parent task's due date
   3. Sort by parent due date ascending (earliest publish date first)
   4. Pick the subtask with the earliest parent due date

   Skip any tasks whose parent publish date has already passed (overdue posts are handled separately by the marketing team). ClickUp due dates are epoch milliseconds — convert to human dates for comparison (e.g., `1772404200000` ÷ 1000 → Unix timestamp → date).

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

1b. **Dedup check for recurring series.** If this is a Biweekly News or Ship with AI brief, check `reference/covered-topics.md` before researching. Exclude any topic already listed. Also read the relevant pillar-specific format guide at `reference/content-pillars/` (`news-roundup.md` for Biweekly News, `ai-coding-tips.md` for Ship with AI). After completing the brief, append all covered topics to the tracker.

2. **Primary research.** Gather facts from authoritative sources:
   - Official documentation and release notes
   - Official tech blogs (company engineering blogs for breakdowns)
   - GitHub repos (stars, recent commits, contributor activity)
   - npm trends / bundlephobia for adoption and size data
   - Reputable tech publications (not random Medium posts)
   - Conference talks and official announcements

3. **Content landscape & social research.** Assess what already exists on this topic and where the audience conversation is:
   - **Competitor content:** Search LinkedIn, YouTube, and tech blogs for existing posts on the same topic. Note which angles have been covered, what formats were used, and what engagement they received. Identify saturated angles to avoid and gaps to exploit.
   - **Social sentiment:** Check Reddit (r/webdev, r/reactjs, r/javascript), Twitter/X, and Hacker News for recent discussions on the topic. What are developers actually saying? What frustrations, debates, or misconceptions are active?
   - **Content gaps:** Based on competitor content and social discussions, identify angles or sub-topics that are underserved. The best-performing posts fill a gap — they say what nobody else has said yet, or say it better.
   - **Audience questions:** Collect the actual questions developers are asking about this topic on Stack Overflow, Reddit, and forums. These can feed directly into hooks and engagement prompts.
   Save landscape findings in the research notes alongside primary research.

4. **Mine for insights.** Separate what's common knowledge from what's genuinely new or surprising. For each major fact or claim, ask:
   - **Would a mid-level engineer already know this?** If yes, it's context — not the headline.
   - **What's the non-obvious layer?** Every topic has a surface understanding and a deeper truth. Dig for the deeper truth. Examples:
     - Surface: "React uses a virtual DOM" → Insight: "React 19's compiler eliminates the need for useMemo/useCallback in most cases"
     - Surface: "Use debounce for search inputs" → Insight: "300ms is the sweet spot — under 200ms wastes API calls, over 500ms feels laggy"
     - Surface: "System design interviews test architecture" → Insight: "Interviewers score on 6 axes, and the 2 most overlooked ones are what flip no-hire to hire"
   - **Is there authoritative data that contradicts popular belief?** Myth-busting backed by official sources is the highest-engagement content pattern.
   - **Can I cite a specific source that gives this credibility?** Insights from official engineering blogs, core team members, or verified benchmarks carry more weight than generic best practices.

5. **Compile research notes.** Save to `reference/topic-research/YYYY-MM-DD-topic-slug.md` with:
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
- ❏ Content landscape checked — competitor posts, social sentiment, and content gaps identified

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
5. **Target 7-10 slides total.** Under 7 feels thin. Over 10, swipe fatigue sets in. Going above 10 is acceptable when slides were split for density reasons (concept + code pairs), but **never exceed 20 slides** — that's the platform cap for both LinkedIn and Instagram carousels. If a brief needs more than 20 slides, the scope is too broad — split into a series.
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

#### Content Density Rule (all visual formats):
Every slide, zone, or frame must be scannable at a glance. If it takes more than 3 seconds to read, it's too dense. Overcrowded slides hurt engagement (people swipe past what looks effortful) and create production issues (cramped layouts, tiny fonts that don't render on mobile).

**Red flags for overcrowding:**
- More than 3 bullet points on a single slide
- A code block (4+ lines) alongside bullet points
- A code block AND a BAD/GOOD contrast pair on the same slide
- Any single-image content zone with more than ~40 words of body text

**When a slide is too dense, fix for engagement first — don't default to splitting.** Evaluate these options in order of preference:
1. **Cut.** Is everything on this slide essential? Remove the weakest element. A slide with 3 strong points beats one with 5 that includes filler.
2. **Shorten.** Can bullet points become single-line fragments? Can a 7-line code block become 4 lines by trimming boilerplate? Can the BAD/GOOD contrast be compressed into one line each?
3. **Restructure.** Would a different visual format (table, diagram, comparison grid) present the same info more compactly than bullet points + code?
4. **Split.** If cutting, shortening, and restructuring still leave too much — then split into two slides. But this adds to slide count and can break reading flow, so it's the last resort, not the first.

**The designer test:** Before finalizing, ask "could the designer lay this out at a readable font size with breathing room?" If the answer is "only if we shrink everything" — go back through options 1-4 above.

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

8. **Write the planned first comment.** The first comment on LinkedIn gets the most visibility after the post itself. Do NOT waste it on a source list. The first comment must serve one of two goals:

   > **Goal A: Engagement** — Add value that extends the post and invites discussion.
   > **Goal B: Conversion** — Drive traffic to a specific GFE resource with a compelling reason to click.

   **First comment structure:**
   1. **Lead with a value-add sentence** — a bonus insight, a practical takeaway, a surprising stat, or a direct question that wasn't in the post. This is the hook of the comment. It must stand on its own as useful content.
   2. **GFE CTA** (when relevant) — Link to the most specific GFE resource for the topic. Frame it as a solution to a problem the post surfaced, not as a generic plug. Use UTM parameters matching the campaign.
   3. **Sources** (optional, brief) — If the post makes factual claims, add a one-line "Sources: [paper title](URL)" at the end. Keep it minimal — 1-2 key sources, not an exhaustive bibliography.

   **What a good first comment looks like:**
   - "The study also found that pilot participants kept sneaking AI use even when told not to — 25-35% non-compliance. If you can't stop using AI even in a controlled study, that says something about how embedded it already is. If you want to strengthen the fundamentals AI is eroding, here's a solid starting point: [specific GFE resource link]"
   - "One thing that didn't fit in the carousel: Cloudflare's engineer found that AI sessions over 45 minutes produced progressively worse code. The sweet spot was 20-30 minutes with a fresh context window. Has anyone else noticed this in their own workflow?"

   **What a bad first comment looks like:**
   - "Sources and further reading: [URL 1], [URL 2], [URL 3], [URL 4]. GFE interview guidebook: [URL]" — this is a bibliography, not a comment. Nobody reads this. Nobody clicks through.

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
- ❏ Planned first comment leads with a value-add (not a source list) and serves engagement or conversion

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

4. **Check for source over-extrapolation.** For every architectural or "how X works" claim in the brief, trace it back to its source and ask:
   - Does the source actually say what the brief claims? A blog post about "alpha blending with WebGL" does NOT mean "the entire editor bypasses the DOM and uses WebGL."
   - Is the scope right? A source about one specific operation (image processing, caching, etc.) does not justify a claim about the entire system architecture.
   - Is this a direct quote/paraphrase, or an inference? If it's an inference, is there a second source that confirms it? Single-source architectural claims are high risk.
   If a claim can't be directly supported by its source at the same scope, either narrow the claim to match what the source actually says, find additional sources that support the broader claim, or drop it entirely.

**Engagement pass:**

4. **Re-read the hook** fresh. Does it still stop the scroll after you've been deep in the content? If not, rewrite it.

5. **Check slide flow.** Read just the headlines of slides 1 through N in sequence. Do they tell a coherent, compelling story on their own? If not, reorder or rewrite headlines.

6. **Kill weak slides.** Any slide that doesn't teach, surprise, or advance the narrative gets cut or merged. 7 strong slides > 10 padded slides.

7. **Check for comment triggers.** Is there at least one moment in the carousel that will make someone think "wait, I disagree" or "yes, this is so true" or "I've experienced this"? If not, sharpen an opinion or add a relatable example.

7b. **First comment check.** Re-read the planned first comment. Does it lead with value (insight, question, bonus stat) or with a source list? If it leads with sources, rewrite it. Apply the same standard as slide content — the first comment is content, not a footnote.

8. **Verify every number in the brief.** Any specific number — product counts, percentages, version numbers, benchmark figures — must be double-checked against its source before the brief is finalized. This applies everywhere: slides, captions, CTAs, footer zones, and first comments. If the number came from research notes, go back to the original source and re-verify. If the source is no longer accessible or the number can't be confirmed, either drop the number or flag it with `[VERIFY]`. Numbers are the easiest thing to get wrong and the fastest way to lose credibility.

9. **Insight freshness check.** Re-read each content section and ask: "Would an engineer with 3 years of experience already know this?" Flag any section where the answer is "yes" for the core point (not just the setup). For flagged sections, either:
   - Replace the common-knowledge point with the deeper insight from the research notes
   - Add a "but here's what most people get wrong" twist that reframes the familiar
   - Cut the section and redistribute its space to sections with genuine insights
   Every section's core point must be something the reader is unlikely to already know, sourced from authoritative references — not generic best-practice advice repackaged.

9b. **Common sense rejection test.** For every "tip," "pattern," "practice," or "rule" in the brief, apply this test:

   > **"Could a senior engineer give this exact advice without reading the source material?"**

   If yes, the tip is common sense — it was already in the audience's head before they saw the post. Cut it or replace it with something the source material actually reveals that contradicts, refines, or adds specificity to what people assume.

   **What passes:** A specific finding, workflow, config, metric, or pattern that the audience could NOT have guessed on their own. The insight must come FROM the research, not from general professional experience.

   **Common sense patterns to REJECT (never include these):**
   - "Always review AI-generated code" — everyone knows this
   - "Ask why before accepting suggestions" — obvious advice
   - "Write tests first" — standard practice, not a new insight
   - "Break large tasks into smaller ones" — generic project management
   - "Don't blindly trust AI output" — assumed knowledge for any professional
   - "Use AI for boilerplate, write complex logic yourself" — every dev already does this
   - "Provide more context in your prompts for better results" — basic prompting 101
   - "Review the code before committing" — not a tip, it's a job requirement
   - "Iterate on your prompts if the first result isn't right" — obvious
   - "Be specific in your prompts" — generic advice, not actionable
   - "Learn the fundamentals, don't just rely on AI" — platitude
   - Anything that amounts to "be more careful" or "think before you act" — not a tip, it's a life philosophy

   **Broader negative patterns (reject content that fits these shapes):**
   - **Repackaged common sense with data:** "Study shows reviewing code is important" — the audience didn't need a study to know this. A study is only valuable if it reveals something that CONTRADICTS or REFINES what people assume.
   - **Generic process advice with an AI wrapper:** "Plan before you code (but with AI)" — old advice wearing a new hat. Only include if the AI-specific version differs in a non-obvious way.
   - **Vague principle without specific mechanism:** "AI works best when you stay engaged" — HOW? With what tool feature, prompt structure, or workflow step? If the tip could apply to any tool or situation, it's too vague.
   - **"Tips" that are actually job descriptions:** "Senior engineers should review AI output for architectural issues" — that's literally what senior engineers do. Not a tip.
   - **Moral advice disguised as technical advice:** "Don't let AI make you lazy" — not actionable, it's a lecture.

9c. **Depth test.** For every framework, workflow, process, or multi-step practice described in the brief, apply this test:

   > **"Could a developer change their behavior tomorrow based on what this slide says?"**

   If the slide names a concept or lists steps but doesn't show what those steps look like in practice, it fails. The audience should leave with a concrete mental model of the work, not just a label for it.

   **How to fix a slide that fails the depth test:**

   1. **Show, don't label.** Replace abstract step names with a concrete example of what the step produces. "Write a spec" → show a 3-line example spec. "Review the PR" → show what a review checklist item looks like. "70% on problem definition" → show what problem definition output looks like (a requirements doc? a test file? a prompt?).
   2. **Add the "what this actually looks like" layer.** Every process slide needs at least one concrete artifact: an example input, an example output, a code snippet, a screenshot description, or a specific tool command. If the slide can't include one, the research wasn't deep enough — go back to the source material.
   3. **Use source material depth, not summary depth.** If the brief is summarizing a blog post, the brief should contain details that go BEYOND what a reader would get from the blog's headline and subheadings. Read deeper into the source — examples, case studies, caveats, specific numbers — and surface those details.

   **What passes:**
   - "The spec is a markdown file with 3 sections: Requirements (user stories), Constraints (tech stack, performance targets), and Test Cases (input → expected output). Here's an example for a search autocomplete..." — shows the artifact
   - "Cursor Cloud Agents run in a sandboxed VM. The agent reads your .cursorrules file for project context, creates a branch, runs tests after each change, and only opens a PR when all tests pass. 30% of Cursor's own merged PRs are agent-generated." — shows the mechanism, not just the label

   **What fails:**
   - "Write a spec. Write tests. Let the agent execute. Review the output." — this is a table of contents, not content
   - "The 70/30 rule: spend 70% on specs and verification, 30% on execution." — this is a ratio without substance. What does the 70% PRODUCE? What artifacts? What does "verification" mean concretely?
   - "Human writes the spec and tests. Agent implements and verifies. Human reviews the PR." — restates the framework at the same abstraction level. The audience already got this from the hook.

10. **Check content progression.** Read the content sections/slides in order. Do they build on each other, or could they be shuffled randomly without losing anything? If the order doesn't matter, restructure into one of these arcs:
   - Familiar → Surprising (what you know → what you're missing)
   - Easy → Hard (progressive difficulty)
   - Problem → Solution (pain point → fix)
   - Common → Overlooked (obvious stuff → hidden factors that actually matter)

11. **Check for concrete anchors.** Count the number of content sections/slides that contain at least one concrete example, code snippet, specific number, or contrast pattern. If fewer than 60% of sections have a concrete anchor, add them. Abstract-only sections are the #1 quality gap between our briefs and top performers.

**Writing pass:**

12. **Cut filler words.** Remove "basically", "essentially", "actually" (unless genuinely needed for contrast), "really", "very", "just".

13. **Activate passive voice.** "The DOM is updated by React" → "React updates the DOM."

14. **Check jargon calibration.** The audience is engineers - don't over-explain basics. But don't assume familiarity with niche tools without context.

15. **Tone check.** Re-read the caption and slide headlines out loud. Do they sound like something you'd post on Reddit, or something a corporate social media manager wrote? Specific red flags:
    - Inspirational closers ("keep learning!", "you've got this!")
    - AI-speak ("it's worth noting", "let's delve", "comprehensive guide")
    - LinkedIn cringe ("thought leaders", "level up", "let's explore")
    - Over-hedging ("it could be argued that", "one might consider")
    If any section fails the vibe check, rewrite it blunter and more direct.

**Visual & copy optimization pass:**

16. **Visual designer + copywriter review.** Before the brief moves to final output, a visual designer and copywriter review each content slide/section to optimize how the information is displayed. Their mandate:

    a. **Copywriter: Tighten the copy.** Compress multi-sentence bullet points into scannable fragments. Preserve the specific data points, stats, and findings — cut the filler words and explanatory padding around them. Every slide should read in under 3 seconds.

    b. **Visual designer: Optimize the layout for each slide's content type.** Not all content works as bullet lists. Consider:
       - Would a comparison table, split-column layout, or diagram communicate this faster than bullets?
       - Should a dense slide be split into two, or can a different visual format (infographic, callout boxes, stat cards) make it work as one?
       - Does the visual hierarchy guide the eye to the most important element first?

    c. **Both: Preserve the meaning.** The research-backed content (specific findings, data points, non-obvious insights) must survive the optimization. The goal is to change HOW the information is presented, not WHAT information is presented. If a stat or finding would be lost by tightening, flag it — don't silently cut it.

    d. **Decide format per slide.** Each slide may benefit from a different visual treatment:
       - Stat slide → large number with one-line context
       - Comparison → side-by-side columns or table
       - List → short fragments with icons, not paragraphs
       - Case study → logo + key stat + one-line lesson
       - Process → flow diagram, not bullet points

    e. **Slide splitting/merging decisions.** The designer and copywriter together decide whether a dense slide should be split (more slides, each scannable) or restructured (same slide count, better layout). This is a design judgment call, not a formula.

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
- ❏ Every tip/pattern/practice passes the common sense rejection test (senior engineer couldn't give this advice without reading the source)
- ❏ Every framework/workflow/process described passes the depth test (developer could change behavior tomorrow)
- ❏ Writing is tight — no filler
- ❏ Visual & copy optimization pass completed (every slide scannable in under 3 seconds, layout matches content type)

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
   - Escape hashtag lines in captions: prefix each `#` with `\` (e.g., `\#ReactJS \#JavaScript`) to prevent ClickUp's markdown parser from interpreting them as headings. When a hashtag line renders as H1, it cascades — the CTA text line below also renders as a heading. Also verify that CTA lines have no heading markup (`##` prefix) after writing.

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
| Source says X about a specific operation but brief claims X about the entire system | Narrow the claim to match the source's actual scope. A blog post about WebGL alpha blending ≠ "the entire editor uses WebGL." Find additional sources before making architectural claims. |

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
