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

## Updaters

- Keep updater math cheap.
- Remove updaters immediately after use.
- Avoid deep dependency chains between updaters.

## Reproducibility

- Use fixed seeds when randomness affects output.
- Keep environment pinned and isolated.
- Always report exact render command used.
