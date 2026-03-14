# HEARTBEAT.md — Frontend Builder

## 1. Identity + Setup
- `GET /api/agents/me`
- Read `../SHARED_CONFIG.md`, `../../SYSTEM_STATE.md`, `../../MEMORY.md`
- Read `docs/lib/` for latest library docs (Context7)
- Verify shadcn: `npx shadcn@latest info --json` (init if needed)

## 2. Component Development
1. Search: `npx shadcn@latest search` → add if found, build if not
2. Server Components by default · `"use client"` only for hooks/interactivity
3. Compound components > boolean props · Single responsibility
4. `lucide-react` icons · `framer-motion` animations · `sonner` toasts
5. No business logic in UI → extract to custom hooks

## 3. State & Data
```
Server → @tanstack/react-query · Client → zustand (persist + devtools)
URL → nuqs · Forms → react-hook-form + zod · HTTP → ky
```
- Immutability · Minimal state (derive, don't store) · No props drilling >3 levels

## 4. Performance (vercel-react-best-practices)
- [ ] `Promise.all()` for parallel fetches · Direct imports (no barrels)
- [ ] `next/dynamic` for heavy components · Server Components for static
- [ ] No inline objects/functions in JSX · `useCallback`/`useMemo` only when needed

## 5. Pre-Delivery
- [ ] Touch targets ≥44px · Contrast ≥4.5:1 · `prefers-reduced-motion`
- [ ] Keyboard navigation · Labels on all form fields · Loading states
- [ ] Tested mobile + tablet + desktop · SYSTEM_STATE.md updated
- Structured PR: What → Why → How → Screenshots

## Rules
- shadcn first, custom second · Never raw color values · TypeScript strict
- Zod at boundaries · SYSTEM_STATE.md always current · Latest package versions
