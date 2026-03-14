# Tools

## Runtime
- **OpenCode** is your runtime.

## Paperclip API
- `GET /api/agents/me` — identity.
- `GET /api/companies/{companyId}/issues?assigneeAgentId={agentId}&status=todo,in_progress,blocked` — inbox.
- `PATCH /api/issues/{issueId}` — status updates. Include `X-Paperclip-Run-Id`.

---

## Pre-Build
Check `docs/lib/` for latest library docs (Context7). Use those over training data.

## shadcn/ui CLI
```bash
npx shadcn@latest search                  # Search before building
npx shadcn@latest add button card dialog  # Add components
npx shadcn@latest docs <component>        # Usage examples
```
- Search before building custom · Compose: Sidebar + Card + Chart + Table
- Variants first: `variant="outline"`, `size="sm"` · Semantic colors: `bg-primary`, never `bg-blue-500`
- Icons: `lucide-react` only, no emojis

---

## Skills

### 1. React Performance — vercel-react-best-practices (197K)

**CRITICAL**: `Promise.all()` for independent ops · Direct imports (no barrel files) · `next/dynamic` for heavy components · `<Suspense>` for streaming

**HIGH**: `React.cache()` for dedup · Minimize client serialization · `after()` non-blocking

**MEDIUM**: Derive state during render (not effects) · `useRef` for transient values · `startTransition` for non-urgent

### 2. Impeccable Design — [pbakaus/impeccable](https://github.com/pbakaus/impeccable)

**Color — OKLCH (mandatory, not HSL)**
```css
--primary: oklch(60% 0.15 250);       /* Perceptually uniform */
--neutral-100: oklch(95% 0.01 60);    /* Tinted neutrals, NEVER pure gray */
/* 60-30-10: 60% neutral, 30% secondary, 10% accent */
```
- ❌ No `#000`/`#fff` · No gray on colored bg · No cyan-on-dark · No gradient text

**Typography — Fluid, Distinctive**
```css
--fs-sm: clamp(0.8rem, 0.17vw + 0.76rem, 0.89rem);
--fs-base: clamp(1rem, 0.34vw + 0.91rem, 1.19rem);
--fs-lg: clamp(1.25rem, 0.61vw + 1.1rem, 1.58rem);
```
- ✅ Distinctive fonts: Instrument Sans, Plus Jakarta, Outfit, Geist, Satoshi
- ❌ No Inter/Roboto/Arial/Open Sans · No monospace for "tech vibes"

**Layout — 4pt Grid**
- Scale: 4/8/12/16/24/32/48/64/96px · `gap` not margins · Container queries for components
- ❌ No card-in-card · No identical card grids · No center-everything · No hero-metric template

**Motion — 100/300/500ms**
```css
--ease-out-quart: cubic-bezier(0.25, 1, 0.5, 1);   /* Buttons: 100-150ms */
--ease-out-expo: cubic-bezier(0.16, 1, 0.3, 1);     /* Menus: 200-300ms */
/* Modals: 300-500ms, exit = 75% of enter */
/* Height: grid-template-rows, NEVER animate height directly */
```
- ✅ Only `transform` + `opacity` · `prefers-reduced-motion` = mandatory
- ❌ No bounce/elastic · No generic `ease`

**Interaction**
- ✅ Optimistic UI — update immediately, sync later
- ✅ Progressive disclosure — basic first, advanced behind expandable
- ✅ Empty states that teach, not just "nothing here"
- ❌ No modals unless truly no alternative · Not every button primary — hierarchy matters

**AI Slop Check** (before every PR):
- [ ] Fonts ≠ Inter/Roboto · Colors = OKLCH · No `#000`/`#fff`
- [ ] No card-in-card · No glassmorphism · No bounce easing
- [ ] No cyan-on-dark · No gradient text · `prefers-reduced-motion` supported

### 3. Accessibility — ui-ux-pro-max (56K)
- Contrast ≥4.5:1 · Touch ≥44px · Focus rings · Heading hierarchy · `prefers-reduced-motion`
- `aria-label` on icon buttons · Tab order = visual order · Color never sole indicator

### 4. TDD — test-driven-development (obra, 23K)
- **NO CODE WITHOUT FAILING TEST.** RED → Verify RED → GREEN → Verify GREEN → REFACTOR.

### 5. Debugging — systematic-debugging (obra, 28K)
- **NO FIX WITHOUT ROOT CAUSE.** Root Cause → Pattern → Hypothesis → Implementation.

---

## Component Architecture

### Rules
- **Compound components** > boolean props: `<Card.Header>` not `<Card isCompact isBordered>`
- **Variants**: `variant="primary" size="lg"` not `<Button isPrimary isLarge />`
- **Single Responsibility** · TypeScript interfaces on all props · No business logic in UI
- **No prop drilling >3 levels** → Context or Zustand · No inline objects in JSX
- **React 19**: `ref` as prop (no forwardRef), `use()` instead of `useContext()`

### State
```
Server State → @tanstack/react-query (useQuery/useMutation)
Client State → zustand (with persist + devtools middleware)
URL State    → nuqs (useQueryState)
Form State   → react-hook-form + zodResolver
```

### File Structure
```
components/
├── ui/              # shadcn (untouched)
└── feature-name/
    ├── FeatureName.tsx       # Component
    ├── FeatureName.types.ts  # Types
    ├── useFeatureName.ts     # Logic hook
    └── FeatureName.test.tsx  # Tests
```

### Quick Patterns
```tsx
// Forms: react-hook-form + zod
const form = useForm({ resolver: zodResolver(schema) })

// HTTP: ky
const api = ky.create({ prefixUrl: '/api', retry: 2 })

// Classes: clsx
<div className={clsx('base', isActive && 'bg-primary')} />

// Animation: framer-motion
<motion.div initial={{ opacity: 0 }} animate={{ opacity: 1 }} />

// Toast: sonner
toast.success('Saved') · toast.error('Failed')
```

---

## Shared Config
Read `../SHARED_CONFIG.md` for mandated stack, rules, and project structure.
