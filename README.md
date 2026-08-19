# MachtIA

"Machtia" = to learn in Nahuatl. **MachtIA** = learning with AI: a framework
for building personal projects with an AI assistant while making sure the
developer — not just the codebase — levels up.

The core loop: the AI explains before implementing, presents alternatives and
waits for the human decision, keeps a controlled pace, and closes every work
block with a comprehension question. On top of that loop, MachtIA adds
**measurement**: every question answered becomes evidence; evidence
accumulates into levels; levels calibrate how the AI teaches.

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
   its `CLAUDE.md` with one line: `@~/.claude/machtia/MACHTIA.md`.
2. **`LEVEL.md`** — the developer's technical profile: a skill map on a
   5-level Nahuatl-named scale (mapped to the Dreyfus model), an append-only
   evidence log, and promotion tracking. Levels rise only with demonstrated
   evidence — organically, never by time alone. The profile is **personal and
   git-ignored** — each developer creates their own from
   [LEVEL_TEMPLATE.md](LEVEL_TEMPLATE.md) (running `machtia-assess` does it
   for you).
3. **Skills** (symlinked into `~/.claude/skills/`, so they work in any project):
   - `machtia-assess` — interview that builds or updates LEVEL.md.
   - `machtia-plug` — connects a new project: adds the import and declares
     the project's learning goals.

## The scale

Yancuic → Momachtiani → Toltecatl → Temachtiani → Tlamatini
(Novice → Advanced Beginner → Competent → Proficient → Expert; full
descriptions in [LEVEL_TEMPLATE.md](LEVEL_TEMPLATE.md)).

## Installation (once per machine)

Claude Code loads personal skills from `~/.claude/skills/` in **every**
session, regardless of the project — that is what makes `/machtia-assess` and
`/machtia-plug` available everywhere. Clone the repo and symlink the skills:

```sh
# clone wherever you keep your repos…
git clone https://github.com/danielpinag/machtia.git
# …and pin it at the canonical path (skip if you cloned directly there):
ln -s "$(pwd)/machtia" ~/.claude/machtia

mkdir -p ~/.claude/skills
ln -s ~/.claude/machtia/skills/machtia-assess ~/.claude/skills/machtia-assess
ln -s ~/.claude/machtia/skills/machtia-plug ~/.claude/skills/machtia-plug
```

The canonical path matters: CLAUDE.md imports need a literal path that is the
same on every machine, and connected projects import the rules via
`@~/.claude/machtia/MACHTIA.md` — the symlink provides that path no matter
where your clone actually lives.

Then build your profile (personal, git-ignored):

```
# in any Claude Code session
/machtia-assess        # interview → creates LEVEL.md from LEVEL_TEMPLATE.md
```

## Connecting a project

In a Claude Code session **inside the project** you want to connect:

```
/machtia-plug          # adds the import + learning goals to its CLAUDE.md
```

That leaves the project's `CLAUDE.md` with a section like:

```markdown
## Learning Mode — MachtIA

@~/.claude/machtia/MACHTIA.md

Learning goals for this project: <areas this project is meant to grow>.
```

From then on, every session in that project runs under the MachtIA rules,
calibrated to your LEVEL.md.
