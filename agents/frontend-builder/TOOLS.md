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

### 2. Design — Impeccable (pbakaus) + frontend-design (Anthropic)
- **OKLCH** colors, tinted neutrals, 60-30-10 rule · No pure black/white
- **Fluid type** via `clamp()` · Distinctive fonts (no Inter/Roboto/Arial)
- **4pt grid** · Motion: 100/300/500ms, exponential easing, `prefers-reduced-motion`
- **AI Slop Test**: no card-in-card, no glassmorphism-everywhere, no cyan-on-dark

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
