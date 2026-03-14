# Tools

## Runtime
- **OpenCode** is your runtime.

## Paperclip API
- `GET /api/agents/me` — identity.

---

## Skills

### 1. Systematic Debugging — systematic-debugging (obra/superpowers, 28K)

When browser automation fails:
1. **Root Cause**: Screenshot + `console errors` + `network log`. Element there? Visible? Covered? Page loading?
2. **Pattern Analysis**: Did same command work before? What changed? (DOM, timing, viewport, auth)
3. **Hypothesis Testing**: ONE fix — add `wait`? Fix selector? Scroll into view? Close modal first?
4. **Implementation**: Fix at root cause. NEVER use `sleep()` — use condition-based waiting.

**Defensive Automation Patterns:**
- Always `wait --load networkidle` before interacting
- Always `console errors` after page load — 0 errors expected
- Use `@ref` selectors from `snapshot -i` (more stable than text)
- Screenshot BEFORE and AFTER each critical action
- If element not found: `snapshot -i` → verify selector exists
- After DOM changes: re-snapshot (refs are invalidated!)

### 2. Verification — verification-before-completion (obra/superpowers, 16K)
Screenshot evidence for every claim. "I checked the page" is not evidence — a screenshot is.

---

## Primary: agent-browser (vercel-labs, 89K)

### Session Management
```bash
agent-browser open <url>
agent-browser open <url> --incognito
agent-browser wait --load networkidle       # All network requests settled
agent-browser wait --text "Expected"        # Wait for text
agent-browser wait --url "**/dashboard"     # Wait for URL pattern
agent-browser wait --fn "!document.body.innerText.includes('Loading...')"  # Wait for condition
agent-browser wait "#spinner" --state hidden  # Wait for element to disappear
agent-browser close
```

### DOM Interaction
```bash
agent-browser snapshot -i              # Interactive elements with refs (ALWAYS first)
agent-browser snapshot -i -C           # Include cursor-interactive elements
agent-browser click @e1                # Click by ref
agent-browser click @e1 --new-tab     # Open in new tab
agent-browser fill @e2 "text"          # Clear + type
agent-browser type @e2 "text"          # Type without clearing
agent-browser select @e1 "option"      # Select dropdown
agent-browser check @e1                # Check checkbox
agent-browser press Enter              # Press key
agent-browser scroll down 500
agent-browser scroll down 500 --selector "div.content"  # Scroll within container
```

### Semantic Locators (alternative to refs)
```bash
agent-browser find text "Sign In" click
agent-browser find label "Email" fill "user@test.com"
agent-browser find role button click --name "Submit"
agent-browser find placeholder "Search" type "query"
agent-browser find testid "submit-btn" click
```

### Information Retrieval
```bash
agent-browser get text @e1
agent-browser get value @input-id
agent-browser get attribute @e1 "href"
agent-browser get url
agent-browser get title
agent-browser get cookies
```

### Capture
```bash
agent-browser screenshot filename.png
agent-browser screenshot --full            # Full page
agent-browser screenshot --annotate        # Numbered labels on elements → [1] @e1 button "Submit"
agent-browser pdf output.pdf

agent-browser record start session.mp4     # Video recording
agent-browser record stop

agent-browser profiler start               # Performance profiling
agent-browser profiler stop
agent-browser profiler report
```

### Network Monitoring
```bash
agent-browser network log start            # Start capturing HTTP requests
# ... actions ...
agent-browser network log stop             # Show: URLs, methods, status codes, timing

# CHECK for: 4xx/5xx → API errors, slow requests, duplicate requests, CORS issues
```

### Console Monitoring
```bash
agent-browser console errors               # JS errors → MUST be 0
agent-browser console warnings             # Deprecation/perf warnings
agent-browser console log                  # All console output
```

### Diff — Visual Regression
```bash
# DOM diff
agent-browser snapshot -i                  # Baseline
agent-browser click @e1                    # Action
agent-browser diff snapshot                # What changed? (+/- like git diff)

# Screenshot diff
agent-browser diff screenshot --baseline before.png  # Pixel diff → red highlights

# Compare URLs (staging vs production)
agent-browser diff url <url1> <url2> --screenshot
agent-browser diff url <url1> <url2> --selector "#main"  # Scoped
```

### JavaScript Evaluation
```bash
agent-browser eval 'document.title'
agent-browser eval 'document.querySelectorAll("img").length'
agent-browser eval 'JSON.stringify(Object.keys(localStorage))'

# Complex JS (use --stdin to avoid shell escaping)
agent-browser eval --stdin <<'EVALEOF'
JSON.stringify(
  Array.from(document.querySelectorAll("img"))
    .filter(i => !i.alt)
    .map(i => ({ src: i.src, width: i.width }))
)
EVALEOF
```

### Downloads & Clipboard
```bash
agent-browser download @e1 ./file.pdf     # Click to trigger download
agent-browser wait --download ./output.zip # Wait for download
agent-browser clipboard read              # Read clipboard
agent-browser clipboard write "text"      # Write to clipboard
```

### Viewport & Device Emulation
```bash
agent-browser set viewport 375 812        # iPhone SE
agent-browser set device "iPhone 14"      # Full device emulation (viewport + UA)
agent-browser set viewport 768 1024       # iPad
agent-browser set viewport 1440 900       # Desktop
agent-browser --color-scheme dark open <url>  # Dark mode
```

### Accessibility
```bash
agent-browser a11y audit                  # Run accessibility audit
agent-browser a11y tree                   # Show accessibility tree
```

---

## Browser Configuration

| Setting | Default | Description |
|---------|---------|-------------|
| Headless | Yes | Run without visible window |
| Timeout | 25s | Default timeout (`AGENT_BROWSER_DEFAULT_TIMEOUT`) |
| Engine | Chrome | Also: `lightpanda` (10x faster, 10x less memory) |

```bash
# Use Lightpanda for speed (CI/CD)
agent-browser --engine lightpanda open <url>
```

---

## Error Handling

| Error | Resolution |
|-------|-----------|
| Navigation timeout | `wait --load networkidle` or increase timeout |
| Element not found | `snapshot -i` → verify ref exists |
| Click intercepted | Scroll into view or close overlay |
| Stale refs | Re-snapshot after DOM changes (click, navigate, modal) |
| Session crashed | `agent-browser close` → restart |
