# Quality Checklist

## Narrative

- Does each beat support the main idea?
- Is progression understandable without pausing every second?

## Visual

- Is text readable at target resolution?
- Is motion hierarchy clear (primary vs secondary)?
- Are colors intentional and consistent?
- Is there one clear focal point per beat?
- Are concurrent independent motions limited (avoid visual overload)?
- Is the background clean dark/black when no different style is requested?

## Layout Integrity

- Does boxed text stay within container bounds with visible padding?
- Are equation/text blocks free from overlap with other labels or graphs?
- Are arrow labels attached to shafts (not arrowheads) with consistent buffers?
- Are titles, core diagrams, and annotations separated into stable zones?

## Pacing

- Are key `play()` calls assigned explicit `run_time` for important beats?
- Are `rate_func` choices intentional for the mood (calm/energetic/emphasis)?
- Are pauses (`wait`) used between conceptual steps so viewers can process changes?
- Does the scene avoid both extremes: rushed transitions and dead air?

## Logic and Causality

- For process diagrams, is animation order topologically valid?
- For neural network flow, does `L1->L2` visually complete before `L2->L3` begins?
- Are parallel animations used only when the script explicitly describes parallelism?

## Technical

- Runs in isolated venv.
- `manim --version` confirms ManimCE.
- TeX scenes compile when `MathTex` is used.
- LaTeX strings are valid (for example `r\"\\mathcal{L}\"`, not malformed tokens).

## Export

- Output format matches request.
- Output path is confirmed.
- Render command is reproducible.
