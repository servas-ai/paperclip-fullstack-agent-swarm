# SHARED_CONFIG.md — Zentrale Konfiguration für alle Agents

> Dieses File wird von JEDEM Agent gelesen. Änderungen hier betreffen alle.
> Letzte Aktualisierung: 2026-03-13 (Skill Registry, Advanced Reasoning, Error Recovery, 30 Agents)

---

## Runtime
- **OpenCode** ist die Agent-Runtime.
- Alle Agents haben Shell-Zugriff, Internet-Zugriff, und MCP-Server Zugriff.

## Paperclip API

| Endpoint | Method | Zweck |
|----------|--------|-------|
| `/api/agents/me` | GET | Agent-Identität |
| `/api/companies/{companyId}/issues?assigneeAgentId={agentId}&status=todo,in_progress,blocked` | GET | Aufgaben-Inbox |
| `/api/issues/{issueId}` | PATCH | Status-Updates (inkl. `X-Paperclip-Run-Id` Header) |
| `/api/companies/{companyId}/issues` | POST | Subtasks erstellen (mit `parentId` + `goalId`) |

---

## Mandated Stack

| Layer | Technologie | Referenz |
|-------|-------------|----------|
| Framework | Next.js 15 (App Router) | `/vercel/next.js` |
| UI Library | React 19 | `/facebook/react` |
| UI Components | shadcn/ui | `/shadcn-ui/ui` |
| Styling | Tailwind CSS 4 | `/tailwindlabs/tailwindcss` |
| State (Client) | Zustand (mit persist + devtools) | `/pmndrs/zustand` |
| State (Server) | TanStack React Query | `/TanStack/query` |
| Validation | Zod | `/colinhacks/zod` |
| Forms | React Hook Form + Zod Resolver | `/react-hook-form/react-hook-form` |
| Icons | lucide-react | — |
| Animation | Framer Motion | — |
| HTTP Client | ky | — |
| Toast | Sonner | — |

> Die Referenz-Spalte sind Context7 Library IDs — für aktuelle Docs.
> Dieser Stack ist **NICHT verhandelbar**. Optimize WITHIN it.

### Backend Stack

| Layer | Technologie | Referenz |
|-------|-------------|----------|
| ORM | Drizzle ORM | `/drizzle-team/drizzle-orm` |
| Migrations | drizzle-kit | — |
| Database | Supabase (PostgreSQL) | `/supabase/supabase` |
| Auth | Supabase Auth / better-auth | `/supabase/supabase` |
| SSR Auth | @supabase/ssr | — |
| Logging | pino | — |
| IDs | nanoid | — |

> Backend Stack gilt für alle API/DB Arbeiten. Wird vom Backend Builder durchgesetzt.

### Test Coverage Targets (Quality Gate)

| Metrik | Minimum | Empfohlen |
|--------|---------|----------|
| Statements | 80% | 90% |
| Branches | 75% | 85% |
| Functions | 80% | 90% |
| Lines | 80% | 90% |

> Coverage wird mit `npx vitest run --coverage` gemessen.
> Features dürfen NICHT shippen wenn Coverage unter Minimum fällt.
> QA Orchestrator prüft Coverage als Teil des QA_REPORT.md.

---

## MCP Server

### Context7 — Aktuelle Library-Dokumentation
```json
{
  "context7": {
    "command": "npx",
    "args": ["-y", "@upstash/context7-mcp"]
  }
}
```
**Tools:** `resolve-library-id`, `get-library-docs`
**Wann:** Vor jeder Implementierung aktuelle Docs fetchen → speichern in `docs/lib/`

### Firecrawl — Web Scraping & Crawling
```json
{
  "firecrawl": {
    "command": "npx",
    "args": ["-y", "firecrawl-mcp"],
    "env": { "FIRECRAWL_API_KEY": "<key>" }
  }
}
```
**Auto-Install:** `which firecrawl || npm install -g firecrawl`

---

## Shared Rules (für ALLE Agents)

### 0. 🔍 Context Discovery (ALLERERSTER Schritt — vor JEDER Arbeit)

> **Bevor du irgendetwas tust: Lies was schon da ist.**
> **Wenn eine Datei fehlt: Erstelle sie aus dem Template.**

