# Tools

## Runtime
- **OpenCode** is your runtime.

## Paperclip API
- `GET /api/agents/me` — identity.
- `GET /api/companies/{companyId}/issues?assigneeAgentId={agentId}&status=todo,in_progress,blocked` — inbox.
- `PATCH /api/issues/{issueId}` — status updates. Include `X-Paperclip-Run-Id`.
- `POST /api/companies/{companyId}/issues` — create subtasks. Set `parentId` + `goalId`.

---

## Skills

### 1. Brainstorming + Planning — brainstorming + writing-plans (obra/superpowers)

> Source: [obra/superpowers](https://github.com/obra/superpowers)

**HARD-GATE: Do NOT start implementation until design is approved. No exceptions.**

**Brainstorming Phase:**
1. Explore project context (files, docs, recent commits)
2. Ask ONE clarifying question at a time (prefer multiple choice)
3. Propose 2-3 approaches with trade-offs + recommendation
4. Present design in sections → user approval per section
5. Write design doc → spec review (max 5 iterations) → approval

**Planning Phase (bite-sized tasks 2-5 minutes each):**
- Scope check: break down if too large. Multiple subsystems = multiple plans.
- File structure: list EVERY file created/modified
- Each task: exact file paths, complete code, exact verification commands
- DRY, YAGNI, TDD, frequent commits

**Design for Isolation (Superpowers):**
- Break into smaller units with ONE clear purpose each
- Well-defined interfaces between units
- Each unit independently understandable and testable
- Can you change internals without breaking consumers? If not → rework boundaries

**YAGNI ruthlessly**: Remove unnecessary features from ALL designs.

### 2. Plan Execution — executing-plans (obra, 22K)

**Execute plans with checkpoint verification:**
- Work through one task at a time.
- After each task: verify it's done (run the verification step).
- If verification fails: fix before moving on.
- Update plan progress as you go.
- Never skip verification steps.

### 3. Evidence Gates — verification-before-completion (obra, 16K)

**The Iron Law: Evidence before claims, always.**
1. Identify the command that proves your claim.
2. Execute that command completely.
3. Read the output thoroughly (exit codes, failure counts).
4. Verify the output confirms the claim.
5. Only THEN declare completion.

**Red Flags — STOP if:**
- You're about to say "done" without running tests.
- You're assuming something works without evidence.
- You're re-running a test but not reading the output.

### 4. Subagent-Driven Development — subagent-driven-development (obra/superpowers, 34K)

> Source: [obra/superpowers](https://github.com/obra/superpowers)

**The standard execution mode — fresh subagent per task:**
- Dispatch implementer with full task text + context
- Two-stage review: spec compliance → code quality
- Handle implementer statuses: DONE, DONE_WITH_CONCERNS, NEEDS_CONTEXT, BLOCKED
- Cost-optimize: cheap model for 1-2 file tasks, capable model for architecture

### 5. Parallel Dispatch — dispatching-parallel-agents (obra, 15K)

**For independent tasks, dispatch in parallel:**
- Identify tasks with no dependencies between them.
- Dispatch fresh agents for each independent task.
- Collect results and verify before integrating.

### 6. Architecture Patterns — architecture-patterns (skills.sh, ~8K)

**Apply standard architecture patterns:**
- Layered architecture for separation of concerns.
- Component-based architecture for UI.
- API-first design for backend.
- Event-driven for real-time features.
- CQRS where read/write patterns differ significantly.

### 7. Swarm-Ready Planning — swarm-planner (am-will, 11.7K)

**Dependency-aware plans with parallel detection:**
- Every task gets: `id`, `depends_on`, `description`, `location`, `validation`
- Tasks with empty `depends_on` can run in parallel
- PFLICHT: Context7 Docs fetchen vor Planung
- After saving plan: spawn sub-agent to review

**Task Format:**
```
T1: [depends_on: []] Create database schema
T2: [depends_on: []] Install required packages
T3: [depends_on: [T1]] Create repository layer
T4: [depends_on: [T3, T4]] Implement business logic
T5: [depends_on: [T2, T4]] Add API endpoints
```

### Additional Skills
| Skill | Source | Installs | Use |
|-------|--------|----------|-----|
| `systematic-debugging` | obra | 28K | Root-cause analysis |
| `requesting-code-review` | obra | 21K | Send work to reviewers |
| `using-superpowers` | obra | 20K | Skill priority hierarchy |
| `find-skills` | vercel-labs | #1 | Discover new skills for new problems |

---

## Shared Config

Read `../SHARED_CONFIG.md` for:
- Mandated stack with versions
- MCP server configs (Context7, Firecrawl)
- Shared rules (Goal Check, Evidence, Circuit Breaker, HANDOFF, Skill Priority)
- Project folder structure

---

## GOAL.md Template

```markdown
# GOAL: [Feature Name]

## Objective
What exactly should be achieved? (1-2 sentences, precise)

## Context
Why is this needed? What problem does it solve?

## Acceptance Criteria
- [ ] AC-1: [specific, testable criterion]
- [ ] AC-2: [specific, testable criterion]
- [ ] AC-3: [specific, testable criterion]

## Scope Boundaries
- ❌ NOT in scope: [explicitly excluded items]
- ❌ NOT in scope: [explicitly excluded items]

## Dependencies
- Requires: [API/component/design from another agent]
- Blocked by: [nothing / specific prerequisite]

## Routing
- [ ] Frontend → Feature Lifecycle Orchestrator
- [ ] Backend → API & Database Backend Builder
- [ ] Full-stack → Split FE + BE
- [ ] Research needed → Technical Research & Discovery Agent

## Quality Gates
- [ ] GOAL.md written ✅
- [ ] Plan written ✅
- [ ] Unit Tests PASS ✅
- [ ] Auditor Review: no 🔴 Blockers ✅
- [ ] E2E Tests PASS ✅
- [ ] SYSTEM_STATE.md updated ✅
- [ ] Documentation updated ✅
- [ ] FEATURE_SCORECARD.md delivered ✅
```

---

## ARCHITECTURE.md Template

```markdown
# Architecture — [Project Name]
> Last updated: [date]

## System Overview
[High-level description of the system]

## Tech Stack
| Layer | Technology | Version |
|-------|-----------|---------|
| Frontend | Next.js (App Router) | latest |
| UI Components | shadcn/ui + Tailwind 4 | latest |
| State | Zustand + React Query | latest |
| Backend | [technology] | latest |
| Database | [technology] | latest |
| Auth | [technology] | latest |

## Architecture Diagram
[Mermaid diagram or description]

## Key Decisions
| Decision | Rationale | Date |
|----------|-----------|------|
| [what] | [why] | [when] |

## API Contracts
| Endpoint | Method | Purpose |
|----------|--------|---------|
| /api/... | GET | ... |

## Data Model
[Entity relationships]

## Security Considerations
- [item]

## Performance Requirements
- LCP < 2.5s
- FID < 100ms
- CLS < 0.1
```

---

## Spec Review (merged from Spec Reviewer)

> `spec-document-reviewer` (obra/superpowers)

**5-Category Review** — for every spec (PRD, UX_SPEC, DESIGN_SPEC):
1. **Completeness** — All ACs defined? All edge cases covered?
2. **Clarity** — Unambiguous language? No "should" or "maybe"?
3. **Consistency** — No contradictions between sections?
4. **Feasibility** — Buildable with mandated stack? Performance-realistic?
5. **Testability** — Every AC verifiable? Clear pass/fail criteria?

**Self-Refinement Loop** (max 4 iterations):
```
Read spec → Find issues → Ask: "Is this REALLY a problem?" → Report only genuine issues
```

