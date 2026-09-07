# Tilicho brand defaults

## Palettes

Two moods; alternate per scene for contrast (dark for mechanism/drama, light
for product-UI tours).

**Dark:**
- Background `#101318`
- Foreground `#EDECE8`
- Accent (red) `#E8384A`

**Light:**
- Background `#F4F3F0`
- Foreground `#0A0E16`
- Accent (red) `#D40816`

Use the accent sparingly — one red element per frame reads as intent; three
read as noise. Evidence-grade chips and secondary labels sit at ~55–65 %
foreground opacity.

## Type

- Display: a grotesk (what the project already loads — reuse the font files
  from an existing build's `assets/fonts/` rather than adding new ones).
- Mono: for chips, tags, eyebrows, data labels (`MEASURED`, `READ-ONLY`,
  `ANY SOURCE` style). Eyebrows are letter-spaced uppercase mono.

## Marks

- **Watermark:** product name, small, top-right, persistent — but hidden under
  full-bleed slams, refusal beats, and end lockups (use `set()` calls or
  `data-layout-allow-overlap` as appropriate).
- **End lockup:** `<product> BY tilicho labs` — product name display-size,
  "BY tilicho labs" small mono beneath. Last beat of the film, on dark.
- Logo files: keep per-project copies in `assets/<project>/logos/`; source
  third-party marks from simpleicons/wikimedia and record where each came from.

## Voice

- Default VO voice: Kokoro `af_sky` at speed `0.80` (see the `vo-pipeline`
  skill for generation rules). Pronounce the company as written "Tilly-cho"
  in VO text.

## Loudness targets

- Final master ≈ **−16.9 LUFS integrated / −3.8 dBTP** (see `mix-master`).
- Music bed −31 LUFS baked, ducked under VO.
