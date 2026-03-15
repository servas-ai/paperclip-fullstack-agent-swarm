# AGENTS_OVERVIEW.md — Alle 23 Agents

> Letzte Aktualisierung: 2026-03-15
> 23 Agents · 17 Skill-Quellen · Methodik: [obra/superpowers](https://github.com/obra/superpowers) + [pbakaus/impeccable](https://github.com/pbakaus/impeccable)

---

## Hierarchie

```
CEO
├── Product Owner (+ Sprint Planning, Parallel Dispatch)
└── Architecture Gatekeeper (+ Spec Review)
    ├── Stack Researcher
    ├── Code Quality Expert
    ├── Systematic Debugger
    ├── Security Auditor
    ├── DevOps Expert → Kubernetes Expert
    │                 → Git Workflow Manager
    │                 → Performance Optimizer
    └── Feature Orchestrator
        ├── UX Researcher
        ├── Design Architect
        ├── Frontend Builder
        ├── Backend Builder (+ Events + API Schema)
        └── QA Orchestrator (+ Docs Update)
            ├── Unit Test Writer (+ Testability Analysis)
            ├── Design Auditor
            ├── E2E Tester (+ VM + Browser)
            ├── Validation Expert
            └── Accessibility Expert

Cross-Cutting: Browser Automation (service)
```

---

## Agent-Liste

| # | Ordner | Squad | Berichtet an |
|---|--------|-------|-------------|
| 1 | `ceo/` | Leadership | Board |
| 2 | `product-owner/` | Leadership | CEO |
| 3 | `architecture-gatekeeper/` | Leadership | CEO |
| 4 | `feature-orchestrator/` | Pipeline | Gatekeeper |
| 5 | `stack-researcher/` | Research | Gatekeeper |
| 6 | `ux-researcher/` | Design | Orchestrator |
| 7 | `design-architect/` | Design | Orchestrator |
| 8 | `frontend-builder/` | Build | Orchestrator |
| 9 | `backend-builder/` | Build | Gatekeeper |
| 10 | `qa-orchestrator/` | QA | Orchestrator |
| 11 | `unit-test-writer/` | QA | QA Mgr |
| 12 | `design-auditor/` | QA | QA Mgr |
| 13 | `e2e-tester/` | QA | QA Mgr |
| 14 | `validation-expert/` | QA | QA Mgr |
| 15 | `accessibility-expert/` | QA | QA Mgr |
| 16 | `code-quality-expert/` | Quality | Gatekeeper |
| 17 | `systematic-debugger/` | Cross | Any Agent |
| 18 | `security-auditor/` | Security | Gatekeeper |
| 19 | `performance-optimizer/` | Perf | Gatekeeper |
| 20 | `devops-expert/` | Infra | Gatekeeper |
| 21 | `kubernetes-expert/` | Infra | DevOps |
| 22 | `git-workflow-manager/` | Infra | Gatekeeper |
| 23 | `browser-automation/` | Infra | Service |

---

## Feature Lifecycle

```
 1. BACKLOG       ← Product Owner
 2. GOAL.md       ← Gatekeeper (+ Spec Review)
 3. PRD           ← Orchestrator
 4. RESEARCH      ← Stack Researcher
 5. UX_SPEC       ← UX Researcher
 6. DESIGN_SPEC   ← Design Architect
 7. VALIDATION    ← Validation Expert
 8. BRANCH        ← Git Workflow Manager
 9. CODE          ← Frontend + Backend Builder
10. SECURITY      ← Security Auditor
11. PERFORMANCE   ← Performance Optimizer
12. ACCESSIBILITY ← Accessibility Expert
13. QA            ← QA Orchestrator (Unit/E2E/Design/UX)
14. QUALITY GATE  ← Code Quality Expert
15. DOCS UPDATE   ← QA Orchestrator
16. MERGE         ← Git Workflow Manager
17. DEPLOY        ← DevOps → K8s Expert
18. SCORECARD     ← Orchestrator → PO
```

---

## Agent Config (4 Dateien pro Agent)

| Datei | Inhalt |
|-------|--------|
| `SOUL.md` | Persona, Anti-Patterns |
| `AGENTS.md` | Rolle, Scope, Workflow |
| `TOOLS.md` | Skills (inline), Commands |
| `HEARTBEAT.md` | Checkliste, Red Flags |

---

## Kern-Prinzipien

1. **Goal Check** — GOAL.md lesen als erstes
2. **Evidence first** — Beweise vor Behauptungen
3. **Circuit Breaker** — Max 3 Iterationen, dann eskalieren
4. **TDD** — Kein Code ohne failing test
5. **HARD-GATE** — Kein Code ohne Design-Approval
6. **Mandated Stack** — Next.js 15 · React 19 · shadcn · Tailwind 4 · Zustand · Zod

## Consolidated Agents (v1.2)

| Entfernt | Merged in | Warum |
|----------|----------|-------|
| Scrum Master | Product Owner | Sprint Planning = PO-Funktion |
| Spec Reviewer | Gatekeeper | Spec Review = Teil des Quality Gate |
| Testability Expert | Unit Test Writer | Testability = Teil des Test-Prozesses |
| VM Tester | E2E Tester | Web-App-Fokus, VM selten nötig |
| Event-System Expert | Backend Builder | Supabase Realtime = Backend-Funktion |
| API Schema Expert | Backend Builder | Zod Schemas = Backend-Prozess |
| Docs Manager | QA Orchestrator | Docs Update = letzter QA-Schritt |
