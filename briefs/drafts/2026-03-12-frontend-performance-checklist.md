# ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
# BRIEF INFO
# ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

# The Frontend Performance Checklist Used in Production

- **Date:** 2026-03-12
- **Topic:** Frontend performance optimization checklist — foundational techniques, image strategies, and rendering optimizations used at scale
- **Pillar:** 🔍 Deep Dive / Technical Education
- **Format:** Single Image (Static Infographic)
- **Format rationale:** A checklist is a single visual artifact — all items visible at once, scannable, and screenshot-worthy. Single image is the highest-save format for checklists/cheatsheets (top performers: Git Skills, localStorage, Hoisting). The last 5 posts were all carousels — this breaks the streak and matches the content shape perfectly. A carousel would force splitting a unified checklist into disconnected slides, losing the "at-a-glance" reference value.
- **Key angle:** Not another generic "optimize your images" list. This checklist focuses on the techniques that actually move metrics in production — including the gotchas most devs get wrong (lazy loading LCP images, fetchpriority overuse, ignoring third-party scripts).
- **GFE tie-in:** Footer zone + caption link to GFE Performance Tips series (interview-relevant techniques).
- **Design inspiration:** ByteByteGo system design style — structured grid layout with icons, category headers, and clear hierarchy
- **Color theme:** Dark (navy/black bg)
- **Accent color:** Green (#4CAF50) for checkmarks/performance wins. Orange (#FF9800) for warning items. White text on dark bg.


# ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
# CAPTION
# ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

## LinkedIn Caption
Lazy loading your hero image? You're making LCP worse.

This is the frontend performance checklist we actually use in production — the techniques that move Core Web Vitals, not the ones that just sound good in blog posts.

Most "performance tips" articles tell you to lazy load everything and use WebP. That's 2020 advice. The real gains come from fetchpriority on your LCP element, AVIF-first image stacks, content-visibility for offscreen rendering, and auditing your third-party scripts (which often outweigh all your images combined).

Save this. Screenshot it. Use it in your next performance audit.

#FrontEnd #WebPerformance #CoreWebVitals #JavaScript #WebDevelopment #GreatFrontEnd

These techniques come up in front-end performance interviews. Detailed breakdowns and practice: https://www.greatfrontend.com/blog/series/performance-tips?utm_source=linkedin&utm_medium=social&utm_campaign=perf-checklist_mar+2026


# ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
# CONTENT BRIEF — Format B: Single Image (Static Infographic)
# ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

## Title
**Main title:** The Frontend Performance Checklist
**Subtitle:** Techniques that actually move metrics in production

## Content Sections

### Section 1: Loading
**Content:**
- ✅ Code-split by route (Pinterest: 2.5MB → <200KB, TTI 23s → 5.6s)
- ✅ Set `fetchpriority="high"` on LCP element (up to 27% LCP improvement in Google's tests)
- ✅ Preload LCP images hidden in CSS backgrounds
- ⚠️ Lazy load below-the-fold ONLY — lazy loading LCP images makes it worse
**Visual direction:**
- Layout: Category header "Loading" with download/speed icon. 4 items as compact checklist rows.
- Key elements: Green checkmarks for do-this items. Orange warning triangle for the lazy loading gotcha.
- Style notes: The lazy loading warning is the engagement hook — highlight it visually.

### Section 2: Images
**Content:**
- ✅ AVIF first, WebP fallback, JPEG safety net via `<picture>`
- ✅ Always set explicit `width` and `height` (60% of CLS comes from missing dimensions)
- ✅ Use responsive images with `srcset` + `sizes`
- ⚠️ Don't over-compress — aggressive compression drops e-commerce conversion
**Visual direction:**
- Layout: Category header "Images" with image/photo icon. 4 items as checklist rows.
- Key elements: AVIF > WebP > JPEG visual chain or label. The CLS stat (60%) emphasized.
- Style notes: Keep the format stack visual simple — text labels, not logos.

### Section 3: Rendering
**Content:**
- ✅ Use `content-visibility: auto` for offscreen content (up to 7x rendering boost)
- ✅ Virtualize lists above 50-100 items (react-window / @tanstack/virtual)
- ✅ Use CSS `contain` to isolate layout recalculations
**Visual direction:**
- Layout: Category header "Rendering" with paint/render icon. 3 items as checklist rows.
- Key elements: "7x" stat highlighted for content-visibility.
- Style notes: Shorter section — 3 items to keep density balanced.

### Section 4: Core Web Vitals
**Content:**
- ✅ LCP: Fix resource discovery, not just image size (<10% of LCP time is image download)
- ✅ CLS: Set dimensions on all images and embeds, use `font-display: swap`
- ✅ INP: Measure in the field with RUM — Lighthouse can't catch INP issues
**Visual direction:**
- Layout: Category header "Core Web Vitals" with metrics/chart icon. 3 items mapped to LCP, CLS, INP.
- Key elements: LCP/CLS/INP labels as small badges. The "<10% is image download" stat is the surprise — emphasize it.
- Style notes: Each item tied to its specific metric.

### Section 5: Network & JS
**Content:**
- ✅ Use Brotli compression (level 4-5 beats max gzip with less CPU)
- ✅ Audit third-party scripts — they often outweigh all your images combined
- ✅ Enforce performance budgets in CI/CD (Pinterest: +44% revenue)
**Visual direction:**
- Layout: Category header "Network & JS" with network/code icon. 3 items as checklist rows.
- Key elements: Third-party scripts warning emphasized. Pinterest revenue stat highlighted.
- Style notes: The third-party scripts point is the insight most devs miss.

### Section 6: Footer / GFE CTA
**Content:**
- GFE logo + "Practice front-end performance questions" + greatfrontend.com
**Visual direction:**
- Layout: Thin footer zone below the checklist grid. GFE logo left, CTA text right.
- Key elements: GFE logo, performance tips link callout.
- Style notes: Subtle, not competing with content. Standard footer CTA treatment.

**Overall layout notes:**
- 6 sections arranged in a 2-column or single-column grid
- Each section has a colored header bar with icon + category name
- Checklist items use green ✅ for standard items, orange ⚠️ for gotcha/warning items
- Dark bg (navy/charcoal), green + orange accent colors, white text
- Total items: 17 checklist items across 5 content zones + 1 CTA zone
- Must be readable at mobile size — keep text concise, one line per item where possible


# ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
# SOURCES
# ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

## Sources
- Code splitting / Pinterest perf budget — https://addyosmani.com/blog/performance-budgets/, https://www.smashingmagazine.com/2022/02/javascript-bundle-performance-code-splitting/
- fetchpriority LCP improvement (27%) — https://web.dev/articles/fetch-priority, https://addyosmani.com/blog/fetch-priority/
- Lazy loading LCP harm — https://web.dev/articles/lcp-lazy-loading, https://gtmetrix.com/dont-lazy-load-lcp-image.html
- AVIF vs WebP compression and browser support — https://elementor.com/blog/webp-vs-avif/, https://crystallize.com/blog/avif-vs-webp
- CLS from missing image dimensions (60%) — https://web.dev/articles/optimize-cls, https://nitropack.io/blog/post/fix-cls
- content-visibility: auto (7x rendering) — https://dev.to/mnathani/two-lines-of-css-that-boosts-7x-rendering-performance-4mjd
- LCP resource discovery (<10% is image download) — https://web.dev/articles/optimize-lcp
- INP replacing FID, field measurement needed — https://web.dev/articles/inp
- Third-party script impact — https://www.debugbear.com/blog/reduce-the-impact-of-third-party-code, https://www.speedcurve.com/web-performance-guide/third-party-web-performance/
- Pinterest performance budget +44% revenue — https://addyosmani.com/blog/performance-budgets/
- Brotli compression — https://www.smashingmagazine.com/2022/07/brotli-compression-speed-up-website/
- GFE Performance Tips Series — https://www.greatfrontend.com/blog/series/performance-tips

**Planned first comment:** "The item most devs get wrong: lazy loading. If your LCP image is lazy-loaded, you're actively making your Largest Contentful Paint worse — the browser won't even start downloading it until JavaScript runs. Google's own tests show fetchpriority='high' on the LCP element gives up to 27% improvement instead. These techniques come up regularly in front-end performance interviews. GFE's Performance Tips series breaks each one down with code examples: https://www.greatfrontend.com/blog/series/performance-tips?utm_source=linkedin&utm_medium=social&utm_campaign=perf-checklist_mar+2026. Source: web.dev LCP optimization guide (web.dev/articles/optimize-lcp)."
