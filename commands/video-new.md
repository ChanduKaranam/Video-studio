---
description: Scaffold the four-folder workspace for a new video project (or a new cut of an existing one)
argument-hint: <project> [cut]
---

Scaffold the workspace for project `$1` (kebab-case) with cut `$2`
(default `main`) in the current working directory:

```bash
P=$1; C=${2:-main}
mkdir -p context/$P/feedback \
         assets/$P/{logos,screenshots,recordings,data} \
         build/$P/$C/script \
         videos/$P/{current,versions}
cp "${CLAUDE_PLUGIN_ROOT}/skills/vo-pipeline/references/gen_vo_template.py"  build/$P/$C/gen_vo.py
cp "${CLAUDE_PLUGIN_ROOT}/skills/mix-master/references/gen_bed_template.py" build/$P/$C/gen_bed.py
```

Then write `context/$P/BRIEF.md` with this stub (fill what's known, leave
questions for the user):

```markdown
# <Project> — video brief
**Audience:**
**Length budget:**
**Core message:**
**Inputs received:** (list every doc/asset as it arrives, with dates)
```

If this is a **new cut of an existing project** (the project already has
another cut): instead of empty scene dirs, copy the source cut's tree into
`build/$P/$C/`, then delete only the sections-to-change's *derived* files
(wavs, words.json, renders, muxed mp4s) — the skip-if-exists VO generator
regenerates only what's missing and untouched sections stay byte-identical.

Finally, load the `video-studio` skill if not already loaded, and remind
yourself of rule 1 (move-in): every input the user pastes or drops from now
on is saved into `context/$P/` or `assets/$P/` with a dated name before use.
