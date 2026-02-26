# ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
# BRIEF INFO
# ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

# Master TypeScript in React: From Props to Hooks

- **Date:** 2026-03-16
- **Topic:** Practical TypeScript patterns in React — typing props, hooks, events, context, and generics
- **Pillar:** 🔍 Deep Dive / Technical Education
- **Format:** Carousel
- **Format rationale:** 6 distinct TypeScript patterns, each requiring its own code snippet and explanation. Carousel is the only format that supports code-per-slide at readable mobile size. The previous post (Performance Checklist) was a single image, so format alternation is restored. 8 slides (hook + 5 patterns + mistakes + CTA) fits the 7-10 ideal range.
- **Key angle:** Expert TypeScript has fewer type annotations, not more. This post teaches the patterns that make your React code safer while writing less — inference-first typing, discriminated unions, typed context, and generic components.
- **GFE tie-in:** CTA slide + caption link to GFE TypeScript interview questions.
- **Design inspiration:** Codemia coding concept style — dark bg, syntax-highlighted code blocks, clean code editor aesthetic
- **Color theme:** Dark (navy/black bg)
- **Accent color:** TypeScript blue (#3178C6) for primary accents. React blue (#61dafb) for React-specific labels. Red for mistake highlights, green for correct patterns.


# ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
# CAPTION
# ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

## LinkedIn Caption
Most devs add TypeScript to React by putting types on everything. Expert TypeScript has fewer annotations, not more.

The real power isn't `string` and `number` on your props. It's discriminated unions that make impossible states unrepresentable, generic components that scale without duplication, and a `useRef` overload that most people have never seen explained properly.

Here are 5 patterns that will change how you write TypeScript in React — from the basics most people get wrong to the advanced patterns that separate senior from mid-level code.

Which pattern was new to you?

#TypeScript #React #JavaScript #FrontEnd #WebDevelopment #GreatFrontEnd #CodingInterview

Practice TypeScript interview questions with detailed solutions: https://www.greatfrontend.com/questions/typescript-interview-questions?utm_source=linkedin&utm_medium=social&utm_campaign=ts-react-mastery_mar+2026


# ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
# CONTENT BRIEF — Format A: Carousel
# ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

## Slide 1 — Hook
**Title:** Master TypeScript in React
**Subtitle:** From Props to Hooks — 5 patterns that change how you write code
**Visual direction:**
- Layout: Large title centered, subtitle below. TypeScript and React logos side by side.
- Key elements: TypeScript blue + React blue accent. "5 patterns" emphasized.
- Style notes: Dark bg, code editor aesthetic. Clean, bold title.

## Slide 2 — Props & Discriminated Unions
**Headline:** Stop Typing Props Wrong
- Most devs type every prop as optional. Use discriminated unions to make impossible states unrepresentable.
- Code snippet:
  ```tsx
  // Bad: nothing stops href + onClick together
  type Props = { variant?: "link" | "button"; href?: string; };

  // Good: TypeScript enforces valid combinations
  type Props =
    | { variant: "link"; href: string }
    | { variant: "button"; onClick: () => void };
  ```
- With discriminated unions, TypeScript catches invalid prop combinations at compile time — not in production.
**Visual direction:**
- Layout: Headline top. Code block centered with Bad/Good split. One-line explanation below.
- Key elements: ❌ Bad pattern in red highlight → ✅ Good pattern in green highlight.
- Style notes: The before/after code contrast is the anchor. Keep explanation to one sentence.

## Slide 3 — Event Handlers
**Headline:** Type Your Event Handlers (Correctly)
- Stop using `(e: any) => void`. React has specific event types for every handler.
- Quick reference:
  ```tsx
  onClick:  (e: React.MouseEvent<HTMLButtonElement>) => void
  onChange: (e: React.ChangeEvent<HTMLInputElement>) => void
  onSubmit: (e: React.FormEvent<HTMLFormElement>) => void
  onKeyDown:(e: React.KeyboardEvent<HTMLInputElement>) => void
  ```
- The generic parameter (`<HTMLButtonElement>`) tells TypeScript which element fired the event — so `e.currentTarget` is fully typed.
**Visual direction:**
- Layout: Headline top. 4-row reference table or aligned code block showing event → type mapping.
- Key elements: Clean type reference. Each event on its own line. Emphasis on the element generic.
- Style notes: This is a "screenshot and save" slide. Make it scannable. Monospace font, generous spacing.

## Slide 4 — useState & useRef
**Headline:** When to Type Your Hooks (and When Not To)
- `useState` infers from initial value. Only add types when inference can't work.
- Code snippet:
  ```tsx
  // Inference works — don't add types
  const [count, setCount] = useState(0);

  // Inference can't work — add the type
  const [user, setUser] = useState<User | null>(null);

  // useRef: null placement matters
  useRef<HTMLInputElement>(null)  // readonly — for DOM refs
  useRef<number | null>(null)    // mutable — for stored values
  ```
- The `useRef` overload is the most confusing in React's API. The position of `null` in the type determines if the ref is mutable.
**Visual direction:**
- Layout: Headline top. Code block centered with inference/explicit examples, then useRef comparison.
- Key elements: "Don't add types" callout on inference examples. useRef readonly vs mutable distinction highlighted.
- Style notes: Two distinct sections in the code block — useState and useRef. Visual separator between them.

## Slide 5 — Typed Context
**Headline:** Context Without the Undefined Checks
- The pattern: create context as `undefined`, wrap in a custom hook that throws if used outside the provider.
- Code snippet:
  ```tsx
  type AuthCtx = { user: User; logout: () => void };
  const Ctx = createContext<AuthCtx | undefined>(undefined);

  function useAuth() {
    const ctx = useContext(Ctx);
    if (!ctx) throw new Error("useAuth outside provider");
    return ctx; // TypeScript knows this is AuthCtx
  }
  ```
- Every consumer gets a fully typed context — no optional chaining, no null checks.
**Visual direction:**
- Layout: Headline top. Code block centered. One-line payoff below: "No more `ctx?.user` everywhere."
- Key elements: The custom hook pattern is the anchor. Highlight the return type inference.
- Style notes: Keep the code compact. The insight is that the `if (!ctx)` check narrows the type for all consumers.

## Slide 6 — Generic Components
**Headline:** One Component, Any Type
- Generic components let you write a single `List<T>` that works with users, products, or any data shape — fully typed.
- Code snippet:
  ```tsx
  function List<T>({ items, renderItem, getKey }: {
    items: T[];
    renderItem: (item: T) => ReactNode;
    getKey: (item: T) => string;
  }) {
    return <ul>{items.map(i =>
      <li key={getKey(i)}>{renderItem(i)}</li>
    )}</ul>;
  }

  // Usage — T inferred from items
  <List items={users} renderItem={u => u.name} getKey={u => u.id} />
  ```
- TypeScript infers `T` from the `items` array. No explicit generic needed at the call site.
**Visual direction:**
- Layout: Headline top. Code block centered showing component definition + usage. Emphasis on "T inferred from items."
- Key elements: Generic type parameter `<T>` highlighted in TypeScript blue. Usage example showing inference.
- Style notes: This is the advanced slide. The code is longer — ensure readable font size. May need slightly smaller code font.

## Slide 7 — Common Mistakes
**Headline:** 3 TypeScript + React Mistakes to Stop Making
- ❌ Using `any` to "fix" type errors — `any` is contagious, poisons every variable it touches. Use `unknown` + narrowing.
- ❌ Adding types where inference works — `useState<number>(0)` adds noise. Let TS infer.
- ❌ Still using `React.FC` — adds no value since `@types/react` 18. Type props directly.
**Visual direction:**
- Layout: Headline top. 3 compact mistake rows, each with ❌ marker and one-line fix.
- Key elements: ❌ markers in red. Keep each mistake to 1-2 lines. This is a quick-hit reference slide.
- Style notes: No code block on this slide — just concise text. Punchy, scannable.

## Final Slide — CTA
**Headline:** Want to Practice TypeScript?
**GFE copy:** TypeScript interview questions with detailed solutions — from basics to advanced patterns.
**CTA button text:** greatfrontend.com → TypeScript Questions
**Visual direction:**
- Layout: Headline centered. GFE logo prominent. CTA text below with arrow/link icon.
- Key elements: GFE logo, TypeScript blue accent as visual callback.
- Style notes: Clean, minimal. Consistent dark bg. GFE branding.

**Target:** 8 slides (Hook + 5 patterns + mistakes + CTA). Within the ideal 7-10 range.


# ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
# SOURCES
# ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

## Sources
- React official TypeScript docs (props, hooks, events) — https://react.dev/learn/typescript
- React TypeScript Cheatsheets (community patterns) — https://github.com/typescript-cheatsheets/react
- Discriminated unions in React components — https://www.totaltypescript.com/workshops/advanced-react-with-typescript/advanced-props/type-checking-react-props-with-discriminated-unions/solution, https://www.developerway.com/posts/advanced-typescript-for-react-developers-discriminated-unions
- useRef overloads (mutable vs readonly) — https://claritydev.net/blog/typescript-typing-react-useref-hook
- ComponentPropsWithoutRef pattern — https://www.totaltypescript.com/react-component-props-type-helper
- Why Gusto removed React.FC — https://engineering.gusto.com/the-journey-to-a-safer-frontend-why-we-removed-react-fc-095ff0b3e2e4
- Custom hook tuple typing with as const — https://fettblog.eu/typescript-react-typeing-custom-hooks/
- GFE TypeScript interview questions — https://www.greatfrontend.com/questions/typescript-interview-questions

**Planned first comment:** "The one that trips up the most people: useRef's null placement. `useRef<HTMLInputElement>(null)` gives you a readonly ref (for DOM elements). `useRef<number | null>(null)` gives you a mutable ref (for stored values). The difference is whether null is in the type parameter or the initial value — React's types use function overloads to distinguish them, and the TypeScript error messages when you get it wrong are completely unhelpful. Practice TypeScript interview questions with detailed solutions: https://www.greatfrontend.com/questions/typescript-interview-questions?utm_source=linkedin&utm_medium=social&utm_campaign=ts-react-mastery_mar+2026."
