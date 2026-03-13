# SKILLS.md — Skill Reference

> Letzte Aktualisierung: 2026-03-13
> Skill-Wissen ist **inline in jeder Agent-TOOLS.md** eingebettet.
> Dieses File ist die Kurzreferenz für alle Skills + Download-Infos.
> Skill-Quellen mit URLs: siehe `SHARED_CONFIG.md`

---

## Skill Discovery

```bash
skills search "<thema>"
skills install <skill-name>
# Oder: curl -sL https://raw.githubusercontent.com/obra/superpowers/main/skills/<name>/SKILL.md
```

---

## Top 23 Skills — Kurzreferenz

### Superpowers (obra) — Kern-Methodik

| Skill | Kern-Regel | Agents |
|-------|-----------|--------|
| `systematic-debugging` | 4 Phasen: Root Cause → Pattern → Hypothesis → Fix. **Kein Fix ohne Root Cause.** | Alle |
| `test-driven-development` | RED → Verify RED → GREEN → Verify GREEN → REFACTOR. Ein Behavior pro Test. | Unit Test Writer, Builder |
| `verification-before-completion` | 5-Step Gate: Identify → Run → Read → Verify → Claim. **Kein "done" ohne Beweis.** | Alle |
| `writing-plans` | Zero-Context, Bite-Sized Tasks (2-5min), File Structure zuerst, Checkbox Syntax. | Gatekeeper, Orchestrator |
| `executing-plans` | Load → Execute (in_progress → completed) → Finish. STOP bei Blockern. | Builder |
| `brainstorming` | Socratic Refinement: 1 Frage/Msg → 2-3 Ansätze → Design → Spec → Review. | Gatekeeper, UX |
| `subagent-driven-development` | Pro Task: Implementer → Spec-Review → Code-Quality-Review (3 Runden). | Orchestrator |
| `dispatching-parallel-agents` | Identify Independent → Create Tasks → Dispatch Parallel → Review & Integrate. | Orchestrator, QA |
| `finishing-a-development-branch` | Verify Tests → Base Branch → Merge Options → Execute → Cleanup Worktree. | Builder |
| `requesting-code-review` | Nach jeder Task: SHAs → Reviewer dispatchen → Critical sofort fixen. | Builder, QA |
| `receiving-code-review` | READ → UNDERSTAND → VERIFY → EVALUATE → RESPOND → IMPLEMENT. Kein "Great point!" | Builder |
| `using-git-worktrees` | Feature-Isolation: `git worktree add ../wt-<name> -b feat/<name>` | Git WF Mgr, Builder |
| `using-superpowers` | Priority: User Instructions > Skills > System Prompt. | Alle |

### Vercel Labs / skills.sh — Frontend & Design

| Skill | Kern-Regel | Agents |
|-------|-----------|--------|
| `vercel-react-best-practices` | `Promise.all()`, keine Barrel Files, `next/dynamic`, Server Components default. | Frontend Builder |
| `web-design-guidelines` | Fetch Guidelines von Vercel → Prüfe gegen alle Rules → Output `file:line`. | Design Auditor |
| `frontend-design` | Typography: nie System Fonts. Color: Dominant + Akzente. Motion: Staggered. | Design Architect |
| `agent-browser` | `open` → `snapshot -i` → `screenshot` → `set viewport` → `close`. | E2E, Design Auditor |
| `next-best-practices` | App Router, Server Components, `loading.tsx` + `error.tsx`, Metadata API. | Frontend Builder |
| `ui-ux-pro-max` | Kontrast ≥4.5:1, Touch ≥44px, Focus Ring, Heading Hierarchy, `prefers-reduced-motion`. | Design Architect |
| `webapp-testing` | Server Tests → `curl`. Visual Tests → `agent-browser`. Recon-Then-Action. | E2E, QA |

### Spezialisiert

| Skill | Kern-Regel | Agents |
|-------|-----------|--------|
| `supabase-postgres` | RLS immer an, Indexes auf FKs, Enums, Prepared Statements, PgBouncer. | Backend Builder |
| `typescript-advanced-types` | Discriminated Unions, Generics, `satisfies`, Type Guards, Utility Types. | Frontend Builder |

---

## Superpowers Workflow → Agent Mapping

```
1. brainstorming        → Gatekeeper + UX Researcher
2. using-git-worktrees  → Git Workflow Manager
3. writing-plans        → Gatekeeper → Orchestrator
4. subagent-driven-dev  → Orchestrator → Builder + QA
5. test-driven-dev      → Unit Test Writer + Builder
6. requesting-review    → Orchestrator → Reviewer
7. finishing-branch     → Builder → Gatekeeper
```

Immer aktiv: `systematic-debugging` (bei Bugs) · `verification-before-completion` (vor Abgabe)

---

## Context Loading Order

```
1. GOAL.md          → Was ist das Ziel?
2. SYSTEM_STATE.md  → Was existiert?
3. MEMORY.md        → Was haben wir gelernt?
4. SHARED_CONFIG.md → Stack, Rules
5. Own TOOLS.md     → Agent-spezifische Skills
```
