# Manim Community Deep Skill

A Codex/agent skill that converts plain-language animation ideas into runnable **Manim Community Edition** scenes and export-ready render commands.

## What It Does

- Translates text concepts and storyboard notes into scene blueprints.
- Generates ManimCE code (`from manim import *`).
- Runs an iteration loop (layout, timing, full draft, final export).
- Produces explicit output contract: file path, render command, and tweak knobs.

## Intended Trigger

Use when a request is fundamentally:

- "Turn this explanation into Manim"
- "Convert these bullets to animation code"
- "Generate scene code and export command from this script"

Not intended for `manimlib` / ManimGL codebases.

## Structure

- `SKILL.md`: main workflow and operating contract
- `agents/openai.yaml`: UI metadata
- `references/`: blueprinting, code-generation, render/export, quality checks, troubleshooting

## Quick Use Prompt

`Use $manim-community-deep to convert my text idea into ManimCE scene code and export-ready render commands.`

## Example Output Contract

A successful run should return:

- Scene code
- Suggested file path (for example `scenes/my_scene.py`)
- Render command (for example `manim render -qh scenes/my_scene.py MyScene`)
- Expected output path
- Short list of tweak knobs

## Validation

If you have the skill tooling available:

```bash
python3 /Users/lmostafa/.codex/skills/.system/skill-creator/scripts/quick_validate.py .
```

## License

MIT
