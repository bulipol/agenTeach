# Design Philosophy

## Why agenTeach Exists

Most AI-assisted learning is passive: you ask a question, the AI answers, you move on. There is no verification, no structure, no memory of what you struggled with yesterday.

agenTeach turns AI agents into structured mentors. It was extracted from a real, working educational project (NeuralSim) where the methodology proved effective over weeks of ML learning. The core insight: **a teaching protocol with verification, persistence, and adaptation produces better learning outcomes than ad-hoc Q&A.**

---

## Core Insight: The Session Protocol

The 5-step session protocol (Orient → Verify → Teach → Practice → Record) exists because each step prevents a specific failure mode:

| Step | Prevents |
|------|----------|
| **Orient** | Starting a session without context. The agent re-reads where you left off. |
| **Verify** | False confidence. You think you remember, but verification catches gaps. |
| **Teach** | Jumping to practice without understanding. Concepts are explained before applied. |
| **Practice** | Passive learning. You must actively do something (code or answer) to prove understanding. |
| **Record** | Forgetting what you struggled with. The learning journal persists across sessions. |

Skipping any step breaks the loop. Without verification, gaps compound. Without recording, the agent has no memory. Without teaching before practice, the learner is lost.

---

## Why Active Learning Rules Matter

Passive knowledge (reading, listening) feels like learning but rarely sticks. Active knowledge (answering, building, explaining back) creates durable understanding.

The most important rule is **#5: Active comprehension check** — ending every explanation with a question. This single rule transforms a monologue into a dialogue. If the learner gets it wrong, that mistake is more valuable than ten correct answers because it reveals a genuine misconception.

---

## Why Dziennik nauki (Learning Journal)

Without a learning journal, the AI agent starts every session from zero. It has no memory of:
- Which questions you answered incorrectly
- What misconceptions you had
- Where breakthroughs happened
- Which topics needed multiple explanations

With Dziennik nauki, the agent can:
- Target weak areas in review sessions
- Avoid repeating questions you already mastered
- Track your progression over weeks and months
- Adapt teaching approach based on what worked before

This is the closest thing to spaced repetition in an AI-assisted context — not algorithmic, but intentional and persistent.

---

## Why Two Modes

Not everything is learned by building code. Certifications require different practice formats (scenarios, quizzes). Theory-heavy domains have no natural "project" to build.

But the core protocol (verify → teach → practice → record) works for both. The modes are thin extensions on top of a shared foundation:

- **Project-based** swaps "practice" for "write code in src/"
- **Concept-based** swaps "practice" for "answer a scenario question"

Everything else — Teaching Principles, Active Learning Rules, Dziennik nauki, Session Protocol — is identical.

---

## Design Constraints

**Simplicity:** Every file earns its place. No bloat, no over-engineering.

**Agent-agnostic:** Works with any AI agent that can read markdown. No special tools, plugins, or APIs required.

**Standalone:** No dependencies, no build tools. Just markdown files in a directory.

**Generator, not runtime:** agenTeach is a template. The agent reads it once during onboarding, generates a learner-specific project, then works entirely within that project. agenTeach itself is never modified during learning.
