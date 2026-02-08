# Visual Clarity and Aesthetic Playbook

Use this when the user cares about how the animation feels, not just whether it runs.

## 1) Clarity before complexity

- One beat = one idea. Do not introduce new text, new geometry, and new motion in the same instant.
- Keep a single visual focal point at a time; secondary elements should be dimmer, smaller, or static.
- Prefer progressive reveal over full-screen dumps (`Write`/`Create`/`LaggedStart` with deliberate pacing).
- Keep text density low: short titles, short labels, and no paragraph blocks on-screen.

## 2) Practical pacing defaults

Manim animations accept explicit `run_time` and `rate_func` controls. The base `Animation` default is `run_time=1.0` and `rate_func=smooth`, but polished videos usually vary timing by intent.

Recommended starting ranges:

- Micro-emphasis (flash/highlight): `0.3` to `0.7` sec
- Standard reveal (`Write`, simple `FadeIn`): `0.8` to `1.6` sec
- Conceptual transform (`Transform`, camera or layout shift): `1.8` to `3.0` sec
- Beat separator pause (`wait`): `0.5` to `2.0` sec
- “Let it sink in” pause after key insight: `2.0` to `3.0` sec

When in doubt, slow down transitions and reduce simultaneous motion before adding more effects.

Observed timing tendencies in `3b1b/videos` (explicit literals):

- Common `run_time` values: `2.0`, `3.0`, `1.0`, `4.0`, `5.0`
- Common `wait()` values: `2.0`, `3.0`, `4.0`, `5.0`, `0.5`

## 3) Graph styles with strong audience response (3Blue1Brown-like motifs)

From the public `3b1b/videos` codebase, the most common building blocks include heavy use of `VGroup`, `FadeIn`/`FadeOut`, `Write`, `Transform`, `LaggedStart`, then graph primitives like `Axes`, `NumberPlane`, `NumberLine`, and `ComplexPlane`.

Empirical primitive frequency snapshot:

- `Axes`: `297`
- `NumberPlane`: `193`
- `NumberLine`: `161`
- `ComplexPlane`: `140`
- `ThreeDAxes`: `83`
- `ValueTracker`: `386`
- `always_redraw`: `236`

Use these graph patterns first:

1. Function story on `Axes`: draw curve, move a tracked point, then reveal slope/area annotation.
2. Transformation story on `NumberPlane`: show grid, apply transform, then compare before/after.
3. Process story on `NumberLine`: animate iterates/probability mass left-to-right with clear markers.
4. Complex mapping story on `ComplexPlane`: anchor reference points before morphing geometry.

## 4) Keep scenes clean

- Cap independent concurrent motions to 1 primary + 1 secondary.
- Use consistent color semantics (for example: neutral/base, active object, result/highlight, warning/error).
- Reserve strongest color for the current idea, not decorative accents.
- Align objects with `next_to`, `align_to`, `to_edge`; avoid ad-hoc offsets unless necessary.
- Use a black or near-black background for technical explainers unless user style says otherwise.
- Keep equations and graph labels in dedicated safe zones to avoid overlap with axes/curves.
- Fit text to containers before reveal; never reveal overflowing labels.

## 5) Beauty-focused render loop

1. Layout pass (stills): verify composition and readability.
2. Timing pass: tune `run_time`, `lag_ratio`, and pauses.
3. Rhythm pass: remove dead time and reduce visual noise.
4. Final quality pass at target resolution/fps (`-qm` or `-qh` depending on delivery).

## Source Notes

- Manim animation parameters (`run_time`, `rate_func`): https://docs.manim.community/en/stable/reference/manim.animation.animation.Animation.html
- Manim quality/fps presets (`-ql/-qm/-qh/-qk`): https://docs.manim.community/en/stable/guides/configuration.html
- 3Blue1Brown workflow notes: https://github.com/3b1b/videos
- 3Blue1Brown scene corpus used for motif/timing frequency sampling: https://github.com/3b1b/videos
