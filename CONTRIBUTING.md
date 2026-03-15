# Contributing to Paperclip Agent Swarm

## Adding a New Agent

Every agent lives in `agents/<agent-name>/` with exactly **4 files**:

| File | Purpose | Target Size |
|------|---------|-------------|
| `SOUL.md` | Persona + anti-patterns | ~30-40 lines |
| `AGENTS.md` | Role, scope, workflow, boundaries | ~20 lines |
| `TOOLS.md` | Skills (inline), commands, templates | ~80-150 lines |
| `HEARTBEAT.md` | Step-by-step checklist | ~40-60 lines |

### Steps

1. **Create folder**: `agents/<agent-name>/`
2. **Write SOUL.md**: Define persona, strategic posture, voice, and 3+ anti-patterns
3. **Write AGENTS.md**: Role (2 lines), scope (bullets), workflow (5 steps), boundaries
4. **Write TOOLS.md**: Runtime, Paperclip API, skills inline, templates
5. **Write HEARTBEAT.md**: Identity → setup → work → delivery → rules
6. **Update docs**: Add to `AGENTS_OVERVIEW.md`, `README.md` Mermaid diagram

### Conventions

- Skills are **embedded inline** in TOOLS.md — no external file references
- Every agent reads `../SHARED_CONFIG.md` for mandated stack + rules
- Use ✅/❌ for DO/DON'T lists
- Compact > verbose: aim for the target sizes above
- Anti-patterns in SOUL.md use format: "NEVER [action] — [reason]"

### Naming

- Folder: `kebab-case` (e.g., `stack-researcher`)
- Agent name: Title Case (e.g., "Stack Researcher")
