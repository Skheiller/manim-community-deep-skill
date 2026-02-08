---
name: manim-community-deep
description: Convert plain-language ideas into Manim Community Edition scene code and exported media. Use when a user provides text concepts, narration, storyboard notes, or rough animation intent and wants complete ManimCE implementation, render commands, iterative revisions, and final output export. Do not use for ManimGL/manimlib codebases.
---

# Manim Community Deep

## Overview

Use this skill to turn user text ideas into production-ready ManimCE output through a strict pipeline:

1. parse idea text,
2. map to scene plan,
3. generate Manim code,
4. render and fix,
5. export final media.

Prefer this skill for requests like “animate this explanation”, “turn this paragraph into a video”, or “convert these bullet points into Manim and export”.

## Idea-to-Export Workflow

1. Intake and normalize intent.
- Extract objective, audience, visual style, duration target, and output format.
- Resolve ambiguity by making minimal explicit assumptions in code comments or summary.
- If core requirements are missing, ask focused clarification questions before coding.

2. Build a scene blueprint from text.
- Convert narrative into ordered beats.
- For each beat define: on-screen objects, transition, duration, and emphasis.
- Split into one or more `Scene` classes if conceptually distinct.

3. Generate runnable ManimCE code.
- Use `from manim import *`.
- Keep `construct()` orchestration-focused.
- Use helper builders for repeated objects/layouts.

4. Render in a fast feedback loop.
- Layout check: `-ql -s`
- Timing check: `-ql -n a,b`
- Full draft: `-qm -p`
- Final export: `-qh` (or higher as needed)

5. Export and report deliverables.
- Return exact render command used.
- Return output path(s) and file format.
- Note assumptions and next tweak knobs (timing/style/text density).

## Implementation Contract

For every idea-to-code request, produce:

- `Scene` class code implementing the described idea.
- A suggested file location (for example `scenes/idea_scene.py`).
- A concrete render command.
- The expected output location/filename.
- A short “edit knobs” list (what to change for speed/style/detail).

## Code Quality Rules

- Use semantic names (`claim_text`, `curve_group`, `highlight_box`).
- Favor composable primitives (`VGroup`, `Axes`, `MathTex`, `Text`, `Transform`).
- Keep updaters minimal and scoped.
- Avoid hidden global mutation.
- Ensure every visual beat is intentional and readable.

## Safety and Validation

- Keep commands non-destructive and scoped to the current project.
- Prefer deterministic commands and explicit paths in export guidance.
- Validate syntax/runtime with at least one render pass before final handoff.
- When TeX is used, verify `latex` and `dvisvgm` availability or report a concrete remediation command.

## Export Rules

- Default output: `mp4` unless user asks otherwise.
- Use transparent renders only when explicitly required (`-t`).
- If user asks for preview artifacts, include still frame via `-s`.
- For multiple sections, use `next_section()` and `--save_sections` where useful.

## Failure Handling

1. If `Tex/MathTex` fails, fix LaTeX toolchain first (`latex`, `dvisvgm`).
2. If rendering is slow, reduce quality and isolate animation ranges.
3. If visuals are cluttered, reduce simultaneous motion and split into more beats.

## References

Load only what is needed.

- `references/idea-to-scene-blueprint.md`
- `references/code-generation-patterns.md`
- `references/render-and-export-playbook.md`
- `references/quality-checklist.md`
- `references/troubleshooting.md`
