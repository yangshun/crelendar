# ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
# BRIEF INFO
# ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

# Here's What Just Happened in Front End

- **Date:** 2026-03-06
- **Topic:** Biweekly front-end news roundup - React Foundation, Oxfmt Beta, TypeScript 5.8 GA, Cloudflare Vinext (AI), Node.js releases, Hono 4.12
- **Pillar:** News
- **Format:** Carousel
- **Format rationale:** Recurring series post (Biweekly News) using the tiered format from the news roundup pillar guide. 3 Tier 1 items get dedicated slides with code/visuals, 1 AI Spotlight item gets a dedicated slide, 2 Tier 2 items grouped on a Quick Hits slide. Research sourced from Bytes #464, JS Weekly #774, This Week in React #269-270, plus direct WebSearch date verification.
- **Key angle:** React just left Meta and joined the Linux Foundation. A Prettier killer hit beta at 30x speed. TypeScript 5.8 finally bridges ESM and CJS. And one engineer rebuilt Next.js with AI in a week for $1,100.
- **GFE tie-in:** CTA slide + caption link to GFE front-end interview handbook.
- **Design inspiration:** Tue Tools series format - clean slide layout with logos, code blocks, and impact text per item.
- **Color theme:** Light (white/cream bg)
- **Accent color:** GFE brand colors for consistency. Item-specific accents: React blue, Oxfmt orange, TypeScript blue, Cloudflare orange.


# ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
# CAPTION
# ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

## LinkedIn Caption
React just left Meta. It's now under the Linux Foundation with Amazon, Microsoft, Vercel, and 5 other founding members.

That alone would be the biggest front-end news of the year. But in the same week: a Prettier alternative that's 30x faster hit beta, TypeScript 5.8 finally lets you require() ESM modules, and one Cloudflare engineer rebuilt Next.js with AI in a week for $1,100.

Here's what you missed in front end this fortnight - 6 updates, all shipping now.

React leaving Meta - good or bad for the ecosystem?

\#FrontEnd \#JavaScript \#WebDevelopment \#React \#TypeScript \#Oxfmt \#GreatFrontEnd

Prepare for front-end interviews with questions and solutions written by ex-FAANG engineers: https://www.greatfrontend.com/front-end-interview-guidebook?utm_source=linkedin&utm_medium=social&utm_campaign=biweekly-news-1_mar+2026


# ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
# CONTENT BRIEF - Format A: Carousel
# ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

## Slide 1 - Hook
**Title:** Here's What Just Happened in Front End
**Subtitle:** 6 updates from Feb 20 - Mar 5
**Visual direction:**
- Layout: Large title centered, subtitle below. Logos for React (+ Linux Foundation), Oxfmt, TypeScript, Cloudflare arranged below.
- Key elements: GreatFrontEnd logo top. Tool/org logos below subtitle. "6 updates" count badge.
- Style notes: Light bg, clean sans-serif title. Same series styling as Tue Tools posts.

## Slide 2 - Tier 1: React Foundation Launch
**Headline:** React Just Left Meta. Here's What That Means.
- React, React Native, and JSX are no longer owned by Meta. Now governed by the React Foundation under the Linux Foundation.
- 8 Platinum founding members (Amazon, Microsoft, Vercel, Meta, + 4 more). Seth Webster as executive director.
- Biggest React governance change since its open-source release in 2013.
**Visual direction:**
- Layout: Headline top. React logo + Linux Foundation logo side by side. Below: grid showing 8 founding member logos. Key takeaway text at bottom.
- Key elements: React + Linux Foundation logo pairing, founding member grid, "Independent governance" callout.
- Style notes: React blue accents. Make the Meta-to-Foundation transition visually clear. No code block - this is governance news, the visual is the member grid.

## Slide 3 - Tier 1: Oxfmt Beta
**Headline:** Oxfmt Beta: A Prettier Alternative, 30x Faster
- Built on Rust (part of the Oxc toolchain). Formats JS, TS, JSX, TSX.
- 100% Prettier conformance - same output, drop-in replacement.
- 30x faster than Prettier in benchmarks. Formats entire codebases in under a second.
- Code snippet:
  ```bash
  # Replace Prettier with Oxfmt
  npm install -D oxfmt
  npx oxfmt .
  ```
**Visual direction:**
- Layout: Headline top with Oxfmt logo. Key stats ("30x faster", "100% Prettier conformance") in highlight boxes. Code snippet centered below.
- Key elements: Oxfmt logo, speed comparison callout, code block showing the install command.
- Style notes: Oxfmt brand colors for accents. Emphasize "drop-in replacement" - most practical takeaway.

