# HEARTBEAT.md — Backend Builder

## 1. Identity + Setup
- `GET /api/agents/me`
- Read `../SHARED_CONFIG.md`, `../../SYSTEM_STATE.md`, `../../MEMORY.md`
- Verify: `DATABASE_URL`, Supabase env vars, `drizzle.config.ts`
- Read `docs/lib/` for latest Drizzle/Supabase/Zod docs

## 2. Schema Design (Drizzle ORM)
1. Define tables in `src/db/schema/[name].ts`
2. Relations in `src/db/relations.ts` · Enums via `pgEnum`
3. Conventions: UUID PKs, `created_at` + `updated_at`, soft delete via `deleted_at`, snake_case DB / camelCase TS
4. `npx drizzle-kit generate` → review SQL → `npx drizzle-kit migrate`

## 3. Validation (Zod)
- Schemas in `src/lib/validations/[name].ts` — shared with frontend
- Schema for every: request body, query params, path params
- `export type CreateUserInput = z.infer<typeof createUserSchema>`

## 4. API Implementation
For each endpoint:
1. Route Handler (complex logic, streaming) or Server Action (simple mutations)
2. Zod validation at entry · Auth check · Business logic · `handleApiError()` · Typed response

Patterns: `GET` list → paginate+sort+filter · `GET` → 404 · `POST` → 201 · `PATCH` → partial · `DELETE` → `{ deleted: true }`

## 5. Auth & Security
- [ ] RLS on every new table · Auth middleware on protected routes
- [ ] Zod on every endpoint · No secrets in code · Errors don't leak internals

## 6. Testing
- Integration tests for every endpoint (happy + error paths)
- `npx vitest run src/app/api/` · Coverage ≥ targets (SHARED_CONFIG)

## 7. Pre-Delivery + Exit
- [ ] Migrations clean · RLS active · Zod everywhere · No `any` types
- [ ] API tests PASS · `npm audit` clean · SYSTEM_STATE.md updated
- Structured PR: What → Why → How → Migrations → Breaking changes

## Rules
- Schema FIRST, code SECOND · Zod at EVERY boundary · RLS on EVERY table
- Tests for EVERY endpoint · TypeScript strict · SYSTEM_STATE.md always current
