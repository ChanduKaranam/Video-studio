# Tilicho Video Studio

A Claude Code plugin that turns a brief into a narrated, mastered product video —
the pipeline Tilicho used for the Pathfinder, BFSI and Edu pitch films, distilled
into skills, commands, and a workspace convention.

**What you get:**

- A **workspace system**: four folders per project — `context/` (every input,
  moved in before use), `assets/` (binaries), `build/` (one live scene tree per
  cut + versioned scripts), `videos/` (`current/` + `versions/` with a README
  per ship).
- An **audio-locked pipeline**: Kokoro VO in breath groups → faster-whisper word
  timestamps → GSAP/HyperFrames comps retimed to the words → per-section render
  and mux → synthesized music bed with sidechain ducking → mastered ≈ −16.9 LUFS.
- **Tilicho brand defaults**: palettes, lockup, watermark rules, voice.

## Install

From a git checkout of this repo:

```bash
claude plugin marketplace add /path/to/tilicho-video-studio
claude plugin install tilicho-video-studio@tilicho
```

Or run Claude Code with the plugin loaded directly:

```bash
claude --plugin-dir /path/to/tilicho-video-studio
```

## First run

1. `/video-setup` — checks and helps install the dependencies: node ≥ 20,
   the `hyperframes` CLI, ffmpeg/ffprobe, Python 3 with `faster-whisper`.
2. `/video-new <project>` — scaffolds the workspace for a new video project.
3. Drop your brief / docs / screenshots in chat — the agent files them into
   `context/` and `assets/` first (that's rule 1), then builds scene by scene.
4. `/video-ship <project>` — masters the final, rotates versions, writes the
   README, hands you the mp4.

## Skills

| Skill | Covers |
|---|---|
| `video-studio` | Entry point: the folder system, the six rules, routing |
| `vo-pipeline` | Kokoro breath-group VO, pronunciation rules, whisper timestamps, retiming |
| `comp-craft` | HyperFrames/GSAP composition contract, beat design, check gates |
| `mix-master` | Mux, assembly, music bed, ducking, mastering — exact ffmpeg recipes |