## Slide 4 - Tier 1: TypeScript 5.8 GA
**Headline:** TypeScript 5.8: require() Finally Works with ESM
- `--module nodenext` now supports `require()` of ECMAScript modules - bridges the long-standing ESM/CJS gap.
- New `--erasableSyntaxOnly` flag ensures your TypeScript is compatible with Node.js's `--experimental-strip-types`.
- Improved narrowing for checked `in` expressions and `return` statements in branches.
- Code snippet:
  ```typescript
  // TypeScript 5.8 + Node.js 22
  // require() of ESM now works under --module nodenext
  const { parse } = require("./parser.mts");
  // No more "require() of ES Module not supported" errors
  ```
**Visual direction:**
- Layout: Headline top with TypeScript logo. Code snippet centered. Key features listed below.
- Key elements: TypeScript logo, "ESM + CJS = finally friends" messaging, code block.
- Style notes: TypeScript blue accents. Emphasize the practical fix - this pain point has existed for years.

## Slide 5 - AI Spotlight: Cloudflare Vinext
**Headline:** One Engineer Rebuilt Next.js with AI in One Week
- Cloudflare's Vinext reimplements the Next.js API surface on Vite — 94% compatibility.
- One engineer, 800+ AI sessions with Claude, $1,100 total. 4.4x faster builds, 57% smaller bundles.
- 1,700+ Vitest tests, 380 Playwright E2E tests, full TypeScript checking via tsgo.
**Visual direction:**
- Layout: Headline top with Cloudflare logo. Key stats in highlight boxes ("$1,100", "800+ AI sessions", "4.4x faster builds"). "AI Spotlight" badge in corner.
- Key elements: Cloudflare logo, stat callouts, "AI Spotlight" label to establish the recurring section.
- Style notes: Cloudflare orange accents. The numbers tell the story - make them large and prominent.

## Slide 6 - Quick Hits
**Headline:** Quick Hits
- **Node.js v25.7.0 (Current) + v24.14.0 (LTS)** - HTTP/2 config improvements and SEA ESM support in Current; LTS maintenance patch with dependency updates.
- **Hono 4.12** - Client improvements, middleware enhancements, router performance boost, and security fixes for the lightweight web framework.
**Visual direction:**
- Layout: "Quick Hits" headline top. Node.js and Hono logos left-aligned. Compact bullet descriptions.
- Key elements: Tool logos, bold names, one-line descriptions.
- Style notes: Compact, scannable. No code blocks. Light bg consistent with series.

## Final Slide - CTA
**Headline:** Stay Updated with GreatFrontEnd
**GFE copy:** Follow us for the latest front-end news, interview prep, and career tips.
**CTA button text:** Share This Post & Follow Us!
**Visual direction:**
- Layout: Headline centered. GFE logo prominent. CTA text below.
- Key elements: GFE logo, standard CTA slide design matching Tue Tools series.
- Style notes: Clean, minimal. Light bg consistent with series.

**Target:** 7 slides (Hook + 3 Tier 1 + 1 AI Spotlight + 1 Quick Hits + CTA). Follows the tiered format from the news roundup pillar guide.


# ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
# SOURCES
# ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

## Sources
- React Foundation launch (Linux Foundation, 8 founding members) - https://react.dev/blog/2026/02/24/the-react-foundation
- Oxfmt Beta announcement (30x faster, 100% Prettier conformance) - https://oxc.rs/blog/2026-02-24-oxfmt-beta
- TypeScript 5.8 GA (require() of ESM, erasableSyntaxOnly) - https://devblogs.microsoft.com/typescript/announcing-typescript-5-8/
- Cloudflare Vinext (AI-rebuilt Next.js, $1,100, 800+ sessions) - https://blog.cloudflare.com/vinext/
- Node.js v25.7.0 (Current) - https://nodejs.org/en/blog/release/v25.7.0
- Hono 4.12 - https://github.com/honojs/hono/releases

**Planned first comment:** "The wildest connection in this roundup: React just left Meta to join the Linux Foundation, and one of the Foundation's partners (Cloudflare) simultaneously showed you can rebuild Next.js with AI for $1,100. The framework is going independent at the exact moment AI is making frameworks cheaper to replace. What does that mean for React's future? Preparing for front-end interviews? GFE's guidebook covers framework questions with solutions by ex-FAANG engineers: https://www.greatfrontend.com/front-end-interview-guidebook?utm_source=linkedin&utm_medium=social&utm_campaign=biweekly-news-1_mar+2026. Sources: React Foundation (react.dev/blog/2026/02/24/the-react-foundation), Cloudflare Vinext (blog.cloudflare.com/vinext/)."
