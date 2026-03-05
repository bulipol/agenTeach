# Concept-Based Mode

Read `AGENTS.md` first. This file extends the core protocol for learning concepts, preparing for certifications, or studying theory without a coding project.

---

## When to Use

The learner wants to understand concepts without building a specific project. Examples: preparing for AWS Solutions Architect exam, studying distributed systems theory, learning design patterns, mastering a domain like networking or security.

---

## Project Structure

Concept-based learning uses a minimal directory structure:

| Path | Purpose |
|------|---------|
| `knowledge/` | Learner's notes organized by topic. Updated after each session. |
| `scenarios/` | (Optional) Practice scenarios, case studies, and worked examples. |

No `src/`, no `playground/` — this is not a coding project. If the learner wants to experiment with code snippets to understand a concept, include them directly in the `knowledge/*.md` file.

### Scenarios (optional)

Use `scenarios/` when a topic benefits from reusable practice materials — especially for certification prep where the same scenario format appears on the exam. Create a scenario file when:
- A topic has 3+ practice questions worth saving for later review
- The learner needs to practice a specific question format repeatedly (e.g., AWS-style multi-choice)

**Scenario file structure:**
```markdown
# [Topic] — Practice Scenarios

## Scenario 1: [short title]
**Setup:** [describe the situation]
**Question:** [what should the learner decide/design/recommend?]
**Answer:** [correct answer with reasoning — hidden until the learner attempts]

## Scenario 2: ...
```

If you don't need reusable scenarios, skip `scenarios/` entirely — practice questions can live directly in the session conversation.

---

## Dashboard (`/teach:status`)

When the learner runs `/teach:status`, show this format for concept-based mode. **Output as a code block** (wrap in ` ``` `) so formatting renders correctly.

```
--- DASHBOARD ---
Temat: [TOPIC]
Typ nauki: concept-based | Poziom: [SKILL_LEVEL] | Tryb: [guided|autonomous]

Roadmapa: [X]/[Y] tematów ([Z]%)
  [##--------] [Temat] — W TRAKCIE | Waga: [%]
  [----------] [Temat] — DO ZROBIENIA | Waga: [%]
  Odblokowane: [tematy gotowe do rozpoczęcia]

Słabe strony: [z LEARNER.md, lub "brak"]
Zaległe powtórki: [lub "brak"]
Sesji: [N] | Ostatnia: [data]
Następny krok: [z SESSION_LOG.md]

Walidacja:
  - LEARNER.md: [OK | BRAK]
  - SESSION_LOG: [OK | brak wpisu z ostatniej sesji]
  - Roadmapa: [OK | N tematów bez knowledge files]
  - Powtórki: [OK | N zaległych]
---
```

To compute overdue reviews: check "Last Reviewed" dates in the roadmap against the spaced repetition schedule below.

---

## Roadmap Format

Concept-based learning uses a single topic list, optionally weighted by importance.

### Topics

| Topic | Status | Weight | Last Reviewed |
|-------|--------|--------|---------------|
| [topic] | ⏳ Not started | [importance or exam %] | — |
| [topic] | 📖 In progress | [importance or exam %] | YYYY-MM-DD |
| [topic] | ✅ Reviewed | [importance or exam %] | YYYY-MM-DD |
| [topic] | 🧠 Mastered | [importance or exam %] | YYYY-MM-DD |

**Status progression:** Not started → In progress → Reviewed → Mastered

**Priority rules:**
- If the learner has a deadline (exam date), prioritize high-weight topics first.
- If no deadline, follow a logical dependency order (fundamentals before advanced topics).
- Flag topics at risk of not being covered before the deadline.

---

## Session Protocol Step 4 — Practice

When the core protocol reaches Step 4 (Practice/Implement), concept-based mode does this instead of coding:

### Practice Activities

Choose the activity that best fits the topic:

1. **Quiz questions** — Multiple choice or short answer. Present quiz questions using numbered options:

   ```
   **Q:** [Question in LANGUAGE]

   1. [Option A]
   2. [Option B]
   3. [Option C]
   4. [Option D]
   ```

   The learner responds with a number or natural language. Wait for the learner's answer, then reveal the correct answer with explanation.

2. **Scenario analysis** — Present a real-world scenario (e.g., "A company needs to serve static assets globally with low latency. What AWS service would you recommend and why?"). Wait for the learner's reasoning before providing feedback.

3. **Compare and contrast** — Ask the learner to compare two approaches, technologies, or patterns. Look for understanding of trade-offs, not just definitions.

4. **"What would happen if..."** — Present a hypothetical change to a system or concept and ask the learner to predict the outcome.

5. **Teach-back** — Ask the learner to explain a concept as if teaching someone else. This reveals gaps in understanding.

### Practice Rules

- Always wait for the learner's answer before revealing the correct one.
- If wrong: explain why, then ask again from a different angle.
- If right: confirm and optionally add nuance or edge cases.
- Record outcomes in Dziennik nauki (wrong answers are the most valuable data).

---

## Spaced Repetition

Concept-based mode uses a simple spaced repetition schedule to prevent forgetting:

### Review Schedule

After initial learning, a topic should be reviewed at increasing intervals:
- **1 day** after first learning
- **3 days** after first review
- **7 days** after second review
- **14 days** after third review
- After that: monthly or on demand

### How to Apply

At the start of each session (Step 2 — Verify previous knowledge):
1. Check the roadmap for topics where "Last Reviewed" is overdue
2. Check Dziennik nauki for topics with recorded struggles
3. Include 1–2 review questions from overdue or weak topics before new content
4. Update "Last Reviewed" date in the roadmap after review

**Overdue signal:** In the Protocol Compliance Checkpoint (SESSION START block), list any overdue topics: `Overdue reviews: [topic1] (7 days late), [topic2] (3 days late)`. This makes overdue topics visible to both the agent and the learner at session start.

### When to Mark "Mastered"

A topic can be marked 🧠 Mastered when:
- The learner has answered correctly across 3+ separate review sessions
- The learner can explain the concept in their own words
- The learner can apply the concept to novel scenarios (not just memorized answers)

**Tracking reviews:** In each topic's Dziennik nauki, count the number of separate sessions where the learner answered review questions correctly. When this count reaches 3, the topic is eligible for Mastered status. The agent should note the review count when updating Dziennik nauki: `Review session [N]/3 — correct`.

---

## Timeline Management

If the learner has a deadline (exam, course completion):

1. **Calculate sessions remaining:** (deadline - today) × sessions per week
2. **Map topics to sessions:** High-weight topics get more sessions. Low-weight topics may be compressed.
3. **Track progress:** At each session start, briefly assess whether the learner is on track.
4. **Raise alerts:** If a high-weight topic hasn't been started and the deadline is approaching, flag it explicitly.

---

## Commit Types

- `learn:` — new knowledge file or updated existing one
- `docs:` — documentation or README changes

No `feat:`, `playground:`, or `refactor:` — there is no code to change.
