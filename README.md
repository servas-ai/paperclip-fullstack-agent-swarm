# 🤖 Paperclip Fullstack Agent Swarm

> **30 specialized AI agents** for end-to-end software development — from idea to deploy.

[![Agents](https://img.shields.io/badge/Agents-30-blue)]() [![Skills](https://img.shields.io/badge/Skills-23+-green)]() [![Skill_Sources](https://img.shields.io/badge/Skill_Sources-17_Repos-orange)]() [![Methodology](https://img.shields.io/badge/Methodology-superpowers+impeccable-blueviolet)]()

---

## ⚡ What Is This?

A multi-agent system where **30 AI agents** collaborate to plan, design, build, test, secure, and deploy software. Each agent has its own persona, expertise, and workflow — defined by 4 configuration files.

**Not a generic chatbot. Every agent is a specialist.**

```
User provides feature goal → 30 agents deliver production-ready software
```

### Key Differentiators

| | What | Why It Matters |
|-|------|---------------|
| 🎯 | [obra/superpowers](https://github.com/obra/superpowers) | TDD Iron Law, 4-Phase Debugging, Verification Evidence |
| 🎨 | [pbakaus/impeccable](https://github.com/pbakaus/impeccable) | OKLCH colors, 4pt grid, AI Slop Test (16 anti-patterns) |
| 🛡️ | Anti-Hallucination Protocol | Every agent self-checks + peer-verifies before delivery |
| 🔌 | [skills.sh](https://skills.sh) | 23+ skills from 17 open-source repositories |

---

## 🏗️ Architecture

> **Note:** Paperclip handles task dispatch, issue assignment, and status tracking natively via its API.
> The hierarchy below shows **expertise flow** — who informs whom, not who "commands" whom.

```mermaid
graph TD
    CEO["👔 CEO<br/>Strategic Vision"]

    PO["📋 Product Owner<br/>Backlog + Priorities"]
    SM["🏃 Scrum Master<br/>Sprint Cadence"]
    AG["🏛️ Gatekeeper<br/>HARD-GATE"]

    CEO --> PO
    CEO --> AG
    PO <--> SM

    %% Gatekeeper approves, then Orchestrator runs the pipeline
    FO["🎯 Feature Orchestrator<br/>21-Step Pipeline"]
    AG --> FO

    %% Pre-Build: Research & Spec
    SPR["📋 Spec Reviewer"]
    SR["🔬 Stack Researcher"]
    AG --> SPR
    AG --> SR

    %% Design Phase
    UX["🧪 UX Researcher"]
    DA["🎨 Design Architect"]
    FO --> UX --> DA

    %% Build Phase
    FB["⚛️ Frontend Builder"]
    BB["🗄️ Backend Builder"]
    FO --> FB
    FO --> BB

    %% Backend sub-specialists
    ES["📡 Event System"]
    API["📐 API Schema"]
    BB --- ES
    BB --- API

    %% Quality Gates (after Build)
    SA["🔒 Security Auditor"]
    PF["⚡ Performance Opt."]
    AE["♿ Accessibility"]
    FO --> SA
    FO --> PF
    FO --> AE

    %% QA Pipeline
    QA["🧪 QA Orchestrator<br/>5-Layer Pipeline"]
    FO --> QA
    UT["Unit Tests"]
    DAU["Design Audit"]
    E2E["E2E + Browser"]
    VE["Validation"]
    QA --> UT
    QA --> DAU
    QA --> E2E
    QA --> VE

    %% Cross-cutting (available to all)
    SD["🔍 Debugger"]
    CQ["✅ Code Quality"]
    GW["🌿 Git Workflow"]
    DO["⚙️ DevOps + K8s"]
    DM["📚 Docs Manager"]

    AG --> SD
    AG --> CQ
    AG --> DO
    AG --> GW
    AG --> DM

    %% Styling
    style CEO fill:#4A90D9,color:#fff
    style AG fill:#E74C3C,color:#fff
    style FO fill:#F39C12,color:#fff
    style QA fill:#27AE60,color:#fff
    style SA fill:#8E44AD,color:#fff
    style PO fill:#4A90D9,color:#fff
```

**What Paperclip handles natively** (no custom Markdown files needed):
- ✅ Task assignment → `PATCH /api/issues/{id}` (status: todo → in_progress → done)
- ✅ Agent-to-agent handoff → Issue reassignment
- ✅ Status tracking → Issue status field
- ✅ Crash recovery → Paperclip knows which issues are `in_progress`

**What agents add on top** (design artifacts, not status):
- `GOAL.md`, `PRD.md`, `UX_SPEC.md`, `DESIGN_SPEC.md` → Design documents
- `TEST_REPORT.md`, `SECURITY_AUDIT.md`, `A11Y_AUDIT.md` → Quality reports
- `SYSTEM_STATE.md`, `MEMORY.md` → Persistent knowledge

---

## 🔄 Feature Lifecycle (20 Steps)

```mermaid
graph LR
    subgraph Planning
        B["1. Backlog"] --> G["2. Goal"] --> SP["3. Spec Review"] --> PRD["4. PRD"]
    end

    subgraph Design
        PRD --> API["5. API Spec"] --> R["6. Research"] --> UX["7. UX Spec"] --> DS["8. Design Spec"] --> V["9. Validation"]
    end

    subgraph Build
        V --> BR["10. Branch"] --> CODE["11. Code"] --> SEC["12. Security"] --> PERF["13. Perf."] --> A11Y["14. A11y"]
    end

    subgraph Delivery
        A11Y --> QA["15. QA"] --> QG["16. Quality"] --> DOC["17. Docs"] --> MG["18. Merge"] --> DEP["19. Deploy"] --> SC["20. Done"]
    end

    style Planning fill:#E8F4FD,stroke:#4A90D9
    style Design fill:#FEF9E7,stroke:#F39C12
    style Build fill:#FDEDEC,stroke:#E74C3C
    style Delivery fill:#E8F8F5,stroke:#27AE60
```

---

## 👥 All 30 Agents

### 🔵 Leadership & Strategy (4)
| Agent | Superpower |
|-------|-----------|
| CEO | Strategic HARD-GATE, P0-P3 Decision Framework |
| Product Owner | Brainstorming, Bite-Sized Writing Plans |
| Scrum Master | Subagent-Driven Development, Sprint Cadence |
| Architecture Gatekeeper | HARD-GATE, Design-for-Isolation, YAGNI |

### 🟢 Design & Research (3)
| Agent | Superpower |
|-------|-----------|
| UX Researcher | Nielsen's 10 Heuristics, Optimistic UI |
| Design Architect | OKLCH, 4pt Grid, AI Slop Test |
| Stack Researcher | Context7, Firecrawl, `skills search` |

### 🟡 Build (3)
| Agent | Superpower |
|-------|-----------|
| Feature Orchestrator | 21-Step Lifecycle, Subagent Dispatch |
| Frontend Builder | TDD Iron Law, React 19, Impeccable Design |
| Backend Builder | Contract-First TDD, Drizzle ORM, RLS |

### 🔴 Quality & Testing (8)
| Agent | Superpower |
|-------|-----------|
| QA Orchestrator | 5-Layer Test Pipeline, Parallel Dispatch |
| Unit Test Writer | RED-GREEN-REFACTOR, Vitest |
| Design Auditor | 16-Point AI Slop Audit, 3 Viewports |
| E2E Tester | Playwright, Network Tab, Console Monitoring |
| VM Tester | Native App Testing, Desktop Automation |
| Testability Expert | 5 Testing Anti-Patterns |
| Validation Expert | Zod Fortress, OWASP Input Validation |
| Code Quality Expert | Pre-Review Checklist, SOLID |

### 🟣 Infrastructure & Architecture (6)
| Agent | Superpower |
|-------|-----------|
| DevOps Expert | CI/CD, Docker, GitHub Actions |
| Kubernetes Expert | Helm, Health Probes, NetworkPolicies |
| Browser Automation | agent-browser, Network/Console/Diff/Eval |
| Docs Manager | Documentation-as-Code, Clear Writing |
| Event-System Expert | Supabase Realtime, Idempotency |
| API Schema Expert | Contract-First TDD, Zod Schemas |

### 🔶 Specialists (6)
| Agent | Deliverable | Superpower |
|-------|-------------|-----------|
| 🔍 Systematic Debugger | `ROOT_CAUSE.md` | 4-Phase Debugging, Chain-of-Thought |
| 📋 Spec Reviewer | `SPEC_REVIEW.md` | 5-Category Review, Self-Refinement |
| 🌿 Git Workflow Manager | `BRANCH_STATUS.md` | Worktree Lifecycle, Commit Discipline |
| 🔒 Security Auditor | `SECURITY_AUDIT.md` | OWASP Top 10, ReAct Protocol |
| ⚡ Performance Optimizer | `PERFORMANCE_REPORT.md` | Core Web Vitals, Bundle Analysis |
| ♿ Accessibility Expert | `A11Y_AUDIT.md` | WCAG 2.1 POUR (50+ Criteria) |

---

## 🔧 Embedded Skills (23)

All skills are **inline in each agent's `TOOLS.md`** — no external loading required at runtime.

### Core Methodology — [obra/superpowers](https://github.com/obra/superpowers)

| # | Skill | What It Does | Used By |
|---|-------|-------------|---------|
| 1 | `systematic-debugging` | 4-Phase: Root Cause → Pattern → Hypothesis → Fix | All agents |
| 2 | `test-driven-development` | RED → GREEN → REFACTOR. No code without failing test | Unit Test, Builders |
| 3 | `verification-before-completion` | 5-step gate: Identify → Run → Read → Verify → Claim | All agents |
| 4 | `writing-plans` | Zero-context bite-sized tasks, checkbox syntax | Gatekeeper, Orchestrator |
| 5 | `executing-plans` | Load → Execute → Finish. STOP at blockers | Builders |
| 6 | `brainstorming` | Socratic refinement: 1 question → 2-3 approaches → spec | Gatekeeper, UX |
| 7 | `subagent-driven-development` | Fresh subagent per task: Implement → Spec Review → Quality Review | Orchestrator |
| 8 | `dispatching-parallel-agents` | Identify independent tasks → dispatch parallel → integrate | Orchestrator, QA |
| 9 | `finishing-a-development-branch` | Verify → Merge → Cleanup worktree | Builders |
| 10 | `requesting-code-review` | After each task: SHAs → dispatch reviewer → fix critical | Builders, QA |
| 11 | `receiving-code-review` | READ → UNDERSTAND → VERIFY → EVALUATE → IMPLEMENT | Builders |
| 12 | `using-git-worktrees` | `git worktree add` for feature isolation | Git Workflow, Builders |
| 13 | `using-superpowers` | Priority: User > Skills > System Prompt | All agents |

### Frontend & Design — [vercel-labs](https://skills.sh) + [anthropics](https://github.com/anthropics/skills) + [pbakaus](https://github.com/pbakaus/impeccable)

| # | Skill | What It Does | Used By |
|---|-------|-------------|---------|
| 14 | `vercel-react-best-practices` | `Promise.all()`, no barrel files, Server Components default | Frontend Builder |
| 15 | `web-design-guidelines` | Vercel design rules, fetch + validate against guidelines | Design Auditor |
| 16 | `frontend-design` | Typography (no system fonts), color (dominant + accents), motion | Design Architect |
| 17 | `agent-browser` | Network tab, console errors, diff, eval, semantic locators | E2E, Browser, Auditor |
| 18 | `next-best-practices` | App Router, `loading.tsx` + `error.tsx`, Metadata API | Frontend Builder |
| 19 | `ui-ux-pro-max` | Contrast ≥4.5:1, touch ≥44px, focus rings, `prefers-reduced-motion` | UX, Design Architect |
| 20 | `webapp-testing` | Server tests → `curl`, visual tests → `agent-browser` | E2E, QA |
| 21 | `impeccable` | OKLCH, 4pt grid, exponential easing, AI Slop Test | Design Architect, Auditor, Frontend |

### Specialized

| # | Skill | What It Does | Used By |
|---|-------|-------------|---------|
| 22 | `supabase-postgres` | RLS, indexes on FKs, enums, prepared statements | Backend Builder |
| 23 | `context7` | Fetch latest version-specific docs for any library | Stack Researcher |

### Skill Workflow (Superpowers → Agent Pipeline)

```
brainstorming → writing-plans → subagent-driven-dev → test-driven-dev → requesting-review → finishing-branch
    ↓               ↓                 ↓                     ↓                  ↓                  ↓
Gatekeeper    Orchestrator        Orchestrator          Unit Test           QA Orch            Builders
  + UX           + Gate           → Builder + QA         + Builders         → Reviewer        → Gatekeeper
```

Always active: `systematic-debugging` (on bugs) · `verification-before-completion` (before delivery)

---

## 🧠 Methodology

### Superpowers ([obra/superpowers](https://github.com/obra/superpowers))

| Principle | Description | Used by |
|-----------|------------|---------|
| 🔴 TDD Iron Law | No code without a failing test first | 8 agents |
| 🔍 4-Phase Debugging | Root Cause → Pattern → Hypothesis → Fix | 15 agents |
| 🚫 HARD-GATE | No code without design approval | 4 agents |
| ✅ Verification Evidence | Proof before claims — always | 20 agents |
| 👥 Subagent-Driven Dev | Fresh subagent per task, two-stage review | 5 agents |
| 🌿 Git Worktrees | Branch isolation via worktrees | 4 agents |

### Impeccable Design ([pbakaus/impeccable](https://github.com/pbakaus/impeccable))
- **OKLCH** Color System with tinted neutrals (no pure black/white)
- **4pt Grid** Spacing (not 8pt — more granular control)
- **Exponential Easing** only (no bounce, no generic `ease`)
- **AI Slop Test** — 16-point audit to avoid generic AI aesthetics

### Advanced Reasoning
| Technique | When | Agent Example |
|-----------|------|--------------|
| Chain-of-Thought | Complex decisions | Debugger: 8-step CoT |
| ReAct | Exploratory tasks | Security Auditor: Reason → Attack → Analyze |
| Self-Refinement | Before delivery | Spec Reviewer: 4-question loop |
| Few-Shot | Teaching | Accessibility Expert: Bad→Good diffs |

---

## 🔧 Skill Sources (17 Repositories)

```bash
skills search "systematic-debugging"
skills install systematic-debugging
```

| Repository | Key Skills | Installs |
|-----------|-----------|----------|
| [obra/superpowers](https://github.com/obra/superpowers) | TDD, Debugging, Plans, Verification, Code Review, Git | 14K–50K |
| [vercel-labs](https://skills.sh) | React, Design Guidelines, Browser, Next.js | 32K–199K |
| [anthropics/skills](https://github.com/anthropics/skills) | Frontend Design, Canvas, Webapp Testing | 17K–145K |
| [pbakaus/impeccable](https://github.com/pbakaus/impeccable) | OKLCH, Grid, Motion, AI Slop Test | — |
| [supabase/agent-skills](https://github.com/supabase/agent-skills) | Postgres Best Practices, RLS | 32K |
| [am-will/codex-skills](https://github.com/am-will/codex-skills) | Context7 (latest docs fetcher) | 12K |
| [currents-dev](https://skills.sh) | Playwright Best Practices | 8K |
| [coreyhaines31](https://skills.sh) | Competitor/Alternatives Analysis | 16K |
| [supercent-io](https://github.com/supercent-io/agent-skills) | Security, Code Review, Design System | 11K |
| [browser-use](https://skills.sh) | Advanced Browser Automation | 48K |
| [nextlevelbuilder](https://skills.sh) | UI/UX Pro Max | 56K |
| [squirrelscan](https://skills.sh) | Audit Website | 34K |
| + 5 more repos | Additional skills | 8K–128K |

> Full registry with URLs: [`agents/SHARED_CONFIG.md`](agents/SHARED_CONFIG.md)

---

## 🛡️ Core Principles

| # | Principle | Description |
|---|-----------|-------------|
| 1 | **Goal Check** | Every agent reads GOAL.md first |
| 2 | **Evidence First** | Proof before assertions |
| 3 | **Circuit Breaker** | Max 3 iterations, then escalate |
| 4 | **Error Recovery** | Self → Peer → Gatekeeper (3-tier) |
| 5 | **Anti-Hallucination** | STOP-CHECK-DELIVER before every delivery |
| 6 | **Mandated Stack** | Next.js 15 · React 19 · shadcn · Tailwind 4 |
| 7 | **Contract-First** | API schema before implementation |
| 8 | **Security Gate** | OWASP Top 10 before deploy |
| 9 | **Performance Budget** | LCP < 2.5s, Bundle < 200KB |
| 10 | **WCAG 2.1 AA** | 50+ accessibility criteria |

---

## 🏗️ Tech Stack

| Layer | Technology |
|-------|-----------|
| Framework | Next.js 15 (App Router) |
| UI | React 19 + shadcn/ui |
| Styling | Tailwind CSS 4 |
| State | Zustand + TanStack React Query |
| Validation | Zod |
| ORM | Drizzle ORM |
| Database | Supabase (PostgreSQL) |
| Testing | Vitest + Playwright |
| CI/CD | GitHub Actions + Docker |
| Orchestration | Kubernetes + Helm |
| Agent Runtime | OpenCode (Paperclip) |

---

## 📁 Project Structure

```
agents/
├── AGENTS_OVERVIEW.md     ← All 30 agents with hierarchy
├── SHARED_CONFIG.md       ← Global rules, skill registry, anti-hallucination
├── SKILLS.md              ← Skill reference & discovery
├── REPORTING_PROTOCOL.md  ← Status reporting
│
└── [agent-name]/          ← 30 folders, 4 files each:
    ├── SOUL.md            ← Persona, anti-patterns, reasoning
    ├── AGENTS.md          ← Role, scope, workflow
    ├── TOOLS.md           ← Skills (inline), commands
    └── HEARTBEAT.md       ← Checklists, red flags
```

| Metric | Value |
|--------|-------|
| Agent Folders | 30 |
| Config Files | 124 |
| Skill Sources | 17 Repositories |
| Embedded Skills | 23 |

---

## 📚 Documentation

| File | Contents |
|------|---------|
| [AGENTS_OVERVIEW.md](agents/AGENTS_OVERVIEW.md) | Agent hierarchy, full list, lifecycle |
| [SHARED_CONFIG.md](agents/SHARED_CONFIG.md) | Global rules, stack, skill registry |
| [SKILLS.md](agents/SKILLS.md) | Skill discovery & top 23 reference |
| [REPORTING_PROTOCOL.md](agents/REPORTING_PROTOCOL.md) | Status reporting templates |

---

## License

MIT

---

<p align="center">
  Built by <a href="https://github.com/servas-ai">servas.ai</a> · Powered by <a href="https://github.com/obra/superpowers">superpowers</a> + <a href="https://github.com/pbakaus/impeccable">impeccable</a> + <a href="https://skills.sh">skills.sh</a>
</p>
