# agenTeach

A reusable framework for AI-assisted interactive learning. Works with any AI agent (Claude, GPT, Cursor, Copilot) that can read markdown.

agenTeach turns AI agents into structured mentors that verify understanding, track learning progress, and adapt to your weak areas across sessions.

---

## Quick Start

1. **Use this template** (click "Use this template" on GitHub, or clone directly):
   ```
   git clone <your-repo-url> my-learning-project
   cd my-learning-project
   ```

2. **Open your AI agent** (Claude, GPT, Cursor, etc.) in this directory.

3. **Say:** *"Read the README and help me start learning [your topic]."*

4. The agent reads `.agenteach/onboarding/interview.md`, interviews you, and sets up your project right here.

That's it. After onboarding, your project directory has your learning files at root level, and the framework stays in `.agenteach/` for reference.

---

## One Repo Per Topic

Each agenTeach repository is one learning project about one topic. If you want to learn two unrelated subjects (e.g., Machine Learning and AWS), create two separate repos from this template. This keeps context focused and prevents knowledge files from mixing unrelated domains.

---

## For AI Agents

**If you are an AI agent reading this file:**

1. Read `.agenteach/onboarding/interview.md` — it contains the full onboarding interview script.
2. Conduct the interview with the learner.
3. Based on the answers, read `.agenteach/AGENTS.md` (core methodology) and the relevant `.agenteach/modes/` file.
4. Generate the learner's project files at root level (AGENTS.md, knowledge/, SESSION_LOG.md, etc.).
5. Do NOT modify files inside `.agenteach/` — they are read-only reference material.
6. After setup, follow the Session Protocol in the generated root-level AGENTS.md.

---

## How It Works

1. **Onboarding:** The agent interviews you about your topic, goals, skill level, and preferences.
2. **Project setup:** The agent creates your learning files (AGENTS.md, knowledge/, roadmap) at root level.
3. **Sessions:** Each session follows a protocol: verify previous knowledge → teach new concepts → practice → record outcomes.
4. **Adaptation:** The agent tracks your mistakes and breakthroughs in a learning journal (Dziennik nauki), targeting weak areas in future sessions.

---

## Two Modes

### Project-based (learn by building)

For topics where you build something while learning. Examples: building a neural simulation, creating a web app with a new framework.

Each concept is first explored in `playground/` (isolated script), then integrated into `src/` (the growing project).

### Concept-based (learn concepts / prepare for certification)

For topics without a coding project. Examples: AWS certification prep, studying distributed systems.

Uses scenario-based practice, spaced repetition, and deadline management.

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
    ├── modes/
    │   ├── project-based.md  # Rules for learn-by-building mode
    │   └── concept-based.md  # Rules for concept/cert learning mode
    ├── templates/            # Skeleton files copied during setup
    ├── onboarding/
    │   └── interview.md      # Onboarding interview script
    ├── examples/
    │   ├── neural-sim/       # Project-based example
    │   └── aws-solutions-architect/  # Concept-based example
    └── docs/
        └── philosophy.md     # Design rationale
```

After onboarding, your root will also contain: `AGENTS.md`, `knowledge/`, `SESSION_LOG.md`, `CHANGELOG.md`, and optionally `src/`, `playground/`.

---

## Key Concepts

**Session Protocol:** 5 steps — Orient, Verify, Teach, Practice, Record. No skipping.

**Active Learning Rules:** The agent ends explanations with comprehension checks. It doesn't continue until you answer correctly.

**Dziennik nauki (Learning Journal):** Each knowledge file includes a learning journal that tracks your mistakes, struggles, and breakthroughs. The agent reads this before every session. The Polish name "Dziennik nauki" is used as a structural term throughout the framework.

**Teaching Principles:** Intuition before formalism. Concrete before abstract. Always explain "why", not just "how".

---

## Design Philosophy

See [.agenteach/docs/philosophy.md](.agenteach/docs/philosophy.md) for the full rationale.

Extracted from a real, working educational project. The core insight: structured verification + persistent memory of learning outcomes beats ad-hoc Q&A.

---

## Version

Current framework version: **0.1.0**

When updating agenTeach in an existing project, compare the version comment at the top of `.agenteach/AGENTS.md` with your project's AGENTS.md. If the framework version is newer, review the changelog for migration notes.
