# 🤖 Paperclip AI Agent System

> **30 KI-Agents** für vollständige Software-Entwicklung — Idee bis Deploy.

---

## Quick Start

Jeder Agent hat 4 Dateien: `SOUL.md` (Persona) · `AGENTS.md` (Rolle) · `TOOLS.md` (Skills) · `HEARTBEAT.md` (Checkliste)

Globale Regeln: `SHARED_CONFIG.md` · Agent-Übersicht: `AGENTS_OVERVIEW.md`

---

## Architektur

```
CEO → Product Owner → Scrum Master
  └→ Architecture Gatekeeper
       ├→ Feature Orchestrator → UX → Design → Build → QA → Docs → Deploy
       ├→ Stack Researcher, Code Quality, Docs Manager
       ├→ DevOps → K8s, Git Workflow, Performance
       └→ Security Auditor, Spec Reviewer
```

---

## 30 Agents nach Bereich

### Leadership
CEO · Product Owner · Scrum Master · Architecture Gatekeeper

### Design & Research
UX Researcher · Design Architect · Stack Researcher

### Build
Feature Orchestrator · Frontend Builder · Backend Builder

### Quality & Testing
QA Orchestrator · Unit Test Writer · Design Auditor · E2E Tester · VM Tester · Testability Expert · Validation Expert · Code Quality Expert

### Infrastructure
DevOps Expert · Kubernetes Expert · Browser Automation · Docs Manager

### Specialists 🆕
Systematic Debugger · Spec Reviewer · Git Workflow Manager · Security Auditor · Performance Optimizer · Accessibility Expert

---

## Feature Lifecycle (21 Schritte)

```
BACKLOG → GOAL → SPEC REVIEW → PRD → API_SPEC → RESEARCH
→ UX_SPEC → DESIGN_SPEC → VALIDATION → BRANCH → CODE
→ SECURITY → PERFORMANCE → ACCESSIBILITY → QA → QUALITY GATE
→ DOCS → MERGE → DEPLOY → SCORECARD
```

---

## Methodik

| Quelle | Technik |
|--------|---------|
| [obra/superpowers](https://github.com/obra/superpowers) | TDD, 4-Phase Debugging, Verification Evidence |
| [pbakaus/impeccable](https://github.com/pbakaus/impeccable) | OKLCH, 4pt Grid, AI Slop Test |
| [skills.sh](https://skills.sh) | 60+ Skills aus 17 Repositories |

---

## Tech Stack

Next.js 15 · React 19 · shadcn/ui · Tailwind 4 · Zustand · Zod · Drizzle · Supabase · Vitest · Playwright

---

## Kern-Prinzipien

1. **Goal Check** — GOAL.md lesen als erstes
2. **Evidence first** — Beweise vor Behauptungen
3. **TDD** — Kein Code ohne failing test
4. **HARD-GATE** — Kein Code ohne Design-Approval
5. **Circuit Breaker** — Max 3 Iterationen, dann eskalieren
6. **Error Recovery** — Selbst → Peer → Gatekeeper

---

📚 Detaillierte Agent-Liste: [AGENTS_OVERVIEW.md](AGENTS_OVERVIEW.md) · Regeln: [SHARED_CONFIG.md](SHARED_CONFIG.md) · Skills: [SKILLS.md](SKILLS.md)
