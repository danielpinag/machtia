---
name: machtia-plug
description: Connect a project to the MachtIA learning framework — add the MACHTIA.md import to its CLAUDE.md, write the AGENTS.md Learning Mode section for other assistants (Cursor, GitHub Copilot, any AGENTS.md reader), and declare the project's learning goals. Use when starting a new personal project or when the developer says "plug this into machtia" / "conecta este proyecto a machtia".
---

# machtia-plug — Connect a project to MachtIA

Goal: the target project's `CLAUDE.md` imports the shared learning-mode rules
and declares what the developer intends to learn by building it.

Conversation in English unless the LEVEL.md header sets a `Conversation
language:`; everything written to files in English.

## Steps

1. **Locate the target project.** Default to the current working directory;
   confirm with the developer if ambiguous.
2. **Ask for the learning goals.** Which areas is this project meant to grow?
   Suggest candidates from the project's stack and from gaps noted in
   `~/.claude/machtia/LEVEL.md`. Wait for the developer's answer.
3. **Edit the project's CLAUDE.md** (create it if missing). Add — near the
   top, after the project intro — a section:

   ```markdown
   ## Learning Mode — MachtIA

   @~/.claude/machtia/MACHTIA.md

   Learning goals for this project: <areas, comma-separated>.
   ```

   If the project needs rules of its own (e.g. "ADR before code"), list them
   under the import with a note that they add to, never override, MachtIA.
   If the CLAUDE.md already has an inline learning-mode section, replace it
   with the import and keep only the project-specific rules.
4. **Write the project's AGENTS.md section** (create the file if missing) so
   assistants other than Claude Code — Cursor, GitHub Copilot, and anything
   else that reads the AGENTS.md standard — run under the same rules.
   AGENTS.md has no import mechanism, so the section is a reference plus a
   digest fallback. Keep the learning goals identical to CLAUDE.md's, and
   replace any existing Learning Mode section rather than duplicating it:

   ```markdown
   ## Learning Mode — MachtIA

   Read `~/.claude/machtia/MACHTIA.md` and follow it as binding rules for
   this session. If the file is unreachable, the core loop is: explain
   before implementing (present alternatives, wait for the developer's
   decision); calibrate depth to `~/.claude/machtia/LEVEL.md`; close every
   work block with one comprehension question and append the evidence to
   LEVEL.md; at most one significant new concept per session.

   Learning goals for this project: <areas, comma-separated>.
   ```
5. **Update LEVEL.md.** Add any learning-goal area missing from the Skill map
   with level "—" and note "unassessed — added by <project>". Suggest running
   `machtia-assess` for the new areas.
6. **Close per MachtIA rule 3**: summarize what was connected and ask one
   comprehension question about a concept the project will exercise.
