# Research: Master TypeScript in React — From Props to Hooks
**Date:** 2026-03-07 (publish date)
**Researched:** 2026-02-25
**CTA:** https://www.greatfrontend.com/questions/typescript-interview-questions

## Manager Requirements
"This post focuses on practical TypeScript usage in React, helping developers go beyond just adding types. It covers typing components, props, hooks, context, and events, showing how TypeScript improves code reliability, readability, and developer confidence."

**Sanity-check notes:**
- CTA URL verified live. Page offers 420+ TypeScript interview questions (coding + quiz), curated by ex-FAANG interviewers. Includes in-browser workspace, detailed solutions, test cases. Premium tier exists. Will NOT hardcode question count per pipeline rules.
- All requirements check out. No flags.

---

## 1. Essential TypeScript + React Patterns (Verified Code Snippets)

All snippets use modern React (function components, hooks). No class components.

### 1A. Component Props — Basic Typing

```tsx
// Explicit prop types with optional fields
type CardProps = {
  title: string;
  description?: string; // optional
  variant?: 'primary' | 'secondary' | 'danger'; // string literal union
};

function Card({ title, description, variant = 'primary' }: CardProps) {
  return (
    <div className={`card card--${variant}`}>
      <h2>{title}</h2>
      {description && <p>{description}</p>}
    </div>
  );
}
```

### 1B. Typing children Correctly

```tsx
// Use React.ReactNode for flexible children (strings, elements, fragments, null)
type ContainerProps = {
  children: React.ReactNode;
};

// Use string when children must be text-only
type LabelProps = {
  children: string;
};

// Use React.ReactElement when you need exactly one React element
type LayoutProps = {
  sidebar: React.ReactElement;
  children: React.ReactNode;
};
```

**Key insight:** `React.ReactNode` is the correct default for `children`. It includes `string | number | ReactElement | ReactFragment | ReactPortal | boolean | null | undefined`. Using `JSX.Element` is overly restrictive (fails for strings and numbers).

### 1C. Discriminated Unions for Component Variants

```tsx
// The discriminant property "as" determines which props are valid
type ButtonProps = {
  label: string;
} & (
  | { as: 'button'; onClick: () => void; href?: never }
  | { as: 'link'; href: string; onClick?: never }
);

function Button(props: ButtonProps) {
  if (props.as === 'link') {
    // TypeScript knows href exists, onClick doesn't
    return <a href={props.href}>{props.label}</a>;
  }
  // TypeScript knows onClick exists, href doesn't
  return <button onClick={props.onClick}>{props.label}</button>;
}

// Usage — TypeScript enforces correct prop combinations:
<Button as="link" href="/about" label="About" />     // valid
<Button as="button" onClick={handleClick} label="Go" /> // valid
// <Button as="link" onClick={fn} label="X" />        // ERROR: onClick not allowed with as="link"
```

**Why this matters:** Without discriminated unions, developers resort to making everything optional, which means TypeScript can't catch impossible states. With them, the compiler enforces valid combinations at build time.

### 1D. Event Handler Types

```tsx
function Form() {
  // onClick — use React.MouseEvent with the specific element
  const handleClick = (e: React.MouseEvent<HTMLButtonElement>) => {
    console.log(e.currentTarget.name);
  };

  // onChange — use React.ChangeEvent
  const handleChange = (e: React.ChangeEvent<HTMLInputElement>) => {
    console.log(e.target.value);
  };

  // onSubmit — use React.FormEvent
  const handleSubmit = (e: React.FormEvent<HTMLFormElement>) => {
    e.preventDefault();
    const formData = new FormData(e.currentTarget);
  };

  // Keyboard events
  const handleKeyDown = (e: React.KeyboardEvent<HTMLInputElement>) => {
    if (e.key === 'Enter') { /* ... */ }
  };

  return (
    <form onSubmit={handleSubmit}>
      <input onChange={handleChange} onKeyDown={handleKeyDown} />
      <button onClick={handleClick}>Submit</button>
    </form>
  );
}
```

**Quick reference table for the post:**
| Event         | Type                                        |
|---------------|---------------------------------------------|
| onClick       | `React.MouseEvent<HTMLButtonElement>`        |
| onChange      | `React.ChangeEvent<HTMLInputElement>`        |
| onSubmit      | `React.FormEvent<HTMLFormElement>`           |
| onKeyDown     | `React.KeyboardEvent<HTMLInputElement>`      |
| onFocus/Blur  | `React.FocusEvent<HTMLInputElement>`         |
| onDrag        | `React.DragEvent<HTMLDivElement>`            |

