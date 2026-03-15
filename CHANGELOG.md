# Changelog

All notable changes to the Paperclip Fullstack Agent Swarm.

## [1.2.0] - 2026-03-15

### Changed
- **Agent Consolidation: 30 → 23 agents** — merged 7 redundant agents:
  - Scrum Master → Product Owner (+sprint planning, parallel dispatch)
  - Spec Reviewer → Architecture Gatekeeper (+5-category spec review)
  - Testability Expert → Unit Test Writer (+test pyramid, mock strategy)
  - VM Tester → E2E Tester (+optional VM mode)
  - Event-System Expert → Backend Builder (+Supabase Realtime)
  - API Schema Expert → Backend Builder (+Contract-First Zod)
  - Docs Manager → QA Orchestrator (+docs update step)
- SHARED_CONFIG.md condensed 325 → 160 lines (-51%)
- 8 HEARTBEAT.md files simplified (~965 → ~350 lines, -64%)
- SOUL.md audit: anti-patterns added to 5 agents
- Feature Lifecycle reduced 20 → 18 steps
- Mermaid architecture diagram redesigned with subgroups

### Added
- 🚀 Quickstart Guide in README
- Impeccable Design integration — full DO/DON'T rules in 3 design agents
- 16-point AI Slop Test table
- Sequence Diagram for feature flow
- CHANGELOG.md, LICENSE, CONTRIBUTING.md

## [1.1.0] - 2026-03-13

### Added
- Impeccable skill (pbakaus) — OKLCH colors, 4pt grid, motion rules
- Advanced agent-browser capabilities (Network Tab, Console errors)
- E2E Iron Laws (zero JS errors, no failed HTTP)
- stack-researcher and unit-test-writer simplified (-66%, -60%)

### Changed
- README rewritten in English with Mermaid diagrams
- AGENTS_OVERVIEW.md with full hierarchy
- SKILLS.md with 23 skills from 17 sources

## [1.0.0] - 2026-03-12

### Added
- Initial release: 30 AI agents for fullstack development
- 4-file agent config system (SOUL, AGENTS, TOOLS, HEARTBEAT)
- Skills from obra/superpowers, Vercel, Anthropic
- Anti-Hallucination Protocol
- Mandated Stack (Next.js 15, React 19, shadcn, Tailwind 4)
