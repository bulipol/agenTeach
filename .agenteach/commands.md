# agenTeach Slash Commands

These commands work in any conversation with the AI agent. The agent reads this file at session start and recognizes these text patterns at any point in the conversation.

**Usage:** Type the command exactly as shown. The agent responds according to the definition below.

**Principle:** Slash commands = navigation. Numbers = quizzes and content choices.

---

## `/teach:start`

**First session** (LEARNER.md does not exist at root): Run full onboarding (`.agenteach/onboarding/interview.md`). Generate LEARNER.md and other project files after confirmation.

**Subsequent sessions** (LEARNER.md exists): Resume learning. Run Session Protocol Steps 1–2 (Orient + Verify) and show the SESSION START status block.

**How to detect first vs subsequent:** Check if `LEARNER.md` exists at the root level. If not → first session. If yes → subsequent.

---

## `/teach:next`

Show what comes next and ask for confirmation before proceeding. This flow is identical regardless of profile (guided or autonomous) — always ask.

**Within a topic:**
```
Jesteś na: [current step, e.g. "Step 3 — Teach: useEffect"]
Następny krok: [next step, e.g. "Step 4 — Practice: ćwiczenie z useEffect"]

1. Przechodzimy
2. Zostańmy jeszcze tutaj
```

**Between topics** (current topic just completed):
```
Temat "[topic]" ukończony!

Odblokowane tematy:
  - [unlocked topic 1]
  - [unlocked topic 2]

Który chcesz teraz?
1. [unlocked topic 1]
2. [unlocked topic 2]
```

Only propose topics whose prerequisites are marked DONE in LEARNER.md. Always wait for learner confirmation before proceeding.

---

## `/teach:status`

Show the full dashboard with progress and validation. **Output it as a code block** (wrap in ` ``` `) so the formatting renders correctly — same as SESSION START/END blocks.

```
--- DASHBOARD ---
Temat: [TOPIC]
Typ nauki: [project-based|concept-based] | Poziom: [SKILL_LEVEL] | Tryb: [guided|autonomous]

Roadmapa: [X]/[Y] etapów ([Z]%)
  [##--------] Etap [N]: [name] — W TRAKCIE
  [----------] Etap [N+1]: [name] — DO ZROBIENIA
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

---

## `/teach:mode`

Switch between guided and autonomous profile. Show current profile first:

```
Aktualny profil: [guided|autonomous]

1. Guided — agent prowadzi krok po kroku, potwierdzenia po każdym etapie
2. Autonomous — więcej treści na raz, mniej micro-interakcji

Zmienić?
1. Tak, przełącz na [the other mode]
2. Nie, zostań
```

After switching, update `Tryb:` in LEARNER.md.

---

## `/teach:stop`

End the current session. Run the full Session End Protocol (defined in AGENTS.md):

1. Update `knowledge/*.md` and Dziennik nauki
2. Update `SESSION_LOG.md`
3. Update `CHANGELOG.md` (if any files changed)
4. Show SESSION END status block
5. Propose a commit if applicable

---

## `/teach:help`

List all available commands:

```
Dostępne komendy:
  /teach:start  — zacznij sesję (onboarding lub kontynuacja)
  /teach:next   — co dalej? (zawsze pyta o potwierdzenie)
  /teach:status — dashboard (postęp, słabe strony, walidacja)
  /teach:mode   — zmień profil (guided / autonomous)
  /teach:stop   — zakończ sesję (zapisz logi, zaproponuj commit)
  /teach:help   — ta lista
```