**Pro tip for the post:** When the handler is inline, TypeScript infers the event type automatically. You only need explicit types when extracting the handler into a named function.

### 1E. useState — Inference vs. Explicit Types

```tsx
// TypeScript infers from initial value — no annotation needed
const [count, setCount] = useState(0);        // inferred: number
const [name, setName] = useState('');          // inferred: string
const [isOpen, setIsOpen] = useState(false);   // inferred: boolean

// MUST annotate when initial value doesn't reveal the full type
const [user, setUser] = useState<User | null>(null);
// Without <User | null>, TypeScript infers type as "null" — setUser(userData) would error

// MUST annotate for union types
const [status, setStatus] = useState<'idle' | 'loading' | 'error'>('idle');

// MUST annotate for arrays initialized empty
const [items, setItems] = useState<string[]>([]);
// Without annotation, TypeScript infers never[] — push/concat would error
```

**The rule of thumb:** Let TypeScript infer when the initial value fully represents the type. Annotate when the state can hold values the initial value doesn't cover (null, union types, empty arrays).

### 1F. useRef with Element Types

```tsx
// DOM ref — pass null, TypeScript returns RefObject (readonly .current)
const inputRef = useRef<HTMLInputElement>(null);

// Access safely with optional chaining
const focusInput = () => {
  inputRef.current?.focus();
};

// Mutable ref (for storing values, not DOM elements)
const intervalRef = useRef<number | null>(null);
intervalRef.current = window.setInterval(() => {}, 1000);

return <input ref={inputRef} />;
```

**Critical distinction:** `useRef<HTMLInputElement>(null)` gives you `RefObject<HTMLInputElement>` (readonly current, designed for DOM). `useRef<HTMLInputElement | null>(null)` gives you `MutableRefObject<HTMLInputElement | null>` (writable current, for storing arbitrary values). The difference is whether `null` is in the type parameter or just the initial value.

**React 19 update:** `forwardRef` is deprecated. Ref is now passed as a regular prop:
```tsx
// React 19+ — no forwardRef needed
type InputProps = {
  ref?: React.Ref<HTMLInputElement>;
  placeholder?: string;
};

function Input({ ref, placeholder }: InputProps) {
  return <input ref={ref} placeholder={placeholder} />;
}
```

### 1G. Custom Hooks with Proper Return Types

```tsx
// Custom hook returning an object — TypeScript infers correctly, no annotation needed
function useToggle(initial = false) {
  const [value, setValue] = useState(initial);
  const toggle = useCallback(() => setValue(v => !v), []);
  const setTrue = useCallback(() => setValue(true), []);
  const setFalse = useCallback(() => setValue(false), []);

  return { value, toggle, setTrue, setFalse };
}

// Custom hook returning a tuple — use "as const" to preserve tuple types
function useLocalStorage<T>(key: string, initialValue: T) {
  const [stored, setStored] = useState<T>(() => {
    const item = localStorage.getItem(key);
    return item ? (JSON.parse(item) as T) : initialValue;
  });

  const setValue = (value: T) => {
    setStored(value);
    localStorage.setItem(key, JSON.stringify(value));
  };

  return [stored, setValue] as const;
  // Without "as const": inferred as (T | (value: T) => void)[]
  // With "as const":    inferred as readonly [T, (value: T) => void]
}

// Usage — destructuring works cleanly because it's a tuple, not an array
const [name, setName] = useLocalStorage('name', '');
//     ^string  ^(value: string) => void — each position typed correctly
```

**Why this matters:** Without `as const`, TypeScript infers `(T | SetterFn)[]` — a mixed array where every element could be either type. Destructuring then gives you union types at every position instead of precise types. `as const` tells TypeScript "this is a fixed-length tuple, not a growable array."

### 1H. Context with Typed Providers