```
STEP 0 — CONTEXT DISCOVERY (PFLICHT für jeden Agent bei jedem Start)

1. Prüfe: Existiert `../../SYSTEM_STATE.md`?
   ├── JA → LESEN. Du weißt jetzt was im System existiert.
   └── NEIN → Erstelle aus Template (siehe SHARED_CONFIG Projekt-Ordnerstruktur)

2. Prüfe: Existiert `../../MEMORY.md`?
   ├── JA → LESEN. Du kennst jetzt bekannte Gotchas und Patterns.
   └── NEIN → Erstelle aus Template.

3. Prüfe: Existiert `../../TASK_LOG.md`?
   ├── JA → LESEN. Du weißt was aktiv, blockiert oder fertig ist.
   └── NEIN → Erstelle aus Template.

4. Prüfe: Existiert `docs/features/<aktuelles-feature>/STATUS.md`?
   ├── JA → LESEN. Du weißt wo das Feature steht und wer zuletzt was gemacht hat.
   └── NEIN → Feature ist neu, Orchestrator erstellt den Ordner.

5. Prüfe: Existiert `docs/lib/`?
   ├── JA → Prüfe ob Docs für deine Libraries vorhanden sind. LESEN.
   └── NEIN → Ordner erstellen, Stack Researcher um Context7 Docs bitten.

6. Lese `../SHARED_CONFIG.md` — Stack, Rules, MCP Server.
7. Lese `../SKILLS.md` — verfügbare Skills und extrahiertes Wissen.
8. Lese `../REPORTING_PROTOCOL.md` — wie du Status reportest.
```

**Warum das wichtig ist:**
- Agent startet → findet vorherigen State → macht WEITER statt von vorne
- Agent crashed → nächster Agent liest STATUS.md → übernimmt
- Kein Agent arbeitet jemals "blind" ohne Kontext

### 1. Goal Check (MANDATORY Step 0)
Jeder Agent liest als ERSTES die GOAL.md des Features. Alle Aktionen müssen dem Goal dienen.

### 2. Evidence before Claims
Kein Agent darf "fertig" sagen ohne Beweis:
- Builder: Tests müssen PASS zeigen
- Tester: Screenshots + Logs
- Auditor: REVIEW.md mit Befund
- Docs: Alle Links verifiziert

### 3. Circuit Breaker
Max 3 Iterationen pro Gate. Danach → Eskalation an Architecture Gatekeeper.

### 4. HANDOFF Protocol
Standard-Format für Agent-zu-Agent Übergaben:
```markdown
# HANDOFF: [From Agent] → [To Agent]
Feature: [name]
Goal: [GOAL.md link]
Deliverables: [was übergeben wird]
Context: [was der Empfänger wissen muss]
Documentation: [docs/lib/ Referenzen]
```

### 5. Skill Loading

```bash
# Suchen + Installieren
skills search "<thema>"
skills install <skill-name>

# Oder direkt von GitHub
curl -sL https://raw.githubusercontent.com/obra/superpowers/main/skills/<name>/SKILL.md
```

### Skill-Quellen

