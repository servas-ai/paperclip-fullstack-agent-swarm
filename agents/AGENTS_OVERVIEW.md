# AGENTS_OVERVIEW.md — Alle 30 Agents

> Letzte Aktualisierung: 2026-03-13
> 30 Agents · 17 Skill-Quellen · Methodik: [obra/superpowers](https://github.com/obra/superpowers) + [pbakaus/impeccable](https://github.com/pbakaus/impeccable)

---

## Hierarchie

```
CEO
├── Product Owner → Scrum Master
└── Architecture Gatekeeper
    ├── Stack Researcher
    ├── Docs Manager
    ├── Code Quality Expert
    ├── Spec Reviewer 🆕
    ├── Security Auditor 🆕
    ├── DevOps Expert → Kubernetes Expert
    │                 → Git Workflow Manager 🆕
    │                 → Performance Optimizer 🆕
    ├── Event-System Expert
    ├── API Schema Expert
    └── Feature Orchestrator
        ├── UX Researcher
        ├── Design Architect
        ├── Frontend Builder
        ├── Backend Builder
        └── QA Orchestrator
            ├── Unit Test Writer
            ├── Design Auditor
            ├── E2E Tester
            ├── VM Tester
            ├── Testability Expert
            ├── Validation Expert
            └── Accessibility Expert 🆕

Cross-Cutting: Systematic Debugger 🆕, Browser Automation
```

---

## Agent-Liste

| # | Ordner | Squad | Berichtet an |
|---|--------|-------|-------------|
| 1 | `ceo/` | Leadership | Board |
| 2 | `product-owner/` | Leadership | CEO |
| 3 | `scrum-master/` | Leadership | PO |
| 4 | `architecture-gatekeeper/` | Leadership | CEO |
| 5 | `feature-orchestrator/` | Build | Gatekeeper |
| 6 | `stack-researcher/` | Research | Gatekeeper |
| 7 | `ux-researcher/` | Design | Orchestrator |
| 8 | `design-architect/` | Design | Orchestrator |
| 9 | `frontend-builder/` | Build | Orchestrator |
| 10 | `backend-builder/` | Build | Gatekeeper |
| 11 | `qa-orchestrator/` | QA | Orchestrator |
| 12 | `unit-test-writer/` | QA | QA Mgr |
| 13 | `design-auditor/` | QA | QA Mgr |
| 14 | `e2e-tester/` | QA | QA Mgr |
| 15 | `vm-tester/` | QA | QA Mgr |
| 16 | `docs-manager/` | Docs | Gatekeeper |
| 17 | `browser-automation/` | Infra | Service |
| 18 | `devops-expert/` | Infra | Gatekeeper |
| 19 | `kubernetes-expert/` | Infra | DevOps |
| 20 | `event-system-expert/` | Arch | Gatekeeper |
| 21 | `api-schema-expert/` | Arch | Gatekeeper |
| 22 | `testability-expert/` | QA | QA Mgr |
| 23 | `code-quality-expert/` | Quality | Gatekeeper |
| 24 | `validation-expert/` | QA | QA Mgr |
| 25 | `systematic-debugger/` 🆕 | Cross | Any Agent |
| 26 | `spec-reviewer/` 🆕 | Quality | Gatekeeper |
| 27 | `git-workflow-manager/` 🆕 | Infra | Gatekeeper |
| 28 | `security-auditor/` 🆕 | Security | Gatekeeper |
| 29 | `performance-optimizer/` 🆕 | Perf | Gatekeeper |
| 30 | `accessibility-expert/` 🆕 | A11y | QA Mgr |

---

## Feature Lifecycle

```
 1. BACKLOG       ← Product Owner
 2. SPRINT_GOAL   ← Scrum Master
 3. GOAL.md       ← Gatekeeper
 4. SPEC REVIEW   ← Spec Reviewer 🆕
 5. PRD           ← Orchestrator
 6. API_SPEC      ← API Schema Expert
 7. RESEARCH      ← Stack Researcher
 8. UX_SPEC       ← UX Researcher
 9. DESIGN_SPEC   ← Design Architect
10. VALIDATION    ← Validation Expert
11. BRANCH        ← Git Workflow Manager 🆕
12. CODE          ← Frontend + Backend Builder
13. SECURITY      ← Security Auditor 🆕
14. PERFORMANCE   ← Performance Optimizer 🆕
15. ACCESSIBILITY ← Accessibility Expert 🆕
16. QA            ← QA Orchestrator (Unit/E2E/Design/UX)
17. QUALITY GATE  ← Code Quality Expert
18. DOCS          ← Docs Manager
19. MERGE         ← Git Workflow Manager 🆕
20. DEPLOY        ← DevOps → K8s Expert
21. SCORECARD     ← Orchestrator → PO
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