```tsx
type Theme = 'light' | 'dark';

type ThemeContextType = {
  theme: Theme;
  toggleTheme: () => void;
};

// Create context with undefined default — forces provider usage
const ThemeContext = createContext<ThemeContextType | undefined>(undefined);

// Custom hook with type guard — eliminates undefined checks at every consumer
function useTheme(): ThemeContextType {
  const context = useContext(ThemeContext);
  if (context === undefined) {
    throw new Error('useTheme must be used within a ThemeProvider');
  }
  return context; // TypeScript narrows to ThemeContextType — no undefined
}

function ThemeProvider({ children }: { children: React.ReactNode }) {
  const [theme, setTheme] = useState<Theme>('light');
  const toggleTheme = useCallback(
    () => setTheme(t => (t === 'light' ? 'dark' : 'light')),
    []
  );

  return (
    <ThemeContext.Provider value={{ theme, toggleTheme }}>
      {children}
    </ThemeContext.Provider>
  );
}

// Consumer — clean, no undefined handling needed
function Header() {
  const { theme, toggleTheme } = useTheme();
  return <button onClick={toggleTheme}>Current: {theme}</button>;
}
```

**The pattern:** `createContext(undefined)` + custom hook with runtime guard = type-safe context that fails fast if misused, instead of silently returning undefined values.

### 1I. Generic Components

```tsx
// A generic List component that works with any item type
type ListProps<T> = {
  items: T[];
  renderItem: (item: T) => React.ReactNode;
  getKey: (item: T) => string | number;
};

function List<T>({ items, renderItem, getKey }: ListProps<T>) {
  return (
    <ul>
      {items.map(item => (
        <li key={getKey(item)}>{renderItem(item)}</li>
      ))}
    </ul>
  );
}

// Usage — TypeScript infers T from the items array
type User = { id: number; name: string; email: string };

<List<User>
  items={users}
  renderItem={(user) => <span>{user.name} ({user.email})</span>}
  getKey={(user) => user.id}
/>

// T is inferred — explicit <User> is optional when items are already typed
<List
  items={users} // users: User[] — TypeScript infers T = User
  renderItem={(user) => <span>{user.name}</span>} // user is typed as User
  getKey={(user) => user.id}
/>
```

**Note for .tsx files:** Arrow function generics need a trailing comma to avoid JSX ambiguity:
```tsx
// This looks like a JSX tag to the parser:
const List = <T>(props: ListProps<T>) => { ... }   // ERROR

// Add trailing comma:
const List = <T,>(props: ListProps<T>) => { ... }  // OK

// Or use function declaration (cleaner):
function List<T>(props: ListProps<T>) { ... }       // OK
```

### 1J. React.ComponentProps and HTMLAttributes Patterns

```tsx
// Extract all native props from an HTML element
type NativeButtonProps = React.ComponentPropsWithoutRef<'button'>;

// Extend native element props with custom ones
type ButtonProps = React.ComponentPropsWithoutRef<'button'> & {
  variant: 'primary' | 'secondary';
  isLoading?: boolean;
};

function Button({ variant, isLoading, children, ...rest }: ButtonProps) {
  return (
    <button className={`btn btn--${variant}`} disabled={isLoading} {...rest}>
      {isLoading ? 'Loading...' : children}
    </button>
  );
}
// Consumers get full autocomplete for onClick, disabled, className, etc.
// PLUS your custom variant and isLoading props

// Extract props from YOUR OWN component
type MyButtonProps = React.ComponentProps<typeof Button>;
// Useful when wrapping or composing components
```

**`ComponentPropsWithoutRef` vs `ComponentPropsWithRef`:** Use `WithoutRef` when your component does NOT forward refs (most components). Use `WithRef` when it does. This prevents consumers from passing a ref that silently gets swallowed.

---

## 2. Common Mistakes (with Fixes)

### Mistake 1: Using `any` as an Escape Hatch
```tsx
// BAD — silently disables all type checking
const handleData = (data: any) => {
  data.whatever.doesnt.exist; // no error, crashes at runtime
};

// GOOD — use unknown + type narrowing
const handleData = (data: unknown) => {
  if (typeof data === 'object' && data !== null && 'name' in data) {
    console.log((data as { name: string }).name);
  }
};
```
**Why it persists:** Developers hit a complex type error, add `any` to unblock themselves, then never come back. Codebases accumulate `any` over time. One `any` infects everything it touches — it propagates through assignments and return types silently.

### Mistake 2: Not Typing Event Handlers
```tsx
// BAD — common in migrated JS codebases
const handleChange = (e: any) => {
  setQuery(e.target.value);
};

// GOOD
const handleChange = (e: React.ChangeEvent<HTMLInputElement>) => {
  setQuery(e.target.value); // autocomplete on target, value, etc.
};
```

