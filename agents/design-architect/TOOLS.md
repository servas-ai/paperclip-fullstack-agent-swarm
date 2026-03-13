# Tools

## Runtime
- **OpenCode** is your runtime.

## Paperclip API
- `GET /api/agents/me` — identity.
- `GET /api/companies/{companyId}/issues?assigneeAgentId={agentId}&status=todo,in_progress,blocked` — inbox.
- `PATCH /api/issues/{issueId}` — status updates. Include `X-Paperclip-Run-Id`.

---

## Skills

### Impeccable Design — [pbakaus/impeccable](https://github.com/pbakaus/impeccable)

**Step 1 — Commit to a direction:**
1. Purpose → Tone → Constraints → Differentiation (what's UNFORGETTABLE?)
2. Pick an extreme: brutally minimal, editorial, retro-futuristic, luxury, playful, industrial...
3. **Bold maximalism and refined minimalism both work — the key is intentionality.**

### Typography
- **Avoid**: Inter, Roboto, Open Sans, Arial → use Instrument Sans, Plus Jakarta Sans, Outfit, Fraunces
- **Modular scale**: 5 sizes with high contrast. Fluid via `clamp()`
- **One font family** in multiple weights > two competing typefaces

### Color — OKLCH (not HSL)
```css
--color-primary: oklch(60% 0.15 250);        /* Perceptually uniform */
--gray-100: oklch(95% 0.01 60);              /* Tinted neutrals, NOT pure gray */
```
- **60-30-10**: 60% neutral, 30% secondary, 10% accent
- **Dark mode** ≠ inverted light mode → reduce chroma, adjust contrast
- **DON'T**: pure black/white, gray on colored bg, cyan-on-dark, gradient text

### Layout — 4pt Grid
- Scale: 4, 8, 12, 16, 24, 32, 48, 64, 96px
- Use `gap` not margins · Container queries for components · Viewport queries for pages
- **Squint Test**: blur eyes → can you still see hierarchy?
- **DON'T**: card-in-card, identical card grids, center everything, glassmorphism everywhere

### Motion — 100/300/500 Rule
| Duration | Use | Easing |
|----------|-----|--------|
| 100-150ms | Button/toggle | `--ease-out-quart: cubic-bezier(0.25, 1, 0.5, 1)` |
| 200-300ms | Menu/tooltip | `--ease-out-expo: cubic-bezier(0.16, 1, 0.3, 1)` |
| 300-500ms | Modal/drawer | Exit = 75% of enter duration |
- Only animate `transform` + `opacity` · `prefers-reduced-motion` = mandatory
- **DON'T**: bounce/elastic easing, generic `ease`

### AI Slop Test
> "If someone said 'AI made this,' would they believe immediately? If yes, that's the problem."

---

## Additional Skills
| Skill | Use |
|-------|-----|
| `web-design-guidelines` (155K) | Compliance check |
| `ui-ux-pro-max` (56K) | A11y: contrast ≥4.5:1, touch ≥44px, focus rings, heading hierarchy |
| `frontend-design-system` (8K) | Token workflow |
| `canvas-design` (17K) | Visual canvas |

---

## DESIGN_SPEC.md Template (Kurzform)

```markdown
# DESIGN_SPEC: [Feature Name]

## Direction
- Tone: [e.g. editorial/magazine]
- Differentiation: [the ONE memorable thing]

## Tokens
- Colors: OKLCH, tinted neutrals, 60-30-10
- Typography: [font], fluid clamp() scale
- Spacing: 4pt grid
- Motion: 100/300/500 rule, exponential easing
- Shadows: subtle (sm/md/lg)

## Layout (Desktop / Tablet / Mobile)
[Grid, breakpoints, container queries]

## Components
[Name → States (default/hover/active/focus/disabled/loading/error) → Variants → A11y]

## AI Slop Checklist
- [ ] No Inter/Roboto · No pure black/white · No card-in-card
- [ ] No bounce easing · No gradient text · No cyan-on-dark
```

---

## Shared Config
Read `../SHARED_CONFIG.md` for mandated stack and rules.
