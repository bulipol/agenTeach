# LEARNER.md — Learner State

<!-- Generated during onboarding. This file holds dynamic learner state.
     AGENTS.md holds the static methodology. Keep this file small and up to date. -->

---

## Profile

- **Topic:** [TOPIC]
- **Goal:** [GOAL]
- **Mode:** [MODE] — `project-based` or `concept-based`
- **Skill level:** [SKILL_LEVEL] — beginner / intermediate / advanced
- **Language:** [LANGUAGE]
- **Code language:** [CODE_LANGUAGE]
- **Timeline:** [TIMELINE]
- **Profile:** guided  <!-- guided | autonomous — change with /teach:mode -->

---

## Decisions Made

These decisions were made during onboarding or sessions. Do not re-litigate unless the learner brings it up.

[DECISIONS — filled during onboarding. Examples:]
- [Communication language and code language choices]
- [Library/framework restrictions, if any]
- [Learning approach: build-first or theory-first]
- [Any strong preferences expressed by the learner]

---

## Roadmap

Topics with dependency graph. Only propose topics whose requirements are marked DONE.

| Topic | Status | Requires | Unlocks |
|-------|--------|----------|---------|
| [Topic 1] | DONE | — | [Topic 2], [Topic 3] |
| [Topic 2] | IN PROGRESS | [Topic 1] | [Topic 4] |
| [Topic 3] | NOT STARTED | [Topic 1] | [Topic 4] |
| [Topic 4] | BLOCKED | [Topic 2] + [Topic 3] | — |

**Status values:** DONE | IN PROGRESS | NOT STARTED | BLOCKED

**Navigation rule:** When a topic is marked DONE, check which new topics are now unblocked (all their requirements are DONE) and surface them with `/teach:next`.

---

## Knowledge Files

| File | Topic | Status |
|------|-------|--------|
| `knowledge/[filename].md` | [Topic name] | [not started \| in progress \| reviewed \| mastered] |

---

## Weak Areas

Aggregated from Dziennik nauki entries across all knowledge files. Update when a pattern of struggle is identified.

- [e.g., "useEffect cleanup — confused dependency array with cleanup return"]
- [e.g., "props drilling — understands the problem but not the solutions"]

---

## Overdue Reviews

Topics due for spaced repetition review. Update based on "Last Reviewed" dates in the roadmap.

| Topic | Last Reviewed | Due |
|-------|---------------|-----|
| [topic] | YYYY-MM-DD | YYYY-MM-DD |