### Mistake 3: Over-Typing (Adding Explicit Types Where Inference Works)
```tsx
// UNNECESSARY — TypeScript already infers these
const [count, setCount] = useState<number>(0);            // remove <number>
const doubled: number = count * 2;                        // remove : number
const names: string[] = users.map((u: User): string => u.name); // remove annotations

// CLEAN — let inference do its job
const [count, setCount] = useState(0);
const doubled = count * 2;
const names = users.map(u => u.name);
```
**The principle:** TypeScript's inference is powerful. Adding redundant types is noise that obscures the types that actually matter (function parameters, complex state, API boundaries).

### Mistake 4: Missing `as const` for String Literals
```tsx
// PROBLEM — TypeScript widens "primary" to string
const config = { variant: 'primary', size: 'large' };
// config.variant: string — not "primary"

// FIX — as const preserves literal types
const config = { variant: 'primary', size: 'large' } as const;
// config.variant: "primary" — exact literal type

// Common in custom hooks returning tuples (see section 1G)
```

### Mistake 5: Using React.FC
```tsx
// AVOID — React.FC has known issues:
// 1. Implicitly accepts children even when component shouldn't
// 2. Breaks generic component type inference
// 3. Makes return type opaque
const Card: React.FC<CardProps> = ({ title }) => { ... };

// PREFERRED — explicit prop typing
function Card({ title }: CardProps) { ... }
```
**Context:** Gusto Engineering published a 2026 case study on removing React.FC across their codebase. React.FC allows invalid default prop values without error, hides unused props (no dead-code warnings), and breaks generic inference.

### Mistake 6: Not Using Discriminated Unions for Component Variants
```tsx
// BAD — everything optional, impossible states are possible
type AlertProps = {
  type: 'success' | 'error';
  message?: string;
  errorCode?: number;
  retryAction?: () => void;
};
// Nothing prevents: <Alert type="success" errorCode={500} retryAction={fn} />

// GOOD — discriminated union enforces valid combinations
type AlertProps =
  | { type: 'success'; message: string }
  | { type: 'error'; message: string; errorCode: number; retryAction: () => void };
// <Alert type="success" errorCode={500} /> — COMPILE ERROR
```

---

## 3. Content Landscape Analysis

### Saturated Angles (Avoid These)
| Format | Why It's Saturated |
|--------|-------------------|
| "How to set up TypeScript with React" | Every framework CLI does this automatically. Vite, Next.js, CRA all scaffold TS by default. |
| "TypeScript basics for React beginners" | Dozens of Medium posts, LinkedIn Learning courses, YouTube tutorials cover this. |
| "Why you should use TypeScript" | The argument is over. 78% adoption among React devs (State of JS 2025). |
| React.FC vs function declarations debate | Extensively covered. The community consensus is clear (avoid React.FC). |
| Generic "10 TypeScript tips" listicles | High volume, low depth. Every dev blog has one. |

### Content Gap Opportunities
| Gap | Why It's Underserved |
|-----|---------------------|
| **Practical patterns with real code** (not theory) | Most posts explain concepts but don't show production-quality snippets with the WHY behind each pattern. |
| **The "inference-first" mindset** | Posts tend to either over-type everything or skip typing. Few teach WHEN to annotate vs. WHEN to let TypeScript infer. |
| **Discriminated unions for component APIs** | A powerful pattern that most posts mention in one bullet point but don't demonstrate with real component design. |
| **React 19 + TypeScript changes** | forwardRef deprecation, ref as prop, new hooks (useActionState, useFormStatus) — most TS+React content is pre-React 19. |
| **The `satisfies` operator in React** | Relatively new (TS 4.9+), almost never covered in React-specific contexts. Combines with `as const` for powerful config patterns. |
| **Generic components beyond basic examples** | Most tutorials show a trivial `<List items={[]} />` example. Few show constrained generics, generic hooks, or generic context patterns. |

