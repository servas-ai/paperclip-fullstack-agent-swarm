# Tools

## Runtime
- **OpenCode** is your runtime.

## Paperclip API
- `GET /api/agents/me` — identity.
- `GET /api/companies/{companyId}/issues?assigneeAgentId={agentId}&status=todo,in_progress,blocked` — inbox.
- `PATCH /api/issues/{issueId}` — status updates. Include `X-Paperclip-Run-Id`.

---

## Primary: agent-browser (vercel-labs, 89K)

### Core E2E Workflow
```bash
# 1. Open + wait
agent-browser open <build-url>
agent-browser wait --load networkidle

# 2. Snapshot interactive elements → use refs
agent-browser snapshot -i              # List all interactive elements
agent-browser click @e1                # Click by ref
agent-browser fill @e2 "test@example.com"  # Clear + type
agent-browser type @e3 "password123"
agent-browser click @e4
agent-browser wait --text "Dashboard"
agent-browser screenshot login-success.png

# 3. Network + Console Monitoring (MANDATORY per test)
agent-browser network log start        # Start capturing requests
# ... test actions ...
agent-browser network log stop         # Stop + show all HTTP requests
agent-browser console errors           # Check for JS errors → MUST be 0
agent-browser console warnings         # Check warnings

# 4. Visual Regression (diff)
agent-browser screenshot baseline.png
# ... make changes ...
agent-browser diff screenshot --baseline baseline.png  # Pixel diff, red highlights
agent-browser diff snapshot            # Compare DOM against last snapshot

# 5. State Inspection (eval)
agent-browser eval 'document.querySelectorAll("[aria-invalid]").length'  # Check form errors
agent-browser eval 'localStorage.getItem("auth-token")'                 # Check state
agent-browser eval 'performance.getEntriesByType("navigation")[0].domContentLoadedEventEnd'  # Load timing

# 6. Responsive Testing
agent-browser set device "iPhone 14"   # Device emulation (viewport + UA)
agent-browser screenshot test-mobile.png
agent-browser set viewport 768 1024    # Tablet
agent-browser screenshot test-tablet.png
agent-browser set viewport 1440 900    # Desktop
agent-browser screenshot test-desktop.png

# 7. Dark Mode
agent-browser --color-scheme dark open <url>
agent-browser screenshot test-dark.png

# 8. Cleanup
agent-browser close
```

### Network Tab — CRITICAL for API Testing
```bash
agent-browser network log start        # Start monitoring ALL HTTP requests

# ... perform user actions (login, form submit, etc.) ...

agent-browser network log stop         # Stop + show:
                                       # - URLs, methods, status codes
                                       # - Response times
                                       # - Failed requests (4xx, 5xx)
                                       # - Payload sizes

# CHECK for:
# ❌ 4xx/5xx status codes → API or auth errors
# ❌ Slow requests (>1s) → performance issues
# ❌ Duplicate requests → waterfall problems
# ❌ Missing CORS headers → cross-origin issues
```

### Console Monitoring — MANDATORY
```bash
agent-browser console errors           # JS errors → MUST be ZERO
agent-browser console warnings         # Deprecation/perf warnings
agent-browser console log              # All console output

# IRON LAW: No E2E test passes with JS errors in console.
# If console errors exist → test FAILS regardless of visual appearance.
```

### Diff Commands — Visual Regression
```bash
# DOM diff (accessibility tree)
agent-browser snapshot -i              # Baseline
agent-browser click @e1                # Action
agent-browser diff snapshot            # What changed? (+/- like git diff)

# Screenshot diff
agent-browser diff screenshot --baseline before.png  # Pixel diff → red highlights

# Compare staging vs production
agent-browser diff url https://staging.example.com https://prod.example.com --screenshot

# Scoped diff (specific component)
agent-browser diff url <url1> <url2> --selector "#main-content"
```

