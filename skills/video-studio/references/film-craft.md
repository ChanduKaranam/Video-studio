# Film craft — direction, rhythm, sound, variants

Distilled 2026-10-16 from the strongest open video skills (onetake by feitangyuan,
guizang-product-video-skill by op7418, bang-motion by Bang Tutorial, hypit) — ideas only,
no code or text copied; their licenses (PolyForm-NC / AGPL / MIT) don't attach.
These fill the gaps our pipeline had: we had seams, carry and visual QA; we did not have
rhythm, a concept step, SFX doctrine, or a variant system.

## 1 · Direction before code (per film, before script v1)

A film needs one sentence about the *picture* — the single idea it is made of — chosen
before any timeline is written. Record it at the top of `script/v1.md`.

- Propose **three concepts that differ in their central idea**, not three stories told with
  the same cards. Axes to differ on: ground & light, type voice, motif source, camera
  language, transition vocabulary, pace, sound. The user picks (or you pick and say so).
- Every visual device must be derivable from the subject: "because the product/story has X,
  the film uses Y." A device with no X is a template — delete it.
- **Anti-repetition:** before starting, look at the previous film shipped from this
  workspace (its script + contact sheet). The new film differs on at least three axes and
  never reuses the last film's opening, section treatment, or background device verbatim.
- The hook→features→logo→CTA skeleton is ONE structure, never the default. Alternatives:
  problem→turn→solution, one real task end-to-end, one continuous dive through scale,
  before/after split, chain reaction, a day of use.

## 2 · Rhythm — the energy curve must have shape

Carry (seam law) kills slide *transitions*; rhythm kills slide *cadence*. Both PPT failure
modes are independent — a film can pass every seam gate and still be a metronome.

Checkable rules, applied to the beat sheet before VO is cut:

- **Shot lengths vary ≥ 4×** (0.3 s hits next to 2.5 s holds). Coefficient of variation of
  shot lengths ≥ 0.25 or it reads as slides.
- **Rests are real:** ≥ 25 % of frames dead-still overall, and at least one ≥ 1 s stretch
  of near-silence in picture AND sound. Rests are dead still — no drift, no settling
  camera, no idle wobble (which our doctrine already bans). Stillness is what makes the
  bursts land.
- **Bursts where the genre has them:** a trailer has at least one burst — ≥ 3 large visual
  changes inside 1.5 s — never at a uniform interval. Bare hard cuts are legal only inside
  a burst or into the end card.
- **Never end two consecutive shots the same way** (spring-out, blur-out, hard cut —
  alternate).
- **≤ 2 text tiers per beat** (one big number/line + one small label). Eyebrow + headline
  + body = a slide.
- **Reference deconstruction:** when the user names a reference or a genre ("trailer
  style"), measure before matching: % dead-still frames, cut count and placement, shot
  lengths, element size vs ground. A trailer reference is typically ~⅓ still — not obvious
  from one viewing, and a film built without the numbers comes out uniform.

## 3 · Sound — a palette in one room, not a beep per event

The bed-and-duck chain (mix-master) stays. On top of it, when a film earns SFX:

- **One material set, one room.** 3–5 synthesized/recorded materials (air whoosh, tick,
  knock, sub hit, pop) all sharing a single reverb. Disparate dry one-shots per event are
  the audio version of the slideshow.
- **Fewer events than beats.** Score the landmarks, not every motion. Two sounds landing
  within 40 ms → keep one.
- **Action sounds must survive the music.** Compare SFX vs music in the actual event
  windows and shared bands, not full-track LUFS — a mix can hit target loudness with every
  hit inaudible. Duck the music under the hits.
- **Dynamics follow the picture's energy map:** the quiet hold is silent after its breath;
  the hits are the loudest thing in the film.
- **No stock ending chime.** End on the music's own cadence or a hit that belongs to the
  film. (The vibraphone-chord-plus-shimmer ending is burned.)
- Pitched runs at F4 or above with short tails; low-mid pileup (100–300 Hz) is the first
  place to look when a mix reads as mud — check band energy per 0.5 s window.

## 4 · First-frame poster rule

Social platforms (X, WhatsApp, LinkedIn) grab frame 1 as the thumbnail. The first 5–10
frames must show a completed composition — usually the opening beat's end state — then fade
into the normal entrance. Frame 1 is never a blank ground or elements waiting to enter.
Check: extract frame 1 of the shipped mp4 and look at it.

## 5 · Per-client variants

When one film ships to many clients (per-college, per-prospect), build ONE comp with
declared slots, never a copied comp per client:

- Slots live in one config block per client (name, logos, headline, accent color, VO
  lines that change). The comp reads slots; nothing else differs.
- Only slot VO lines are regenerated per client (gen_vo.py skip-if-exists already gives
  this); fixed sections stay byte-identical across variants.
- Variant = cut directory per the existing cuts convention, but derived from config, and
  the config is committed in `context/<project>/clients/<name>.md`.
- A copied comp doubles every later fix. One fix, N re-renders.

## 6 · Mechanical PPT checks (pre-render, alongside the seam gate)

Run on the comp before rendering, no judgment required:

1. ≥ 3 beats implemented as sibling containers toggled with autoAlpha/display and no
   carried element across them → slide deck; rebuild the seams.
2. Count text tiers per beat (§2).
3. The same transition three times in a row → vary it.
4. Scale 1.0→1.05 drift as a beat's only motion → it's a Ken Burns slide; give the beat a
   performed motion or cut it. (Idle-wobble ban already covers the rest.)
5. Shot-length list from the beat sheet: compute min/max ratio and CV (§2).
