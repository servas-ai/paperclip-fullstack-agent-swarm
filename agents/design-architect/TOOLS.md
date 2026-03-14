# Tools

## Runtime
- **OpenCode** is your runtime.

## Paperclip API
- `GET /api/agents/me` — identity.
- `GET /api/companies/{companyId}/issues?assigneeAgentId={agentId}&status=todo,in_progress,blocked` — inbox.
- `PATCH /api/issues/{issueId}` — status updates. Include `X-Paperclip-Run-Id`.

---

## Impeccable Design — [pbakaus/impeccable](https://github.com/pbakaus/impeccable)

> "If someone said 'AI made this,' would they believe immediately? If yes, that's the problem."

### Step 1 — Design Direction (MANDATORY before any design)
1. **Purpose** → What problem does this interface solve? Who uses it?
2. **Tone** → Pick an extreme: brutally minimal · maximalist chaos · retro-futuristic · organic/natural · luxury/refined · playful/toy-like · editorial/magazine · brutalist/raw · art deco/geometric · soft/pastel · industrial/utilitarian
3. **Differentiation** → What's the ONE thing someone will remember?
4. **Constraints** → Framework, performance, accessibility

**CRITICAL**: Bold maximalism and refined minimalism both work — the key is **intentionality, not intensity**. Never converge on common choices. EVERY design must be unique.

---

