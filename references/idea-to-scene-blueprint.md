# Idea to Scene Blueprint

## Input expected

- Raw paragraph, bullets, or narration text.
- Optional constraints: duration, tone, brand colors, audience level.

## Preflight gate (before detailed blueprint)

1. Produce mini blueprint (4-7 bullets).
2. Ask targeted preference questions (theme, motion, camera, 2D/3D, pacing, style, duration).
3. Wait for confirmation (or apply explicit defaults if user says proceed without details).

## Transformation steps

1. Extract core claim and 2-5 supporting beats.
2. Convert beats into visual verbs:
- introduce
- compare
- transform
- emphasize
- conclude
3. Assign mobject strategy per beat:
- prose: `Text` / `MarkupText`
- equations: `MathTex`
- geometry/process: shapes + transforms
- data/trends: `Axes` + plotted objects
4. For process diagrams, declare edge dependencies and animation order (topological order, not all-at-once).
5. Allocate spatial budget per beat (title zone, core diagram zone, annotation zone).
6. Define a motion plan per beat (transform, tracker update, reflow, camera emphasis).
7. Define semantic color map (`color_map`) linking symbols to visuals.
8. For text-heavy beats, compute read-time dwell using `seconds = (word_count / wpm) * 60 + 1`.

## Beat template

- `beat_id`
- `intent`
- `objects`
- `animation`
- `duration`
- `voice/text sync note`
- `dependency_preconditions` (what must already be visible before this beat starts)
- `layout_constraints` (max text width, label buffers, keepout zones)
- `reflow_actions` (which existing objects move/scale before new objects appear)
- `camera_action` (`hold`, `zoom_in`, `zoom_out`, `pan`)
- `state_driver` (`tracker_name` and what depends on it, if applicable)
- `read_time_seconds` (derived from on-screen word count, with +1s safety margin)

## Split rule

If one scene exceeds ~6-8 major beats or becomes visually dense, split into multiple `Scene` classes.

## Process logic rule

- For neural network or pipeline visuals, animate stage-by-stage:
1. upstream edges
2. upstream node activation
3. downstream edges
4. downstream node activation
- Never trigger downstream flow before upstream state exists.
