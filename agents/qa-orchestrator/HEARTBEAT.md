# HEARTBEAT.md — QA Orchestrator

## 1. Identity + Setup
- `GET /api/agents/me`
- Read GOAL.md + PRD ACs → every AC must be covered by at least one test layer

## 2. Analyze Code Delivery
- What files created/modified? Components, hooks, stores?
- User-facing functionality? API endpoints? Web-only or native?

## 3. Write TEST_PLAN.md (before dispatching)
| Layer | What | When |
|-------|------|------|
| 1. Unit/Integration | Components, hooks, stores → map to ACs | Phase 1 (parallel) |
| 2. Visual/A11y Audit | Design-critical areas, 3 viewports, themes | Phase 1 (parallel) |
| 3. E2E | ACs → user journeys + error paths | Phase 2 (after Phase 1 passes) |
| 4. UX Review | Relevant heuristics, a11y concerns | Phase 3 |
| 5. VM (optional) | Native/desktop only — skip for web-only | Phase 4 |

## 4. Phase 1 — Dispatch Parallel
```
→ Unit Test Writer: "Tests for [feature]. Files: [list]. ACs: [list]."
→ Design Auditor: "Review [feature] at [URL]. Design, WCAG, 3 viewports, dark mode."
```
Wait for both. If FAIL → iteration += 1 → Builder fixes → re-test. If ≥3 iterations → ESCALATE.

## 5. Phase 2 — E2E (only after Phase 1 passes)
```
→ E2E Tester: "E2E [feature] at [URL]. Journeys: [from TEST_PLAN]."
```
If FAIL → same circuit breaker. If PASS → Phase 3.

## 6. Phase 3 — UX Review
```
→ UX Researcher (Mode B): "Usability review [feature] at [URL] against UX_SPEC."
```
If 🔴 Critical → route to Builder. If ✅ USABLE → proceed.

## 7. Phase 4 — VM (if needed)
Skip for web-only. Otherwise → VM Tester.

## 8. Synthesize QA_REPORT.md
- Collect all results → QA_REPORT template (TOOLS.md)
- AC coverage matrix · Iteration counts · Verdict: QA PASS or QA FAIL
- Deliver to Orchestrator

---

## Rules
- Every AC tested by ≥1 layer · Never skip Unit Tests (Layer 1)
- Audit runs PARALLEL with Unit Tests · E2E only AFTER Unit Tests pass
- Circuit Breaker: 3 iterations per sub-agent → escalate
- TEST_PLAN.md BEFORE dispatching · QA_REPORT.md = single source of truth
