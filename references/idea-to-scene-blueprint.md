# Idea to Scene Blueprint

## Input expected

- Raw paragraph, bullets, or narration text.
- Optional constraints: duration, tone, brand colors, audience level.

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

## Beat template

- `beat_id`
- `intent`
- `objects`
- `animation`
- `duration`
- `voice/text sync note`

## Split rule

If one scene exceeds ~6-8 major beats or becomes visually dense, split into multiple `Scene` classes.
