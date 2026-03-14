# HEARTBEAT.md — Performance Optimizer

## Iron Law
**MEASURE BEFORE AND AFTER.** No optimization without baseline. No "done" without improved numbers.

## Core Web Vitals (MANDATORY)

| Metric | Good | Poor |
|--------|------|------|
| LCP | ≤ 2.5s | > 4.0s |
| INP | ≤ 200ms | > 500ms |
| CLS | ≤ 0.1 | > 0.25 |
| FCP | ≤ 1.8s | > 3.0s |
| TTFB | ≤ 800ms | > 1.8s |

## Bundle Targets
- Total JS ≤ 200KB gzipped · Largest chunk ≤ 100KB · No single dep > 50KB (unless justified)
- `npx next build && npx @next/bundle-analyzer` · `npx depcheck` for unused deps

## React Performance
- [ ] `Promise.all()` for parallel fetches (no waterfalls)
- [ ] No inline objects/functions in JSX props
- [ ] Heavy components: `next/dynamic` · Non-interactive: Server Components
- [ ] Images: `next/image` with `width`/`height` · Fonts: `next/font`
- [ ] Derived state during render, not `useEffect`

## Resource Optimization
- [ ] Brotli/Gzip · CDN for static · Immutable cache headers for hashed assets
- [ ] No unused CSS · Code splitting per route · Third-party scripts `afterInteractive`

## 🔴 Red Flags (STOP)
- Bundle > 500KB → CRITICAL · LCP > 4s → Google penalizes
- CLS > 0.25 → layout jumps · No `loading.tsx` on data routes → fix immediately

## Rules
- Measure first, optimize second · Only optimize what's measured slow
- Deliver PERFORMANCE_REPORT.md with before/after numbers
