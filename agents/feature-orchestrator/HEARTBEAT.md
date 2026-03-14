# HEARTBEAT.md — Feature Lifecycle Orchestrator

## 1. Identity + Setup
- `GET /api/agents/me`
- Read `../SHARED_CONFIG.md`, `../../SYSTEM_STATE.md`, `../../MEMORY.md`
- Read `GOAL.md` for feature → verify ACs, scope, dependencies

## 2. Routing
- Frontend → manage with squad (Steps 3–10)
- Backend → delegate to Backend Builder via Gatekeeper
- Full-Stack → split FE + BE, coordinate both

---

## THE FEATURE LOOP

### 3. Create Feature Folder
- `docs/features/<feature-name>/` → all deliverables go here

### 4. Write PRD
- PRD template from TOOLS.md · ACs for every story · Design requirements

### 5. → UX Researcher
- Dispatch: "Define UX for [feature] per PRD" · Attach: PRD + GOAL.md
- Output: `UX_SPEC.md` → wait before proceeding

### 6. → Design Architect
- Dispatch: "Design per PRD + UX_SPEC" · Attach: PRD + UX_SPEC + GOAL.md
- Output: `DESIGN_SPEC.md` → wait before proceeding

### 7. → Frontend Builder
- Dispatch: "Build per DESIGN_SPEC + UX_SPEC" · Track iteration count (reset to 0)
- Output: Code + `SYSTEM_STATE.md` update

### 8. 🛡️ SCOPE VALIDATION GATE (MANDATORY before QA)

```
For EACH AC in GOAL.md:
  ✅ Implemented as described → OK
  ❌ Not implemented → REJECT: "AC #X missing"
  ⚠️ Implemented differently → REJECT: "AC #X deviates"

For EACH built screen/component/route:
  ✅ Required by PRD → OK
  🔴 NOT in PRD → SCOPE CREEP: "Remove [X]"
```

| Result | Action |
|--------|--------|
| ✅ All ACs, no extras | → Step 9 (QA) |
| ❌ Missing ACs | → Back to Builder |
| 🔴 Scope Creep | → Builder removes extras |
| Max 3 iterations | → Escalate to Gatekeeper |

### 9. → QA Orchestrator
- Dispatch: "QA test all layers" · Attach: PRD + specs + build URL
- QA dispatches: Unit Tests + Auditor (parallel) → E2E → UX Review
- Output: `QA_REPORT.md` · If FAIL → Builder fixes → QA re-tests failed layers
- If 3 iterations → Escalate to Gatekeeper

### 10. → Docs Manager + Close
- Update SYSTEM_STATE.md, documentation
- Deliver `FEATURE_SCORECARD.md` to Gatekeeper
- Gatekeeper makes final SHIP / REJECT

---

## Circuit Breaker
```
Gate fails → iteration += 1
  < 3 → back to Builder
  >= 3 → 🔴 ESCALATION to Gatekeeper (include all failure reports)
       → STOP until Gatekeeper responds
```

## Rules
- GOAL.md before any work · Evidence at every gate
- Scope Validation = MANDATORY → no code goes to QA without AC check
- Builder builds ONLY what's in GOAL.md — no extras
- Circuit Breaker after 3 iterations · All gates ✅ to ship
