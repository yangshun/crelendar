# Research: Build These 5 Projects and Get Yourself Hired
**Publish date:** TBD
**Researched:** 2026-02-25

---

## 1. The 5 Best Portfolio Projects for Front-End Devs

### Selection criteria applied
Evaluated 8 candidate projects against: (a) skills tested in actual frontend interviews at top companies, (b) real-world relevance (something a company would actually build), (c) coverage of distinct skill areas, (d) alignment with GFE Projects platform offerings, (e) differentiation from saturated "bootcamp project" lists.

### Eliminated candidates and why

| Candidate | Verdict | Reason |
|---|---|---|
| Full-stack app with auth | Cut | Auth is a backend concern - portfolio should prove frontend depth, not breadth. Auth flows are increasingly handled by services (Clerk, Auth0, Supabase Auth). Doesn't demonstrate unique frontend skills. |
| Content management system | Cut | Too broad, hard to scope well for a portfolio piece. Tends to become a half-finished CRUD app. |
| Landing page with animations | Cut | Saturated - every YouTube "build a portfolio" tutorial covers this. Doesn't demonstrate complex state or data handling. Useful as a skill but not portfolio-worthy on its own. |

### The 5 Selected Projects

---

#### Project 1: E-Commerce Product Page
**One-line description:** A performance-optimized product page with image gallery, variant selection, and cart functionality.

**Key skills demonstrated:**
- Performance optimization (Core Web Vitals, lazy loading, image optimization)
- Responsive design with complex layouts
- State management for cart/variant logic
- Accessibility (keyboard navigation, screen reader support for interactive elements)

**What makes it stand out to interviewers:**
This is the #1 thing frontend devs are hired to build. Every company with a web product has product pages. Interviewers can immediately assess real-world readiness. A product page with a 90+ Lighthouse score shows you understand what production code demands - not just what "works."

**Specific technical challenge:**
Implementing an image gallery with lazy-loaded thumbnails, zoom-on-hover, responsive srcset/sizes for different viewports, and skeleton loading states - all while keeping Largest Contentful Paint under 2.5s.

**Interview skill match:**
- Frontend system design interviews ask about image optimization, responsive strategies, and state management patterns
- Machine coding rounds test interactive components (image carousels, variant selectors)
- Companies like Amazon, Shopify, and every D2C brand test these skills directly

**GFE alignment:** GFE has Product Details Page, Shopping Cart Section, Checkout Section, and a full E-Commerce Website (Nightmare tier) challenge. The E-Commerce component track lets users build individual pieces that compose into a full store.

