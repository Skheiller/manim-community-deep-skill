# Preflight Brief and Preference Handshake

Use this at the start of a new animation request.

Purpose:

- align style and constraints early,
- avoid wasted rendering time,
- prevent mismatches in theme, pacing, and complexity.

## Step A: Mini Blueprint (short)

Return a compact draft (about 4-7 bullets), for example:

1. Visual objective (what viewer should understand)
2. Core structure (2-5 beats)
3. Main visual metaphors (graph, diagram, equation, simulation)
4. Motion style (calm/medium/high)
5. Expected duration range
6. Preview + final export plan

Do not provide full object-level details yet.

## Step B: Preference Questions (targeted)

Ask short, concrete questions:

1. Theme: dark / light / custom colors?
2. Motion intensity: calm / medium / dynamic?
3. Camera: no zoom / selective zoom-pan / cinematic movement?
4. 3D usage: avoid 3D / light 3D / heavy 3D?
5. Style target: 3B1B-like / clean-minimal / custom reference?
6. Text pacing: default readable / very slow and explanatory / faster concise?
7. Duration target: short (<60s) / medium (1-3m) / long (>3m)?

If user already specified one of these, do not ask it again.

## Step C: Confirmation Gate

- Summarize selected preferences in one compact block.
- Ask for explicit confirmation to proceed with detailed blueprint and code.
- If user says "proceed", continue.
- If user does not answer, use conservative defaults and state them clearly.

## Default Preferences (when unanswered)

- Theme: dark
- Motion intensity: medium
- Camera: selective zoom-pan
- 3D: avoid unless concept clearly benefits
- Style: clean explanatory with 3B1B-inspired pacing
- Text pacing: reading-speed based (`wpm=180`, `+1s` margin)
- Duration: keep concise by default

## Output Template

```text
Mini Blueprint
- ...
- ...

Quick Preferences
1) Theme: ...
2) Motion intensity: ...
3) Camera style: ...
4) 3D usage: ...
5) Style target: ...
6) Text pacing: ...
7) Duration target: ...

Reply with edits or say: "proceed".
```
