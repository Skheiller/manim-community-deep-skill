# CLI and Config

## Core command patterns

```bash
manim render -pql file.py SceneName
manim -pql file.py SceneName
```

## High-value flags

- `-q l|m|h|p|k`: quality tier
- `-s`: save last frame
- `-n a,b`: animation index range
- `-o`: output name
- `--format`: output format
- `--renderer cairo|opengl`
- `-t`: transparent background

## Config precedence

1. library defaults
2. user config (`~/.config/manim/manim.cfg`)
3. project config (`./manim.cfg`)
4. CLI flags

## Recommended development cycle

1. `-ql -s` for layout.
2. `-ql -n` for segment timing.
3. `-qm -p` for integrated review.
4. `-qh` (or above) for final render.