### Typography
> Reference: [typography.md](https://github.com/pbakaus/impeccable/blob/main/source/skills/frontend-design/reference/typography.md)

- ✅ **DO**: Modular type scale with fluid sizing `clamp()`
- ✅ **DO**: Vary font weights and sizes for clear visual hierarchy
- ✅ **DO**: Choose beautiful, unique fonts. Pair distinctive display + refined body
- ❌ **DON'T**: Inter, Roboto, Arial, Open Sans, system defaults — *overused*
- ❌ **DON'T**: Monospace as lazy "technical/developer" shorthand
- ❌ **DON'T**: Large icons with rounded corners above every heading — *templated*

**Recommended fonts**: Instrument Sans, Plus Jakarta Sans, Outfit, Fraunces, Geist, Space Grotesk, Satoshi, Cabinet Grotesk

### Color — OKLCH (not HSL)
> Reference: [color-and-contrast.md](https://github.com/pbakaus/impeccable/blob/main/source/skills/frontend-design/reference/color-and-contrast.md)

```css
--color-primary: oklch(60% 0.15 250);        /* Perceptually uniform */
--gray-100: oklch(95% 0.01 60);              /* Tinted neutrals, NOT pure gray */
```

- ✅ **DO**: `oklch()`, `color-mix()`, `light-dark()` for maintainable palettes
- ✅ **DO**: Tint neutrals toward brand hue — subtle hint = subconscious cohesion
- ✅ **DO**: 60-30-10 rule: 60% neutral, 30% secondary, 10% accent
- ❌ **DON'T**: Gray text on colored backgrounds → use shade of bg color
- ❌ **DON'T**: Pure `#000` or `#fff` — always tint; pure doesn't exist in nature
- ❌ **DON'T**: The AI palette: cyan-on-dark, purple-to-blue gradients, neon accents
- ❌ **DON'T**: Gradient text for "impact" — decorative, not meaningful
- ❌ **DON'T**: Default to dark mode with glowing accents — lazy, not designed
- **Dark mode** ≠ inverted light → reduce chroma, adjust contrast independently

### Layout — 4pt Grid
> Reference: [spatial-design.md](https://github.com/pbakaus/impeccable/blob/main/source/skills/frontend-design/reference/spatial-design.md)

- Scale: 4, 8, 12, 16, 24, 32, 48, 64, 96px
- ✅ **DO**: Create visual rhythm through varied spacing — tight groupings, generous separations
- ✅ **DO**: Fluid spacing with `clamp()` that breathes on larger screens
- ✅ **DO**: Asymmetry and unexpected compositions — break the grid intentionally
- ✅ **DO**: `gap` not margins · Container queries for components · Viewport queries for pages
- ❌ **DON'T**: Wrap everything in cards — not everything needs a container
- ❌ **DON'T**: Cards inside cards — flatten the hierarchy
- ❌ **DON'T**: Identical card grids — same size, icon + heading + text, endlessly repeated
- ❌ **DON'T**: Hero metric layout template — big number, small label, gradient accent
- ❌ **DON'T**: Center everything — left-aligned with asymmetric layouts feels more designed
- ❌ **DON'T**: Same spacing everywhere — without rhythm, layouts feel monotonous
- **Squint Test**: blur eyes → can you still see hierarchy?

### Visual Details
- ✅ **DO**: Intentional, purposeful decorative elements that reinforce brand
- ❌ **DON'T**: Glassmorphism everywhere — blur/glass/glow used decoratively, not purposefully
- ❌ **DON'T**: Rounded elements with thick colored border on one side — lazy accent
- ❌ **DON'T**: Sparklines as decoration — tiny charts that convey nothing meaningful
- ❌ **DON'T**: Rounded rectangles with generic drop shadows — safe, forgettable
- ❌ **DON'T**: Modals unless truly no better alternative — modals are lazy

### Motion — 100/300/500 Rule
> Reference: [motion-design.md](https://github.com/pbakaus/impeccable/blob/main/source/skills/frontend-design/reference/motion-design.md)

| Duration | Use | Easing |
|----------|-----|--------|
| 100-150ms | Button, toggle | `cubic-bezier(0.25, 1, 0.5, 1)` ease-out-quart |
| 200-300ms | Menu, tooltip | `cubic-bezier(0.16, 1, 0.3, 1)` ease-out-expo |
| 300-500ms | Modal, drawer | Exit = 75% of enter duration |

- ✅ **DO**: Staggered reveals on page load — ONE well-orchestrated moment > scattered micro-interactions
- ✅ **DO**: For height: `grid-template-rows` transitions, not animating `height`
- ✅ **DO**: Only `transform` + `opacity` — never width/height/padding/margin
- ✅ **DO**: `prefers-reduced-motion` = MANDATORY
- ❌ **DON'T**: Bounce/elastic easing — dated and tacky; real objects decelerate smoothly

### Interaction
> Reference: [interaction-design.md](https://github.com/pbakaus/impeccable/blob/main/source/skills/frontend-design/reference/interaction-design.md)

- ✅ **DO**: **Optimistic UI** — update immediately, sync later. Instagram likes work offline — UI updates instantly
- ✅ **DO**: **Progressive disclosure** — start simple, reveal sophistication through interaction
- ✅ **DO**: **Empty states that teach** — not just "nothing here," show HOW to use the interface
- ✅ **DO**: Make every interactive surface feel intentional and responsive
- ❌ **DON'T**: Repeat information — redundant headers, intros that restate the heading
- ❌ **DON'T**: Every button primary — ghost, text links, secondary; **hierarchy matters**

### Responsive
> Reference: [responsive-design.md](https://github.com/pbakaus/impeccable/blob/main/source/skills/frontend-design/reference/responsive-design.md)

- ✅ **DO**: Container queries `@container` for component-level responsiveness
- ✅ **DO**: Adapt the interface for different contexts — don't just shrink it
- ❌ **DON'T**: Hide critical functionality on mobile — adapt, don't amputate

### UX Writing
> Reference: [ux-writing.md](https://github.com/pbakaus/impeccable/blob/main/source/skills/frontend-design/reference/ux-writing.md)

- ✅ **DO**: Make every word earn its place
- ✅ **DO**: Buttons = verb + noun ("Create Project", not "Submit")
- ✅ **DO**: Error messages = what went wrong + how to fix it
- ❌ **DON'T**: Repeat information users can already see

---

## The AI Slop Test — 16 Anti-Patterns

Before delivering ANY design, check EVERY item:

| # | Anti-Pattern | What to Look For |
|---|-------------|-----------------|
| 1 | Overused fonts | Inter, Roboto, Arial, Open Sans? → CHANGE |
| 2 | Pure black/white | `#000` or `#fff`? → Tint |
| 3 | Gray on color | Gray text on colored background? → Use shade |
| 4 | Card-in-card | Nested cards? → Flatten hierarchy |
| 5 | Identical card grids | Same-size icon+heading+text repeated? → Vary |
| 6 | Bounce/elastic easing | Any bounce animation? → Exponential easing |
| 7 | Glassmorphism everywhere | Blur/glass/glow decorative? → Remove or justify |
| 8 | Cyan-on-dark | AI palette (cyan, purple-blue gradient)? → CHANGE |
| 9 | Gradient text | Gradient on headings/metrics? → Solid color |
| 10 | Hero metric template | Big number + small label + gradient? → Redesign |
| 11 | Sparkline decoration | Tiny charts conveying nothing? → Remove |
| 12 | One-sided borders | Thick colored border on one side? → Remove |
| 13 | Generic shadows | Rounded rect + drop shadow? → Be specific |
| 14 | Center everything | All-centered layout? → Asymmetric |
| 15 | Monospace = "tech" | Monospace for "developer vibes"? → Use proper fonts |
| 16 | Dark + glow = "cool" | Dark mode + glow accents as default? → Design intentionally |

---

## Additional Skills
| Skill | Use |
|-------|-----|
| `web-design-guidelines` (155K) | Compliance check against Vercel standards |
| `ui-ux-pro-max` (56K) | A11y: contrast ≥4.5:1, touch ≥44px, heading hierarchy |
| `frontend-design-system` (8K) | Token workflow |

---

## DESIGN_SPEC.md Template

```markdown
# DESIGN_SPEC: [Feature Name]

## Direction
- Tone: [e.g. editorial/magazine]
- Differentiation: [the ONE memorable thing]
- Inspiration: [specific references, NOT generic]

## Tokens
- Colors: OKLCH, tinted neutrals, 60-30-10
- Typography: [font], fluid clamp() scale (5 sizes)
- Spacing: 4pt grid (4/8/12/16/24/32/48/64/96)
- Motion: 100/300/500 rule, exponential easing only
- Shadows: subtle, purposeful (not generic drop shadows)

## Layout (Desktop / Tablet / Mobile)
[Grid, breakpoints, container queries for components]

## Components
[Name → States (default/hover/active/focus/disabled/loading/error) → Variants → A11y]

## AI Slop Checklist
- [ ] Unique fonts (no Inter/Roboto/Arial)
- [ ] No pure black/white · No gray on color
- [ ] No card-in-card · No identical card grids
- [ ] No bounce easing · No gradient text
- [ ] No cyan-on-dark · No glassmorphism-everywhere
- [ ] No all-centered layout · No hero metric template
- [ ] prefers-reduced-motion supported
```
