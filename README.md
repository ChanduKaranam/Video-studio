# Video Studio

A Claude Code plugin that turns a brief into a narrated, mastered product
video — a battle-tested pipeline distilled into skills, commands, and a
workspace convention.

**What you get:**

- A **workspace system**: four folders per project — `context/` (every input,
  moved in before use), `assets/` (binaries), `build/` (one live scene tree per
  cut + versioned scripts), `videos/` (`current/` + `versions/` with a README
  per ship).
- An **audio-locked pipeline**: Kokoro VO in breath groups → faster-whisper word
  timestamps → GSAP/HyperFrames comps retimed to the words → per-section render
  and mux → synthesized music bed with sidechain ducking → mastered ≈ −16.9 LUFS.
- A **design system per project**: drop a `design.md` into a project's
  `context/` folder and every visual follows it; without one, a clean built-in
  default design applies.

## Install

```bash
claude plugin marketplace add ChanduKaranam/Video-studio
claude plugin install video-studio@video-studio
```

Then restart Claude Code. To get updates later: `claude plugin update video-studio`.

Alternatives: from a local checkout, `claude plugin marketplace add
/path/to/video-studio` (same install command), or run directly with
`claude --plugin-dir /path/to/video-studio`.

## First run

1. `/video-setup` — checks and helps install the dependencies: node ≥ 20,
   the `hyperframes` CLI, ffmpeg/ffprobe, Python 3 with `faster-whisper`.
2. `/video-new <project>` — scaffolds the workspace for a new video project
   (and asks whether you have a `design.md` for it).
3. Drop your brief / docs / screenshots in chat — the agent files them into
   `context/` and `assets/` first (that's rule 1), then builds scene by scene.
4. `/video-ship <project>` — masters the final, rotates versions, writes the
   README, hands you the mp4.

New-user walkthrough: open `GUIDE.html` in a browser.

## Skills

| Skill | Covers |
|---|---|
| `video-studio` | Entry point: the folder system, the six rules, design.md resolution, routing |
| `vo-pipeline` | Kokoro breath-group VO, pronunciation rules, whisper timestamps, retiming |
| `comp-craft` | HyperFrames/GSAP composition contract, beat design, check gates |
| `mix-master` | Mux, assembly, music bed, ducking, mastering — exact ffmpeg recipes |
