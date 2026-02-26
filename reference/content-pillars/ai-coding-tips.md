# AI Coding Tips Pillar: "Ship with AI" Series Guide

This guide applies to all **Ship with AI** posts (pillar: News). This series replaces the former Tue Tools series. It publishes biweekly on Tuesdays, alternating with Biweekly News.

## Concept

Curated, practical tips for using AI to code in engineering teams. Each post shares one actionable insight, workflow, or practice - sourced from real developer discussions on Reddit, HN, Twitter/X, and engineering blogs.

**What this series is NOT:** Tool comparison roundups, AI hype, or generic "AI will change everything" takes. Every post must contain a specific, actionable tip a dev can try today.

## Research & Selection

### 1. Source Scan

Search each source for AI coding content from the **last 2-4 weeks before publish date**. Sort by recent + top engagement. Never rely on AI memory for what's trending - always fetch live data.

| Source | What to Look For | How to Search |
|---|---|---|
| Reddit r/ExperiencedDevs | Team workflows, senior dev perspectives | Search "AI" or "copilot" or "cursor" or "claude", sort by Top (Past Month) |
| Reddit r/cursor_ai | Cursor-specific tips, new features | Sort by Top (Past Month), look for workflow posts |
| Reddit r/ClaudeAI | Claude coding tips, agent workflows | Sort by Top (Past Month), filter coding-related |
| Reddit r/webdev, r/programming | General AI coding discussions | Search "AI coding" or "LLM", sort by Top (Past Month) |
| Hacker News | Viral AI coding posts, debates | Search "AI coding" or "LLM programming", filter last 30 days |
| Dev blogs | Addy Osmani, Kent C. Dodds, company eng blogs | Check recent posts (last 2-4 weeks) |
| Twitter/X | Viral threads from devs sharing AI workflows | Search "AI coding workflow" or "vibe coding", filter recent |

### 2. Selection Criteria

1. **Recency is mandatory.** Only cover topics that are currently trending or emerged in the last 2-4 weeks. Check post dates, upvote velocity, and comment recency. Never cover outdated workflows or stale opinions - if a tip was viral 6 months ago, it's too late.
2. **Practical and actionable.** The tip should be something a dev can try TODAY. No vague "AI will change everything" takes. Look for specific workflows, prompt patterns, tool configurations, or team practices.
3. **High engagement signal.** Prioritize posts with high upvotes, active comment threads, or cross-platform buzz (appeared on Reddit AND HN, or went viral on Twitter/X).
4. **Novelty over repetition.** Prefer first-of-its-kind workflows, new tool capabilities, or fresh perspectives. Skip "10 tips for using Copilot" rehashes.
5. **Front-end relevant.** The tip should be applicable to front-end/full-stack engineering. General AI coding tips are fine if they clearly apply to web dev workflows.
6. **Passes the common sense test.** For every tip in the post, ask: "Could a senior engineer give this advice without reading the source?" If yes, the tip is too generic. The insight must come FROM the research - a specific finding, metric, workflow detail, or tool behavior the audience couldn't have guessed. See the **Reject List** below for explicit examples of content that always fails this test.
7. **Passes the depth test.** For frameworks and workflows, the post must go beyond naming the steps to showing what they look like in practice. If the tip is "use this workflow: A → B → C," the post must show a concrete example of at least one step's input or output. A developer should be able to change their behavior tomorrow based on what the post says — not just know a new vocabulary word. See the depth test in `EXECUTION.md` Stage 4 for details.

**Freshness check:** For every candidate topic, verify the source post date. If the original discussion/post is older than 4 weeks from the publish date, it's too stale - skip it.

### Reject List - Content That Always Fails the Common Sense Test

