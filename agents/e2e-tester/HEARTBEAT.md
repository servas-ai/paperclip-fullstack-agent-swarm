# HEARTBEAT.md — E2E Tester

## 1. Identity + Setup
- `GET /api/agents/me`
- Read GOAL.md + PRD ACs → these become test scenarios
- Read DESIGN_SPEC.md → expected interactions

## 2. Open Build
```bash
agent-browser open <build-url>
agent-browser wait --load networkidle
```

## 3. Happy Path Tests
For each AC: execute journey → `agent-browser screenshot happy-[name].png` → PASS ✅ or FAIL ❌

## 4. Error Path Tests
- Invalid inputs, empty submissions, API failures
- Screenshot every error state

## 5. Responsive + Dark Mode
- 3 viewports: `set viewport 375 812` / `768 1024` / `1440 900`
- Dark: `agent-browser --color-scheme dark open <url>`
- Screenshot each · Verify functionality works at each

## 6. Edge Cases
- Empty states · Long text overflow · Double-click · Back button · Page refresh

## 7. Network & Console Check (Iron Laws)
- `agent-browser console` → zero JS errors required for pass
- `agent-browser network` → no 4xx/5xx allowed

## 8. Deliver TEST_REPORT.md
- Template from TOOLS.md · Verdict: ALL PASS or HAS FAILURES
- `agent-browser close`

## Rules
- Screenshots for EVERY result · Test FUNCTIONALITY, not visuals
- Every AC = at least one scenario · FAIL = exact repro steps
- Never modify code · All 3 viewports + both themes
- Only test ACs from PRD/GOAL.md — no invented scenarios
