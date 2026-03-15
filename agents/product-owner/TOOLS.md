# Tools

## Runtime
- **OpenCode** is your runtime.

## Paperclip API
- `GET /api/agents/me` — identity.
- `GET /api/companies/{companyId}/issues?assigneeAgentId={agentId}&status=todo,in_progress,blocked` — inbox.
- `PATCH /api/issues/{issueId}` — status updates. Include `X-Paperclip-Run-Id`.

---

## Skills

### 1. Brainstorming — brainstorming (obra/superpowers, 51K)

> Source: [obra/superpowers](https://github.com/obra/superpowers)

**HARD-GATE: Do NOT invoke implementation until design is approved. Every project, no matter how "simple."**

**Socratic Refinement Process:**
1. Explore project context — check files, docs, recent commits
2. Ask ONE clarifying question at a time (prefer multiple choice)
3. Propose 2-3 approaches with trade-offs + your recommendation
4. Present design in sections, get approval after each
5. Write design doc → spec review loop (max 5 iterations) → user approval
6. Transition to implementation via writing-plans

**Anti-Pattern: "This Is Too Simple To Need A Design"**
Every project goes through this process. "Simple" projects are where unexamined assumptions cause the most wasted work. Design can be short, but you MUST present it.

**YAGNI ruthlessly**: Remove unnecessary features from ALL designs.

### 2. Writing Plans — writing-plans (obra/superpowers, 26K)

> Source: [obra/superpowers](https://github.com/obra/superpowers)

**Overview**: Write plans assuming the implementer has ZERO codebase context and questionable taste. Document everything.

**Bite-Sized Task Granularity (2-5 minutes each):**
- "Write the failing test" — step
- "Run it to make sure it fails" — step
- "Implement the minimal code" — step
- "Run tests, make sure they pass" — step
- "Commit" — step

**Every task must have:**
- Exact file paths
- Complete code (not "add validation")
- Exact commands with expected output
- DRY, YAGNI, TDD, frequent commits

### 3. PRD Template — prd (12K)
**Standard PRD format for feature handoff to Gatekeeper.**

### 4. Sprint Planning (merged from Scrum Master)
- **Dispatching Parallel Agents** (obra, 15K): Identify independent work → dispatch parallel → review + integrate
- **Subagent-Driven Development** (obra, 14K): Fresh subagent per task → Spec Review → Code Quality Review
- Sprint cadence: plan → execute → review → retro
- RICE scoring for prioritization · MoSCoW for sprint selection

---

## Templates

### USER_STORY.md
```markdown
# User Story: [Title]

**As a** [persona],
**I want** [action],
**So that** [benefit].

## Acceptance Criteria

- [ ] **Given** [precondition], **When** [action], **Then** [expected result]
- [ ] **Given** [precondition], **When** [action], **Then** [expected result]

## Priority
- RICE Score: [number]
- MoSCoW: [Must/Should/Could/Won't]

## Estimation
- Story Points: [1/2/3/5/8/13]
- Sprint Target: [Sprint N]

## Notes
[Additional context, constraints, dependencies]
```

### BACKLOG.md
```markdown
# Product Backlog

> Last updated: [timestamp]
> Next Sprint Goal: [goal]

## 🔴 Must Have (Sprint N)

| # | Story | Points | RICE | AC Count | Status |
|---|-------|--------|------|----------|--------|
| 1 | [title] | 5 | 42 | 3 | Ready |

## 🟠 Should Have (Sprint N+1)

| # | Story | Points | RICE | AC Count | Status |
|---|-------|--------|------|----------|--------|

## 🟡 Could Have (Later)

| # | Story | Points | RICE | AC Count | Status |
|---|-------|--------|------|----------|--------|

## ⚪ Won't Have (Parked)

| # | Story | Reason |
|---|-------|--------|
```

### SPRINT_GOAL.md
```markdown
# Sprint [N] Goal

> Start: [date] | End: [date]
> Velocity (avg): [points]

## Goal
[ONE sentence: "Users can [do X] with [quality Y]"]

## Selected Stories

| # | Story | Points | AC Link |
|---|-------|--------|---------|
| 1 | [title] | 5 | docs/features/[name]/GOAL.md |

## Total Points: [sum] / Velocity: [avg]

## Risks
- [risk 1]
```

---

## Shared Config

Read `../SHARED_CONFIG.md` for:
- Mandated stack with versions
- Shared rules (Goal Check, Evidence, Circuit Breaker, HANDOFF, Skill Priority)
- Anti-Hallucination Protocol