| Quelle | GitHub | Top Skills |
|--------|--------|-----------|
| obra/superpowers | [GitHub](https://github.com/obra/superpowers) | TDD, Debugging, Plans, Verification, Git, Subagent, Code Review |
| Vercel Labs | [skills.sh](https://skills.sh) | React Best Practices, Design Guidelines, Browser, Next.js |
| Anthropic | [GitHub](https://github.com/anthropics/skills) | Frontend Design, Canvas, Webapp Testing |
| pbakaus/impeccable | [GitHub](https://github.com/pbakaus/impeccable) | OKLCH, 4pt Grid, Motion, AI Slop Test |
| supercent-io | [GitHub](https://github.com/supercent-io/agent-skills) | Security, Code Review, Design System |
| coreyhaines31 | [GitHub](https://github.com/coreyhaines31/marketingskills) | SEO, Content Strategy, Competitor Analysis |
| google-labs-code | [GitHub](https://github.com/google-labs-code/stitch-skills) | React Components, Design |
| supabase | [GitHub](https://github.com/supabase/agent-skills) | Postgres Best Practices |
| nextlevelbuilder | [GitHub](https://github.com/nextlevelbuilder/ui-ux-pro-max-skill) | UI/UX Pro Max |
| browser-use | [GitHub](https://github.com/browser-use/browser-use) | Browser Automation |
| better-auth | [GitHub](https://github.com/better-auth/skills) | Auth Best Practices |
| currents-dev | [GitHub](https://github.com/currents-dev/playwright-best-practices-skill) | Playwright |
| wshobson | [GitHub](https://github.com/wshobson/agents) | TypeScript, Tailwind |
| sleekdotdesign | [GitHub](https://github.com/sleekdotdesign/agent-skills) | Mobile App Design |
| am-will | [GitHub](https://github.com/am-will/codex-skills) | Context7, Find-Skills |
| Intopia | [Website](https://intopia.digital) | Web Accessibility (WCAG) |
| Trail of Bits | [Website](https://www.trailofbits.com) | Security Auditing |

> Skills sind **inline in TOOLS.md** eingebettet. URLs dienen zum Nachlesen oder Aktualisieren.

### Skill Priority
1. **User Instructions** → HÖCHSTE
2. **Skills** → Override Defaults
3. **System Prompt** → NIEDRIGSTE

### 6. State Tracking
- Nach JEDEM Build: `SYSTEM_STATE.md` updaten.
- Vor JEDEM Feature: `SYSTEM_STATE.md` lesen.

### 7. Advanced Reasoning

Bei komplexen Aufgaben:
- **Chain-of-Thought**: Denkschritte zeigen (Problem → Optionen → Entscheidung)
- **ReAct**: Abwechselnd denken + handeln (Reason → Act → Reason → Act)
- **Self-Refinement**: Vor Abgabe: Vollständig? Korrekt? Minimal?

### 8. Error Recovery

```
Stufe 1: Selbst lösen (max 3 Versuche)
Stufe 2: Systematic Debugger fragen
Stufe 3: BLOCKED setzen → Gatekeeper
```

### 9. Progress Reporting
- STATUS.md updaten bei Start/Ende von Arbeit
- TASK_LOG.md für Feature-Übersicht
- Bei Crash: STATUS.md lesen → ab letztem ✅ weitermachen

### 10. 🛡️ Anti-Hallucination Protocol (PFLICHT für JEDEN Agent)

> **Eiserne Regel: Kein Agent liefert ab, ohne sich selbst zu prüfen UND vom Empfänger geprüft zu werden.**

#### A. STOP-CHECK-DELIVER (vor jeder Abgabe)

Jeder Agent MUSS vor dem Abliefern diese 3 Fragen beantworten:

```
STOP: Ist mein Output GENAU das was angefordert wurde?
  1. Habe ich GOAL.md / den Auftrag nochmal gelesen? (Pflicht!)
  2. Enthält mein Output NUR was gefordert wurde? (Keine Extras!)
  3. Fehlt etwas das gefordert wurde? (Vollständigkeit!)

Wenn EINE Antwort NEIN → FIX IT before delivering.
```

#### B. Hierarchische Validierung (Empfänger prüft IMMER)

```
Agent liefert ab
    ↓
Empfänger (höhere Hierarchie) prüft:
  ├── Entspricht dem Auftrag? → ✅ Akzeptiert
  ├── Fehlt etwas? → 🔴 REJECT: "AC #X fehlt"
  ├── Zu viel drin? → 🔴 REJECT: "Entferne [X], nicht gefordert"
  └── Anders als gefordert? → 🔴 REJECT: "Soll [A] sein, ist [B]"
```

#### C. Agent-spezifische Anti-Hallucination Regeln

| Agent | Prüft sich gegen | Wird geprüft von |
|-------|------------------|-----------------|
| Stack Researcher | GOAL.md — nur recherchieren was gefragt ist | Gatekeeper / Orchestrator |
| UX Researcher | PRD — nur Flows für geforderte Features | Orchestrator |
| Design Architect | UX_SPEC + PRD — nur Screens designen die gefordert sind | Orchestrator |
| Frontend Builder | DESIGN_SPEC + GOAL.md — nur bauen was designed ist | Orchestrator (Scope Gate) |
| Backend Builder | API_SPEC + GOAL.md — nur API-Endpoints die spezifiziert sind | Gatekeeper |
| Unit Test Writer | Code + PRD ACs — nur testen was existiert und gefordert | QA Orchestrator |
| Design Auditor | DESIGN_SPEC — reviewen gegen Spec, nicht persönliche Meinung | QA Orchestrator |
| E2E Tester | PRD ACs — nur User Journeys testen die im PRD stehen | QA Orchestrator |
| QA Orchestrator | PRD + DESIGN_SPEC — nur relevante Tests dispatchen | Orchestrator |
| Docs Manager | SYSTEM_STATE + Code — nur dokumentieren was existiert | Orchestrator |
| Spec Reviewer | GOAL.md — nur reviewen was im Scope steht | Gatekeeper |
| Systematic Debugger | Bug-Report — nur den gemeldeten Bug untersuchen | Aufrufender Agent |
| Security Auditor | OWASP + Code — nur Schwachstellen die existieren, keine Phantome | Gatekeeper |
| Performance Optimizer | Messdaten — nur optimieren was gemessen langsam ist | Gatekeeper |
| Accessibility Expert | WCAG 2.1 + Code — nur existierende Barrieren melden | QA Orchestrator |
| Git Workflow Manager | Branch-Policy — nur definierte Branch-Operationen ausführen | Gatekeeper |

#### D. Verbotene Patterns (🔴 SOFORT STOPPEN)

1. **"Ich füge noch schnell X hinzu"** → NEIN. Wenn X nicht im GOAL.md steht, nicht bauen.
2. **"Das wäre doch besser wenn..."** → NEIN. Verbesserungsvorschläge als Kommentar, nicht als Code.
3. **"Ich habe auch noch Y gemacht"** → NEIN. Nur den Auftrag erfüllen.
4. **"Vielleicht braucht man auch Z"** → NEIN. Scope ist definiert.
5. **Eigene ACs erfinden** → NEIN. Nur die ACs aus GOAL.md/PRD umsetzen.
6. **Tests für nicht-existierenden Code schreiben** → NEIN. Nur testen was gebaut wurde.
7. **Design-Reviews nach persönlichem Geschmack** → NEIN. Nur gegen DESIGN_SPEC prüfen.

---

## Projekt-Ordnerstruktur

```
project-root/
├── SYSTEM_STATE.md         ← Aktueller Systemzustand (Routes, Components, Stores, APIs)
├── MEMORY.md               ← Gelernte Patterns, Entscheidungen, Gotchas
├── TASK_LOG.md             ← Zentrale Feature-Übersicht (aktiv/blockiert/fertig)
├── docs/
│   ├── lib/                ← Context7 Docs (vom Stack Researcher)
│   ├── architecture/       ← Architektur-Docs (vom Gatekeeper)
│   ├── features/           ← Feature-Docs (pro Feature ein Ordner)
│   │   └── <feature>/
│   │       ├── STATUS.md           ← LIVE Status, Fortschritt, Änderungsprotokoll
│   │       ├── GOAL.md             ← Acceptance Criteria
│   │       ├── SPEC_REVIEW.md      ← Spec Review Ergebnis (Spec Reviewer)
│   │       ├── PRD.md              ← Product Requirements
│   │       ├── UX_SPEC.md          ← User Flows
│   │       ├── DESIGN_SPEC.md      ← Design Tokens + Layout
│   │       ├── BRANCH_STATUS.md    ← Git Branch Lifecycle (Git Workflow Manager)
│   │       ├── ROOT_CAUSE.md       ← Bug Root Cause (Systematic Debugger)
│   │       ├── SECURITY_AUDIT.md   ← Security Findings (Security Auditor)
│   │       ├── PERFORMANCE_REPORT.md ← Performance Metrics (Performance Optimizer)
│   │       ├── A11Y_AUDIT.md       ← Accessibility Findings (Accessibility Expert)
│   │       ├── QA_REPORT.md        ← Test-Ergebnisse (QA Orchestrator)
│   │       └── FEATURE_SCORECARD.md ← Finale Bewertung
│   └── api/                ← API-Docs (vom Docs Manager)
├── agents/                 ← Agent-Konfigurationen (dieses Verzeichnis)
│   ├── README.md           ← Übersicht + Quick Start
│   ├── AGENTS_OVERVIEW.md  ← Alle 30 Agents Detailübersicht
│   ├── SHARED_CONFIG.md    ← DIESES FILE
│   ├── SKILLS.md           ← Skill Discovery + extrahiertes Wissen
│   ├── REPORTING_PROTOCOL.md ← Status-Reporting Regeln + Templates
│   └── [agent-ordner]/     ← 30 Individuelle Agent-Configs (je 4 Dateien)
└── src/                    ← Source Code
```
