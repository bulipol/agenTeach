# Project-Based Mode

Read `AGENTS.md` first. This file extends the core protocol for learning by building a project.

---

## When to Use

The learner wants to build something while learning. They have a concrete project idea (or will develop one during onboarding). Examples: building a neural simulation, creating a web app with a new framework, implementing a game engine from scratch.

---

## Project Structure

A project-based learning project uses these directories:

| Path | Purpose |
|------|---------|
| `src/` | Active project code. The main codebase being built. |
| `playground/` | Scratchpad for isolated experiments. Not imported by `src/`. |
| `knowledge/` | Learner's notes organized by topic. Updated after each session. |
| `reference/` | (Optional) Read-only archive of initial explorations or external examples. |

### Playground Rules

`playground/` is for learning, not production. Use it when:
- Introducing a new concept that benefits from an isolated experiment
- Building a small interactive demo (sliders, live output, visualizations)
- Running quick experiments before touching `src/`

Files in `playground/` are throwaway — they are not imported by `src/`.
Name them descriptively: `test-activation.js`, `auth-flow-demo.html`, `routing-experiment.ts`.

**Cleanup:** When a playground experiment has been integrated into `src/` and the learner has confirmed understanding, the playground file can be deleted. Review `playground/` at the end of each stage — remove files that have served their purpose. Don't let it become a junkyard.

### Playground Before src/

When a new concept is introduced, use `playground/` for isolated experiments first. Move to `src/` only when the concept is understood and tested. This prevents half-understood ideas from polluting the main codebase.

---

## Dashboard (`/teach:status`)

When the learner runs `/teach:status`, show this format for project-based mode:

```
--- DASHBOARD ---
Topic: [TOPIC]
Mode: project-based | Level: [SKILL_LEVEL] | Profile: [guided|autonomous]
Stack: [TECH_STACK]

Track A (Build): [X]/[Y] stages ([Z]%)
  [####------] Stage [N]: [name] — IN PROGRESS
  [----------] Stage [N+1]: [name] — NOT STARTED
  ...

Track B (Learn): [X]/[Y] topics done
  Done: [topic1], [topic2]
  Odblokowane: [topics ready to start based on dependency graph]
  Następne: [topics unlocked by current stage]

Słabe strony: [from LEARNER.md Weak Areas, or "brak"]
Sesji: [count] | Ostatnia: [date]
Next step: [from SESSION_LOG.md]

Walidacja:
  - LEARNER.md: [OK | MISSING]
  - SESSION_LOG: [OK | brak wpisu z ostatniej sesji]
  - Roadmapa: [OK | N tematów bez knowledge files]
---
```

---

## Roadmap Format

Project-based learning uses two parallel tracks:

### Track A — Build

Stage-based table showing what is being built, step by step.

| Stage | Status | Description |
|-------|--------|-------------|
| Stage 1: [name] | ⏳ Current | [what this stage builds] |
| Stage 2: [name] | ⏳ Planned | [what this stage builds] |
| ... | ... | ... |

**Rules:**
- Do not skip stages. Do not implement Stage 2 features when Stage 1 is current.
- Each stage introduces new concepts which are taught before implementation.
- When a stage is completed, update its status to ✅ Done.

### Track B — Learn

Topics studied alongside or after Track A. Each completed topic gets a `knowledge/*.md` file.

| Topic | Status | Connection to project |
|-------|--------|----------------------|
| [topic] | ✅ Done | [how it relates to the project] |
| [topic] | ⏳ After Stage X | [why it matters for that stage] |
| [topic] | ⏳ On demand | [when it would become relevant] |

**Navigation rules:**
- Topics marked **"After Stage X"** — introduce naturally when that Track A stage begins.
- Topics marked **"On demand"** — do NOT introduce unprompted, UNLESS it directly applies to something being built. When it applies, mention the connection and ask: "This relates to [topic] — want me to explain how it connects?"
- Track B can run **in parallel** with Track A — learner sets the pace.
- When a topic is completed: mark it ✅, create the `knowledge/*.md` file, update the table.

---

## Development Principles

These extend the core Teaching Principles for code-writing sessions:

1. **Simplicity first.** The smallest change that demonstrates the concept is the right change.

2. **[LIBRARY_DECISIONS]** — Filled during onboarding. Example: "No external ML libraries — everything from scratch" or "Use established libraries for non-core functionality."

3. **Stack:** [TECH_STACK] — Filled during onboarding. Example: "Node.js, TypeScript, Canvas 2D."

4. **Standalone modules.** Each new `src/` file should be runnable on its own before being integrated. This makes debugging and understanding easier.

5. **Minimal file changes.** State which files will be changed before making changes. Touch only what is necessary.

---

## Learning-to-Integration Flow

This is how new concepts become part of the growing project:

1. **Playground first** — New concept → small standalone script in `playground/`. Isolated, easy to understand, no dependencies on existing code. Example: `playground/test-streaming.ts`.

2. **Comprehension check** — The learner demonstrates understanding (Active Learning Rule #5). The agent does not proceed until the learner answers correctly.

3. **Integrate into src/** — Once understood, the concept is adapted and integrated into the main project in `src/`. The integrated version may look different from the playground experiment — it is shaped to fit the project's architecture.

4. **Project grows** — The main project grows lesson by lesson. Each lesson adds a real, functional piece. Over time, `src/` becomes a complete working project built from understood components.

**Why this flow matters:** If you skip the playground step and go straight to `src/`, half-understood code pollutes the codebase. If you stay in `playground/` forever, you never build anything real. The hybrid gives you both: safe experimentation AND a growing project.

---

## Session Protocol Step 4 — Implement

When the core protocol reaches Step 4 (Practice/Implement), project-based mode does this:

1. If the concept is new, **start in `playground/`** with an isolated experiment.
2. After the learner confirms understanding, **move to `src/`**.
3. Write code in `src/` following Teaching Principles and Development Principles.
4. Every new function introduced in code should follow this structure:
   - One sentence describing what it does
   - Key variables listed with types and example values
   - The math or logic shown as a code comment with real numbers (if applicable)
   - Then the implementation

---

## Commit Types

- `feat:` — new code in `src/`
- `learn:` — knowledge-only session (no code changed)
- `docs:` — documentation or README changes
- `playground:` — playground experiments only
- `refactor:` — restructuring existing code without changing behaviour
