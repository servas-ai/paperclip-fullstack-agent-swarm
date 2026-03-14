# Tools

## Runtime
- **OpenCode** is your runtime.

## Paperclip API
- `GET /api/agents/me` — identity.
- `GET /api/companies/{companyId}/issues?assigneeAgentId={agentId}&status=todo,in_progress,blocked` — inbox.
- `PATCH /api/issues/{issueId}` — status updates. Include `X-Paperclip-Run-Id`.

---

## Skills

| Skill | Source | Use |
|-------|--------|-----|
| `find-skills` | vercel-labs (#1) | Find skills for problems: `skills search "date picker"` |
| `competitor-alternatives` | coreyhaines31 (16K) | Package comparison matrix |
| `firecrawl` | firecrawl/cli (11K) | Crawl docs: `npx -y firecrawl scrape <url>` |
| `brainstorming` | obra (50K) | Structured ideation for approaches |
| `agent-browser` | vercel-labs (89K) | Research live docs, bundlephobia screenshots |
| `context7` | am-will/codex-skills (12K) | **Latest version-specific docs** (see below) |
| `security-best-practices` | supercent-io (11K) | Auth, CSRF, XSS, dependency audit |
| `code-review` | supercent-io (11K) | Evaluate library code quality |

---

## Context7 — Latest Documentation (CRITICAL)

Fetch current API docs to prevent hallucinated code. Available as MCP or script.

### Quick Reference — Mandated Stack
| Library | Context7 ID | Example Queries |
|---------|-------------|----------------|
| Next.js 15 | `/vercel/next.js` | "app router", "server actions", "middleware" |
| React 19 | `/facebook/react` | "server components", "suspense", "transitions" |
| Tailwind 4 | `/tailwindlabs/tailwindcss` | "v4 config", "custom properties" |
| Zustand | `/pmndrs/zustand` | "persist middleware", "slices pattern" |
| Zod | `/colinhacks/zod` | "schema validation", "discriminated unions" |
| shadcn/ui | `/shadcn-ui/ui` | "dialog", "form", "data-table" |
| React Hook Form | `/react-hook-form/react-hook-form` | "zod resolver" |
| TanStack Query | `/TanStack/query` | "mutations", "prefetching" |
| Supabase | `/supabase/supabase` | "auth", "rls", "realtime" |
| Drizzle ORM | `/drizzle-team/drizzle-orm` | "schema", "migrations" |
| Vitest | `/vitest-dev/vitest` | "mocking", "coverage" |
| Playwright | `/microsoft/playwright` | "locators", "assertions" |

### Workflow
```bash
# 1. Resolve library → 2. Fetch docs → 3. Save for builders
mcp context7 resolve-library-id "next.js"
mcp context7 get-library-docs "/vercel/next.js" "app router" > docs/lib/nextjs-app-router.md
```

---

## npm Research
```bash
npm list --depth=0          # Current versions
npm outdated                # Outdated packages
npm audit --production      # Vulnerabilities
npm info <pkg> version      # Package info
npm install --dry-run <pkg> # Test install without conflicts
npm dedupe --dry-run        # Check duplicates
```

### Package Evaluation (agent-browser)
```bash
agent-browser open https://bundlephobia.com/package/<pkg>@latest  # Bundle size
agent-browser open https://npmtrends.com/<a>-vs-<b>-vs-<c>        # Trends
agent-browser screenshot comparison.png
```

---

## Deliverables

### RESEARCH.md (Library Recommendation)
```markdown
# RESEARCH: [Topic]
> Date: [date] | Requested by: [agent]

## Question
Best [library type] for [use case]?

## Requirements
Must work with: Next.js 15, React 19, Tailwind 4 · TypeScript required · Bundle < [X]KB

## Comparison
| Criterion | Pkg A | Pkg B | Pkg C |
|-----------|-------|-------|-------|
| Version / Last update | | | |
| Bundle (gzip) | | | |
| TypeScript | | | |
| Peer dep conflicts | | | |
| GitHub stars | | | |

## Recommendation
**Use [Pkg]** because: [1-3 reasons]

## Integration
\`\`\`bash
npm install <pkg>
\`\`\`
```

### STACK_AUDIT.md (Health Check)
```markdown
# STACK_AUDIT: [Project]
> Date: [date]

## Package Versions
| Package | Current | Latest | Status |
|---------|---------|--------|--------|

## Vulnerabilities
🔴 Critical: [N] · 🟡 High: [N] · 🟢 Low: [N]

## Verdict
- [ ] ✅ Healthy · [ ] ⚠️ Updates needed · [ ] 🔴 Critical vulns
```

---

## Rules
- EVERY recommendation needs data (bundle size, downloads, last update)
- NEVER recommend packages last updated >6 months or without TypeScript
- ALWAYS check peer dependencies BEFORE recommending
- ALWAYS use Context7 to verify API signatures
- ALWAYS save fetched docs to `docs/lib/`
- Mandated stack is NOT replaceable — optimize WITHIN it
