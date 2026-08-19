# MachtIA

"Machtia" = to learn in Nahuatl. **MachtIA** = learning with AI: a framework
for building personal projects with an AI assistant while making sure the
developer — not just the codebase — levels up.

Abstracted from the "Learning Mode" that Otoch Home pioneered: the AI explains
before implementing, presents alternatives and waits for the human decision,
keeps a controlled pace, and closes every work block with a comprehension
question. MachtIA adds the missing piece: **measurement**. Every question
answered becomes evidence; evidence accumulates into levels; levels calibrate
how the AI teaches.

## How it works

```
project CLAUDE.md ──imports──▶ MACHTIA.md (the rules)
        │                            │ reads & calibrates
        │ work sessions              ▼
        └──── evidence ────▶ LEVEL.md (the profile)
                                     ▲
              machtia-assess ────────┘ (interview builds/updates it)
```

1. **`MACHTIA.md`** — the learning-mode rules. Every project imports it from
   its `CLAUDE.md` with one line: `@~/personal_projects/machtia/MACHTIA.md`.
2. **`LEVEL.md`** — the developer's technical profile: a skill map on a
   5-level Nahuatl-named scale (mapped to the Dreyfus model), an append-only
   evidence log, and promotion tracking. Levels rise only with demonstrated
   evidence — organically, never by time alone.
3. **Skills** (symlinked into `~/.claude/skills/`, so they work in any project):
   - `machtia-assess` — interview that builds or updates LEVEL.md.
   - `machtia-plug` — connects a new project: adds the import and declares
     the project's learning goals.

## The scale

Yancuic → Momachtiani → Toltecatl → Temachtiani → Tlamatini
(Novice → Advanced Beginner → Competent → Proficient → Expert; full
descriptions in [LEVEL.md](LEVEL.md)).

## Quick start

```
# in any Claude Code session
/machtia-assess        # build your initial LEVEL.md
/machtia-plug          # connect the current project to MachtIA
```