**Sources:**
- [Frontend Mentor E-commerce Projects](https://www.frontendmentor.io/use-cases/e-commerce-projects)
- [GFE E-Commerce Website Challenge](https://www.greatfrontend.com/projects/challenges/e-commerce-website)
- [Amazon 100ms delay = 1% sales loss](https://nitropack.io/blog/post/best-image-optimization-tricks-for-ecommerce)

---

#### Project 2: Analytics Dashboard with Data Visualization
**One-line description:** An interactive dashboard with charts, filters, and real-time data updates displaying meaningful metrics.

**Key skills demonstrated:**
- Data visualization (D3.js, Chart.js, Recharts, or similar)
- Complex state management (filters, date ranges, cross-chart interactions)
- API integration and data transformation
- Responsive layouts with CSS Grid for dashboard panels

**What makes it stand out to interviewers:**
Dashboards are one of the most common things frontend devs build professionally (internal tools, admin panels, analytics products). Most portfolio dashboards just render a chart - a standout one has cross-filtering (clicking a bar chart filters the table below), handles loading/error/empty states gracefully, and works on mobile.

**Specific technical challenge:**
Building a date-range filter that updates multiple chart components simultaneously with debounced API calls, skeleton loading states per panel, and client-side data caching to avoid refetching when toggling between previously-viewed ranges.

**Interview skill match:**
- Frontend system design interviews frequently ask about dashboard architecture, data fetching strategies (polling vs WebSocket vs SSE), and client-side caching
- State management is the #1 tested skill in React interviews - dashboards force you to handle shared state across many components
- Companies like Stripe, Datadog, Vercel, and every SaaS product test dashboard-building skills

**GFE alignment:** GFE's Billing History Section, Billing Information Section, and Account Settings Section are dashboard-adjacent components. The Web Apps track covers interactive data-driven interfaces.

**Sources:**
- [Tinybird: Real-time Data Visualization](https://www.tinybird.co/blog/real-time-data-visualization)
- [Frontend System Design Handbook](https://frontendlead.com/system-design/frontend-system-design-interview-guide)
- [React + D3.js for interactive dashboards](https://www.zigpoll.com/content/which-frontend-frameworks-or-tools-are-best-suited-for-building-interactive-data-visualization-dashboards-for-a-data-science-team)

---

#### Project 3: Kanban Task Board with Drag-and-Drop
**One-line description:** A Trello-style task board with drag-and-drop between columns, keyboard accessibility, and persistent state.

**Key skills demonstrated:**
- Drag-and-drop implementation (HTML Drag and Drop API or dnd-kit)
- Complex state management (optimistic updates, column reordering, task CRUD)
- Accessibility (keyboard navigation for drag-and-drop, ARIA live regions)
- Local persistence (localStorage or IndexedDB)

**What makes it stand out to interviewers:**
Drag-and-drop with accessibility is a notorious interview differentiator. Most devs can make drag-and-drop "work" visually - very few make it keyboard-accessible. The Frontend Interview Handbook explicitly states that "knowledge of a11y is one of the differentiating factors between junior vs senior engineers." A Kanban board that works with keyboard-only navigation immediately signals senior-level thinking.

**Specific technical challenge:**
Making drag-and-drop fully keyboard-accessible: users should be able to pick up a task with Enter/Space, move it between columns with arrow keys, see clear visual focus indicators, and hear screen reader announcements ("Task moved to In Progress column, position 3 of 5").

**Interview skill match:**
- Machine coding rounds frequently ask for interactive list manipulation (sortable lists, drag reorder)
- Accessibility questions are becoming standard in interviews at companies that care about compliance (banks, government, enterprise SaaS)
- Frontend system design interviews ask about optimistic updates and offline-capable state management
- Companies like Atlassian, Linear, Notion, and Monday.com build exactly this

**GFE alignment:** GFE's component tracks teach the building blocks (buttons, inputs, cards) that compose into a Kanban board. The modular design system approach mirrors how real teams build complex UIs.

**Sources:**
- [MDN: Kanban Board with Drag and Drop](https://developer.mozilla.org/en-US/docs/Web/API/HTML_Drag_and_Drop_API/Kanban_board)
- [dnd-kit: Lightweight drag-and-drop with keyboard/screen reader support](https://radzion.com/blog/kanban/)
- [Frontend Interview Handbook: a11y as junior vs senior differentiator](https://www.frontendinterviewhandbook.com/coding/build-front-end-user-interfaces)
- [Marmelab: Kanban Board with Shadcn](https://marmelab.com/blog/2026/01/15/building-a-kanban-board-with-shadcn.html)

---

#### Project 4: Design System / Component Library
**One-line description:** A documented, tested library of reusable UI components with Storybook, unit tests, and accessibility baked in.

**Key skills demonstrated:**
- Component API design (props, composition patterns, polymorphism)
- Testing (unit tests with Testing Library, visual regression with Storybook)
- Documentation (Storybook stories as living docs)
- Accessibility (WCAG compliance, ARIA patterns across all components)

**What makes it stand out to interviewers:**
This is the most "senior-level" project on the list. Building individual components is junior. Building a system of components that work together - with consistent APIs, theme support, and documentation that other devs can follow - is what senior/staff engineers do. No other portfolio project demonstrates this level of engineering maturity.

**Specific technical challenge:**
Building a compound component pattern (e.g., a Tabs component with `<Tabs>`, `<TabList>`, `<Tab>`, `<TabPanel>`) that manages shared state via React Context, supports controlled and uncontrolled modes, handles keyboard navigation per WAI-ARIA Tabs pattern, and has full Storybook documentation with interactive controls.

**Interview skill match:**
- Machine coding rounds test component design directly (build a Modal, build a Select, build an Autocomplete)
- Senior frontend interviews assess your ability to design reusable APIs and think about component consumers
- Frontend system design interviews ask about design system architecture and component composition
- Companies like Google, Meta, Airbnb, and Shopify all have internal design systems - showing you can build one is a direct skill match

**GFE alignment:** GFE has an entire Design System track (Premium, +1.7k rep) where users build design system components from scratch. Free starter challenges like Button Component, Badge Component, Checkbox Component, and Text Input Component are the building blocks of a design system. This is a direct 1:1 alignment.

**Sources:**
- [Storybook: Frontend workshop for UI development](https://storybook.js.org/)
- [Frontend Masters: Create Consistent UIs with Storybook](https://frontendmasters.com/courses/design-systems-v2/)
- [GFE Design System Track](https://www.greatfrontend.com/projects/tracks/design-system)
- [Storybook Design System on GitHub](https://github.com/storybookjs/design-system)

---

#### Project 5: Real-Time Chat Interface
**One-line description:** A messaging interface with WebSocket-powered real-time updates, message history, typing indicators, and online status.

**Key skills demonstrated:**
- WebSocket/real-time communication (Socket.IO or native WebSocket API)
- Optimistic UI updates (show message immediately, reconcile with server)
- Virtualized lists for message history (performance with thousands of messages)
- Complex UI states (typing indicators, read receipts, connection status)

**What makes it stand out to interviewers:**
Real-time UIs expose edge cases that simple CRUD apps never touch: What happens when the connection drops? How do you handle messages sent while offline? How do you prevent the UI from freezing when rendering 10,000 messages? These are production-level problems that separate portfolio projects from tutorial copies.

**Specific technical challenge:**
Implementing optimistic message sending with offline queue: messages appear instantly in the UI, get queued when offline (with visual "pending" state), automatically retry on reconnect, and reconcile with server-assigned IDs/timestamps - all without duplicate messages appearing.

**Interview skill match:**
- Frontend system design interviews commonly ask "Design a chat application" or "Design a messaging feed" - this is one of the most-asked system design questions
- Real-time patterns (WebSocket, SSE, polling) are tested at companies building collaborative tools
- Optimistic updates and offline support are becoming standard interview topics
- Companies like Slack, Discord, Meta (Messenger), and any product with real-time features test these skills

**GFE alignment:** GFE has a Chat AI challenge (Nightmare tier) for building a responsive chat application to interact with LLMs. The underlying UI patterns (message lists, input fields, real-time updates) are the same as a general chat app.

**Sources:**
- [DEV Community: Frontend System Design - Building a Web Chat Application](https://dev.to/vishwark/frontend-system-design-deep-dive1-building-a-web-chat-application-5c8j)
- [Frontend Interview Handbook: Frontend System Design](https://www.frontendinterviewhandbook.com/front-end-system-design)
- [Socket.IO Real-Time Chat Application](https://github.com/shaikahmadnawaz/chat-app)
- [Deno WebSocket Chat Tutorial](https://docs.deno.com/examples/chat_app_tutorial/)

---

## 2. Why These 5 vs Random Projects

### What hiring managers actually look for

**Key statistics:**
- 84% of employers want to see working deployed applications, not just code repos ([Nucamp](https://www.nucamp.co/blog/top-10-full-stack-portfolio-projects-for-2026-that-actually-get-you-hired))
- 60%+ of recruiters want projects that solve actual problems, demonstrating problem-solving with complex scenarios ([Nucamp](https://www.nucamp.co/blog/coding-bootcamp-job-hunting-selecting-projects-for-your-portfolio-what-recruiters-look-for))
- 70% of hiring managers want variety across projects, proving adaptability ([Nucamp](https://www.nucamp.co/blog/coding-bootcamp-job-hunting-selecting-projects-for-your-portfolio-what-recruiters-look-for))
- Portfolios with 4-10 strong projects impress nearly 60% of recruiters ([Dev.to](https://dev.to/siddheshcodes/frontend-developer-portfolio-tips-for-2025-build-a-stunning-site-that-gets-you-hired-3hga))
- Hiring managers spend ~30 seconds on a portfolio - projects need to make an immediate impact ([Skillcrush](https://skillcrush.com/blog/front-end-developer-portfolio/))

**What skills get tested in actual frontend interviews (2025-2026):**

| Interview Round | What's Tested | Which Project Proves It |
|---|---|---|
| Machine Coding | Build a UI component from scratch (autocomplete, modal, tabs, image carousel) | Design System (#4), E-Commerce (#1) |
| Frontend System Design | Design architecture for a complex UI (chat app, news feed, dashboard) | Chat Interface (#5), Dashboard (#2) |
| JavaScript/React Deep Dive | State management, hooks, performance patterns, event handling | All 5 - each forces different state patterns |
| Accessibility | ARIA patterns, keyboard navigation, screen reader support | Kanban Board (#3), Design System (#4) |
| Performance | Core Web Vitals, lazy loading, code splitting, rendering strategies | E-Commerce (#1), Dashboard (#2) |

Sources: [Frontend Interview Handbook 2026](https://www.frontendinterviewhandbook.com/), [Elite Brains Frontend Interview Guide](https://www.elitebrains.com/blog/how-to-screen-frontend-engineers-int-questions), [InterviewKickstart Meta Frontend Masterclass](https://interviewkickstart.com/masterclass/frontend-masterclass-page)

### Common portfolio mistakes

**From reviewing 200+ developer portfolios ([DEV Community](https://dev.to/matthewhou/ive-reviewed-200-developer-portfolios-90-make-the-same-4-mistakes-16kd)):**

1. **Tutorial clones without differentiation.** Weather apps, Netflix clones, and to-do apps are the most common - they signal "I followed a tutorial" not "I can build software." Hiring managers see these 50+ times per hiring cycle.

2. **Broken live demos.** Heroku error pages, blank screens, login forms with no test credentials. A broken demo is worse than no demo - it suggests you don't maintain your work.

3. **No project context.** Listing technologies without explaining what the project does, who it's for, or what problems you solved. Writing for engineers rather than evaluators.

4. **Accessibility neglected entirely.** "Accessibility was the biggest mistake made throughout portfolio reviews" - one of the first things reviewers do is try to navigate without a mouse. Color contrast failures, no keyboard navigation, missing alt text. ([freeCodeCamp: 50 Portfolio Reviews](https://www.freecodecamp.org/news/i-reviewed-fifty-portfolios-on-reddit-and-this-is-what-i-learned-e5d2b43150bc/))

**Additional common mistakes from LinkedIn/Reddit research:**
- Including old, outdated projects that use deprecated libraries or patterns
- No README or documentation explaining the project
- Overstuffing with 10-15 simple projects instead of 3-5 excellent ones
- Inconsistent styling, typos, and broken links signal poor attention to detail

Sources: [LinkedIn Portfolio Mistakes](https://www.linkedin.com/advice/0/what-most-important-things-avoid-your-web-developer-lk51e), [freeCodeCamp: 50 Portfolios Reviewed](https://www.freecodecamp.org/news/i-reviewed-fifty-portfolios-on-reddit-and-this-is-what-i-learned-e5d2b43150bc/)

### What makes a project "senior-level" vs "bootcamp-level"

| Bootcamp-Level | Senior-Level |
|---|---|
| "It works" is the bar | Performance, accessibility, and edge cases handled |
| Single component or page | System of components that work together |
| Follows a tutorial step-by-step | Makes architectural decisions and explains them |
| No error handling or loading states | Graceful degradation, skeleton screens, retry logic |
| Works in Chrome on desktop | Responsive, cross-browser, keyboard-navigable |
| State lives in one component | Intentional state architecture (what's local vs global vs URL) |
| No tests | Unit tests, integration tests, or visual regression |
| No documentation | README explains decisions, tradeoffs, and what you'd do differently |

**Key differentiator:** Senior projects show evidence of engineering judgment - decisions about what NOT to build, what tradeoffs were made, and why. A README that says "I chose client-side filtering over server-side because the dataset is <1000 items and this avoids API round trips" demonstrates more maturity than a project with 10x more features.

Sources: [DistantJob: Junior vs Senior Developer Skills](https://distantjob.com/blog/junior-front-end-developer-skills/), [Codecademy: Junior Developer Portfolio](https://www.codecademy.com/resources/blog/what-to-include-in-a-junior-developer-portfolio), [Frontend Interview Handbook](https://www.frontendinterviewhandbook.com/coding/build-front-end-user-interfaces)

---

## 3. Content Landscape Research

### Saturated angles (avoid these)
- **"Top 10/15/20 Frontend Projects for Beginners"** - Every YouTube channel and blog has this. WSCubeTech, DEV Community, Career Boss, GeeksforGeeks all have near-identical lists. The projects are always: to-do app, weather app, calculator, portfolio website, quiz game.
- **"Netflix/Instagram/Amazon Clone"** - Tutorial clone content is ubiquitous. Hiring managers specifically cite these as red flags.
- **"Build a Portfolio Website"** - Meta-ironic: telling people to build a portfolio as their portfolio project. Every beginner tutorial covers this.
- **Generic "projects to learn React/JavaScript"** lists with no hiring angle

### Fresh angles (differentiation opportunities)
- **"Quality over quantity" framing** - Some posts mention this in passing, but none make it the CORE thesis with evidence. "5 targeted projects > 15 random ones" is contrarian enough to drive debate.
- **Mapping projects to actual interview rounds** - No viral post explicitly maps portfolio projects to the 4-5 rounds of a frontend interview (machine coding, system design, JS deep dive, accessibility, behavioral). This is a genuine content gap.
- **Hiring manager perspective** - Most "portfolio project" content is written by bootcamps and tutorial creators. Very few posts come from the perspective of "what interviewers actually evaluate."
- **GFE platform tie-in as a builder** - Competitors (Frontend Mentor, devChallenges) get mentioned in generic lists, but nobody has tied "here's WHY these projects matter" to a structured building platform with specs, designs, and community review.

### Existing content by channel

**LinkedIn:**
- Yomesh Gupta's "Top Frontend Projects That Will Get You HIRED!" - popular post listing project types without interview-mapping depth ([LinkedIn](https://www.linkedin.com/posts/yomeshgupta_top-frontend-projects-that-will-get-you-hired-activity-7133703621199675392-5eIO))
- Several "Top 5 Frontend Projects" posts exist from 2023-2024, mostly shallow lists
- "Today I learned" posts about specific projects get high engagement
- Portfolio advice posts are common but lack specificity about which projects map to which interview skills

**YouTube:**
- "5 Projects to Get Hired" is a common video title format - appears on channels ranging from 10K to 500K+ subscribers
- Most recommend beginner projects (to-do, weather, calculator) - the "advanced projects that impress hiring managers" angle is less covered
- Frontend Mentor and similar platforms are frequently recommended but without the "why these skills matter for interviews" framing

**Reddit (r/webdev, r/frontend, r/reactjs):**
- Recurring advice: "quality over quantity" and "solve a real problem"
- Frequent criticism of tutorial clones
- Community values accessibility and performance - mentioning these as explicit project goals resonates
- Skepticism toward "build X projects to get hired" content because it usually recommends basic projects

**Blogs/Publications:**
- Codecademy's "5 Eye-Catching Projects for a Front-End Developer Portfolio" - good but generic, no interview mapping ([Codecademy](https://www.codecademy.com/resources/blog/projects-for-a-front-end-developer-portfolio))
- Frontend Mentor's "Building an Effective Frontend Developer Portfolio" - solid advice but platform-agnostic ([Frontend Mentor](https://www.frontendmentor.io/articles/building-an-effective-frontend-developer-portfolio--7cE8BfMG_))
- Medium posts like "5 Advanced Projects to Land a Frontend Developer Job" exist but lack the data-backed hiring manager angle ([Medium](https://medium.com/@amolrai3/5-advanced-projects-to-land-a-frontend-developer-job-in-2024-8f62b642e6c2))

### Content gap we can fill
Nobody has published a post that:
1. Names exactly 5 projects with clear rationale for why THESE 5 and not others
2. Maps each project to specific frontend interview rounds
3. Backs claims with hiring manager statistics
4. Provides a pathway to actually build them (GFE as the platform)
5. Explicitly shows the "bootcamp-level vs senior-level" distinction for each project

This is the angle - not "here are projects you can build" but "here's exactly what interviewers evaluate and which projects prove you can pass each round."

---

## 4. GFE Projects Page Findings

### Platform overview
- **66 total challenges** across 4 difficulty tiers (Starter, Mid, Senior, Nightmare)
- **80% of challenges are free** - this is a key CTA stat
- Projects are modular and composable - components from one challenge fit into others
- Provides production-ready specs, professional Figma designs, API specifications, and starter code

### Component tracks (curated paths)
| Track | Focus | Paid/Free |
|---|---|---|
| Marketing | Landing pages, features pages, pricing pages, about/contact pages | Mix |
| E-Commerce | Product pages, shopping carts, checkout flows, billing sections | Mix |
| Web Apps | Interactive application interfaces, account settings, dashboards | Mix |
| Design System | Reusable component library foundation (buttons, inputs, badges, etc.) | Premium (+1.7k rep) |

### Key challenges relevant to brief
| Challenge | Tier | Relevant Project |
|---|---|---|
| Button Component | Starter (Free) | Design System (#4) |
| Badge Component | Starter (Free) | Design System (#4) |
| Checkbox Component | Starter (Free) | Design System (#4) |
| Text Input Component | Starter (Free) | Design System (#4) |
| Product Details Page | Senior | E-Commerce (#1) |
| Shopping Cart Section | Senior | E-Commerce (#1) |
| Checkout Section | Senior (Premium) | E-Commerce (#1) |
| E-Commerce Website | Nightmare (Premium) | E-Commerce (#1) |
| Account Settings Section | Mid | Dashboard (#2) |
| Billing History Section | Mid | Dashboard (#2) |
| Billing Information Section | Mid | Dashboard (#2) |
| Chat AI | Nightmare | Chat Interface (#5) |

### CTA alignment
- Primary CTA: https://www.greatfrontend.com/projects
- Strong selling points: 80% free, production-ready specs, professional designs, community code reviews, modular component system
- Natural tie-in: "These aren't tutorial projects - they come with the same specs, designs, and requirements you'd get at a real company"

---

## 5. Insight Map

### What the audience already knows (surface-level)
- You need portfolio projects to get hired
- To-do apps and weather apps aren't impressive
- React, TypeScript, and modern frameworks matter
- You should have a GitHub and deployed demos

### What would be new/surprising (the insights)
1. **5 targeted projects map 1:1 to the 5 rounds of a frontend interview** - most devs build random projects without connecting them to what's actually assessed. Each interview round (machine coding, system design, JS deep dive, accessibility, performance) has a specific project that proves competence.

2. **Accessibility is the #1 differentiator between junior and senior portfolios** - not TypeScript, not testing, not complex state management. The Frontend Interview Handbook explicitly states this. Most devs skip it entirely.

3. **84% of employers want deployed apps, but the bar is higher than "it runs"** - a broken Heroku link is worse than no demo. A Lighthouse score under 60 signals you don't know what production means.

4. **A README explaining your tradeoffs is worth more than 3 extra features** - hiring managers spend 30 seconds. They're looking for engineering judgment, not feature count. "I chose X over Y because..." is the signal.

5. **The "random projects" problem is quantified** - 60% of recruiters want problem-solving depth, 70% want variety across skill areas. Building 15 React CRUD apps shows neither.

### Debate hooks
- "Design systems are the most senior-level project" - will trigger debate from full-stack advocates
- "Auth flows don't belong in a frontend portfolio" - controversial take that challenges the full-stack-or-bust mentality
- "5 projects > 15 projects" - provokes response from people with large portfolios
- "Accessibility is the #1 skill gap" - accessibility advocates will amplify, skeptics will push back

---

## Sources Index

### Primary sources
- [Frontend Interview Handbook 2026](https://www.frontendinterviewhandbook.com/)
- [GFE Projects Platform](https://www.greatfrontend.com/projects)
- [GFE Projects Challenges](https://www.greatfrontend.com/projects/challenges)
- [GFE Blog: Announcing Projects Platform](https://www.greatfrontend.com/blog/a-real-world-projects-platform-for-front-end-engineers)
- [GFE Design System Track](https://www.greatfrontend.com/projects/tracks/design-system)
- [GFE E-Commerce Website Challenge](https://www.greatfrontend.com/projects/challenges/e-commerce-website)
- [GFE Frontend System Design Playbook](https://www.greatfrontend.com/front-end-system-design-playbook)

### Hiring manager / recruiter research
- [Nucamp: Top 10 Full Stack Portfolio Projects for 2026](https://www.nucamp.co/blog/top-10-full-stack-portfolio-projects-for-2026-that-actually-get-you-hired)
- [Nucamp: Selecting Projects - What Recruiters Look For](https://www.nucamp.co/blog/coding-bootcamp-job-hunting-selecting-projects-for-your-portfolio-what-recruiters-look-for)
- [Skillcrush: Front End Developer Portfolio](https://skillcrush.com/blog/front-end-developer-portfolio/)
- [RocketDevs: Frontend Developer Portfolios - How Employers Evaluate](https://rocketdevs.com/blog/frontend-developer-portfolios)
- [Codecademy: Junior Developer Portfolio Must-Haves](https://www.codecademy.com/resources/blog/what-to-include-in-a-junior-developer-portfolio)

### Portfolio reviews and mistakes
- [freeCodeCamp: 50 Portfolios Reviewed on Reddit](https://www.freecodecamp.org/news/i-reviewed-fifty-portfolios-on-reddit-and-this-is-what-i-learned-e5d2b43150bc/)
- [DEV Community: 200+ Developer Portfolios - 4 Common Mistakes](https://dev.to/matthewhou/ive-reviewed-200-developer-portfolios-90-make-the-same-4-mistakes-16kd)
- [LinkedIn: Common Web Portfolio Mistakes](https://www.linkedin.com/advice/0/what-most-important-things-avoid-your-web-developer-lk51e)
- [Frontend Mentor: Building an Effective Frontend Developer Portfolio](https://www.frontendmentor.io/articles/building-an-effective-frontend-developer-portfolio--7cE8BfMG_)
- [DEV Community: Frontend Developer Portfolio Tips for 2025](https://dev.to/siddheshcodes/frontend-developer-portfolio-tips-for-2025-build-a-stunning-site-that-gets-you-hired-3hga)

### Interview skills research
- [Elite Brains: How to Screen Frontend Engineers 2026](https://www.elitebrains.com/blog/how-to-screen-frontend-engineers-int-questions)
- [InterviewKickstart: Frontend Masterclass - Meta Engineers](https://interviewkickstart.com/masterclass/frontend-masterclass-page)
- [Mimo: 43 Real-World Front-End Developer Interview Questions](https://mimo.org/blog/front-end-developer-interview-questions)
- [Coursera: Front-end Developer Interview Questions 2026](https://www.coursera.org/articles/front-end-developer-interview-questions)
- [Frontend Interview Handbook: UI Component Building](https://www.frontendinterviewhandbook.com/coding/build-front-end-user-interfaces)
- [Frontend System Design Handbook](https://frontendlead.com/system-design/frontend-system-design-interview-guide)

### Project-specific sources
- [MDN: Kanban Board with HTML Drag and Drop API](https://developer.mozilla.org/en-US/docs/Web/API/HTML_Drag_and_Drop_API/Kanban_board)
- [dnd-kit Kanban Implementation](https://radzion.com/blog/kanban/)
- [Marmelab: Kanban Board with Shadcn (Jan 2026)](https://marmelab.com/blog/2026/01/15/building-a-kanban-board-with-shadcn.html)
- [Storybook: Frontend Workshop](https://storybook.js.org/)
- [Tinybird: Real-time Data Visualization](https://www.tinybird.co/blog/real-time-data-visualization)
- [DEV Community: Frontend System Design - Chat Application](https://dev.to/vishwark/frontend-system-design-deep-dive1-building-a-web-chat-application-5c8j)
- [Socket.IO Chat App](https://github.com/shaikahmadnawaz/chat-app)
- [NitroPage: E-Commerce Image Optimization](https://nitropack.io/blog/post/best-image-optimization-tricks-for-ecommerce)

### Content landscape
- [LinkedIn: Top Frontend Projects That Will Get You HIRED](https://www.linkedin.com/posts/yomeshgupta_top-frontend-projects-that-will-get-you-hired-activity-7133703621199675392-5eIO)
- [Medium: 5 Advanced Projects to Land a Frontend Developer Job](https://medium.com/@amolrai3/5-advanced-projects-to-land-a-frontend-developer-job-in-2024-8f62b642e6c2)
- [Codecademy: 5 Eye-Catching Projects](https://www.codecademy.com/resources/blog/projects-for-a-front-end-developer-portfolio)
- [WSCubeTech: Top 20 Front-end Development Projects 2026](https://www.wscubetech.com/blog/front-end-development-projects/)
- [DistantJob: Junior vs Senior Developer Skills](https://distantjob.com/blog/junior-front-end-developer-skills/)
