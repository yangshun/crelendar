# Research Notes: Canva Tech Stack Breakdown
**Date:** 2026-03-03 (publish date)
**Researched:** 2026-02-25

## Decision: Canva over Framer
Canva wins on all 5 engagement factors: brand recognition (265M MAU vs niche), tech stack novelty (MobX + Bazel + monorepo at scale vs standard React), debate potential (MobX/Bazel/monorepo controversies), relatability (migration stories, state management debates), and content gap (no definitive breakdown exists).

## Key Tech Stack Facts

| Technology | Role | Source |
|---|---|---|
| React + TypeScript | UI framework for editor chrome (toolbars, panels, menus) | [Canva Careers](https://www.canva.com/careers/frontend-development/), [GitNation Talk](https://gitnation.com/contents/canvas-app-ui-kit-empowering-developers-with-modern-web-technologies) |
| MobX | State management via custom "Store-Presenter-Component" pattern (modified MVP) | [GitNation Talk](https://gitnation.com/contents/canvas-app-ui-kit-empowering-developers-with-modern-web-technologies) |
| WebGL (for image processing) | Used for specific operations like alpha blending - NOT the entire rendering engine. Canva's editor still uses the DOM. | [Canva Engineering Blog](https://www.canva.dev/blog/engineering/alpha-blending-and-webgl/) |
| Bazel | Build system for the monorepo | [Canva Engineering Blog](https://www.canva.dev/blog/engineering/we-put-half-a-million-files-in-one-git-repository-heres-what-we-learned/) |
| Monorepo | ~60M lines of code, 500K+ files, thousands of PRs/week | [Canva Engineering Blog](https://www.canva.dev/blog/engineering/we-put-half-a-million-files-in-one-git-repository-heres-what-we-learned/) |
| Java + Kotlin | Backend microservices | [StackShare](https://stackshare.io/canva/canva) |
| Spring Boot | Backend framework | [StackShare](https://stackshare.io/canva/canva) |
| MongoDB + Redis | Databases and caching | [Quora](https://www.quora.com/What-is-the-technology-stack-behind-Canva) |
| AWS (EC2, S3, CloudFront) | Cloud infrastructure and CDN | [StackShare](https://stackshare.io/canva/canva) |
| Python | Machine learning models (Magic Eraser, background removal) | [Canva Engineering Blog](https://www.canva.dev/blog/engineering/why-well-always-be-exploring-new-programming-languages-at-canva/) |

## Insight Map

**What audience already knows (surface):**
- Canva is a popular design tool
- It's web-based and has a drag-and-drop interface
- It's used by non-designers for social media graphics, presentations, etc.

**What would be new/surprising (insights):**
1. MobX over Redux/Zustand - controversial choice, uses a custom "Store-Presenter-Component" pattern
2. 60M lines of code in a single monorepo with 500K+ files, built with Bazel
3. The entire editor UI is React + TypeScript - toolbars, panels, and the design surface
4. WebGL used for specific image processing (alpha blending, filters) - not a full rendering engine
5. Migrated from vanilla JS to React + TypeScript ("Canva 2.0") as team scaled

**Debate hooks:**
- MobX in 2026? Most teams have moved to Zustand or Jotai
- Bazel for frontend? Most companies use Turborepo or Nx
- 60M LOC monorepo - is this good engineering or tech debt?
- React + TypeScript for a design tool at this scale - right call?

## Prior Art in Repo
- Netflix: single image, dark theme, ~15 technologies across 6 categories
- Shopify: single image, ~13 technologies, same template as Netflix
- Figma: animated GIF, mapping tech to UI regions with overlays
- No existing Canva or Framer posts

## GFE CTA
- Best URL: https://www.greatfrontend.com/system-design
- Relevant questions: Diagram Tool (Lucidchart), Google Docs (collaborative editor), Pinterest
- CTA angle: "Want to architect apps like this?" - system design course with RADIO framework
