# Scene Best Practices

## Structure

- Keep timeline logic in `construct`.
- Move reusable mobject creation into helper functions.
- Group related mobjects for coherent transforms.

## Animation composition

- Use explicit `run_time` and `rate_func` when pacing matters.
- Avoid visually noisy simultaneous effects.
- Build rhythm with clear transitions and short waits.

## Layout

- Use alignment methods (`next_to`, `align_to`, `to_edge`) over ad-hoc constants.
- Centralize spacing constants for consistency.
- Keep primary groups inside frame-safe margins and centered unless intentional offset.
- Reflow existing content before adding new dense blocks to avoid overlap.

## Updaters

- Keep updater math cheap.
- Remove updaters immediately after use.
- Avoid deep dependency chains between updaters.

## Text pacing

- Keep text visible long enough for comprehension.
- Baseline dwell formula: `seconds = (word_count / wpm) * 60 + 1`.
- Adult silent reading is often around `~238 wpm` in research settings; use a conservative on-screen default of `180 wpm`.
- For dense technical paragraphs, use `140-160` wpm.

## Reproducibility

- Use fixed seeds when randomness affects output.
- Keep environment pinned and isolated.
- Always report exact render command used.

## Source Notes

- Reading-speed meta-analysis reference (silent reading around ~238 wpm): https://www.sciencedirect.com/science/article/abs/pii/S0749596X19300786
