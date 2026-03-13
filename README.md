# 🤖 Paperclip Fullstack Agent Swarm

> **30 specialized AI agents** for end-to-end software development — from idea to deploy.

[![Agents](https://img.shields.io/badge/Agents-30-blue)]() [![Skills](https://img.shields.io/badge/Skills-60+-green)]() [![Skill_Sources](https://img.shields.io/badge/Skill_Sources-17_Repos-orange)]() [![Lines](https://img.shields.io/badge/Config-12.9K_Lines-purple)]()

---

## ⚡ What Is This?

A multi-agent system where **30 AI agents** collaborate to plan, design, build, test, secure, and deploy software. Each agent has its own persona, expertise, and workflow — defined by 4 configuration files.

**Not a generic chatbot. Every agent is a specialist.**

```
User provides feature goal → 30 agents deliver production-ready software
```

Built on [obra/superpowers](https://github.com/obra/superpowers) + [pbakaus/impeccable](https://github.com/pbakaus/impeccable) methodology.

---

## 🏗️ Architecture

```
                    ┌─────────┐
                    │   CEO   │ Strategic Vision
                    └────┬────┘
                         │
              ┌──────────┼──────────┐
              │                     │
     ┌────────┴────────┐   ┌───────┴──────────┐
     │ Product Owner   │   │ Architecture &   │
     │ + Scrum Master  │   │ Quality Gatekeeper│
     └────────┬────────┘   └───────┬──────────┘
              │                     │
     ┌────────┴────────┐   ┌───────┴──────────────────────────────────┐
     │ Spec Reviewer   │   │ Stack Researcher · Code Quality Expert  │
     │ (Pre-Code Gate) │   │ Docs Manager · DevOps · K8s Expert      │
     └─────────────────┘   │ Git Workflow Mgr · Security Auditor     │
                           └───────┬──────────────────────────────────┘
                                   │
                    ┌──────────────┴──────────────┐
                    │   Feature Orchestrator      │
                    │   (Feature-Lifecycle-Engine) │
                    └────┬────────────────────┬───┘
                         │                    │
         ┌───────────────┤    ┌───────────────┤
         │               │    │               │
    ┌────┴────┐    ┌─────┴──┐│  ┌────────────┴┐
    │ UX      │    │ Design ││  │ Frontend    │
    │ Research│    │ Archit.││  │ Builder     │
    └─────────┘    └────────┘│  └─────────────┘
                        ┌────┴────────┐
                        │ Backend     │
                        │ Builder     │
                        └─────────────┘
                              │
              ┌───────────────┴───────────────┐
              │       QA Orchestrator         │
              │   (5-Layer Test Pipeline)     │
              └───┬───┬───┬───┬───┬───┬───┬───┘
                  │   │   │   │   │   │   │
                 UT  DA  E2E  VM  TE  VE  AE
```

**Legend**: UT=Unit Test Writer, DA=Design Auditor, E2E=E2E Tester, VM=VM Tester, TE=Testability Expert, VE=Validation Expert, AE=Accessibility Expert

---

## 👥 All 30 Agents

### 🔵 Leadership & Strategy (4)
| Agent | Codename | Superpower |
|-------|----------|-----------|
| CEO | Chief Strategy Officer | Strategic HARD-GATE, P0-P3 Decision Framework |
| Product Owner | Product Owner | Brainstorming, Bite-Sized Writing Plans |
| Scrum Master | Sprint Commander | Subagent-Driven Development, Sprint Cadence |
| Architecture Gatekeeper | Quality Gatekeeper | HARD-GATE, Design-for-Isolation, YAGNI |

### 🟢 Design & Research (3)
| Agent | Codename | Superpower |
|-------|----------|-----------|
| UX Researcher | UX Researcher | Nielsen's 10 Heuristics, Optimistic UI |
| Design Architect | Visual Architect | OKLCH, 4pt Grid, AI Slop Test |
| Stack Researcher | Stack Researcher | Context7, Firecrawl, `skills search` |

### 🟡 Build (3)
| Agent | Codename | Superpower |
|-------|----------|-----------|
| Feature Orchestrator | Feature Orchestrator | 21-Step Feature Lifecycle, Subagent Dispatch |
| Frontend Builder | Frontend Builder | TDD Iron Law, React 19, Impeccable Design |
| Backend Builder | Backend Builder | Contract-First TDD, Drizzle ORM, RLS |

### 🔴 Quality & Testing (8)
| Agent | Codename | Superpower |
|-------|----------|-----------|
| QA Orchestrator | QA Manager | 5-Layer Test Pipeline, Parallel Dispatch |
| Unit Test Writer | Test Writer | RED-GREEN-REFACTOR, Vitest |
| Design Auditor | Design Auditor | 16-Point AI Slop Audit, 3 Viewports |
| E2E Tester | E2E Tester | Playwright, User Journey Testing |
| VM Tester | VM Tester | Native App Testing, Desktop Automation |
| Testability Expert | Testability Expert | 5 Testing Anti-Patterns |
| Validation Expert | Validation Expert | Zod Fortress, OWASP Input Validation |
| Code Quality Expert | Code Quality Expert | Pre-Review Checklist, SOLID |

### 🟣 Infrastructure (4)
| Agent | Codename | Superpower |
|-------|----------|-----------|
| DevOps Expert | DevOps Expert | CI/CD, Docker, GitHub Actions |
| Kubernetes Expert | K8s Expert | Helm, Health Probes, NetworkPolicies |
| Browser Automation | Browser Runtime | agent-browser, Headless Chrome |
| Docs Manager | Docs Manager | Documentation-as-Code, Clear Writing |

### 🔶 Skill-Based Specialists (6) — NEW
| Agent | Codename | Deliverable | Superpower |
|-------|----------|-------------|-----------|
| 🔍 Systematic Debugger | Root Cause Hunter | `ROOT_CAUSE.md` | 4-Phase Debugging, Chain-of-Thought |
| 📋 Spec Reviewer | Quality Gate Keeper | `SPEC_REVIEW.md` | 5-Category Review, Self-Refinement |
| 🌿 Git Workflow Manager | Branch Shepherd | `BRANCH_STATUS.md` | Worktree Lifecycle, Commit Discipline |
| 🔒 Security Auditor | Red Team | `SECURITY_AUDIT.md` | OWASP Top 10, ReAct Protocol |
| ⚡ Performance Optimizer | Speed Demon | `PERFORMANCE_REPORT.md` | Core Web Vitals, Bundle Analysis |
| ♿ Accessibility Expert | A11y Guardian | `A11Y_AUDIT.md` | WCAG 2.1 POUR (50+ Criteria) |

### 🏛️ Architecture (2)
| Agent | Codename | Superpower |
|-------|----------|-----------|
| Event-System Expert | Event Expert | Supabase Realtime, Idempotency |
| API Schema Expert | API Expert | Contract-First TDD, Zod Schemas |

---

## 🔄 Feature Lifecycle (21 Steps)

```
 1. BACKLOG      ← Product Owner
 2. SPRINT_GOAL  ← Scrum Master
 3. GOAL.md      ← Gatekeeper
 4. SPEC REVIEW  ← Spec Reviewer          ← 🆕
 5. PRD          ← Feature Orchestrator
 6. API_SPEC     ← API Schema Expert
 7. RESEARCH     ← Stack Researcher
 8. UX_SPEC      ← UX Researcher
 9. DESIGN_SPEC  ← Design Architect
10. VALIDATION   ← Validation Expert
11. BRANCH SETUP ← Git Workflow Manager    ← 🆕
12. CODE         ← Frontend + Backend Builder
    └── DEBUG    ← Systematic Debugger     ← 🆕
13. SECURITY     ← Security Auditor        ← 🆕
14. PERFORMANCE  ← Performance Optimizer   ← 🆕
15. ACCESSIBILITY← Accessibility Expert    ← 🆕
16. QA REPORT    ← QA Orchestrator (5 Layers)
17. QUALITY GATE ← Code Quality Expert
18. DOCS         ← Docs Manager
19. BRANCH MERGE ← Git Workflow Manager    ← 🆕
20. DEPLOY       ← DevOps → Kubernetes Expert
21. SCORECARD    ← Orchestrator → PO (Acceptance)
```

---

## 🧠 Methodology

### Superpowers (obra/superpowers)
Core methodology for all 30 agents:

| Principle | Description | Agents |
|-----------|------------|--------|
| 🔴 TDD Iron Law | No code without a failing test first | 8 Agents |
| 🔍 4-Phase Debugging | Root Cause → Pattern → Hypothesis → Fix | 15 Agents |
| 🚫 HARD-GATE | No code without design approval | 4 Agents |
| ✅ Verification Evidence | Proof before claims | 20 Agents |
| 👥 Subagent-Driven Dev | Fresh subagent per task, two-stage review | 5 Agents |
| 🌿 Git Worktrees | Branch isolation via worktrees | 4 Agents |

### Impeccable Design (pbakaus/impeccable)
Anti-AI-Slop design for Design Architect, Design Auditor, Frontend Builder:
- OKLCH Color System with tinted neutrals
- 4pt Grid Spacing
- Exponential Easing (no generic animations)
- 16-Point AI Slop Audit

### Advanced Reasoning (all agents)
| Technique | When | Example |
|-----------|------|---------|
| Chain-of-Thought | Complex decisions | Debugger: 8-step CoT |
| ReAct | Exploratory tasks | Security Auditor: Reason → Attack → Analyze |
| Self-Refinement | Before every delivery | Spec Reviewer: 4-question loop |
| Few-Shot | Teaching situations | Accessibility Expert: Bad→Good diffs |

---

## 🔧 Skill Sources

Skills come from **17 repositories** and are loaded via:

```bash
# 1. skills.sh CLI (recommended)
skills search "systematic-debugging"
skills install systematic-debugging

# 2. GitHub Raw Download
curl -sL https://github.com/obra/superpowers/tree/main/skills/systematic-debugging/SKILL.md

# 3. Skill Registry → SHARED_CONFIG.md
```

Top repositories:
| Repository | Skills | Installs |
|-----------|--------|----------|
| [obra/superpowers](https://github.com/obra/superpowers) | 13 Skills (TDD, Debug, Plans, Review...) | 14K–50K |
| [vercel-labs](https://skills.sh) | 10 Skills (React, Design, Browser...) | 32K–199K |
| [anthropics/skills](https://github.com/anthropics/skills) | 4 Skills (Frontend Design, Testing...) | 17K–145K |
| [pbakaus/impeccable](https://github.com/pbakaus/impeccable) | Design Aesthetics | — |
| + 13 more repos | 30+ Skills | 8K–128K |

> Full Skill Registry with download URLs: see `agents/SHARED_CONFIG.md`

---

## 📁 File Structure

```
workspace/
├── SYSTEM_STATE.md          # Current system state
├── MEMORY.md                # Learned patterns & gotchas
│
└── agents/                  # Agent configurations
    ├── README.md            # Agent-level overview
    ├── AGENTS_OVERVIEW.md   # All 30 agents with hierarchy
    ├── SHARED_CONFIG.md     # Global rules, stack, skill registry
    ├── SKILLS.md            # Skill discovery & knowledge
    ├── REPORTING_PROTOCOL.md # Status reporting
    │
    └── [agent-name]/        # 30 agent folders, 4 files each:
        ├── SOUL.md          # Persona, anti-patterns, reasoning protocol
        ├── AGENTS.md        # Role, scope, reporting chain, workflow
        ├── HEARTBEAT.md     # Checklists, red flags, human partner signals
        └── TOOLS.md         # Skills (inline), commands, templates
```

**Stats:**
| Metric | Value |
|--------|-------|
| Agent Folders | 30 |
| Markdown Files | 124 |
| Config Lines | 12,986 |
| Skill Sources | 17 Repositories |
| Embedded Skills | 60+ |

---

## 🛡️ Core Principles

1. **Goal Check** — every agent reads GOAL.md first
2. **Evidence before claims** — proof before assertions
3. **Circuit Breaker** — max 3 iterations, then escalate
4. **Error Recovery** — 3-tier: Self → Peer → Gatekeeper
5. **Anti-Hallucination** — STOP-CHECK-DELIVER before every delivery
6. **Mandated Stack** — Next.js 15 · React 19 · shadcn · Tailwind 4 · Zustand · Zod
7. **Contract-First** — API schema before implementation
8. **Security Gate** — OWASP Top 10 before deploy
9. **Performance Budget** — LCP < 2.5s, Bundle < 200KB
10. **WCAG 2.1 AA** — 50+ accessibility criteria

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

## 📚 Documentation

| File | Contents |
|------|---------|
| [AGENTS_OVERVIEW.md](agents/AGENTS_OVERVIEW.md) | Complete agent overview with hierarchy |
| [SHARED_CONFIG.md](agents/SHARED_CONFIG.md) | Global rules, stack, skill registry |
| [SKILLS.md](agents/SKILLS.md) | Skill discovery & top 23 skill reference |
| [REPORTING_PROTOCOL.md](agents/REPORTING_PROTOCOL.md) | Status reporting templates |

---

## License

MIT

---

<p align="center">
  Built by <a href="https://github.com/servas-ai">servas.ai</a> · Powered by <a href="https://github.com/obra/superpowers">superpowers</a> + <a href="https://github.com/pbakaus/impeccable">impeccable</a> + <a href="https://skills.sh">skills.sh</a>
</p>
