# Research: React Machine Coding Round — Star Rating Walkthrough
**Date:** 2026-03-02
**ClickUp Task:** 86ewn4ef0 (subtask: 86ewnep2h)

## Source 1: GFE Star Rating Question
**URL:** https://www.greatfrontend.com/questions/user-interface/star-rating

- Medium difficulty, ~20 min recommended
- Requirements: configurable max stars, click-to-fill, hover preview with revert, multiple instances
- Premium solutions behind paywall
- Part of 91 React coding questions on GFE

## Source 2: GFE React Interview Questions Page
**URL:** https://www.greatfrontend.com/questions/react-interview-questions

- 91 coding questions (Easy/Medium/Hard)
- Company filters: Google, Amazon, Apple, ByteDance, Microsoft, OpenAI, TikTok, Uber, etc.
- Star rating explicitly listed as a question
- 41.4k+ completions across platform
- Study plans: 1-week, 1-month, 3-month

## Source 3: Frontend Interview Handbook — Build UI Components
**URL:** https://www.frontendinterviewhandbook.com/coding/build-front-end-user-interfaces

- "Knowledge of a11y is one of the differentiating factors between junior vs senior engineers"
- "What if you need multiple instances on the page?" — common follow-up
- "Mention how you would do things differently if you had more time and were writing production code" — great candidates do this

## Source 4: FrontendLead Star Rating Question
**URL:** https://frontendlead.com/coding-questions/star-rating-component-react

- Includes reset-on-double-click requirement (most tutorials miss this)
- Full ARIA requirements: role="radiogroup", role="radio", aria-checked, aria-label
- Keyboard navigation: arrow keys + Enter/Space + Escape
- SVG-only constraint option

## Source 5: DEV Community — Accessible Star Ratings
**URL:** https://dev.to/grahamthedev/5-star-rating-system-actually-accessible-no-js-no-wai-aria-3idl

- Most implementations have terrible contrast ratios (yellow stars, no border)
- Color-only state changes fail color-blind users
- Proper approach: native <input type="radio"> within <fieldset>, visually-hidden text

## Prior Art in Our Content
- **Uber Interview Question** — Carousel. Machine coding challenge (interactive shape). Progressive complexity. Code snippets. Similar format but different component.
- **FE System Design Interviewers** — Single image. Evaluation criteria angle. Different interview type.
- **React Hooks** — Carousel. Hooks overview. Educational, not walkthrough.

**Gap:** No prior post covers a step-by-step machine coding walkthrough with actual code. The Uber post is closest but focuses on the problem challenge, not the solving process.

## Insight Map

### Surface → Insight pairs
1. Surface: "Star rating is a beginner component" → **Insight: It's a calibration tool. Basic = 5 min, production-ready = 2 hours. Interviewers use the same question to find every candidate's ceiling.**
2. Surface: "Add accessibility if you have time" → **Insight: Accessibility is the stealth senior-level test. Browsers provide ZERO keyboard support for custom ARIA widgets. Bringing up role="radiogroup" unprompted signals senior awareness.**
3. Surface: "Manage state with useState" → **Insight: The real challenge is managing 3 simultaneous states (committed rating, hover preview, keyboard focus) and ensuring clean revert-on-hover-exit. This is where most implementations break.**
4. Surface: "Build the component, then submit" → **Insight: "What would you do with more time?" is the most powerful closing statement. It proves you know the gap between time-constrained and production code.**
5. Surface: "Machine coding tests coding ability" → **Insight: It tests whether you can hold design thinking AND code execution simultaneously — neither DSA nor system design tests this.**

### Myth-busts
- "Star rating is too easy for interviews" — It's intentionally simple-looking to expose skill ceilings
- "Accessibility is a nice-to-have follow-up" — It's increasingly the PRIMARY evaluation criterion at senior levels
- "Finish all features to pass" — A well-structured partial solution beats a complete messy one

## Competitive Landscape
Top Google results for "star rating component interview":
- Most are code-only tutorials (build it, here's the code)
- None weave interview STRATEGY into the component build
- None lead with accessibility as the differentiator
- None frame the "progressive disclosure" approach (build in layers, narrate priorities)
- Nobody covers the double-click-to-reset edge case

## GFE Tie-in
Natural: Star rating is an actual GFE question. CTA to React interview questions page (91 questions). RADIO-like progressive structure maps to machine coding approach.
