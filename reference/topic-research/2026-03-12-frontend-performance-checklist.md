# Research Notes: Frontend Performance Checklist (Used in Production)
**Publish date:** TBD
**Researched:** 2026-02-25

## Manager Requirements
From parent task description:
- Present a frontend performance guide combining foundational techniques, optimizations, and image strategies
- Cover all strategies that directly impact UX, engagement, and conversion
- CTA: Performance tips series at https://www.greatfrontend.com/blog/series/performance-tips

**Sanity-check notes:**
- CTA URL verified live. Series contains 3 articles: "Core Web Vitals Metrics in 5 Minutes," "Front End Performance Techniques," and "Image Performance Techniques."
- Post should align with but NOT duplicate GFE's existing content. GFE covers fundamentals; this post should go deeper on production realities and non-obvious insights.

---

## 1. PRIMARY RESEARCH: Production Performance Techniques

### A. Loading Performance

| Technique | What It Does | Production Impact | Source |
|---|---|---|---|
| Code splitting (route-based) | Breaks JS bundle into per-route chunks loaded on demand | Reduces initial load by 30-60%. Pinterest cut JS from 2.5MB to <200KB, TTI from 23s to 5.6s | [Smashing Magazine](https://www.smashingmagazine.com/2022/02/javascript-bundle-performance-code-splitting/), [Addy Osmani](https://addyosmani.com/blog/performance-budgets/) |
| Tree shaking | Eliminates dead/unused code from bundles at build time | Bundled packages often contain large swaths of unused third-party code | [Calibre](https://calibreapp.com/blog/bundle-size-optimization) |
| `fetchpriority="high"` on LCP element | Tells browser to prioritize the LCP resource over competing downloads | Google's tests: LCP improved from 2.6s to 1.9s (27% improvement). Some sites saw 20-30% gains | [web.dev](https://web.dev/articles/fetch-priority), [Addy Osmani](https://addyosmani.com/blog/fetch-priority/) |
| Preload (`<link rel="preload">`) | Tells browser to fetch a critical resource early, before the parser discovers it | Required for LCP images that are CSS backgrounds. Combine with fetchpriority for max effect | [web.dev](https://web.dev/articles/optimize-lcp), [Chrome Developers](https://developer.chrome.com/docs/performance/insights/lcp-discovery) |
| Prefetch (`<link rel="prefetch">`) | Low-priority fetch of resources likely needed for future navigations | Warms cache for subsequent page loads without competing with current-page resources | [MDN](https://developer.mozilla.org/en-US/docs/Web/Performance/Guides/Speculative_loading) |
| Speculation Rules API | JSON-based rules for prefetching/prerendering future navigations | Enables near-instant page transitions in Chromium browsers. Chrome caches prefetched pages for 5 min. Already in production at WordPress and Cloudflare scale | [MDN](https://developer.mozilla.org/en-US/docs/Web/API/Speculation_Rules_API), [Chrome Developers](https://developer.chrome.com/docs/web-platform/prerender-pages), [DebugBear](https://www.debugbear.com/blog/speculation-rules) |
| Lazy loading (below-the-fold only) | Defers loading of offscreen resources until user scrolls near them | Reduces initial page weight by 30-50%, but ONLY for below-the-fold content | [web.dev](https://web.dev/articles/lcp-lazy-loading) |

### B. Image Optimization

| Technique | What It Does | Production Impact | Source |
|---|---|---|---|
| AVIF format | Next-gen image format with superior compression (AV1-based) | ~20-25% smaller than WebP, ~50% smaller than JPEG. Supports HDR and wide gamut. 93.8% browser support as of late 2025 | [Elementor](https://elementor.com/blog/webp-vs-avif/), [Crystallize](https://crystallize.com/blog/avif-vs-webp), [SpeedVitals](https://speedvitals.com/blog/webp-vs-avif/) |
| WebP format | Modern image format with good compression | ~30% smaller than JPEG. Faster decoding than AVIF (lower CPU). 95.29% browser support | [Crystallize](https://crystallize.com/blog/avif-vs-webp), [ShortPixel](https://shortpixel.com/blog/avif-vs-webp/) |
| Progressive format strategy | Serve AVIF > WebP > JPEG using `<picture>` element | Maximizes savings without breaking compatibility. Use `<picture>` with `<source>` elements | [Elementor](https://elementor.com/blog/webp-vs-avif/) |
| Responsive images (`srcset` + `sizes`) | Deliver appropriately sized images matching display dimensions | Prevents mobile devices from downloading desktop-sized images | [Talent500](https://talent500.com/blog/frontend-performance-checklist-2025/) |
| Image CDN delivery | Transform, optimize, and cache images at the edge | Automates format selection, resizing, and compression per-request | [GFE](https://www.greatfrontend.com/blog/front-end-performance-techniques) |
| Explicit width/height attributes | Reserves space for images before they load | Images without dimensions cause ~60% of all layout shifts | [web.dev](https://web.dev/articles/optimize-cls), [NitroPack](https://nitropack.io/blog/post/fix-cls) |

### C. Rendering Performance

| Technique | What It Does | Production Impact | Source |
|---|---|---|---|
| CSS `contain` property | Isolates DOM subtrees so changes don't trigger full-page recalculations | Browser can skip layout/paint for contained elements when siblings change | [LogRocket](https://blog.logrocket.com/using-css-contain-property-deep-dive/), [MDN](https://developer.mozilla.org/en-US/docs/Learn_web_development/Extensions/Performance/CSS) |
| `content-visibility: auto` | Skips rendering for offscreen content entirely | Can provide up to 7x rendering performance boost on initial load. Vercel uses this in production | [DEV.to](https://dev.to/mnathani/two-lines-of-css-that-boosts-7x-rendering-performance-4mjd), [cekrem.github.io](https://cekrem.github.io/posts/content-visibility-auto-performance/) |
| List virtualization (react-window) | Only renders visible items in long lists | Rule of thumb: consider windowing above 50-100 items, especially on mobile | [LogRocket](https://blog.logrocket.com/how-to-virtualize-large-lists-using-react-window/), [Steve Kinney](https://stevekinney.com/courses/react-performance/windowing-and-virtualization) |
| `will-change` CSS property | Hints to browser that an element will animate, promoting it to its own compositor layer | Isolates animated elements from triggering reflow on unrelated content. Overuse wastes GPU memory | [MDN](https://developer.mozilla.org/en-US/docs/Learn_web_development/Extensions/Performance/CSS) |
| Minimizing reflows | Batch DOM reads/writes; avoid layout thrashing | Reflow recalculates position and size of elements -- one of the most expensive browser operations | [Medium](https://medium.com/@weijunext/performance-optimization-thoroughly-understanding-and-deconstructing-reflow-repaint-and-d5d9118f2cdf) |
| `content-visibility` vs. virtualization tradeoff | `content-visibility` loads all data but skips rendering; virtualization loads only visible data | `content-visibility` is simpler but causes continuous paint on scroll. Virtualization is better for truly massive lists (1000+ items) | [DEV.to (Sebastien Lorber)](https://dev.to/sebastienlorber/css-content-visibility-for-react-devs-4a3i) |

### D. Core Web Vitals Optimization

#### LCP (Largest Contentful Paint) -- Target: < 2.5s

| What Moves LCP | Details | Source |
|---|---|---|
| Eliminate resource load delay | The majority of origins with poor LCP spend <10% of p75 LCP time downloading the LCP image. The real issue is DISCOVERY delay -- the browser doesn't find the image early enough | [sia.codes](https://sia.codes/posts/web-perf-tips-2025/), [web.dev](https://web.dev/articles/optimize-lcp) |
| `fetchpriority="high"` on LCP image | Signals priority to browser. Do NOT set it on more than 1-2 images (creates bandwidth competition) | [DebugBear](https://www.debugbear.com/blog/avoid-overusing-fetchpriority-high), [web.dev](https://web.dev/articles/fetch-priority) |
| Never lazy-load LCP image | Lazy-loaded pages have median p75 LCP of 3,546ms vs 2,922ms for non-lazy-loaded pages | [web.dev](https://web.dev/articles/lcp-lazy-loading), [GTmetrix](https://gtmetrix.com/dont-lazy-load-lcp-image.html) |
| Preload for CSS background images | Preload is required when LCP is a CSS background-image (parser can't discover it from HTML alone) | [web.dev](https://web.dev/articles/optimize-lcp) |
| Inline critical CSS | Extract above-the-fold CSS into `<head>` to eliminate render-blocking stylesheet fetch | [Strapi](https://strapi.io/blog/frontend-performance-checklist) |
| SSR/SSG for initial HTML | Server-render critical content so browser doesn't wait for JS to execute before painting | [Talent500](https://talent500.com/blog/frontend-performance-checklist-2025/) |

#### INP (Interaction to Next Paint) -- Target: < 200ms (replaced FID in March 2024)

| What Moves INP | Details | Source |
|---|---|---|
| Break up long tasks | INP = Input Delay + Processing Time + Presentation Delay. Long main-thread tasks block all three phases | [web.dev](https://web.dev/articles/inp), [DebugBear](https://www.debugbear.com/docs/metrics/interaction-to-next-paint) |
| Yield to main thread | Use `scheduler.yield()` or `setTimeout` to break JS execution and let the browser paint between chunks | [NitroPack](https://nitropack.io/blog/improve-interaction-to-next-paint-inp/) |
| Reduce third-party script main thread time | Third-party scripts (analytics, ads, chat) can block main thread for 500-1500ms+ | [DebugBear](https://www.debugbear.com/blog/reduce-the-impact-of-third-party-code) |
| Minimize DOM size | Large DOM trees make style recalculations and layout more expensive after every interaction | [NitroPack](https://nitropack.io/blog/improve-interaction-to-next-paint-inp/) |
| Field measurement is essential | INP can only be meaningfully measured with real users (RUM), not lab tools. Lab tools test single interactions; INP captures the worst across the entire session | [web.dev](https://web.dev/articles/inp), [Catchpoint](https://www.catchpoint.com/core-web-vitals/interaction-to-next-paint) |

#### CLS (Cumulative Layout Shift) -- Target: < 0.1

| What Moves CLS | Details | Source |
|---|---|---|
| Set explicit dimensions on images/video | Images without dimensions cause ~60% of layout shifts | [web.dev](https://web.dev/articles/optimize-cls), [NitroPack](https://nitropack.io/blog/post/fix-cls) |
| Use CSS `aspect-ratio` | Modern alternative to padding-bottom hack for reserving space | [web.dev](https://web.dev/articles/optimize-cls) |
| Font loading strategy | Web fonts cause ~25% of layout shifts. Use `font-display: optional` or `swap` with `size-adjust`, `ascent-override`, `descent-override` to match fallback metrics. Can reduce CLS by up to 70% | [DebugBear](https://www.debugbear.com/docs/fix-cls-issues), [Natclark](https://natclark.com/how-to-fix-cumulative-layout-shift-cls-in-2025/) |
| Reserve space for ads/embeds | Use placeholder containers with fixed dimensions for dynamically injected content | [web.dev](https://web.dev/articles/optimize-cls), [Aditude](https://www.aditude.com/blog/what-is-cls) |
| Avoid inserting content above existing content | Any DOM insertion that pushes visible elements down causes shift | [DebugBear](https://www.debugbear.com/docs/fix-cls-issues) |

### E. Network Optimization

| Technique | What It Does | Production Impact | Source |
|---|---|---|---|
| Brotli compression | Successor to gzip; supported by all major browsers | Level 4-5 recommended: smaller than max gzip without significant CPU overhead. Better than gzip for text assets | [Nooshu](https://nooshu.com/blog/2025/01/05/cranking-brotli-up-to-11-with-cloudflare-pro-and-11ty/), [Kong](https://docs.konghq.com/gateway/latest/production/performance/brotli/) |
| HTTP/2 multiplexing | Multiple requests over a single TCP connection | Eliminates head-of-line blocking at the HTTP level. Free via Cloudflare | [Pixel Free Studio](https://blog.pixelfreestudio.com/the-role-of-http-2-in-web-performance-optimization/) |
| HTTP/3 + QUIC | UDP-based transport; eliminates TCP head-of-line blocking | Faster connection setup, improved reliability on lossy networks (mobile) | [Cloudflare](https://developers.cloudflare.com/speed/optimization/content/compression/) |
| Service worker caching | Network proxy that intercepts requests and serves from cache | Can reduce repeat page loads to milliseconds. Enables offline-first patterns | [Crystallize](https://crystallize.com/blog/frontend-performance-checklist) |
| CDN for static assets | Serve assets from edge locations geographically close to users | Reduces TTFB. Standard practice at scale | General best practice |
| Cache-Control headers | `immutable` for hashed assets; `stale-while-revalidate` for dynamic content | Prevents unnecessary revalidation requests for content that hasn't changed | General best practice |

### F. JavaScript Optimization

| Technique | What It Does | Production Impact | Source |
|---|---|---|---|
| Performance budgets | Set max bundle sizes and fail CI if exceeded | Pinterest: <200KB JS budget led to TTI 23s -> 5.6s, revenue +44%, sign-ups +753% | [Addy Osmani](https://addyosmani.com/blog/performance-budgets/) |
| `async` vs `defer` scripts | `async`: download + execute ASAP (no order guarantee). `defer`: download async, execute in order after HTML parse | `defer` for most scripts; `async` for independent analytics scripts | [Strapi](https://strapi.io/blog/frontend-performance-checklist) |
| Replace heavy libraries | Swap Moment.js -> Day.js, Lodash -> native methods or lodash-es with tree shaking | Can remove 50-200KB from bundle with zero functionality loss | [Crystallize](https://crystallize.com/blog/frontend-performance-checklist) |
| Third-party script audit | Categorize scripts as essential/non-essential. Use Chrome Coverage tab to find unused code | Third-party scripts often contribute more performance overhead than all images combined | [DebugBear](https://www.debugbear.com/blog/reduce-the-impact-of-third-party-code), [SpeedCurve](https://www.speedcurve.com/web-performance-guide/third-party-web-performance/) |
| Partytown (web workers) | Moves third-party scripts off main thread into web workers | Eliminates main thread blocking from analytics/ads without removing them | [DebugBear](https://www.debugbear.com/blog/partytown-web-workers) |
| Dynamic `import()` | Load components/routes only when needed | Foundation of route-based code splitting in React, Next.js, etc. | [Smashing Magazine](https://www.smashingmagazine.com/2022/02/javascript-bundle-performance-code-splitting/) |

---

## 2. CONTENT LANDSCAPE RESEARCH

### Saturated Angles (What Everyone Covers)
Based on analysis of 10+ recent checklist articles from DEV.to, Medium, Strapi, Crystallize, Talent500, and FreeCodeCamp:

1. **Generic "top 10 performance tips" listicles** -- Every platform has multiple versions. Shallow coverage of the same techniques (lazy loading, code splitting, image optimization) without production context.
2. **Core Web Vitals explainers** -- Basic "what is LCP/CLS/FID" articles are everywhere. Most still mention FID rather than INP.
3. **Image format comparisons** -- WebP vs JPEG is heavily covered. AVIF comparisons are catching up.
4. **Lighthouse score optimization** -- Many articles frame performance as "get a high Lighthouse score" rather than real user experience.

### Content Sources Analyzed

| Platform | Content Type | Observation |
|---|---|---|
| DEV.to | Multiple "ultimate checklist" posts | Heavy on theory, light on production data. Most are variations of the same list. Few mention INP or Speculation Rules API | Sources: [DEV.to (tahamjp)](https://dev.to/tahamjp/frontend-performance-in-2025-the-ultimate-checklist-49f2), [DEV.to (hamzakhan)](https://dev.to/hamzakhan/front-end-performance-optimization-tips-for-2025-boost-your-web-apps-speed-1gbg), [DEV.to (jacobandrewsky)](https://dev.to/jacobandrewsky/frontend-web-performance-checklist-2o9j) |
| Medium | Senior developer guides | More depth, but often framework-specific (Next.js/React). Better on measurement strategy | Source: [Medium (ndmangrule)](https://medium.com/@ndmangrule/frontend-performance-optimization-a-guide-for-senior-frontend-developers-part-ii-aeef3f1d9224) |
| Crystallize | Comprehensive 2025 checklist | Best of the bunch -- covers HTML, CSS, JS, images, video, fonts, hosting. Still lacks "gotchas" layer | Source: [Crystallize](https://crystallize.com/blog/frontend-performance-checklist) |
| Strapi | Speed-focused checklist | Good structure but basic. No production case studies | Source: [Strapi](https://strapi.io/blog/frontend-performance-checklist) |
| LinkedIn | "Website Performance Checklist" post | Generic, no depth | Source: [LinkedIn (Prasanna Jathan)](https://www.linkedin.com/pulse/website-performance-checklist-front-end-prasanna-jathan) |
| GitHub | Front-End-Performance-Checklist repo (thedaviddias) | Comprehensive but aging. Community-maintained | Source: [GitHub](https://github.com/thedaviddias/Front-End-Performance-Checklist) |
| Smashing Magazine | 2021 checklist (PDF) | Historically the gold standard but showing its age. Doesn't cover INP, Speculation Rules, AVIF adoption, content-visibility | Source: [Smashing Magazine](https://www.smashingmagazine.com/2021/01/front-end-performance-2021-free-pdf-checklist/) |

### Gaps / Differentiation Opportunities

1. **"What you THINK you know vs. what actually matters"** -- Almost no existing content explicitly addresses common performance misconceptions in a structured way.
2. **INP optimization** -- Most checklists still mention FID. INP replaced it in March 2024 but content hasn't caught up.
3. **Speculation Rules API** -- Virtually absent from checklist-format content. This is a real production tool (WordPress, Cloudflare) that most devs haven't heard of.
4. **The "third-party scripts are the real problem" angle** -- Most checklists bury third-party scripts as one item among 20. In reality, they're often the single largest performance bottleneck.
5. **`content-visibility: auto`** -- Rarely mentioned in checklists despite Vercel using it in production and it providing up to 7x rendering gains.
6. **Performance budgets in CI/CD** -- Most articles mention budgets conceptually but don't show how to enforce them in a pipeline.
7. **The LCP discovery problem** -- Most content says "optimize your images" but the real LCP issue is often that the browser doesn't discover the LCP resource early enough, not that the image is too large.

---

## 3. GFE PERFORMANCE TIPS PAGE ANALYSIS

**URL:** https://www.greatfrontend.com/blog/series/performance-tips
**Series title:** "Performance tips for building blazing fast front end websites"
**Level:** Intermediate
**Category:** Real world front end

### Articles in Series (3 total)

| # | Title | Level | Published | Key Topics |
|---|---|---|---|---|
| 1 | Core Web Vitals Metrics in 5 Minutes | Starter | Feb 16, 2024 | LCP, FID (pre-INP replacement), CLS definitions and thresholds |
| 2 | Front End Performance Techniques | Starter | Mar 26, 2024 | List virtualization, bundle/code splitting, dynamic imports, lazy loading, optimize loading sequence, prefetching, preloading, compression, tree shaking |
| 3 | Image Performance Techniques | Starter | Jun 3, 2024 | CDN, WebP/AVIF formats, responsive images, adaptive images, offscreen image deferral, lazy loading, progressive JPEGs, preloading images, compression |

### Alignment Strategy
- GFE covers the **foundational techniques** at a starter level. The checklist post should build ON TOP of these, adding the "used in production" and "what most devs get wrong" layers.
- GFE still references FID (pre-March 2024 replacement). The checklist post should use INP throughout.
- GFE's content is clean and educational. The checklist post can be more opinionated and production-focused without conflicting.
- CTA should frame GFE series as "dive deeper into the fundamentals" after the checklist gives the high-level view.

---

## 4. INSIGHT MINING: What Devs Get Wrong

### Misconception 1: "Just lazy load everything"
**Reality:** Lazy loading above-the-fold images HURTS LCP. Median p75 LCP is 3,546ms for pages with lazy loading vs 2,922ms without. The LCP image should use `fetchpriority="high"` and `loading="eager"` (or simply omit the loading attribute).
- Source: [web.dev](https://web.dev/articles/lcp-lazy-loading), [Google warning](https://www.stanventures.com/news/google-warns-lazy-loading-above-the-fold-images-can-hurt-lcp-4118/)

### Misconception 2: "Focus on image file size to fix LCP"
**Reality:** The majority of origins with poor LCP spend less than 10% of their p75 LCP time downloading the LCP image. The real bottleneck is usually resource discovery delay (browser doesn't know about the image early enough) or render-blocking resources.
- Source: [sia.codes](https://sia.codes/posts/web-perf-tips-2025/), [web.dev](https://web.dev/articles/optimize-lcp)

### Misconception 3: "Minimize bundle size" (but ignore third-party scripts)
**Reality:** Third-party scripts (analytics, ads, chat widgets, social embeds) often contribute more performance overhead than all images combined. One case study showed third-party scripts increasing LCP from <1s to 26.82s. Your own code might be well-optimized while third parties destroy the experience.
- Source: [DebugBear](https://www.debugbear.com/blog/reduce-the-impact-of-third-party-code), [SpeedCurve](https://www.speedcurve.com/web-performance-guide/third-party-web-performance/)

### Misconception 4: "Use WebP for everything"
**Reality:** AVIF is 20-25% smaller than WebP with better quality, supports HDR and wide gamut, and has 93.8% browser support (vs WebP's 95.29%). The gap is closing fast. Production strategy should be AVIF-first with WebP fallback. However, AVIF has higher decode CPU cost -- WebP may actually load faster on low-end devices despite being larger.
- Source: [Elementor](https://elementor.com/blog/webp-vs-avif/), [SpeedVitals](https://speedvitals.com/blog/webp-vs-avif/)

### Misconception 5: "Lighthouse score = real performance"
**Reality:** Lighthouse is a lab tool that tests a single synthetic visit. Real users have diverse devices, networks, and interaction patterns. INP (the responsiveness metric) can ONLY be meaningfully measured with real users -- lab tools test single interactions while INP captures the worst across the full session. Start with RUM (Real User Monitoring) data, not Lighthouse.
- Source: [sia.codes](https://sia.codes/posts/web-perf-tips-2025/), [web.dev](https://web.dev/articles/inp)

### Misconception 6: "Performance optimization = writing better code"
**Reality:** Architecture choices (framework selection, rendering strategy, build tooling) have 10x more impact than code-level micro-optimizations. A CrUX analysis of different tech stacks shows dramatic performance differences before any custom optimization. Headless ecommerce doesn't guarantee better performance than traditional solutions.
- Source: [sia.codes](https://sia.codes/posts/web-perf-tips-2025/)

### Misconception 7: "Set fetchpriority=high on all important images"
**Reality:** Setting fetchpriority="high" on more than 1-2 images makes priority setting unhelpful. It creates bandwidth competition between resources that are all marked as important, negating the benefit.
- Source: [DebugBear](https://www.debugbear.com/blog/avoid-overusing-fetchpriority-high)

### Misconception 8: "Aggressive image compression = better performance"
**Reality:** Over-compressing images can reduce e-commerce conversion rates. Product image quality directly impacts purchase decisions. The goal is optimal compression, not maximum compression.
- Source: [sia.codes](https://sia.codes/posts/web-perf-tips-2025/)

---

## 5. BUSINESS IMPACT DATA

| Metric | Data Point | Source |
|---|---|---|
| Speed vs. conversion | 1-second delay reduces conversions by 7% | [Cloudflare](https://www.cloudflare.com/learning/performance/more/website-performance-conversion-rates/) |
| Speed vs. conversion (B2B) | Site loading in 1s converts 3x higher than 5s, 5x higher than 10s | [Cloudflare](https://www.cloudflare.com/learning/performance/more/website-performance-conversion-rates/) |
| Mobile abandonment | 50%+ mobile users abandon if site takes >3 seconds to load | [Talent500](https://talent500.com/blog/frontend-performance-checklist-2025/) |
| Mobile speed gap | Pages load 70.9% slower on mobile than desktop | [HubSpot](https://blog.hubspot.com/marketing/page-load-time-conversion-rates) |
| Pinterest case study | JS <200KB budget: TTI 23s -> 5.6s, revenue +44%, sign-ups +753%, weekly active mobile users +103% | [Addy Osmani](https://addyosmani.com/blog/performance-budgets/) |
| Revenue impact | $10M/year site + 2s faster + 4% conversion lift = $400K/year additional revenue | [Cloudflare](https://www.cloudflare.com/learning/performance/more/website-performance-conversion-rates/) |
| Google ranking | 2025-2026 updates increased weight of page experience signals. Equal content relevance = better CWV wins | [OWDT](https://owdt.com/insight/how-to-improve-core-web-vitals/), [Raga Advertisers](https://ragaadvertisers.com/how-to-improve-core-web-vitals-in-2026-for-better-rankings-ux/) |

---

## 6. RECOMMENDED POST STRUCTURE

Based on landscape gaps, the post should differentiate by:

1. **Lead with the "what you get wrong" angle** -- Hook readers by challenging assumptions, not repeating the same tips they've seen 50 times.
2. **Organize by Core Web Vital**, not by technique type -- Most devs care about "how do I fix my LCP score" not "tell me about preloading." Map every technique to the metric it impacts.
3. **Include the non-obvious layer** for each technique -- Not just "use lazy loading" but "use lazy loading... except for your LCP image, where it actively hurts you."
4. **Mention production proof points** -- Pinterest, Vercel, WordPress, Cloudflare. Real companies, real results.
5. **Cover the newer techniques** that competitors miss -- Speculation Rules API, `content-visibility: auto`, INP (not FID), font metric overrides for CLS, Partytown for third-party scripts.

---

## 7. GFE CTA

- **URL:** https://www.greatfrontend.com/blog/series/performance-tips
- **Page verified live.** Contains 3 articles covering Core Web Vitals basics, front-end performance techniques, and image performance techniques.
- **CTA angle:** "Want to go deeper on each technique? Check out our Performance Tips series for step-by-step guides on implementation."
- **Alignment:** Post gives the checklist/overview; GFE series provides the deep-dive tutorials.

---

## 8. KEY TOOLS MENTIONED ACROSS RESEARCH

| Tool | Use Case | Source |
|---|---|---|
| Chrome DevTools Performance panel | Trace main thread activity, identify long tasks | [sia.codes](https://sia.codes/posts/web-perf-tips-2025/) |
| Chrome DevTools Coverage tab | Find unused CSS/JS | [DebugBear](https://www.debugbear.com/blog/reduce-the-impact-of-third-party-code) |
| Lighthouse (lab) | Synthetic performance audit | [sia.codes](https://sia.codes/posts/web-perf-tips-2025/) |
| CrUX (field) | Real user metrics from Chrome users | [sia.codes](https://sia.codes/posts/web-perf-tips-2025/) |
| WebPageTest | Advanced waterfall analysis and filmstrip comparison | [Talent500](https://talent500.com/blog/frontend-performance-checklist-2025/) |
| @next/bundle-analyzer | Visualize Next.js bundle composition | [Pagepro](https://pagepro.co/blog/nextjs-performance-optimization-in-9-steps/) |
| Partytown | Move third-party scripts to web workers | [DebugBear](https://www.debugbear.com/blog/partytown-web-workers) |
| Google Search Console | CWV field data for your site | [Google](https://developers.google.com/search/docs/appearance/core-web-vitals) |
