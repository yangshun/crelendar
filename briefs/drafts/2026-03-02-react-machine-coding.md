# ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
# BRIEF INFO
# ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

# React Machine Coding Round: 1 Question, 5 Levels

- **Date:** 2026-03-02
- **Topic:** React machine coding interview — star rating component walkthrough
- **Pillar:** 💼 Career / Interview Preparation & Strategy
- **Format:** Carousel
- **Format rationale:** Step-by-step progressive walkthrough with code snippets at each level requires multiple slides. 5 levels + hook + CTA = 8-9 slides, ideal carousel range. Prior interview post (System Design Interviewers) was a single image — carousel maintains format variety. Uber Interview Question (similar format, carousel) is our closest comparable top performer.
- **Key angle:** The star rating question isn't a "beginner" question — it's a calibration tool. Interviewers use one question to find 5 different skill ceilings, and most candidates plateau at level 2.
- **GFE tie-in:** CTA slide + caption link — star rating is an actual GFE question. Link to React interview questions page.
- **Design inspiration:** NeetCode / Codemia explainer style — dark bg, numbered levels, code blocks per slide
- **Color theme:** Dark (navy/black bg)
- **Accent color:** React blue (#61dafb) for levels 1-3, gold/amber for levels 4-5 (the differentiator levels)


# ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
# CAPTION
# ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

## LinkedIn Caption
"Build a star rating component." Sounds easy — until the interviewer keeps adding requirements.

This is one of the most common React machine coding questions at FAANG companies, and it's intentionally designed to find your ceiling. The basic version takes 5 minutes. The production-ready version — with hover preview, keyboard navigation, ARIA roles, and fractional stars — can take 2 hours.

I broke it down into 5 levels. Most candidates plateau at level 2. Level 4 (accessibility) is the one that separates senior hires from everyone else — and almost nobody practices it.

Which level would you reach in a timed interview? Be honest.

#ReactJS #FrontEndInterview #MachineCoding #CodingInterview #FrontEndDevelopment #GreatFrontEnd #WebDevelopment #InterviewPrep

Practice this exact question + more React interview questions with detailed solutions: https://www.greatfrontend.com/questions/react-interview-questions?utm_source=linkedin&utm_medium=social&utm_campaign=react-machine-coding_mar+2026


# ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
# CONTENT BRIEF — Format A: Carousel
# ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

## Slide 1 — Hook
**Title:** 1 React Interview Question, 5 Levels
**Subtitle:** Most candidates stop at level 2. Where's your ceiling?
**Visual direction:**
- Layout: Large title centered, subtitle below. "⭐⭐⭐⭐⭐" visual at top (5 stars, first 2 filled gold, last 3 dimmed) to reinforce the "level 2" claim visually.
- Key elements: React logo subtle watermark. Star icons as visual hook. Level indicator: "Lv 1 ■ Lv 2 ■ Lv 3 □ Lv 4 □ Lv 5 □" progress bar at bottom.
- Style notes: Dark bg, React blue accent. Title in bold sans-serif. Stars as the dominant visual element.

## Slide 2 — The Question
**Headline:** "Build a star rating component"
- Interviewer gives you: "Build a reusable star rating component in React. The user should be able to click a star to set their rating."
- ❌ What most candidates think: "Easy — just map over an array and track clicks"
- ✅ What the interviewer is really doing: Testing how far you go beyond the minimum. This one question has 5 layers of complexity.
**Visual direction:**
- Layout: Interview prompt in a "chat bubble" or terminal-style block at top. ❌/✅ contrast below.
- Key elements: Interviewer prompt styled as a code comment or chat message. ❌/✅ markers with contrasting colors.
- Style notes: Monospace for the interview prompt. Red/green for ❌/✅.

## Slide 3 — Level 1: Basic Click-to-Fill
**Headline:** Level 1: The Basics (Everyone Gets Here)
- What to build: Click a star → fill that star and all stars before it
- Code anchor:
  ```jsx
  const [rating, setRating] = useState(0);

  {[1, 2, 3, 4, 5].map((star) => (
    <span
      key={star}
      onClick={() => setRating(star)}
      style={{ color: star <= rating ? '#ffc107' : '#e0e0e0' }}
    >
      ★
    </span>
  ))}
  ```
- ⏱ Time: ~3 minutes. This is table stakes — don't celebrate here.
**Visual direction:**
- Layout: "Level 1" badge top-left with React blue bg. Headline below. Code block centered. Timer icon with "~3 min" bottom-right.
- Key elements: Code snippet is the dominant element. Star icons showing filled state transition.
- Style notes: Code in monospace with syntax highlighting. "Level 1" badge consistent across all level slides.

## Slide 4 — Level 2: Hover Preview
**Headline:** Level 2: Hover Preview (Where Most Stop)
- What to add: Stars highlight on hover to preview the rating before clicking. When the cursor leaves, revert to the actual rating.
- The tricky part: You now need **two separate states** — the committed rating AND the hover preview. Most bugs happen when the hover state doesn't revert cleanly.
- Code anchor:
  ```jsx
  const [rating, setRating] = useState(0);
  const [hover, setHover] = useState(0);

  style={{ color: star <= (hover || rating)
    ? '#ffc107' : '#e0e0e0' }}
  onMouseEnter={() => setHover(star)}
  onMouseLeave={() => setHover(0)}
  ```
- ❌ Common bug: Forgetting `onMouseLeave` — the hover state sticks after the cursor exits
**Visual direction:**
- Layout: "Level 2" badge top-left. Headline. Code block showing the two-state pattern. Bug callout in a warning box at bottom.
- Key elements: Visual showing hover vs committed state (e.g., 3 stars filled from click, 4 stars highlighted from hover). Code snippet. ❌ bug callout box.
- Style notes: Warning box for the bug in orange/amber. Hover state stars shown in a lighter shade vs committed state.

## Slide 5a — Level 3: Edge Cases (Concepts)
**Headline:** Level 3: Edge Cases (The Detail Test)
- The requirements most candidates miss:
  - **Reset on double-click:** Click the same star twice → clears to 0
  - **Configurable max stars:** Accept `maxStars` as a prop, don't hard-code 5
  - **Read-only mode:** A `disabled` prop that blocks interaction but still displays
- 💡 Interviewers often add these mid-interview to test adaptability
**Visual direction:**
- Layout: "Level 3" badge top-left. Headline. 3 edge cases as a compact checklist with icons. Pro tip callout at bottom.
- Key elements: Checklist with ✓/✗ marks. "💡 Pro tip" callout.
- Style notes: Clean, text-only slide. No code block — that's on the next slide.

## Slide 5b — Level 3: Edge Cases (Code)
**Headline:** Level 3: The Code
- Code anchor:
  ```jsx
  // Reset logic
  onClick={() =>
    setRating(star === rating ? 0 : star)
  }

  // Configurable
  {Array.from({ length: maxStars }, (_, i) => i + 1)
    .map((star) => ...)}
  ```
**Visual direction:**
- Layout: "Level 3" badge top-left (same as 5a). Code block centered, dominant element.
- Key elements: Code snippet with syntax highlighting. Minimal surrounding text.
- Style notes: Let the code breathe. Same styling as slides 3-4 code blocks.

## Slide 6a — Level 4: Accessibility (The Senior-Level Differentiator)
**Headline:** Level 4: Accessibility ⚠️ This Is Where Senior Hires Separate
- The insight most candidates miss: Browsers provide **ZERO** keyboard support for custom ARIA widgets. You build it all from scratch.
- What senior candidates do unprompted:
  - `role="radiogroup"` + `role="radio"` with `aria-checked`
  - ←/→ arrow keys to move, Enter/Space to select
  - Visible focus indicator (outline) — not just `:hover`
- ❌ Most candidates: Never mention accessibility unless asked
- ✅ Senior signal: Bring it up before the interviewer does
**Visual direction:**
- Layout: "Level 4" badge top-left with **gold/amber bg** (color shift from React blue to signal "this is the differentiator"). ⚠️ badge on headline. ❌/✅ contrast at bottom.
- Key elements: ⚠️ badge. 3 compact bullet points. ❌/✅ contrast pair. No code block — that's on the next slide.
- Style notes: **Gold/amber accent** on this slide and the next. Bolder border.

## Slide 6b — Level 4: Accessibility (Code)
**Headline:** Level 4: The Code
- Code anchor:
  ```jsx
  <div role="radiogroup" aria-label="Rating">
    <span
      role="radio"
      aria-checked={star === rating}
      aria-label={`${star} star${star > 1 ? 's' : ''}`}
      tabIndex={star === 1 ? 0 : -1}
      onKeyDown={handleKeyDown}
    >
  ```
**Visual direction:**
- Layout: "Level 4" badge top-left with gold/amber bg. Code block centered, dominant element.
- Key elements: Code snippet with ARIA attributes highlighted. Minimal surrounding text.
- Style notes: Gold/amber accent continues. Let the code breathe.

## Slide 7 — Level 5: The Meta-Game
**Headline:** Level 5: What You SAY Matters as Much as What You CODE
- Machine coding rounds test whether you can think architecturally while writing code. The best candidates:
  - **Narrate tradeoffs out loud:** "I'm using inline styles for speed, but in production I'd use CSS modules for maintainability."
  - **Ask before building:** "Should I prioritize keyboard support or fractional stars given our time?"
  - **Close with the power move:** "If I had more time, I'd add fractional stars using getBoundingClientRect(), SVG gradients for smooth rendering, and unit tests for the keyboard navigation."
- ❌ The worst pattern: Coding silently for 20 minutes, then presenting a finished result
- ✅ The best pattern: Treating the interview as a pair-programming session
**Visual direction:**
- Layout: "Level 5" badge top-left with gold/amber bg. Headline. 3 "best candidate" quotes in speech-bubble style. ❌/✅ contrast at bottom.
- Key elements: Speech bubbles with the tradeoff narration quotes. ❌/✅ contrast. No code on this slide (intentional — the point is about communication, not code).
- Style notes: Gold/amber accent continues. Speech bubbles in lighter bg to stand out. Quotes in italic or lighter weight.

## Slide 8 — The Scoring Summary
**Headline:** Where Do You Plateau?
- Quick-reference scoring grid:

| Level | What It Tests | % Who Reach It |
|---|---|---|
| Level 1: Click-to-fill | Basic React state | ~95% |
| Level 2: Hover preview | Multi-state management | ~70% |
| Level 3: Edge cases | Attention to detail, adaptability | ~40% |
| Level 4: Accessibility | Senior-level awareness | ~15% |
| Level 5: Communication | Interview meta-game | ~10% |

- *Note for designer: Percentages are illustrative estimates based on interviewer observations, not a formal study. Use "~" prefix to signal approximation.*
- "The question is the same. Your ceiling is the variable."
**Visual direction:**
- Layout: Headline top. Scoring table centered, full-width. Quote at bottom.
- Key elements: Table with level numbers, colored progress bar showing drop-off (bars shrink from 95% to 10%). Levels 4-5 rows in gold/amber.
- Style notes: Progress bars make the drop-off visual and dramatic. The table is the dominant element — highly save-worthy as a reference card.

## Final Slide — CTA
**Headline:** Ready to Ace the Interview?
**GFE copy:** This star rating question — plus React coding challenges — with detailed solutions and in-browser practice.
**CTA button text:** greatfrontend.com → React Interview Questions
**Visual direction:**
- Layout: Headline centered. GFE logo prominent. CTA text below with arrow/link icon.
- Key elements: GFE logo, 5 filled gold stars as visual callback to the post theme.
- Style notes: Clean, minimal. Consistent dark bg. GFE branding.

**Target:** 11 slides (Hook + 9 content + CTA). Slides 5 and 6 were each split into concept + code pairs to avoid overcrowding. Slightly above the 7-10 ideal range, but justified — each slide is now scannable at a glance.


# ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
# SOURCES
# ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

## Sources
- Star rating question requirements and ARIA patterns — https://www.greatfrontend.com/questions/user-interface/star-rating
- 91 React interview questions on GFE — https://www.greatfrontend.com/questions/react-interview-questions
- Accessibility as senior differentiator — https://www.frontendinterviewhandbook.com/coding/build-front-end-user-interfaces
- ARIA radiogroup keyboard behavior — https://www.w3.org/WAI/ARIA/apg/practices/keyboard-interface/
- Star rating accessibility deep-dive — https://dev.to/grahamthedev/5-star-rating-system-actually-accessible-no-js-no-wai-aria-3idl
- Reset-on-double-click and SVG constraint — https://frontendlead.com/coding-questions/star-rating-component-react
- Machine coding round evaluation criteria — https://www.frontendinterviewhandbook.com/coding/build-front-end-user-interfaces

**Planned first comment:** "Want to practice this exact question? GreatFrontEnd has the star rating question with test cases and a detailed solution — plus more React coding challenges with solutions. All solvable in-browser: https://www.greatfrontend.com/questions/react-interview-questions"
