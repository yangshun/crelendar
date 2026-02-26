# Research Notes: Can You Debug This React Code?
**Date:** 2026-03-05 (publish date)
**Researched:** 2026-02-25

## Manager Requirements
From parent task description:
- Interactive React debugging challenge
- Readers prompted to find and fix issues in a code snippet
- Focus on practical problem-solving, "learn by doing"
- CTA: React coding interview questions with solutions at https://www.greatfrontend.com/blog/practice-50-react-coding-interview-questions-with-solutions

**Sanity-check notes:**
- "Interactive" on a static post = "spot the bug" carousel with reveal mechanic. Valid approach. ✅
- CTA URL verified live. Will NOT hardcode question count per pipeline rules. ✅
- All requirements check out. No flags.

## Bug Selection

Designed a single UserProfile component with 3 bugs. Selection criteria: common enough to recognize, tricky enough to miss at first glance, clear explanation and fix.

### The Buggy Component
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

### Bug 1: Missing dependency in useEffect
- `userId` is used inside the effect but not in the dependency array `[]`
- When `userId` changes, the effect won't re-run — shows stale data
- Fix: `[userId]` in the dependency array
- Source: https://react.dev/reference/react/useEffect#specifying-reactive-dependencies

### Bug 2: Double setState with stale closure
- Both `setCount(count + 1)` calls use the same `count` value from the closure
- React batches them, and the second call overwrites the first
- Result: count increments by 1, not 2 — despite the button saying "+2"
- Fix: `setCount(prev => prev + 1)` (functional update)
- Source: https://react.dev/learn/queueing-a-series-of-state-updates

### Bug 3: Conditional rendering with falsy 0
- `{count && <p>...</p>}` — when count is 0, evaluates to `0`
- React renders `0` as visible text on screen
- Fix: `{count > 0 && <p>...</p>}` or `{count ? <p>...</p> : null}`
- Source: https://react.dev/learn/conditional-rendering#logical-and-operator-

## Insight Map

**What audience already knows:**
- React hooks basics (useState, useEffect)
- Component rendering
- Event handlers

**What would be new/surprising:**
1. The "double setState" bug is extremely common and rarely practiced — people learn functional updates but forget why
2. The falsy 0 rendering bug is a gotcha that even senior devs miss in code review
3. The missing dependency bug is ubiquitous but the mental model of "why" (stale closure) is less understood

**Debate hooks:**
- "How many did you find before swiping?" — ego challenge
- "Is the ESLint exhaustive-deps rule enough?" — dev tooling debate
- "I've shipped all 3 of these bugs to production" — relatability

## Prior Art
- No "spot the bug" or debugging challenge posts in the repo (novel format)
- Adjacent: React Machine Coding brief (Mar 2) and Uber Interview Question post — both are coding challenges but walkthrough-style, not bug-finding
- The debugging/quiz format is untested for this account — good for experimentation

## GFE CTA
- URL: https://www.greatfrontend.com/blog/practice-50-react-coding-interview-questions-with-solutions
- Page verified live. Contains React coding challenges organized by difficulty with solutions.
- CTA angle: "Practice React coding challenges with solutions"
- DO NOT hardcode question count.

## Sources
- useEffect dependencies: https://react.dev/reference/react/useEffect#specifying-reactive-dependencies
- Batched state updates / functional updates: https://react.dev/learn/queueing-a-series-of-state-updates
- Conditional rendering falsy values: https://react.dev/learn/conditional-rendering#logical-and-operator-
