# Setup and Versioning

## Version boundary

- ManimCE package name: `manim`
- ManimGL package name: `manimgl`
- CE code usually imports from `manim`
- GL code usually imports from `manimlib`

## Isolation policy

- Create a dedicated venv per project.
- Activate venv before every render.
- Avoid global installs for `manim` and `manimgl`.

## Minimum validation commands

```bash
python --version
manim --version
manim checkhealth
```

## macOS dependency highlights

- `ffmpeg` required for video output.
- `pkg-config` and cairo/pango stack needed by related dependencies.
- `latex` + `dvisvgm` required for `Tex`/`MathTex`.

## Practical install sequence

```bash
python3.13 -m venv .venv
source .venv/bin/activate
pip install -U pip setuptools wheel
pip install manim
manim checkhealth
```

Use `pip install -e .` when working from a local clone.
