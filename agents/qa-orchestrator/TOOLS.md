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

### Orchestration

> Source: [obra/superpowers](https://github.com/obra/superpowers)

| Skill | Source | Installs | Use |
|-------|--------|----------|-----|
| `subagent-driven-development` | obra/superpowers | 34K | **Fresh subagent per test layer.** Two-stage review: spec compliance → quality. Handle DONE / DONE_WITH_CONCERNS / NEEDS_CONTEXT / BLOCKED. |
| `writing-plans` | obra/superpowers | 26K | Write structured test plans with bite-sized tasks, exact specs |
| `executing-plans` | obra/superpowers | 22K | Execute test plan with checkpoint verification |
| `dispatching-parallel-agents` | obra/superpowers | 15K | Layer 1 + Layer 2 in parallel, then Layer 3 sequential |
| `verification-before-completion` | obra/superpowers | 16K | **Evidence before QA PASS**: show test counts, coverage, screenshots |

**QA Verification Gate (Superpowers):**
- Before claiming "QA PASS": verify EVERY layer has evidence
- Don't trust "tests pass" — read the actual output (total, passed, failed, skipped)
- If ANY layer reports DONE_WITH_CONCERNS → investigate before passing
- Screenshot evidence for visual checks (not just "looks good")

### Testing Knowledge

> Source: [obra/superpowers](https://github.com/obra/superpowers)

| Skill | Source | Installs | Use |
|-------|--------|----------|-----|
| `webapp-testing` | anthropics | 22K | Web app test strategies |
| `test-driven-development` | obra/superpowers | 23K | TDD Iron Law for test planning |
| `systematic-debugging` | obra/superpowers | 28K | 4-phase root cause when tests fail |
| `playwright-best-practices` | skills.sh | ~8K | E2E test best practices |

---

## Sub-Agent Dispatch Guide

### Layer 1: Unit & Integration Tests
```markdown
# DISPATCH → Component & Integration Test Writer
Feature: [name]
Files to test: [list of new/modified files]
PRD ACs to cover: [AC-1, AC-2, ...]
Expected: Test files + PASS/FAIL result + coverage
```

### Layer 2: Visual & Accessibility Review
```markdown
# DISPATCH → Design & Accessibility Auditor
Feature: [name]
Build URL: [url]
Against: PRD + DESIGN_SPEC.md
Focus: Design compliance, WCAG 2.1 AA, responsive (3 viewports), dark mode
Expected: REVIEW.md (🔴/🟡/🟢)
```

### Layer 3: E2E User Journey Tests
```markdown
# DISPATCH → End-to-End Test Automation Agent
Feature: [name]
Build URL: [url]
User journeys to test:
1. [Journey from AC-1: step by step]
2. [Journey from AC-2: step by step]
Error paths to test:
1. [Invalid input scenario]
2. [Empty state scenario]
Expected: TEST_REPORT.md (PASS/FAIL + screenshots)
```

### Layer 4: Usability Review
```markdown
# DISPATCH → UX Research & Usability Expert (Mode B: Post-Build Review)
Feature: [name]
Build URL: [url]
Against: UX_SPEC.md
Focus: Nielsen's 10 Heuristics + accessibility audit
Expected: USABILITY_REVIEW.md
```

### Layer 5: VM Tests (Optional)
```markdown
# DISPATCH → VM Integration Test Runtime
Feature: [name]
Trigger: [why VM test is needed — desktop app / native features / etc.]
Build artifact: [download URL]
Expected: VM_TEST_REPORT.md
```

---

## Templates

### TEST_PLAN.md
```markdown
# TEST_PLAN: [Feature Name]
> QA Manager: Frontend Quality Assurance Manager
> Date: [date]
> Based on: PRD + GOAL.md

## Acceptance Criteria Coverage

| AC | Description | Layer 1 (Unit) | Layer 2 (Audit) | Layer 3 (E2E) | Layer 4 (UX) |
|----|-------------|-----------------|------------------|---------------|--------------|
| AC-1 | [description] | ✅ | ✅ | ✅ | — |
| AC-2 | [description] | ✅ | — | ✅ | ✅ |
| AC-3 | [description] | — | ✅ | ✅ | — |

## Test Strategy

### Layer 1: Unit & Integration Tests
- Components to test: [list]
- Hooks to test: [list]
- Stores to test: [list]
- Estimated test count: [N]

### Layer 2: Visual & Accessibility Review
- Viewports: 375px, 768px, 1440px
- Themes: light + dark
- Focus areas: [specific concerns from DESIGN_SPEC]

### Layer 3: E2E User Journeys
- Happy paths: [list with steps]
- Error paths: [list with scenarios]
- Edge cases: [list]

### Layer 4: Usability Review
- Heuristics to focus on: [H1, H3, H9 etc.]
- Accessibility concerns: [from UX_SPEC]

### Layer 5: VM Tests
- [ ] Needed / [ ] Not needed (web-only)
- If needed: [what to test]

## Execution Order
1. Layer 1 (Unit) + Layer 2 (Audit) → parallel
2. Wait for both → Layer 3 (E2E)
3. Pass → Layer 4 (UX Review)
4. Pass → Layer 5 (VM, if needed)
5. All pass → QA_REPORT.md
```

### QA_REPORT.md
```markdown
# QA_REPORT: [Feature Name]
> QA Manager: Frontend Quality Assurance Manager
> Date: [date]
> Goal: [GOAL.md link]

## Executive Summary
[X] test layers executed. [N] PASS, [N] FAIL.

## Layer Results

| Layer | Sub-Agent | Status | Iterations | Evidence |
|-------|-----------|--------|------------|----------|
| 1. Unit Tests | Component & Integration Test Writer | ✅ 47/47 PASS | 1 | test-results.log |
| 2. Audit | Design & Accessibility Auditor | ✅ 0🔴 2🟡 | 1 | REVIEW.md |
| 3. E2E | End-to-End Test Automation Agent | ✅ 12/12 PASS | 2 | TEST_REPORT.md |
| 4. UX | UX Research & Usability Expert | ✅ USABLE | 1 | USABILITY_REVIEW.md |
| 5. VM | VM Integration Test Runtime | ⏭️ Skipped | — | Web-only |

## Failures & Fixes (if any)
| Layer | Iteration | Issue | Fix Applied | Re-test |
|-------|-----------|-------|-------------|---------|
| 3. E2E | 1/3 | Login redirect broken | Builder fixed auth check | ✅ PASS on retry |

## AC Coverage Matrix
| AC | Unit | Audit | E2E | UX | Covered? |
|----|------|-------|-----|-----|----------|
| AC-1 | ✅ | ✅ | ✅ | — | ✅ |
| AC-2 | ✅ | — | ✅ | ✅ | ✅ |

## Verdict
- [ ] ✅ QA PASS — All layers green, all ACs covered
- [ ] ❌ QA FAIL — [N] layers failed, see details above
```

---

## Documentation Update (merged from Docs Manager)

> Final QA step: update all documentation before shipping.

After QA PASS:
1. Update `../../SYSTEM_STATE.md` — routes, components, stores, APIs, DB tables
2. Update component docs — new props, usage examples, types
3. Update CHANGELOG.md — what changed, breaking changes
4. Verify: all links work, all paths correct, no stale references

**Rules**: Scannable (headers, tables, code blocks) · Precise (exact paths, exact names) · Current (matches actual code)
