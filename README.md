# agenTeach

A reusable framework for AI-assisted interactive learning. Works with any AI agent (Claude, Cursor, Codex, OpenCode) that can read markdown.

agenTeach turns AI agents into structured mentors that verify understanding, track learning progress, and adapt to your weak areas across sessions.

---

## Quick Start

### Option A — CLI (recommended)

```bash
npx agenteach
```

Run this in any empty directory. The CLI downloads the framework and installs IDE skills for your tool of choice. Then open your IDE in that folder and type `/teach-start`.

> `npx agenteach` downloads from this repo at setup time and installs the `/teach-*` skill files for your IDE. The CLI source is at [bulipol/agenteach-cli](https://github.com/bulipol/agenteach-cli).

### Option B — Use this template

Click **"Use this template"** on GitHub, or clone directly:

```bash
git clone https://github.com/bulipol/agenTeach my-learning-project
cd my-learning-project
```

Then open your AI agent in the directory and type `/teach-start`.

---

## One Repo Per Topic

Each agenTeach repository is one learning project about one topic. If you want to learn two unrelated subjects (e.g., Machine Learning and AWS), create two separate repos. This keeps context focused and prevents knowledge files from mixing unrelated domains.

---

## How It Works

1. **Onboarding:** The agent interviews you about your topic, goals, skill level, and preferences.
2. **Project setup:** The agent creates your learning files (`AGENTS.md`, `knowledge/`, roadmap) at root level.
3. **Sessions:** Each session follows a 5-step protocol: Orient → Verify → Teach → Practice → Record. No skipping.
4. **Adaptation:** The agent tracks mistakes and breakthroughs in a learning journal (Dziennik nauki), targeting weak areas in future sessions.

---

## Two Modes

### Project-based (learn by building)

For topics where you build something while learning. Examples: building a neural simulation, creating a web app with a new framework.

Each concept is first explored in `playground/` (isolated script), then integrated into `src/` (the growing project).

### Concept-based (learn concepts / prepare for certification)

For topics without a coding project. Examples: AWS certification prep, studying distributed systems.

Uses scenario-based practice, spaced repetition, and deadline management.

---

## Key Concepts

**Session Protocol:** Every session runs 5 steps — Orient (review previous session), Verify (check retention from last time), Teach (new concept), Practice (hands-on), Record (update knowledge files). Steps cannot be skipped. This mirrors spaced repetition research: retrieval before new input improves long-term retention.

**Slash Commands:** Navigation shortcuts the agent recognizes at any point.
- `/teach-start` — begin or resume a session
- `/teach-next` — show what's next (always asks for confirmation first)
- `/teach-status` — full progress dashboard: roadmap, session count, weak areas
- `/teach-mode` — switch between guided and autonomous profiles
- `/teach-stop` — end the session and save all progress
- `/teach-help` — list all commands

**LEARNER.md:** Your learner state lives in a separate file — profile, roadmap with dependency graph, decisions, and weak areas. `AGENTS.md` holds methodology. This split keeps each file small and focused.

**Learner Profiles:** Two modes. **Guided** (default) — step-by-step with confirmation at each stage. **Autonomous** — more content at once, fewer checkpoints. Switch anytime with `/teach-mode`. Both always ask for confirmation on `/teach-next`.

**Active Learning Rules:** The agent ends every explanation with a comprehension check. It doesn't advance until you answer correctly. This enforces active recall rather than passive reading.

**Persistent State:** All learning outcomes persist across sessions in `knowledge/*.md` files. Each file includes a Dziennik nauki (learning journal) that tracks mistakes, struggles, and breakthroughs. The agent reads this at the start of every session so context is never lost.

**Teaching Principles:** Intuition before formalism. Concrete before abstract. Always explain "why", not just "how".

---

## Repository Structure

```
agenTeach/
├── README.md                 # This file (entry point)
├── .gitignore
│
└── .agenteach/               # Framework files (read-only reference)
    ├── AGENTS.md             # Core teaching methodology
    ├── CLAUDE.md             # Claude Code-specific extensions
    ├── commands.md           # /teach-* slash command definitions
    ├── modes/
    │   ├── project-based.md  # Rules for learn-by-building mode
    │   └── concept-based.md  # Rules for concept/cert learning mode
    ├── templates/
    │   ├── learner-profile.md  # LEARNER.md template (generated at root)
    │   ├── knowledge-file.md   # knowledge/*.md template
    │   └── ...
    ├── onboarding/
    │   └── interview.md      # Onboarding interview script
    ├── examples/
    │   ├── neural-sim/       # Project-based example
    │   └── aws-solutions-architect/  # Concept-based example
    └── docs/
        └── philosophy.md     # Design rationale
```

After onboarding, your root will also contain: `AGENTS.md`, `LEARNER.md`, `knowledge/`, `SESSION_LOG.md`, `CHANGELOG.md`, and optionally `src/`, `playground/`.

---

## Design Philosophy

See [.agenteach/docs/philosophy.md](.agenteach/docs/philosophy.md) for the full rationale.

Extracted from a real, working educational project. The core insight: structured verification + persistent memory of learning outcomes beats ad-hoc Q&A.

---

## Version

Current framework version: **0.1.0**

When updating agenTeach in an existing project, compare the version comment at the top of `.agenteach/AGENTS.md` with your project's AGENTS.md. If the framework version is newer, review the changelog for migration notes.

---

## For AI Agents

**If you are an AI agent reading this file:**

1. Read `.agenteach/AGENTS.md` (methodology), `.agenteach/commands.md` (navigation commands), and `.agenteach/onboarding/interview.md` (onboarding script).
2. Parse the learner's first message — auto-detect topic, mode, level, and language before asking questions.
3. Conduct the interview with the learner (2–3 exchanges, not 5–8).
4. Based on the answers, read the relevant `.agenteach/modes/` file.
5. Generate the learner's project files at root level: `AGENTS.md`, `LEARNER.md`, `knowledge/`, `SESSION_LOG.md`, etc.
6. Do NOT modify files inside `.agenteach/` — they are read-only reference material.
7. After setup, follow the Session Protocol in the generated root-level `AGENTS.md`. Recognize `/teach-*` commands throughout the conversation.