**Never include tips like these:**
- "Always review AI-generated code" - everyone knows this
- "Ask why before accepting suggestions" - obvious advice
- "Write tests first" - standard practice, not a new insight
- "Break large tasks into smaller ones" - generic project management
- "Don't blindly trust AI output" - assumed knowledge for any professional
- "Use AI for boilerplate, write complex logic yourself" - every dev already does this
- "Provide more context in your prompts for better results" - basic prompting 101
- "Review the code before committing" - not a tip, it's a job requirement
- "Be specific in your prompts" - generic advice, not actionable
- "Learn the fundamentals, don't just rely on AI" - platitude
- Anything that amounts to "be more careful" or "think before you act"

**Reject these broader patterns:**
- **Repackaged common sense with data:** "Study shows reviewing code is important" - the audience didn't need a study to know this. A study is only valuable if it reveals something that CONTRADICTS or REFINES what people assume.
- **Generic process advice with an AI wrapper:** "Plan before you code (but with AI)" - old advice wearing a new hat.
- **Vague principle without specific mechanism:** "AI works best when you stay engaged" - HOW? What tool feature, prompt structure, or workflow step?
- **"Tips" that are actually job descriptions:** "Senior engineers should review AI output for architectural issues" - that's literally what they do.
- **Moral advice disguised as technical advice:** "Don't let AI make you lazy" - not actionable, it's a lecture.

### 3. Content Categories (prioritize what's trending NOW)

| Category | Example Topics | Trending Signal |
|---|---|---|
| **New tool features** | "Claude Code just shipped hooks - here's how teams use them" / "Cursor's new background agents" | New release or feature launch in last 2-4 weeks |
| **Viral workflows** | "This AI coding workflow just blew up on Reddit" / "The 'plan-code-review' loop everyone's talking about" | High-upvote post or viral thread in last 2 weeks |
| **Team practices** | "How [Company] ships 3x faster with AI pair programming" / "New data: how top teams review AI-generated PRs" | Recent blog post, survey, or case study |
| **Emerging patterns** | "AI agents are replacing junior dev tasks - here's the real workflow" / "Why senior devs are switching from Copilot to Claude" | Trend shift visible across multiple sources |
| **Anti-patterns** | "This viral AI coding mistake is costing teams hours" / "Why 'vibe coding' fails in production" | Trending criticism or cautionary post |
| **Case studies** | "How Cloudflare built Vinext with 800+ AI sessions" / "Shopify's new AI-first dev policy" | Recent company announcement or blog |

### 4. Topic Selection

Select **one main topic** per post (not a roundup of 3-5 items). The post should go deep on one actionable idea rather than skim across many. If multiple strong candidates exist, pick the one with the highest engagement signal and save others for future posts.

### 5. Dedup Check

Cross-reference against `reference/covered-topics.md`. Don't repeat a topic already covered in a previous Ship with AI post.

## Format Options (rotate for variety)

| Format | When to Use | Example |
|---|---|---|
| **Single image** | Visual tip, before/after, workflow diagram | "The prompt-output-review cycle" infographic |
| **Carousel (3-5 slides)** | Step-by-step workflow or numbered tips | "5 rules our team uses for AI-generated code" |
| **Code screenshot** | Before/after showing AI prompt and result | "How I prompted Cursor to refactor this component" |
| **Text post** | Hot take or discussion starter | "I review AI code differently than human code. Here's why." |

**Key rule:** Do NOT default to carousel every time. Rotate formats to avoid monotony. Check the last 3 posts in `briefs/drafts/` and `briefs/approved/` before selecting format.

## Content Structure (when carousel)

```
Slide 1: Hook - sharp claim or question ("Most devs use AI wrong. Here's one pattern that actually works.")
Slides 2-4: The tip/workflow - step by step with code or visuals
Final Slide: CTA - "Follow for more AI dev tips" + GFE link
```

Target: **3-5 slides** for carousels (shorter than news roundups - focused, not comprehensive).

## Post-Brief: Update Dedup Tracker

After finalizing the brief, append the covered topic to `reference/covered-topics.md` under the "Ship with AI" series name.
