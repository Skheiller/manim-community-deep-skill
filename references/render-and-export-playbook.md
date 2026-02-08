# Render and Export Playbook

## Development loop

```bash
manim render -ql -s file.py SceneName
manim render -ql -n 0,4 file.py SceneName
manim render -ql -p file.py SceneName
```

## Required preview gate (before full export)

1. Render and share a low-quality preview first:

```bash
manim render -ql -p file.py SceneName
```

2. Ask user confirmation.
3. Only then run high-quality export.

## Final export (after confirmation)

```bash
manim render -qh file.py SceneName
```

## Alternate formats

```bash
manim render --format gif file.py SceneName
manim render --format webm file.py SceneName
manim render -t file.py SceneName
```

## Sectioned output

Use scene sections in code:

```python
self.next_section("intro")
```

Then render with:

```bash
manim render --save_sections file.py SceneName
```

## Reporting requirement

When finished, always provide:

- command executed
- absolute output path
- format/resolution tier used
- whether this was preview or final
