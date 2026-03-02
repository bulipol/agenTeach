# Onboarding Interview

This script guides the AI agent through the initial interview with a new learner. The agent reads this file, conducts the interview conversationally, then generates a project-specific AGENTS.md from the answers.

---

## Instructions for the Agent

- Be conversational, not interrogative — this is a dialogue, not a form
- Adapt follow-up questions based on answers
- If the learner provides a documentation link or resource, read it to understand the topic scope
- **Be proactive:** propose concrete options instead of asking open-ended questions. The learner picks a number or writes their own answer.
- **Be efficient:** extract information from the learner's messages instead of re-asking. If the first message already contains the topic, don't ask Q1 again — confirm it.
- **Question formatting:** Follow `.agenteach/question-formats.md` for how to present choices, confirmations, and transitions.
- **Fast path:** If the learner says "defaults", "just set it up", or similar at any point — skip remaining questions, use sensible defaults, and jump to Phase 4 (Confirmation).

---

## Phase 0 — Welcome

Before asking any questions, the agent introduces the process. Keep it short (3–5 sentences):

1. **What this is:** "I'm your AI tutor. I'll guide you through learning [topic] step by step — with explanations, practice, and regular knowledge checks."
2. **How it works:** "First, a few quick questions to set up your learning plan. Then we start right away."
3. **How to answer:** "I'll give you numbered options — just type a number. You can always write your own answer if none fit."

Adapt the wording to [TOPIC] and keep it natural. Do NOT read this template verbatim. If the learner's first message already contains the topic, incorporate it into the welcome.

---

## Phase 1 — Topic, Goal, and Level

This phase collects three things: what to learn, how to learn it, and the starting level. Combine and skip questions when the learner's messages already provide the answers.

**Q1:** "What do you want to learn?"
- If the learner's first message already states the topic (e.g., "I want to learn AI agents"), **do not re-ask**. Confirm it: "Got it — [TOPIC]." and move to Q2.
- If the learner provides a link (e.g., documentation URL), the agent should read it to understand the scope.

**Q2:** "How do you want to learn?"
- Type: **Quick Choice**
- Options:
  1. Build a project — learn by building something concrete → MODE = `project-based`
  2. Study concepts — systematic learning, possibly for an exam → MODE = `concept-based`
- If ambiguous, the agent asks a clarifying follow-up.
- The learner can also type their own answer — the agent determines MODE from their intent.

**Q3:** "How much do you already know about [TOPIC]?"
- Type: **Quick Choice**
- Options:
  1. Nothing — never touched it → beginner
  2. A little — read/watched tutorials → beginner-plus
  3. Some — built small things / did exercises → intermediate
  4. A lot — used it professionally → advanced

**Conditional Q4 (only if level >= intermediate):** "Anything specific you already know well or struggle with?"
- Skip this for beginners — they don't know enough to answer usefully. The agent will discover gaps during sessions.
- For intermediate+: this seeds Dziennik nauki priorities and roadmap calibration.

---

## Phase 2 — Language

**Q5:** Detect the language the learner has been using and confirm it.
- Type: **Yes/No**
- Example: "We've been writing in Polish — should I continue in Polish for explanations and knowledge files?"
- Options:
  1. Yes
  2. No, I'd prefer [agent asks which language]
- Sets [LANGUAGE] in AGENTS.md.
- **Do NOT present a list of languages.** Just confirm the one already being used.

**Code language rule:** Regardless of [LANGUAGE], code and technical artifacts are always in English:
- Code: variable names, comments, function names → English
- Commit messages → English
- File names, directory names → English
- README.md → English

[LANGUAGE] applies to:
- Explanations, questions, and dialogue during sessions
- Knowledge files (`knowledge/*.md`) — content and Dziennik nauki
- Session log entries (the "Learned" and "Next step" parts)

The agent states this once during onboarding: "I'll explain everything in [LANGUAGE], but code and commits will be in English — that's the industry standard."

---

## Phase 3 — Setup

This phase configures the learning path. The agent is **proactive** — it proposes a concrete plan, the learner confirms or adjusts.

### If project-based:

**Q6:** The agent proposes a project AND tech stack together in one message:

"Based on [TOPIC] and your level, here are some project ideas:"
- Type: **Quick Choice** (agent-generated options)
- The agent proposes 3–4 concrete projects tailored to [TOPIC] and [SKILL_LEVEL]. Each project should progressively cover key concepts.
- Include the suggested tech stack in each option.
- Example for "AI agents" + beginner:
  1. CLI Agent (TypeScript + AI SDK) — terminal agent that reads files, searches the web, executes tasks
  2. Chatbot with tools (TypeScript + AI SDK) — bot that checks weather, calculates, searches
  3. Multi-agent pipeline (TypeScript + AI SDK) — multiple agents collaborating on a task
- The learner picks a number or writes their own idea.

**Defaults applied automatically (no questions asked):**
- Libraries: use established libraries for non-core stuff (focus on learning [TOPIC] itself)
- Starting point: from scratch
- If the learner has existing code or wants to build from scratch differently, they'll mention it. No need to ask.

### If concept-based:

**Q6:** The agent proposes an exam/structure AND timeline together:

"Here are common paths for learning [TOPIC]:"
- Type: **Quick Choice** (agent-generated options)
- The agent proposes likely certifications/exams for [TOPIC], plus a general option. Include timeline assumptions.
- Example for "AWS":
  1. AWS Solutions Architect Associate (SAA-C03) — at your own pace
  2. AWS Developer Associate (DVA-C02) — at your own pace
  3. General AWS knowledge — no specific exam, just understanding
- The learner picks a number or writes their own path.

**If the learner picks a specific exam, follow up:**

**Q7:** "Do you have a deadline for this?"
- Type: **Quick Choice**
- Options:
  1. No — learning at my own pace
  2. Yes (agent asks for the date)
- Sets [TIMELINE] in AGENTS.md.
- Skip this question for "general knowledge" path — default to no deadline.

**Defaults applied automatically (no questions asked):**
- Study materials: agent proposes a topic structure. If the learner has materials, they'll mention them.
- Teaching preferences: balanced approach (follow Teaching Principles). Learner can request changes anytime.

---

## Phase 4 — Confirmation

The agent presents a structured summary:

```
Here's the plan:

**Topic:** [TOPIC]
**Mode:** [MODE]
**Skill level:** [SKILL_LEVEL]
**Language:** [LANGUAGE]
**Timeline:** [TIMELINE]

**Project/Path:** [chosen project or study path]
**Tech stack:** [TECH_STACK] (project-based only)

**Proposed roadmap (high level):**
[For project-based: Track A stages + Track B topics]
[For concept-based: Topic list with weights/priorities]

**Defaults I'm using:**
- [list any defaults: libraries, from scratch, balanced teaching, etc.]
- You can change any of these anytime — just tell me.
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
