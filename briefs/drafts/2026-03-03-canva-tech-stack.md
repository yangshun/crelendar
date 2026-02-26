# ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
# BRIEF INFO
# ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

# How Canva Is Actually Built

- **Date:** 2026-03-03
- **Topic:** Canva tech stack breakdown — frontend architecture of a 265M-user design tool
- **Pillar:** 🏗️ Tech Breakdown
- **Format:** Single Image (Static Infographic)
- **Format rationale:** All 3 prior tech stack breakdowns (Netflix, Shopify, Figma) performed as single images or GIFs — not carousels. Tech stack posts are information-dense and save-worthy as reference cards. Under 7 distinct sections = single image per format guide. This also breaks the recent carousel streak (last 2 briefs were carousel and single image).
- **Key angle:** The gap between perception and reality. Everyone thinks Canva is "just a drag-and-drop design tool." In reality, it runs a 60M-line monorepo built with Bazel, uses MobX with a custom Store-Presenter-Component pattern (not Redux), and leverages WebGL for specific image processing like alpha blending. Natural sequel to the Figma breakdown post.
- **GFE tie-in:** Footer CTA linking to GFE system design interview questions. Post delivers full value standalone.
- **Design inspiration:** Figma breakdown style — Canva interface screenshot with tech logos overlaid, arrows mapping each technology to the UI region it powers. Dark theme.
- **Color theme:** Dark (navy/black bg)
- **Accent color:** Canva's brand purple (#7D2AE8) and teal (#00C4CC) for tech labels. White text on dark bg.


# ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
# CAPTION
# ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

## LinkedIn Caption
265 million people use Canva every month. Almost nobody knows how it's built.

You'd expect a drag-and-drop design tool to have a simple stack. Instead, Canva runs a 60 million line monorepo with 500K+ files, built with Bazel — not Turborepo or Nx. State management? MobX with a custom Store-Presenter-Component pattern — not Redux, not Zustand. And for heavy image processing like alpha blending, they reach for WebGL to get GPU-level performance.

The toolbars, sidebars, and editor are all React + TypeScript. But the architectural decisions underneath — MobX, Bazel, monorepo at that scale — that's where it gets interesting.

What surprised you most about this stack?

#Canva #TechStack #FrontEndDevelopment #React #MobX #SystemDesign #GreatFrontEnd #WebDevelopment

Want to ace front-end system design interviews? GFE has system design practice questions using the RADIO framework - covering collaborative editors, image-heavy platforms, and more: https://www.greatfrontend.com/system-design?utm_source=linkedin&utm_medium=social&utm_campaign=canva-tech-stack_mar+2026


# ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
# CONTENT BRIEF — Format B: Single Image
# ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

## Title
**Main title:** How Canva Is Actually Built
**Subtitle:** The tech stack behind 265M monthly users

## Content Sections

Structure: Canva UI screenshot as the base, with tech logos/labels overlaid and arrows pointing to the UI regions they power. Similar approach to the Figma breakdown, but using Canva's design language.

### Section 1: Editor Architecture (Center)
**Content:**
- React + TypeScript powers the entire editor UI
- MobX for state management with a custom "Store-Presenter-Component" pattern (modified MVP)
- WebGL used for specific image processing operations (alpha blending, filters) — not a separate rendering engine
- Migrated from vanilla JS to React + TypeScript as the team scaled

**Visual direction:**
- Layout: React + TypeScript + MobX logos placed in the center editor area of the Canva screenshot
- Key elements: Arrow pointing to the editor with label "React + TypeScript + MobX (Store-Presenter-Component)"
- Style notes: This is the hero section. MobX choice is the surprising element. Canva purple accent.

### Section 2: Image Processing
**Content:**
- WebGL for GPU-accelerated operations: alpha blending, image filters, compositing
- Not a full rendering engine like Figma's WebAssembly approach — used for specific heavy computations
- Enables real-time filter previews and image manipulation at scale

**Visual direction:**
- Layout: WebGL logo near the image editing / filter area of the Canva screenshot
- Key elements: Label "WebGL — GPU Image Processing" pointing to filter/effects area
- Style notes: Smaller than Section 1. Make clear this is targeted WebGL usage, not a full rendering engine.

### Section 3: Build System & Monorepo
**Content:**
- Bazel — handles the build for a monorepo with 500K+ files
- ~60 million lines of code
- Thousands of PRs merged per week
- Chose Bazel over Turborepo/Nx for scale

**Visual direction:**
- Layout: Bottom section or separate zone below the screenshot. Bazel logo with key stats.
- Key elements: Stats callout: "60M LOC | 500K+ files | Bazel"
- Style notes: Clean, minimal stat display. This section is about scale, so the numbers should be large and prominent.

### Section 4: Backend & Infrastructure
**Content:**
- Java + Kotlin — microservices on Spring Boot
- MongoDB + Redis — data storage and caching
- AWS (EC2, S3, CloudFront) — cloud infrastructure and CDN
- Python — ML models (Magic Eraser, background removal, text suggestions)

**Visual direction:**
- Layout: Right side or bottom row, listing backend technologies with logos and one-line descriptions
- Key elements: Tech logos in a grid or row. Tags: [Backend], [Database], [Cloud], [ML]
- Style notes: More compact than the frontend sections. Backend is context, not the headline.

### Footer Zone
**Content:** "Canva looks simple on the surface. Under the hood, it's a 60M-line monorepo, MobX with a custom architecture pattern, and WebGL for image processing."
**Visual direction:**
- Layout: Full-width footer bar below the main content
- Key elements: GFE logo left, takeaway text centered, "greatfrontend.com" right. CTA: "Practice front-end system design > greatfrontend.com"
- Style notes: Slightly lighter bg than the main content. GFE branding consistent with standard footer.


# ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
# SOURCES
# ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

## Sources
- Canva's WebGL alpha blending (image processing, not rendering engine) — https://www.canva.dev/blog/engineering/alpha-blending-and-webgl/
- 500K+ file monorepo with Bazel — https://www.canva.dev/blog/engineering/we-put-half-a-million-files-in-one-git-repository-heres-what-we-learned/
- React + TypeScript + MobX "Store-Presenter-Component" pattern — https://gitnation.com/contents/canvas-app-ui-kit-empowering-developers-with-modern-web-technologies
- Frontend development at Canva — https://www.canva.com/careers/frontend-development/
- Canva's tech stack overview — https://stackshare.io/canva/canva
- Multi-language engineering strategy — https://www.canva.dev/blog/engineering/why-well-always-be-exploring-new-programming-languages-at-canva/

**Planned first comment:** "If you liked this breakdown, check out the Figma tech stack comparison — Figma took a completely different approach with C++ compiled to WebAssembly for their rendering engine, while Canva uses React + TypeScript for the editor with targeted WebGL for image processing. GFE has system design interview questions if you want to practice architecting apps like these: https://www.greatfrontend.com/system-design"