### Competitive Landscape Summary
**Top Google results for "TypeScript React":**
- [React official docs](https://react.dev/learn/typescript): High quality but reference-style, not opinionated
- [React TypeScript Cheatsheets (GitHub)](https://github.com/typescript-cheatsheets/react): Comprehensive but dense, no narrative
- [Total TypeScript (Matt Pocock)](https://www.totaltypescript.com/): Best depth but paywalled workshops
- [LogRocket blog](https://blog.logrocket.com/react-typescript-10-patterns-writing-better-code/): Pattern-focused but aging
- [GFE blog](https://www.greatfrontend.com/blog/typescript-for-react-developers): 12 mistakes format, solid coverage

**Our angle:** The gap is in the "practical playbook" format — not a reference, not a tutorial, but a curated set of "here's the exact pattern, here's why, and here's the mistake it prevents." The inference-first philosophy (know WHEN to type and when NOT to) is the differentiating narrative.

---

## 4. Non-Obvious Insights

### Insight 1: TypeScript's Real Value in React Isn't Catching Typos — It's Designing Component APIs
**Surface understanding:** "TypeScript catches bugs."
**Deeper truth:** The biggest productivity gain comes from using types to DESIGN component interfaces. Discriminated unions prevent impossible states. Generic constraints enforce data flow contracts. The type system becomes a design tool, not just a safety net. When you type your props well, the component's usage documentation writes itself via autocomplete.

### Insight 2: The Best TypeScript Code Has FEWER Type Annotations, Not More
**Surface understanding:** "TypeScript means adding types everywhere."
**Deeper truth:** Over-typing is the #1 sign of a TypeScript beginner. Expert TS code leans heavily on inference: letting useState infer from initial values, letting map/filter/reduce infer return types, letting callback parameters inherit their types from context. You should only write an explicit type annotation when: (a) TypeScript can't infer it (function parameters, complex state), or (b) you want to constrain a value more narrowly than inference would (union types, literal types). The "inference-first" mindset produces cleaner, more maintainable code.

### Insight 3: `any` Doesn't Just Remove One Type Check — It Poisons Everything It Touches
**Surface understanding:** "Using any skips type checking for that variable."
**Deeper truth:** `any` is contagious. When you assign an `any` value to a typed variable, the receiving variable becomes effectively untyped too. One `any` in a function return type propagates to every consumer. Codebases accumulate `any` through copy-paste — one developer adds `any` to unblock themselves, another developer copies that pattern. `unknown` is the safe alternative: it forces you to narrow before you use.

### Insight 4: The useRef Overload Signature Is the Most Confusing Part of React's TypeScript API
**Surface understanding:** "useRef holds a reference."
**Deeper truth:** `useRef<T>(null)` and `useRef<T | null>(null)` produce fundamentally different types (RefObject vs MutableRefObject). This catches almost every developer at least once. The mental model: if null is ONLY in the initial value (not the type param), React assumes you're making a DOM ref and makes `.current` readonly. If null is IN the type param, React assumes you're storing a mutable value. This distinction has no equivalent in plain JavaScript — it's pure TypeScript-level API design.

### Insight 5: React 19 Eliminates the Single Most Common TypeScript Frustration Point
**Surface understanding:** "React 19 deprecated forwardRef."
**Deeper truth:** forwardRef was the #1 source of TypeScript confusion in React. It required knowing the correct generic parameter order (ref type first, props second — opposite of what you'd expect), it couldn't be combined with generics without helper utilities, and it added a wrapper that made component types harder to inspect. React 19's "ref as prop" pattern means refs are typed exactly like every other prop — no special syntax, no wrapper, no generic gymnastics. This is the single biggest DX improvement for TypeScript + React in years.

### Insight 6: The `satisfies` Operator Solves a Problem Most React Devs Don't Know They Have
**Surface understanding:** "satisfies is like a type annotation."
**Deeper truth:** With a type annotation (`const x: Type = value`), the type wins — TypeScript widens your value to match the type. With `satisfies` (`const x = value satisfies Type`), the value wins — TypeScript validates the structure matches BUT preserves the narrower inferred type. Combined with `as const`, this gives you both validation AND exact literal inference. In React, this is powerful for config objects, route definitions, and theme tokens where you want compile-time validation without losing autocomplete on specific values.

---

## 5. GFE CTA Page Analysis

**URL:** https://www.greatfrontend.com/questions/typescript-interview-questions

**What it offers:**
- 420+ TypeScript interview questions (coding + quiz format)
- Curated by ex-FAANG interviewers
- Two main categories:
  - **Coding questions** (232 questions, ~86 hours): JavaScript functions, algorithmic problems, in-browser workspace with instant feedback
  - **Quiz questions**: Multiple-choice on interfaces, generics, conditional types, advanced typing
- Sample questions include: Flatten, Debounce, Promise.all/race/any implementations, Stack, Queue, Linked List, Binary Tree, sorting/searching/DP algorithms
- Solutions with detailed explanations
- Premium tier for full access (specific pricing not captured)
- "Get full access" CTA and pricing link visible

**Tie-in with post content:** Natural fit. The post teaches practical TypeScript patterns in React. The CTA extends that into interview preparation — same skill set, deeper practice. The bridge: "These patterns aren't just for production code — they're exactly what interviewers test."

---

## Insight Map (for Content Brief)

### Surface --> Insight Pairs
1. Surface: "Add types to your React props" --> **Insight: Types are a component API design tool. Well-typed props make impossible states unrepresentable and generate their own documentation via autocomplete.**
2. Surface: "TypeScript means more code to write" --> **Insight: Expert TypeScript has FEWER annotations. Inference-first is the pro pattern — annotate only at boundaries and ambiguous points.**
3. Surface: "useRef is simple, just pass null" --> **Insight: The null placement (type param vs initial value) creates fundamentally different types. It's the most confusing TypeScript overload in React's API.**
4. Surface: "forwardRef is how you pass refs" --> **Insight: React 19 killed forwardRef because it was TypeScript's biggest pain point. Ref-as-prop is the biggest TS DX improvement in years.**
5. Surface: "Use any when types get complicated" --> **Insight: any is contagious — it infects every variable it touches. unknown forces narrowing and keeps the rest of your codebase safe.**

### Myth-Busts
- "More type annotations = better TypeScript" --> Over-typing is noise. It obscures the annotations that actually matter.
- "TypeScript is just catching typos" --> The real value is designing component APIs that prevent impossible states at compile time.
- "Generic components are an advanced topic" --> They're the natural solution once you build your second `<List>` or `<Table>` — the pattern is simpler than it looks.
- "You need React.FC to type a component" --> React.FC is actively harmful (implicit children, broken generics). Plain function + prop type is better.

---

## Sources
- [React Official TypeScript Docs](https://react.dev/learn/typescript)
- [React TypeScript Cheatsheets (GitHub)](https://github.com/typescript-cheatsheets/react)
- [Total TypeScript — ComponentProps Helper](https://www.totaltypescript.com/react-component-props-type-helper)
- [Total TypeScript — Discriminated Unions in React](https://www.totaltypescript.com/workshops/advanced-react-with-typescript/advanced-props/type-checking-react-props-with-discriminated-unions/solution)
- [Total TypeScript — as const for Tuple Inference](https://www.totaltypescript.com/workshops/advanced-react-with-typescript/advanced-hooks/fixing-type-inference-in-a-custom-react-hook/solution)
- [Total TypeScript — satisfies Operator](https://www.totaltypescript.com/how-to-use-satisfies-operator)
- [GFE Blog — 12 TypeScript React Mistakes](https://www.greatfrontend.com/blog/typescript-for-react-developers)
- [LogRocket — 10 React TypeScript Patterns](https://blog.logrocket.com/react-typescript-10-patterns-writing-better-code/)
- [DeveloperWay — Discriminated Unions](https://www.developerway.com/posts/advanced-typescript-for-react-developers-discriminated-unions)
- [Gusto Engineering — Why We Removed React.FC](https://engineering.gusto.com/the-journey-to-a-safer-frontend-why-we-removed-react-fc-095ff0b3e2e4)
- [ClarityDev — Typing useRef](https://claritydev.net/blog/typescript-typing-react-useref-hook)
- [fettblog.eu — Typing Custom Hooks with Tuple Types](https://fettblog.eu/typescript-react-typeing-custom-hooks/)
- [tinytip.co — Custom Hooks Named Tuples](https://tinytip.co/tips/react-hook-tuple/)
- [React TypeScript Cheatsheets — Forms and Events](https://react-typescript-cheatsheet.netlify.app/docs/basic/getting-started/forms_and_events/)
- [OneUpTime — Discriminated Unions React Props](https://oneuptime.com/blog/post/2026-01-15-typescript-discriminated-unions-react-props/view)
- [OneUpTime — Generic Components React TypeScript](https://oneuptime.com/blog/post/2026-01-15-generic-components-react-typescript/view)
- [DEV Community — 5 Common TypeScript React Mistakes](https://dev.to/roladev/5-most-common-mistakes-when-using-typescript-with-react-1ch0)
- [Kent C. Dodds — How to Write a React Component in TypeScript](https://kentcdodds.com/blog/how-to-write-a-react-component-in-typescript)
- [Medium — React 19 Ref as Prop](https://medium.com/@ignatovich.dm/the-new-approach-to-passing-refs-in-react-19-typescript-a5762b938b93)
- [LogRocket — 8 Trends Web Dev 2026](https://blog.logrocket.com/8-trends-web-dev-2026/)
