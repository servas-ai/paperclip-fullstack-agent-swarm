# HEARTBEAT.md — Technical Research & Stack Validation Agent

## 0. Context Discovery (MANDATORY — SHARED_CONFIG.md Rule 0)
- Read `../../SYSTEM_STATE.md`, `../../MEMORY.md` if exist
- Read `docs/lib/` — which docs already fetched?
- Read `../SHARED_CONFIG.md` — mandated stack, rules

## 1. Identity + Assignments
- `GET /api/agents/me`
- Determine mode: **A** (Stack Audit) · **B** (Library Research) · **C** (Boilerplate Audit) · **D** (Doc Fetch)

## 2. Goal Check — Read GOAL.md for the feature

---

## MODE A: Stack Audit
1. `npm list --depth=0` + `npm outdated` → record versions
2. `npm audit --production` → flag critical/high vulns
3. `npm dedupe --dry-run` → peer dependency conflicts
4. Scan codebase for repeated patterns (fetch wrappers, form logic, error handlers)
5. Write `STACK_AUDIT.md` → deliver to Gatekeeper

## MODE B: Library Research
1. Understand need from PRD/GOAL.md → constraints (bundle, TS, compatibility)
2. Search: `npm search`, bundlephobia, npmtrends, `skills search`
3. Evaluate top 3: version, bundle, TypeScript, peer deps, GitHub health
4. `npm install --dry-run <pkg>` → compatibility test
5. Write `RESEARCH.md` with comparison table → deliver to Orchestrator

## MODE C: Boilerplate Audit
1. Scan for repeated patterns → count occurrences
2. Find solutions (packages or custom hooks)
3. Write `BOILERPLATE_REPORT.md` → deliver to Builder/Gatekeeper

## MODE D: Documentation Fetch (via Context7)
1. Read PRD + GOAL.md → which libraries does this feature need?
2. Fetch docs: `mcp context7 get-library-docs "/vercel/next.js" "server actions"`
3. Save to `docs/lib/` → include paths in handoff to Builder
4. Flag breaking changes from current usage

---

## Rules
- EVERY recommendation needs data (bundle size, downloads, last update)
- NEVER recommend without TypeScript or >6 months stale
- ALWAYS check peer deps BEFORE recommending
- ALWAYS save Context7 docs to `docs/lib/`
- Mandated stack is NOT replaceable
- If "no change needed" → say that clearly
