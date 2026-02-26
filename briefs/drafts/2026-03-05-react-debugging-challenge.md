# ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
# BRIEF INFO
# ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

# Can You Debug This React Code?

- **Date:** 2026-03-05
- **Topic:** Interactive React debugging challenge — 3 common bugs hidden in one component
- **Pillar:** 💼 Career / Interview Preparation & Strategy
- **Format:** Carousel
- **Format rationale:** The "spot the bug" format fundamentally requires a reveal mechanic — show the code, then reveal the bugs one by one. This creates suspense and encourages pausing before swiping. Carousel is the only format that supports this. 7 slides (hook + code + 3 bugs + fixed code + CTA). Last 4 formats: Single Image, Carousel, Single Image, Carousel — this is the 3rd carousel in 5, acceptable since the format is mechanically required.
- **Key angle:** One innocent-looking React component, 3 bugs that most devs have shipped to production. The challenge format drives comments ("I found 2/3!", "Wait, what's the third one?") and saves (reference card for code review).
- **GFE tie-in:** CTA slide + caption link to GFE React coding interview questions blog post.
- **Design inspiration:** Codemia coding concept style — dark bg, code editor aesthetic, syntax-highlighted code blocks
- **Color theme:** Dark (navy/black bg)
- **Accent color:** React blue (#61dafb) for UI elements. Red (#ff4444) for bug highlights, green (#4caf50) for fixes. White text on dark bg.


# ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
# CAPTION
# ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

## LinkedIn Caption
3 bugs. 1 React component. Most devs find 2.

This is a real-world component — `UserProfile` with a data fetch, a click counter, and conditional rendering. It looks fine at first glance. It compiles without errors. But it has 3 bugs that will bite you in production.

Try to find all 3 before swiping to the answers. One of them has been shipped to production by almost everyone reading this.

How many did you find? Drop your count below — no cheating.

#ReactJS #JavaScript #FrontEndDevelopment #CodingChallenge #WebDevelopment #GreatFrontEnd #InterviewPrep #Debugging

Practice React coding interview questions with detailed solutions: https://www.greatfrontend.com/blog/practice-50-react-coding-interview-questions-with-solutions?utm_source=linkedin&utm_medium=social&utm_campaign=react-debug-challenge_mar+2026


# ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
# CONTENT BRIEF — Format A: Carousel
# ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

## Slide 1 — Hook
**Title:** Can You Debug This React Code?
**Subtitle:** 3 bugs. 1 component. Find them before swiping.
**Visual direction:**
- Layout: Large title centered, subtitle below. React logo subtle watermark. Bug/beetle icon or magnifying glass icon at top.
- Key elements: "3 bugs" emphasized in red (#ff4444). Challenge framing: "Find them before swiping →"
- Style notes: Dark bg, React blue accent. Code editor aesthetic — monospace font hints. The challenge framing should create urgency to pause and think.

## Slide 2 — The Code
**Headline:** Find the 3 Bugs
- Code block (the entire buggy component):
  ```jsx
  function UserProfile({ userId }) {
    const [user, setUser] = useState({});
    const [count, setCount] = useState(0);

    useEffect(() => {
      fetch(`/api/users/${userId}`)
        .then(res => res.json())
        .then(data => setUser(data));
    }, []);

    const increment = () => {
      setCount(count + 1);
      setCount(count + 1);
    };

    return (
      <div>
        <h1>{user.name}</h1>
        {count && <p>Clicked {count} times</p>}
        <button onClick={increment}>+2</button>
      </div>
    );
  }
  ```
- No hints on this slide — let the reader study the code
**Visual direction:**
- Layout: "Find the 3 Bugs" headline top. Full code block centered, filling the slide. No other elements.
- Key elements: Syntax-highlighted code in a dark code editor frame. Line numbers visible. No bug markers — this is the challenge slide.
- Style notes: Code must be readable at mobile size. Monospace font, generous line spacing. The code IS the slide.

## Slide 3 — Bug #1
**Headline:** Bug 1: Missing Dependency
- The bug (highlight line): `}, []);`
- `userId` is used inside the effect but not in the dependency array
- When `userId` changes, the effect won't re-run — shows stale data for the previous user
- The fix:
  ```jsx
  }, [userId]);
  ```
**Visual direction:**
- Layout: "Bug 1" badge top-left in red. The buggy line highlighted in red in a mini code block. Explanation below. Fix shown in green.
- Key elements: ❌ buggy line in red highlight → ✅ fixed line in green highlight. Brief explanation between them.
- Style notes: Show just the relevant lines (the useEffect closing), not the full component. Red/green contrast for bug/fix.

## Slide 4 — Bug #2
**Headline:** Bug 2: setState Won't Double
- The bug (highlight lines):
  ```jsx
  setCount(count + 1);
  setCount(count + 1);
  ```
- Both calls use the same `count` value from the closure. React batches them — the second overwrites the first. The button says "+2" but only increments by 1.
- The fix:
  ```jsx
  setCount(prev => prev + 1);
  setCount(prev => prev + 1);
  ```
**Visual direction:**
- Layout: "Bug 2" badge top-left in red. Buggy lines in red, fix in green. One-line explanation between.
- Key elements: ❌ `count + 1` (uses stale closure) → ✅ `prev => prev + 1` (functional update). Explanation: "Both calls read the same `count`. Use functional updates."
- Style notes: Same layout as slide 3. Keep explanation to one sentence.

## Slide 5 — Bug #3
**Headline:** Bug 3: The Sneaky Zero
- The bug (highlight line):
  ```jsx
  {count && <p>Clicked {count} times</p>}
  ```
- When `count` is 0, this evaluates to `0` — and React renders the literal text "0" on screen. Not nothing. Not null. The number zero.
- The fix:
  ```jsx
  {count > 0 && <p>Clicked {count} times</p>}
  ```
**Visual direction:**
- Layout: "Bug 3" badge top-left in red. Buggy line in red, fix in green. One-line explanation.
- Key elements: ❌ `count && ...` (renders "0") → ✅ `count > 0 && ...` (renders nothing). Optional: mini screenshot/mockup showing "0" rendered on screen.
- Style notes: This is the "gotcha" slide — the one most people miss. Make the "renders 0 on screen" point visually clear.

## Slide 6 — The Fixed Code
**Headline:** The Fixed Component
- Full fixed code:
  ```jsx
  function UserProfile({ userId }) {
    const [user, setUser] = useState({});
    const [count, setCount] = useState(0);

    useEffect(() => {
      fetch(`/api/users/${userId}`)
        .then(res => res.json())
        .then(data => setUser(data));
    }, [userId]);

    const increment = () => {
      setCount(prev => prev + 1);
      setCount(prev => prev + 1);
    };

    return (
      <div>
        <h1>{user.name}</h1>
        {count > 0 && <p>Clicked {count} times</p>}
        <button onClick={increment}>+2</button>
      </div>
    );
  }
  ```
- 3 fixes highlighted in green: `[userId]`, `prev => prev + 1`, `count > 0`
**Visual direction:**
- Layout: "Fixed" badge top-left in green. Full code block with the 3 fixed lines highlighted in green.
- Key elements: Green highlights on the 3 changed lines. Checkmarks or ✅ next to each. This is the save-worthy reference slide.
- Style notes: Same code editor frame as slide 2. Green accents instead of neutral. This slide is designed to be screenshot/saved.

## Final Slide — CTA
**Headline:** Want More React Challenges?
**GFE copy:** Practice React coding interview questions with detailed solutions — from basic components to advanced patterns.
**CTA button text:** greatfrontend.com → React Coding Questions
**Visual direction:**
- Layout: Headline centered. GFE logo prominent. CTA text below with arrow/link icon.
- Key elements: GFE logo, React blue accent as visual callback. Optional: 3 checkmarks (✅✅✅) as callback to the 3 bugs.
- Style notes: Clean, minimal. Consistent dark bg. GFE branding.

**Target:** 7 slides (Hook + 5 content + CTA). Within the ideal 7-10 range.


# ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
# SOURCES
# ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

## Sources
- useEffect dependency array and stale closures — https://react.dev/reference/react/useEffect#specifying-reactive-dependencies
- Batched state updates and functional updates — https://react.dev/learn/queueing-a-series-of-state-updates
- Conditional rendering with falsy values (0 rendering) — https://react.dev/learn/conditional-rendering#logical-and-operator-

**Planned first comment:** "Bug #3 (the sneaky zero) is the most commonly shipped to production — React's docs added a dedicated warning about it because `{count && ...}` trips up even experienced devs. The fix is one character: `count > 0`. If you got all 3, you're ahead of most candidates in React interviews. Practice more React challenges with solutions: https://www.greatfrontend.com/blog/practice-50-react-coding-interview-questions-with-solutions?utm_source=linkedin&utm_medium=social&utm_campaign=react-debug-challenge_mar+2026. Sources: React docs on useEffect dependencies (react.dev/reference/react/useEffect), batched state updates (react.dev/learn/queueing-a-series-of-state-updates), falsy rendering (react.dev/learn/conditional-rendering)."
