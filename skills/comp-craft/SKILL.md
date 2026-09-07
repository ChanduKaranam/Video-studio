---
name: comp-craft
description: Use when authoring or editing a video scene composition — HyperFrames/GSAP HTML comps, timeline beats, layout, diagrams, on-screen copy, lint/check gates, and rendering. Covers the comp contract (window.__timelines, data-start/data-duration), whole-block timeline rewrites, show-don't-tell copywriting, and frame verification.
---

# Composition craft

Each scene is a self-contained HTML file at
`build/<project>/<cut>/secN/comp/index.html`, rendered headlessly to a silent
`comp.mp4`. Start new comps from `references/comp-skeleton.html` (lint-clean).

## The contract

- 1920×1080; root element: `class="clip" data-composition-id="main"
  data-width="1920" data-height="1080" data-start="0" data-duration="<secs>"`.
- One `gsap.timeline({ paused: true })` registered as
  `window.__timelines = { main: tl }` — id must match `data-composition-id`.
- GSAP from cdnjs. Fonts/images referenced locally (copy into the comp dir or
  `assets/`), never hotlinked.
- Colors/type/watermark/lockup: `video-studio/references/tilicho-brand.md`.

## Timeline rules

- **Beat times come from `words.json`:** triggering word's `start` + 0.3 s
  (the mux lead). See `vo-pipeline`.
- **Whole-block rewrites only.** When the VO changes, rewrite the entire
  timeline block against the new words. Generic sed/patches of bare time
  literals (`, 3.4)`) hit unrelated lines and corrupt timelines silently —
  this has happened; don't repeat it.
- Beat anatomy that works: mono eyebrow (context label) → display headline
  (one claim, key word italic/accent) → mechanism animation (the thing the VO
  describes, actually moving). One red accent element per frame.

## Copy and diagram semantics

- **Show, don't tell:** on-screen copy must never print the VO sentence.
  Reword to a compressed label (VO "every move carries its evidence" →
  footer "EVERY MOVE CARRIES ITS EVIDENCE" is WRONG; reword or cut).
- Diagram direction is a claim: **symmetric wiring reads as interoperability;
  converging one-directional arrows read as migration.** Pick deliberately;
  use SVG `<marker>` arrowheads when direction matters.
- Numbers that are projections get evidence-grade chips (`logged`, `modelled`,
  `measured`, `assumed`) — never let a modelled figure look measured.
- Privacy: mask real names, emails, and local paths visible in screenshots or
  recordings before they render.

## Gates and rendering

```bash
npx hyperframes lint  <secN/comp dir>     # structure errors
npx hyperframes check <secN/comp dir>     # runtime, layout overlap, motion, WCAG contrast
npx hyperframes render <secN/comp dir> -o secN/comp.mp4 -w 2   # ONE comp at a time
```

- Render with `-w 2` and one comp at a time (memory).
- Contrast gate note: a warning sampled mid-tween on an animating element
  (e.g. a chip at 2.3:1 for a frame while fading between two valid states) is
  a false positive when both end states pass — check passes overall; leave it.
- Full-bleed slams/lockups that cover the watermark need explicit hide
  (`set()` autoAlpha) or `data-layout-allow-overlap` to satisfy the layout gate.
- **Frame-verify every changed beat by eye** before mux:
  `ffmpeg -i secN/comp.mp4 -vf "select=eq(n\,<frame>)" -vframes 1 f.png`
  (or extract at beat timestamps) and Read the images. First-render-clean is
  the norm when beats were placed from words.json — but verify anyway.
