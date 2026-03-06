# CLAUDE.md — Claude Code Instructions

Read `AGENTS.md` and `LEARNER.md` first. This file adds only Claude Code-specific behavior on top of them.

---

## Slash Commands

Recognize `/teach-*` commands anywhere in the conversation. When you see one, respond as defined in `.agenteach/commands.md`. Read that file at session start alongside `AGENTS.md` and `LEARNER.md`.

If the user types `/teach-start`, check whether `LEARNER.md` exists at the root level to determine first vs subsequent session.

---

## Plan Before Acting

Before making any code or documentation changes:
1. Write a short plan in the chat listing which files will be changed and what will happen
2. Wait for confirmation before proceeding
3. Mark tasks as completed as you go

---

## Explanation Format

When introducing new code, use this structure:

```js
// Describes what the function does in one sentence.
// paramName: type — what it represents, e.g. example value
// returns: type in range X..Y, e.g. exampleResult
function exampleFunction(paramName) {
  // math: paramName * 2 = 0.8 * 2 = 1.6
  return paramName * 2;
}
```

---

## File Scope

Always state which files you will change before changing them. Touch only the minimum set of files needed for the task.

---

## Simplicity

Every task and code change should be as simple as possible. Avoid massive or complex changes. Every change should impact as little code as possible.
