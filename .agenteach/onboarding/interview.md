# Onboarding Interview

This script guides the AI agent through the initial interview with a new learner. The agent reads this file, conducts the interview conversationally, then generates a project-specific AGENTS.md from the answers.

---

## Instructions for the Agent

- Ask questions **one phase at a time** (not all at once)
- Be conversational, not interrogative — this is a dialogue, not a form
- Adapt follow-up questions based on answers
- If the learner provides a documentation link or resource, read it to understand the topic scope
- At the end: summarize all choices and ask for confirmation before generating files
- **Question formatting:** Follow `.agenteach/question-formats.md` for how to present choices, confirmations, and transitions. Each question below is annotated with its type.

---

## Phase 1 — Topic and Goals

**Q1:** "What do you want to learn?"
- Free text. The agent categorizes into a domain.
- If the learner provides a link (e.g., documentation URL), the agent should read it to understand the scope.

**Q2:** "What's your goal?"
- Type: **Quick Choice**
- Options:
  1. Build something specific → MODE = `project-based`
  2. Understand concepts / prepare for exam → MODE = `concept-based`
- If ambiguous (e.g., "I want to learn React"), the agent asks: "Do you want to build a specific project with React, or learn React concepts systematically? Or both?"
- The learner can also type their own answer — the agent determines MODE from their intent.

**Determine MODE here.** All subsequent questions branch based on this choice.

---

## Phase 2 — Skill Level

**Q3:** "How much do you already know about [TOPIC]?"
- Type: **Quick Choice**
- Options:
  1. Never touched it → beginner
  2. Read about it / watched tutorials → beginner-plus
  3. Built small things / did exercises → intermediate
  4. Used it professionally / built real projects → advanced

**Q4:** "Is there anything specific you already understand well? Anything you know you struggle with?"
- This seeds the initial roadmap priorities and the first Dziennik nauki entries.
- If the learner mentions weak areas, note them for early coverage.

---

## Phase 3 — Communication Preferences

**Q5:** "What language should we communicate in? (for explanations, questions, knowledge files)"
- Type: **Quick Choice**
- Options:
  1. English
  2. Polski
  3. Other (agent asks which)
- Sets [LANGUAGE] in AGENTS.md.

**Q6:** "Any preferences for how I teach?"
- More examples / more theory / faster pace / slower pace
- Stored in Decisions Made section.
- If no preference: use default (balanced, follow Teaching Principles).

---

## Phase 4 — Mode-Specific Questions

### If project-based:

**Q7:** "What do you want to build?"
- Concrete project description. If vague, help the learner refine it through dialogue.
- If the learner has no idea: suggest a project based on the topic that covers key concepts progressively.

**Q8:** "What tech stack? (or should I suggest one?)"
- Sets [TECH_STACK] in the mode extension.
- If the learner is unsure, suggest based on the topic and their skill level.

**Q9:** "Any strong opinions on libraries, frameworks, or patterns?"
- Example: "I want to build everything from scratch" or "Use established libraries for non-core stuff"
- Sets [LIBRARY_DECISIONS] in Decisions Made.

**Q10:** "Have you started already, or is this from scratch?"
- If started: agent should read existing code to understand the current state.
- If from scratch: agent will create the project structure.

### If concept-based:

**Q7:** "Is this for a specific exam or certification? Which one?"
- If yes: agent looks up the exam structure (domains, weights) to build a weighted roadmap.
- If no: agent builds a dependency-ordered topic list.

**Q8:** "Do you have a deadline? (exam date, course end date)"
- Sets [TIMELINE] in AGENTS.md.
- If yes: agent will manage timeline and flag at-risk topics.

**Q9:** "Do you have study materials already? (books, courses, documentation links)"
- If yes: agent can reference them for content and structure.
- If no: agent proposes a topic structure based on the domain.

**Q10:** "Any specific topics or domains you know are your weak spots?"
- Prioritizes these in the roadmap.
- Seeds initial Dziennik nauki awareness.

---

## Phase 5 — Confirmation

The agent presents a structured summary:

```
Here's what I understood:

**Topic:** [TOPIC]
**Goal:** [GOAL]
**Mode:** [MODE]
**Skill level:** [SKILL_LEVEL]
**Language:** [LANGUAGE]
**Timeline:** [TIMELINE]

**Key decisions:**
- [decision 1]
- [decision 2]
- ...

**Proposed roadmap (high level):**
[For project-based: Track A stages + Track B topics]
[For concept-based: Topic list with weights/priorities]

**Project structure:**
[Directory tree showing what will be created]
```

- Type: **Yes/No**
- Options:
  1. Looks good, let's start
  2. I want to change something

**Only after learner confirms:** proceed to file generation.

---

## File Generation Checklist

**Important architecture note:** This repo IS the learner's project. The framework lives in `.agenteach/` (read-only, never modified). The agent generates learner files at the **root level** of the repo.

**Where to read from:**
- Templates: `.agenteach/templates/`
- Core methodology: `.agenteach/AGENTS.md`
- Mode rules: `.agenteach/modes/project-based.md` or `.agenteach/modes/concept-based.md`
- Examples (for reference): `.agenteach/examples/`

**Where to generate (root level):**

- [ ] `AGENTS.md` — filled in from `.agenteach/AGENTS.md` template + mode extension + interview answers. This is the project's own AGENTS.md (NOT a copy of the template — it has real values, not placeholders).
- [ ] `CLAUDE.md` — from `.agenteach/CLAUDE.md` template (if using Claude)
- [ ] `README.md` — overwrite the existing README with a project-specific one (what is being learned, goals, structure)
- [ ] `knowledge/` directory — empty, or with first topic file seeded from `.agenteach/templates/knowledge-file.md`
- [ ] `SESSION_LOG.md` — from `.agenteach/templates/session-log.md`
- [ ] `CHANGELOG.md` — from `.agenteach/templates/changelog.md`
- [ ] Update `.gitignore` — add project-specific ignores (node_modules, etc.)
- [ ] Include the Protocol Compliance Checkpoint section with the two status block templates (SESSION START and SESSION END)

**Project-based only:**
- [ ] `src/` directory (empty)
- [ ] `playground/` directory (empty)
- [ ] `reference/` directory (if learner has existing materials)

**Do NOT modify anything inside `.agenteach/`.** It stays as read-only reference material for the duration of the project.

**Post-generation validation:** Before starting the first session, verify the generated project:
- [ ] AGENTS.md has all sections filled in (no remaining `[PLACEHOLDER]` text)
- [ ] AGENTS.md has the Protocol Compliance Checkpoint with both status block templates
- [ ] `knowledge/` directory exists (with at least one seed file or empty)
- [ ] SESSION_LOG.md exists
- [ ] Roadmap has at least one entry

If anything is missing, fix it now before proceeding.

**After file generation:** Begin the first session immediately (Step 1 of Session Protocol in the newly generated root-level AGENTS.md).
