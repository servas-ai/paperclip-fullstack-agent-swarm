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

---

## Skills

### 1. Database — supabase-postgres-best-practices (32K)
- RLS ALWAYS on · Indexes on FKs · Enums via `pgEnum` · UUID PKs · `created_at`/`updated_at` on every table
- Prepared statements · Connection pooling · Service role key server-only

### 2. Security — security-best-practices (11K)
- Zod validation on EVERY endpoint · Auth + Authorization checks · Rate limiting on auth
- CORS, CSRF (built-in), CSP headers · No sensitive data in URLs

### 3. TDD — test-driven-development (obra, 23K)
- **NO CODE WITHOUT FAILING TEST FIRST.** RED → Verify RED → GREEN → Verify GREEN → REFACTOR.
- YAGNI: nothing beyond what the test requires.

### 4. Debugging — systematic-debugging (obra, 28K)
- **NO FIX WITHOUT ROOT CAUSE.** Root Cause → Pattern → Hypothesis → Implementation.

### 5. Verification — verification-before-completion (obra, 16K)
- Before "done": run ALL tests, check migrations, verify RLS, test error paths, show evidence.

---

## Patterns (Kurzreferenz)

### Drizzle Schema
```typescript
// src/db/schema/users.ts
export const users = pgTable('users', {
  id: uuid('id').primaryKey().defaultRandom(),
  email: text('email').notNull().unique(),
  name: text('name').notNull(),
  role: roleEnum('role').notNull().default('user'),
  createdAt: timestamp('created_at', { withTimezone: true }).notNull().defaultNow(),
  updatedAt: timestamp('updated_at', { withTimezone: true }).notNull().defaultNow(),
})
```

### API Route Handler
```typescript
// src/app/api/users/route.ts — Pattern: Zod validate → Drizzle query → NextResponse
export async function GET(request: NextRequest) {
  const params = querySchema.parse(Object.fromEntries(request.nextUrl.searchParams))
  const data = await db.select().from(users).limit(params.limit).offset((params.page - 1) * params.limit)
  return NextResponse.json({ data })
}

export async function POST(request: NextRequest) {
  const validated = createSchema.parse(await request.json())
  const [item] = await db.insert(users).values(validated).returning()
  return NextResponse.json(item, { status: 201 })
}
```

### Server Action
```typescript
// src/app/actions/users.ts — Pattern: 'use server' → Zod validate → Drizzle mutate → revalidatePath
'use server'
export async function createUser(formData: FormData) {
  const validated = schema.parse({ email: formData.get('email'), name: formData.get('name') })
  await db.insert(users).values(validated)
  revalidatePath('/users')
}
```

### Error Handling
```typescript
// src/lib/api-error.ts — Pattern: ZodError→400, unique→409, not found→404, else→500
export function handleApiError(error: unknown) {
  if (error instanceof ZodError) return NextResponse.json({ error: 'Validation', details: error.flatten().fieldErrors }, { status: 400 })
  return NextResponse.json({ error: 'Internal server error' }, { status: 500 })
}
```

### Supabase Auth (SSR)
```typescript
// src/lib/supabase/server.ts — createServerClient with cookies
// src/middleware.ts — getUser() → redirect to /login if !user on /dashboard/*
```

### Migration Commands
```bash
npx drizzle-kit generate  # Generate from schema changes
npx drizzle-kit migrate   # Apply
npx drizzle-kit studio    # Visual DB browser
```

---

## File Structure

```
src/
├── app/api/[resource]/route.ts    ← Route Handlers (GET/POST/PATCH/DELETE)
├── app/actions/                   ← Server Actions
├── db/schema/                     ← Drizzle schemas
├── db/index.ts                    ← DB client
├── lib/supabase/{server,client}.ts ← Supabase clients
├── lib/api-error.ts               ← Error handling
├── lib/validations/               ← Shared Zod schemas
├── middleware.ts                  ← Auth middleware
└── types/                         ← TypeScript types
```

---

## Shared Config
Read `../SHARED_CONFIG.md` for mandated stack, rules, and project structure.
