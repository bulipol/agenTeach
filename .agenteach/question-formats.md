# Question Formats

This file defines how the AI agent presents questions to the learner. It applies everywhere: onboarding, sessions, quizzes, and micro-transitions.

**Read this file** at onboarding start and follow it throughout all interactions.

---

## Core Principle

**Numbers are the universal shortcut.** When presenting options, number them. The learner can respond with:
- A **number** (`2`)
- **Natural language** (`I want to build a project`)
- **Their own answer** if none of the options fit

The agent always accepts all three. Never reject a response just because it doesn't match a predefined option — interpret the learner's intent.

**Do not explain this system.** Just use it consistently. The learner will pick it up naturally after 2–3 questions.

**All question text and options are presented in [LANGUAGE].**

---

## Question Types

### 1. Quick Choice

Use when there are 2–6 predefined options to pick from.

```
[Question in LANGUAGE]

1. [Option A]
2. [Option B]
3. [Option C]

(1/2/3 or your own answer)
```

The `(1/2/3 or your own answer)` hint at the end signals that shortcuts work AND that a custom response is welcome.

### 2. Yes/No

Use for confirmations and binary decisions.

```
[Question or summary in LANGUAGE]

1. [Affirmative option]
2. [Alternative option]

(1/2 or your own answer)
```

### 3. Open-Ended

Use when the answer is genuinely unpredictable. Just ask the question naturally.

**Important:** Even for open-ended questions, if you suggest examples or ideas for the learner to choose from, **always number them**. Never use bullet points or asterisks for suggested options. The learner can pick a number, write their own answer, or combine ideas.

```
[Question in LANGUAGE]

1. [Suggestion A]
2. [Suggestion B]
3. [Suggestion C]

(1/2/3 or your own answer)
```

### 4. Quiz

Use for multiple-choice practice questions (especially certification prep).

```
**Q:** [Question in LANGUAGE]

1. [Option A]
2. [Option B]
3. [Option C]
4. [Option D]
```

No `(1/2/3/4)` hint needed — the format is self-evident. Wait for the learner's answer before revealing the correct one.

### 5. Flow Control

Use for micro-transitions after feedback (e.g., "ready for next question?"). Keep it **inline and lightweight** — one line, not a full question block.

```
[Feedback on previous answer]

→ 1. [Continue option] | 2. [Alternative option]
```

Example: `→ 1. Next question | 2. Let's dig deeper`

The arrow (`→`) and inline format signal this is a quick transition, not a content question.

---

## Interview Question Mapping

| Question | Type | Options |
|----------|------|---------|
| Q1: What to learn? | Open-Ended | — |
| Q2: What's your goal? | Quick Choice | 1. Build a project / 2. Learn concepts |
| Q3: How much do you know? | Quick Choice | 1. Never touched / 2. Tutorials / 3. Small projects / 4. Professional |
| Q4: Strengths/weaknesses? | Open-Ended | — |
| Q5: What language? | Quick Choice | 1. English / 2. Polski / 3. Other |
| Q6: Teaching preferences? | Open-Ended | — |
| Q7–Q10: Mode-specific | Open-Ended | — |
| Phase 5: Confirmation | Yes/No | 1. Looks good / 2. I want to change something |

## Session Moment Mapping

| Moment | Type |
|--------|------|
| Step 2: Verification questions | Open-Ended |
| Step 2: After feedback | Flow Control |
| Step 3: Teach-back ("explain back") | Open-Ended |
| Step 3: Transition to practice | Flow Control |
| Step 4: Quiz (concept-based) | Quiz |
| Step 4: Scenario/compare/teach-back | Open-Ended |
| Session end: Commit confirmation | Yes/No |
