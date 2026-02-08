# Troubleshooting

## No scenes found

- Verify class name in render command.
- Verify file saved and imports `from manim import *`.

## Black frame

- Ensure `construct` method exists and runs.
- Ensure visible mobjects are added/played.

## MathTex compile failures

- Confirm `latex` and `dvisvgm` on PATH.
- Install missing LaTeX packages reported in logs (`standalone`, language packs, etc.).

## Slow renders

- Lower quality during iteration.
- Render specific animation ranges.
- Reduce expensive updaters and excessive per-frame transformations.

## Version confusion

- CE CLI should print `Manim Community v...`.
- `manimlib` imports indicate ManimGL, not CE.
