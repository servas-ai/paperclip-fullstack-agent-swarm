# SHARED_CONFIG.md — Zentrale Konfiguration für alle Agents

> Dieses File wird von JEDEM Agent gelesen. Änderungen hier betreffen alle.
> Letzte Aktualisierung: 2026-03-15 (23 Agents after consolidation)

---

## Runtime
- **OpenCode** ist die Agent-Runtime.
- Agents haben Shell-Zugriff, Internet-Zugriff, und MCP-Server Zugriff.

## Paperclip API

| Endpoint | Method | Zweck |
|----------|--------|-------|
| `/api/agents/me` | GET | Agent-Identität |
| `/api/companies/{companyId}/issues?assigneeAgentId={agentId}&status=todo,in_progress,blocked` | GET | Aufgaben-Inbox |
| `/api/issues/{issueId}` | PATCH | Status-Updates (inkl. `X-Paperclip-Run-Id` Header) |
| `/api/companies/{companyId}/issues` | POST | Subtasks erstellen (mit `parentId` + `goalId`) |

---

## Mandated Stack

| Layer | Technologie | Context7 ID |
|-------|-------------|-------------|
| Framework | Next.js 15 (App Router) | `/vercel/next.js` |
| UI | React 19 + shadcn/ui | `/facebook/react` · `/shadcn-ui/ui` |
| Styling | Tailwind CSS 4 | `/tailwindlabs/tailwindcss` |
| State | Zustand (persist + devtools) + TanStack Query | `/pmndrs/zustand` · `/TanStack/query` |
| Validation | Zod + React Hook Form | `/colinhacks/zod` |
| Icons | lucide-react · Animation: Framer Motion · HTTP: ky · Toast: Sonner |
| ORM | Drizzle ORM + drizzle-kit | `/drizzle-team/drizzle-orm` |
| Database | Supabase (PostgreSQL) | `/supabase/supabase` |
| Auth | Supabase Auth / better-auth |
| Logging | pino · IDs: nanoid |

> Stack ist **NICHT verhandelbar**. Optimize WITHIN it.

### Test Coverage (Quality Gate)

| Metrik | Minimum | Empfohlen |
|--------|---------|-----------|
| Statements / Lines | 80% | 90% |
| Branches | 75% | 85% |
| Functions | 80% | 90% |

> `npx vitest run --coverage` · Features NICHT shippen wenn unter Minimum.

---

## MCP Server

```json
{
  "context7": { "command": "npx", "args": ["-y", "@upstash/context7-mcp"] },
  "firecrawl": { "command": "npx", "args": ["-y", "firecrawl-mcp"], "env": { "FIRECRAWL_API_KEY": "<key>" } }
}
```

---

## Shared Rules

### 0. Context Discovery (PFLICHT — vor jeder Arbeit)

Bevor du arbeitest, lies was existiert:
1. `../../SYSTEM_STATE.md` → was im System existiert (erstellen wenn fehlt)
2. `../../MEMORY.md` → bekannte Gotchas und Patterns (erstellen wenn fehlt)
3. `docs/features/<feature>/GOAL.md` → Acceptance Criteria
4. `docs/lib/` → vorhandene Context7 Docs
5. `../SHARED_CONFIG.md` + `../SKILLS.md` → Stack, Rules, Skills

> Agent startet → liest State → macht WEITER statt von vorne.
> Agent crashed → nächster Agent liest State → übernimmt.

### 1. Goal Check
Jeder Agent liest GOAL.md des Features als erstes. Alle Aktionen müssen dem Goal dienen.

### 2. Evidence before Claims
Kein "fertig" ohne Beweis: Builder → Tests PASS · Tester → Screenshots + Logs · Auditor → REVIEW.md mit Befund.

### 3. Circuit Breaker
Max 3 Iterationen pro Gate → Eskalation an Architecture Gatekeeper.

### 4. Error Recovery
```
Stufe 1: Selbst lösen (max 3 Versuche)
Stufe 2: Systematic Debugger fragen
Stufe 3: BLOCKED setzen → Gatekeeper
```

### 5. Advanced Reasoning (bei komplexen Aufgaben)
- **Chain-of-Thought**: Problem → Optionen → Entscheidung
- **ReAct**: Reason → Act → Reason → Act
- **Self-Refinement**: Vor Abgabe: Vollständig? Korrekt? Minimal?

### 6. Skill Priority
```
1. User Instructions → HÖCHSTE
2. Skills → Override Defaults
3. System Prompt → NIEDRIGSTE
```

---

## Skill-Quellen (17 Repositories)

| Quelle | Top Skills |
|--------|-----------|
| [obra/superpowers](https://github.com/obra/superpowers) | TDD, Debugging, Plans, Verification, Git, Code Review |
| [vercel-labs / skills.sh](https://skills.sh) | React, Design Guidelines, Browser, Next.js |
| [anthropics](https://github.com/anthropics/skills) | Frontend Design, Webapp Testing |
| [pbakaus/impeccable](https://github.com/pbakaus/impeccable) | OKLCH, 4pt Grid, Motion, AI Slop Test |
| [supabase](https://github.com/supabase/agent-skills) | Postgres, RLS |
| [am-will/codex-skills](https://github.com/am-will/codex-skills) | Context7, Find-Skills |
| + 11 weitere | Security, Playwright, UI/UX, SEO, Browser-Use |

> Skills sind **inline in TOOLS.md** eingebettet. `skills search "<thema>"` zum Suchen.

---

## 🛡️ Anti-Hallucination Protocol

### STOP-CHECK-DELIVER (vor jeder Abgabe)
```
1. GOAL.md nochmal gelesen? (Pflicht)
2. Output enthält NUR was gefordert? (Keine Extras)
3. Fehlt etwas was gefordert wurde? (Vollständig)
→ EINE Antwort NEIN → FIX IT before delivering.
```

### Validierungskette
Agent liefert → Empfänger prüft gegen Auftrag → ✅ Akzeptiert / 🔴 REJECT mit Grund

### Verbotene Patterns (🔴 SOFORT STOPPEN)
1. "Ich füge noch schnell X hinzu" → NEIN. Nicht im GOAL.md = nicht bauen
2. "Das wäre doch besser wenn..." → Verbesserung als Kommentar, nicht als Code
3. "Ich habe auch noch Y gemacht" → Nur den Auftrag erfüllen
4. Eigene ACs erfinden → Nur ACs aus GOAL.md/PRD umsetzen
5. Tests für nicht-existierenden Code → Nur testen was gebaut wurde

---

## Projekt-Ordnerstruktur

```
project-root/
├── SYSTEM_STATE.md         ← Aktueller Systemzustand
├── MEMORY.md               ← Patterns, Entscheidungen, Gotchas
├── docs/
│   ├── lib/                ← Context7 Docs
│   ├── features/<feature>/ ← Pro Feature:
│   │   ├── GOAL.md · PRD.md · UX_SPEC.md · DESIGN_SPEC.md
│   │   ├── QA_REPORT.md · SECURITY_AUDIT.md · A11Y_AUDIT.md
│   │   └── FEATURE_SCORECARD.md
│   └── api/                ← API-Docs
├── agents/                 ← Dieses Verzeichnis (30 Agents × 4 Dateien)
└── src/                    ← Source Code
```