### JavaScript Evaluation (eval)
```bash
# Simple checks
agent-browser eval 'document.title'
agent-browser eval 'document.querySelectorAll("img").length'

# State inspection
agent-browser eval 'JSON.stringify(Object.keys(localStorage))'
agent-browser eval 'document.cookie'

# Complex checks (use --stdin for multi-line/nested quotes)
agent-browser eval --stdin <<'EVALEOF'
JSON.stringify(
  Array.from(document.querySelectorAll("img"))
    .filter(i => !i.alt)
    .map(i => ({ src: i.src.split("/").pop(), width: i.width }))
)
EVALEOF
```

### Semantic Locators (when refs unavailable)
```bash
agent-browser find text "Sign In" click
agent-browser find label "Email" fill "user@test.com"
agent-browser find role button click --name "Submit"
agent-browser find placeholder "Search" type "query"
agent-browser find testid "submit-btn" click
```

### Annotated Screenshots (Vision Mode)
```bash
agent-browser screenshot --annotate    # Numbers on every interactive element
# Output: [1] @e1 button "Submit", [2] @e2 link "Home", [3] @e3 textbox "Email"
# Use for: unlabeled icon buttons, canvas elements, spatial layout verification
```

---

## Skills

### Testing Methodology

| Skill | Source | Use |
|-------|--------|-----|
| `webapp-testing` | anthropics | Web app test patterns |
| `playwright-best-practices` | currents-dev | E2E best practices |
| `systematic-debugging` | obra/superpowers | 4-phase root cause analysis |
| `verification-before-completion` | obra/superpowers | Evidence before claims |
| `browser-use` | browser-use (48K) | Advanced browser automation |

**Systematic Debugging for E2E (4-Phase):**
1. **Root Cause** — Screenshot + `console errors` + `network log`. Timing? DOM? Selector? Auth?
2. **Pattern Analysis** — Compare working vs failing. Check selectors, waits, viewport
3. **Hypothesis Testing** — SINGLE change. Verify BEFORE stacking fixes
4. **Implementation** — Fix at root cause. NEVER use `sleep()` — use condition-based waiting

**Verification Gate:**
- Run FULL test suite, not just one scenario
- `console errors` MUST be 0
- `network log` — no 4xx/5xx
- Screenshots for EVERY scenario
- Only report PASS with evidence

---

## E2E Test Scenarios (Standard)

### Happy Path
1. User completes intended journey start-to-finish
2. All form submissions work · Navigation flows correctly
3. Data persists after refresh (if expected)

### Error Path
1. Invalid inputs show proper error messages
2. Empty required fields prevent submission
3. API errors show user-friendly messages (check `network log` for 4xx/5xx)

### Edge Cases
1. Empty states · Very long text · Rapid clicking · Back button · Refresh

### Responsive (3 viewports)
```bash
agent-browser set device "iPhone 14"   # 390x844
agent-browser set viewport 768 1024    # Tablet
agent-browser set viewport 1440 900    # Desktop
```

### Dark Mode + Console + Network
1. Functional test in dark mode (not just visual)
2. `console errors` → ZERO in both themes
3. `network log` → no failed requests

---

## TEST_REPORT.md Template

```markdown
# TEST_REPORT: [Feature Name]
> Tested: [date] | Build URL: [url]

## Summary
[X] scenarios: [N] ✅ PASS, [N] ❌ FAIL

## Network & Console Health
- JS Console Errors: [0 / N errors]
- Failed HTTP Requests: [0 / N failed]
- Slowest Request: [url] ([Xms])

## ✅ PASS Scenarios
### 1. [Scenario]
- Steps → Expected → Actual → Evidence: ![screenshot](path)

## ❌ FAIL Scenarios
### 1. [Scenario]
- Steps → Expected → Actual → Error → Console Output → Network Log
- Severity: Critical / Major / Minor

## Responsive | Viewport | Status |
## Dark Mode  | Theme    | Status |

## Verdict
- [ ] ✅ ALL PASS + 0 console errors + 0 network errors → ready
- [ ] ❌ HAS FAILURES → [N] scenarios need fixing
```
