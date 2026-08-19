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
   its `CLAUDE.md` with one line — `@~/.claude/machtia/MACHTIA.md` — and
   points every other assistant at it from its `AGENTS.md` (see
   [Supported assistants](#supported-assistants)).
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
cd machtia

# …and pin it at the canonical path:
ln -sfn "$(pwd)" ~/.claude/machtia

mkdir -p ~/.claude/skills
ln -sfn ~/.claude/machtia/skills/machtia-assess ~/.claude/skills/machtia-assess
ln -sfn ~/.claude/machtia/skills/machtia-plug ~/.claude/skills/machtia-plug
```

The block is idempotent — safe to re-run any time (e.g. after moving the
clone). `-f` replaces an existing link instead of failing; `-n` stops `ln`
from following an existing symlink-to-a-directory and planting the new link
*inside* it, which is how you end up with infinite symlink loops.

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

From **Claude Code**, in a session inside the project you want to connect:

```
/machtia-plug          # asks for learning goals, writes both files below
```

From **any other supported assistant** (Cursor, GitHub Copilot, anything
that reads AGENTS.md): a SKILL.md is a plain-markdown playbook — Claude
Code's skill packaging only adds the auto-trigger — so point your agent at
the same file. In a session inside the project, ask:

```
Read ~/.claude/machtia/skills/machtia-plug/SKILL.md and follow it
to connect this project.
```

Either way, the `~/.claude/machtia` symlink from
[Installation](#installation-once-per-machine) must exist first — it is what
makes these paths work on every machine (the `~/.claude/skills/` links
matter only to Claude Code).

Connecting leaves the project's `CLAUDE.md` with a section like:

```markdown
## Learning Mode — MachtIA

@~/.claude/machtia/MACHTIA.md

Learning goals for this project: <areas this project is meant to grow>.
```

It also writes (or updates) the project's `AGENTS.md` with a Learning Mode
section — a reference to the same rules plus a short digest as fallback — so
the project stays in learning mode outside Claude Code too.

From then on, every session in that project runs under the MachtIA rules,
calibrated to your LEVEL.md.

## Supported assistants

| Assistant | How the rules load | Support |
|-----------|--------------------|---------|
| **Claude Code** | `CLAUDE.md` `@`-import injects MACHTIA.md into every session | Full: rules + skills. |
| **Cursor** | Reads `AGENTS.md` natively and follows the reference to MACHTIA.md | Rules. |
| **GitHub Copilot** | Reads `AGENTS.md` natively and follows the reference to MACHTIA.md | Rules. Its cloud coding agent (github.com) cannot reach `~/`, so there it falls back to the digest inside AGENTS.md. |

Anything else that reads the AGENTS.md standard (Codex CLI, Gemini CLI,
Windsurf, Zed, …) gets the same rules-level support for free. The skills
(`machtia-assess`, `machtia-plug`) are packaged as Claude Code skills, but
each SKILL.md is a plain-markdown playbook any agentic assistant can follow
when pointed at it — see [Connecting a project](#connecting-a-project) for
the plug; the assessment works the same way:

```
Read ~/.claude/machtia/skills/machtia-assess/SKILL.md and follow it.
```

## What runs when

| What | How often |
|------|-----------|
| Installation block | Once per machine (idempotent — re-run freely). |
| `/machtia-assess` | Once, to create your profile. After that only on demand: a new area, or one flagged rusty 🕸. **Not** per project. |
| `/machtia-plug` | Once **per project**, the day you connect it. |
| A regular work session | Nothing. Claude Code loads the project's `CLAUDE.md` automatically, and its `@~/.claude/machtia/MACHTIA.md` import pulls in the rules; other assistants load `AGENTS.md`. |

The `/command` form is Claude Code's; from any other assistant, point the
agent at the corresponding SKILL.md instead (see
[Connecting a project](#connecting-a-project)).

Working on several connected projects at the same time is the normal case,
not a special one: they all read and write the **same** LEVEL.md, each
project declares its own learning goals in its own CLAUDE.md, and every
evidence line is tagged with the project it came from.

## Scaling

One profile per developer — never one file per technology. The part the AI
reads to calibrate, the Skill map, stays small because areas are
coarse-grained ("Ruby/Rails", not "ActiveRecord callbacks"); splitting it per
area would multiply the common read (the whole map, since a session usually
touches several areas) to optimize the rare one (deep per-area history). Note
that LEVEL.md is not loaded into context every session anyway — MACHTIA.md
instructs the AI to read it on demand, when planning, designing, or
explaining something non-trivial.

What does grow without bound is the Evidence log (~one line per work block),
so it rotates by *temperature* instead: past ~150 lines, entries older than
90 days move verbatim to `EVIDENCE_ARCHIVE.md` (personal and git-ignored,
like LEVEL.md). The 90-day window mirrors the rusty 🕸 rule, the Skill map
keeps each area's last-evidence date, and promotion checks search the
archive — so nothing downstream breaks.
