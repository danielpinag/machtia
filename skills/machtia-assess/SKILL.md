---
name: machtia-assess
description: Interview the developer to build or update LEVEL.md (the MachtIA technical profile). Use for the initial full assessment, to assess a single new area, or to re-assess a rusty one. Triggers on "assess my level", "evaluate me", "update my level", "assessment".
---

# machtia-assess — Level assessment interview

You are building an honest, calibrated technical profile at
`~/.claude/machtia/LEVEL.md`. Read that file first — the scale, the
current Skill map, and the Evidence log define where to start. If it doesn't
exist yet (it is personal and git-ignored), create it from
`~/.claude/machtia/LEVEL_TEMPLATE.md`, filling in the developer's
name and today's date.

Conversation in Spanish (es-MX); everything written to LEVEL.md in English.

## 1. Scope

- **First run** (skill map empty): full assessment.
- Otherwise: assess only the areas the developer names, or the ones flagged
  rusty 🕸.

## 2. Choose the areas

Propose an area list drawn from: the developer's active projects (the current
one, plus any others they mention), the learning goals declared in their
projects' CLAUDE.md files, and anything they say they want measured. Keep areas
coarse-grained (e.g. "GraphQL & federation", "Relational data & SQL",
"Distributed systems", "Ruby/Rails", "Testing") — 4 to 8 areas max per
session. **Confirm the list with the developer before interviewing.**

## 3. Interview protocol (per area)

Adaptive, 3–5 questions, one at a time — never a questionnaire dump:

1. Start at level 2–3 depth. Move up after a solid answer, down after a gap.
2. Mix question types across the area:
   - **Explain**: "explain X as if to a colleague" (probes levels 1–3).
   - **Decide**: "in situation Y, what would you do and why?" (probes 3–4).
   - **Critique**: show a short flawed snippet or design and ask what's wrong
     (probes 3–5).
3. Honor system: answers come from the developer's head, not from looking
   things up. Remind them once at the start.
4. A wrong or partial answer is good data — acknowledge it plainly, note the
   specific gap, and move on. Never soften verdicts and never coach mid-question.

## 4. Scoring

- Record the level **demonstrated**, per the Dreyfus descriptions in LEVEL.md.
  When in doubt between two levels, record the lower one — an honest floor
  beats a flattering ceiling, and promotions are cheap later.
- For each area, note 1–2 concrete observed gaps: these become the learning
  targets that future project plans should attack.

## 5. Write LEVEL.md

- Update the Skill map (level, trend `→`, last evidence date, notes with gaps).
- Append one Evidence log line per question asked, with verdicts.
- Add a History entry: date, areas assessed, summary of movement.
- Do not delete old evidence; the log is append-only.

## 6. Close

Per MachtIA rule 3: summarize what the assessment revealed (strengths, gaps,
suggested next learning targets) — but do NOT ask an extra comprehension
question; the interview itself was the probe.
