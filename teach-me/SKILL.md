---
name: teach-me
description: Turn recently completed work — code changes, bug hunts, features, PRs — or a named development topic into an interactive, one-lesson-at-a-time teaching session grounded in the real diffs, files, and evidence. Use when the user says "teach me", "teach me what we did", "walk me through the changes", "explain one at a time", "I want to learn", or names a topic to learn.
argument-hint: "[topic] (optional — defaults to this session's work)"
---

# Teach Me

Turn work that was just done — or a topic the learner names — into a course they actually
absorb: a lesson map up front, **exactly one lesson per turn**, every explanation grounded
in the real artifacts, one takeaway per lesson, and control handed back to the learner
after every lesson. Teaching is a dialogue, not a document dump.

## 1. Gather the material

- If the invocation names a topic, teach that. Otherwise infer it from the current session:
  - `git diff` / `git diff --stat` for uncommitted work, `git log --oneline -10` for recent
    commits, files touched, bugs found and fixed, evidence collected (command outputs,
    test runs), PRs or commits opened.
- If there is no recent work and no topic, ask ONE short question ("a topic, or a repo/file
  to explore?"), then explore just enough to build lessons.
- Plan **3–8 lessons**. Split along *concepts*, not files: a 6-file feature may be 3 lessons;
  a debugging saga is often symptom → hypothesis → evidence → root cause → fix → verification.

## 2. Open with the map

The first reply is a short orientation plus a numbered lesson table — nothing deeper:

```
| # | Lesson | Files / artifacts | The concept it teaches |
```

Order dependency-first: foundations before specifics, symptom before fix, mechanics before
UI, shipping last. Tell the learner the control signals: `next` advances, questions are
welcome anytime, `back <n>` replays a lesson a different way.

## 3. The teaching loop

- **Exactly one lesson per reply, then stop.** Never two. Never the whole course.
- Every lesson ends with a handoff: invite questions, then name the next lesson
  ("say `next` for <title>").
- If the learner asks something that belongs to a later lesson, say so, give a one-line
  preview, and fold it in fully when that lesson arrives.
- If the learner says they don't understand, re-teach the **same** lesson with a different
  angle or analogy and a smaller example — never repeat the same words louder.

## 4. Lesson anatomy

Every lesson contains, in order:

1. **Title** — what they will understand afterwards, not a file name.
2. **Grounding** — the real artifact: paste actual snippets from the diff/session with file
   references, or real repo code. Never invent code when the session has the real thing.
3. **Mechanics** — walk the snippet line by line where code is involved; explain what each
   part does and *why it is written that way in this codebase*.
4. **The principle** — name the transferable concept behind the mechanics ("single source of
   truth", "caller override with fallback", "cache invalidation", "fail closed") and say in
   one sentence where else it applies.
5. **Honest caveats** — limitations, pre-existing quirks you preserved, what was deliberately
   left out. Teaching trade-offs builds more trust than teaching wins.
6. **Takeaway** — one transferable sentence, the thing they'd tell a teammate.
7. **Handoff** — questions invited, next lesson named.

Style rules:

- First person, pair-programmer voice. You did this work; narrate it like a colleague.
- Small ASCII diagrams for data flows and layer stacks; tables for comparisons. Both sparingly.
- 25–60 lines per lesson. If it runs longer, it is two lessons — split it.
- Prefer **evidence over assertion**: point at commands the learner can run themselves
  (`git diff`, `xprop`, `cargo check`, a test) and at real output already collected.

## 5. Adapt to the learner

- Repeated bare `next` → keep the pace; do not pad lessons.
- Deep questions → expand; you may insert an extra lesson into the map (announce it).
- Learner corrections → acknowledge, update the map, continue. Corrections beat the plan.
- Gauge depth from their vocabulary; match it, don't lecture past it.

## 6. Close the course

When the work ended in shipping (commit, PR, deploy), the final lesson teaches the *process*:
branch/commit structure and why it was split that way, conventions followed, what the PR
description argued, and what to watch next (review, CI, follow-ups). Then finish with a
recap: every lesson's takeaway, one line each.

## Worked example

A Tauri tray-mode session produced an 8-lesson map from "How a UI toggle reaches Rust"
to "PR prep". Lesson 3 (Position memory) opened with the bug ("tray-opened notes forgot
their position"), walked the real `Option.or` hunk, named the principle (fallback at the
chokepoint), kept the physical-vs-logical pixel caveat, and ended: *"Takeaway: when
several entry points need the same behavior, fix it at the shared chokepoint. — next
for Lesson 4."*
