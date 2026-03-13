# 🤖 Paperclip Fullstack Agent Swarm

> **30 AI agents** for end-to-end software development — from idea to deploy.
>
> Built on [obra/superpowers](https://github.com/obra/superpowers) + [pbakaus/impeccable](https://github.com/pbakaus/impeccable)

---

## What Is This?

A fully configured multi-agent system where **30 specialized AI agents** collaborate through a structured 21-step feature lifecycle. Each agent has a defined persona, scope, tools, and checklist — no ambiguity, no scope creep.

### Key Differentiators
- 🎯 **obra/superpowers** — TDD Iron Law, 4-Phase Debugging, Verification Evidence, Subagent-Driven Development
- 🎨 **pbakaus/impeccable** — OKLCH colors, 4pt grid, AI Slop Test (16 anti-patterns), fluid typography
- 🛡️ **Anti-Hallucination Protocol** — every agent self-checks against source docs and is verified by a peer
- 🔄 **60+ skills** from 17 open-source repositories, integrated inline

---

## Architecture

```
CEO → Product Owner → Scrum Master
  └→ Architecture Gatekeeper
       ├→ Feature Orchestrator → UX → Design → Build → QA → Docs → Deploy
       ├→ Stack Researcher, Code Quality, Docs Manager
       ├→ DevOps → K8s, Git Workflow, Performance
       └→ Security Auditor, Spec Reviewer
```

## 30 Agents

| Area | Agents |
|------|--------|
| **Leadership** | CEO · Product Owner · Scrum Master · Architecture Gatekeeper |
| **Design & Research** | UX Researcher · Design Architect · Stack Researcher |
| **Build** | Feature Orchestrator · Frontend Builder · Backend Builder |
| **Quality & Testing** | QA Orchestrator · Unit Test Writer · Design Auditor · E2E Tester · VM Tester · Testability Expert · Validation Expert · Code Quality Expert |
| **Infrastructure** | DevOps Expert · Kubernetes Expert · Browser Automation · Docs Manager |
| **Specialists** 🆕 | Systematic Debugger · Spec Reviewer · Git Workflow Manager · Security Auditor · Performance Optimizer · Accessibility Expert |

## Agent Config (4 files per agent)

| File | Purpose |
|------|---------|
| `SOUL.md` | Persona, anti-patterns, reasoning protocol |
| `AGENTS.md` | Role, scope, workflow, reporting chain |
| `TOOLS.md` | Skills (inline), commands, templates |
| `HEARTBEAT.md` | Checklist, red flags, human partner signals |

---

## Feature Lifecycle (21 Steps)

```
 1. BACKLOG        ← Product Owner
 2. SPRINT_GOAL    ← Scrum Master
 3. GOAL.md        ← Gatekeeper
 4. SPEC REVIEW    ← Spec Reviewer 🆕
 5. PRD            ← Orchestrator
 6. API_SPEC       ← API Schema Expert
 7. RESEARCH       ← Stack Researcher
 8. UX_SPEC        ← UX Researcher
 9. DESIGN_SPEC    ← Design Architect
10. VALIDATION     ← Validation Expert
11. BRANCH         ← Git Workflow Manager 🆕
12. CODE           ← Frontend + Backend Builder
13. SECURITY       ← Security Auditor 🆕
14. PERFORMANCE    ← Performance Optimizer 🆕
15. ACCESSIBILITY  ← Accessibility Expert 🆕
16. QA             ← QA Orchestrator
17. QUALITY GATE   ← Code Quality Expert
18. DOCS           ← Docs Manager
19. MERGE          ← Git Workflow Manager 🆕
20. DEPLOY         ← DevOps → K8s Expert
21. SCORECARD      ← Orchestrator → Product Owner
```

---

## Methodology

| Source | Techniques |
|--------|-----------|
| [obra/superpowers](https://github.com/obra/superpowers) | TDD, 4-Phase Debugging, Verification Evidence, Plans, Subagent-Driven Dev |
| [pbakaus/impeccable](https://github.com/pbakaus/impeccable) | OKLCH, 4pt Grid, Fluid Type, Motion 100/300/500, AI Slop Test |
| [skills.sh](https://skills.sh) | 60+ skills from 17 repositories |

## Skill Sources

| Repository | Key Skills |
|-----------|-----------|
| [obra/superpowers](https://github.com/obra/superpowers) | TDD, Debugging, Plans, Verification, Code Review, Git, Subagent |
| [Vercel Labs](https://skills.sh) | React Best Practices, Design Guidelines, Browser, Next.js |
| [Anthropic](https://github.com/anthropics/skills) | Frontend Design, Canvas, Webapp Testing |
| [pbakaus/impeccable](https://github.com/pbakaus/impeccable) | OKLCH, 4pt Grid, Motion, AI Slop Test |
| [supercent-io](https://github.com/supercent-io/agent-skills) | Security, Code Review, Design System |
| [supabase](https://github.com/supabase/agent-skills) | Postgres Best Practices |
| [better-auth](https://github.com/better-auth/skills) | Auth Best Practices |
| + 10 more | See [SHARED_CONFIG.md](agents/SHARED_CONFIG.md) |

---

## Tech Stack

Next.js 15 · React 19 · shadcn/ui · Tailwind 4 · Zustand · Zod · Drizzle · Supabase · Vitest · Playwright

---

## Core Principles

1. **Goal Check** — every agent reads GOAL.md first
2. **Evidence first** — proof before claims
3. **TDD** — no code without a failing test
4. **HARD-GATE** — no code without design approval
5. **Circuit Breaker** — max 3 iterations, then escalate
6. **Error Recovery** — Self → Peer → Gatekeeper (3-tier)
7. **Anti-Hallucination** — self-check + peer verification on every deliverable

---

## File Structure

```
agents/
├── README.md              ← This file
├── AGENTS_OVERVIEW.md     ← All 30 agents, hierarchy, lifecycle
├── SHARED_CONFIG.md       ← Global rules, skill sources, anti-hallucination
├── SKILLS.md              ← Skill reference + discovery
├── REPORTING_PROTOCOL.md  ← Status reporting + crash recovery
└── [30 agent folders]/    ← Each with SOUL.md, AGENTS.md, TOOLS.md, HEARTBEAT.md
```

---

## License

MIT

---

<p align="center">
  Built by <a href="https://github.com/servas-ai">servas.ai</a> · Powered by <a href="https://github.com/obra/superpowers">superpowers</a> + <a href="https://github.com/pbakaus/impeccable">impeccable</a>
</p>
