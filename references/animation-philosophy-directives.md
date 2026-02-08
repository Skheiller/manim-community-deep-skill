# Animation Philosophy Directives

Use these directives by default unless the user explicitly requests a minimal/static style.

Goal: build intuition through motion, not just display finished objects.

## Directive 1: Conservation of Visual Mass (Morphing over spawning)

- Prefer `ReplacementTransform`, `Transform`, and `TransformMatchingTex` over frequent raw `FadeIn`.
- New information should visibly come from existing objects whenever reasonable.
- If a scene must introduce a truly new object, establish context first (make room, then reveal).

Examples:

- Equation simplification: move matching symbols into new positions (`TransformMatchingTex`).
- Data-to-chart: morph numbers/tokens into bars/points.
- Grid-to-vector intuition: transform a line/grid element rather than spawning a separate object.

## Directive 2: State Driver Rule (Tracker-driven scenes)

- Use `ValueTracker` for changing quantities (time, angle, threshold, layer step).
- Bind dependent visuals with `always_redraw` or updaters so multiple objects evolve together.
- Avoid hardcoded disconnected snapshots when a continuous parameter explains the concept.

## Directive 3: Semantic Color Rule (Color as syntax)

- Define a `color_map` dictionary early in the scene.
- Reuse the same variable colors across formulas, labels, arrows, and diagrams.
- Treat color as semantic linkage, not decoration.

## Directive 4: Relative Layout + Reflow Rule

- Use relative positioning (`next_to`, `align_to`, `arrange`, `to_edge`) over brittle absolute coordinates.
- Group related elements in `VGroup` so they can move together.
- Before adding new information, reflow existing groups (`animate.shift/scale`) to open space.
- Never drop new objects on top of active objects unless overlap is intentional.

## Directive 5: Dual-View Intuition Rule

- When useful, split the scene into:
1. abstract view (equation/code/logic)
2. geometric or process view (graph/diagram/simulation)
- Drive both views with shared trackers so the relationship is explicit and synchronized.

## Motion and Camera Choreography Defaults

- Keep at least one meaningful motion in most explanatory beats (transform, pointer travel, tracker change, camera move).
- Add camera emphasis where it improves clarity:
- zoom in for detail inspection
- zoom out for context reset
- pan when shifting focus across large layouts
- Prefer purposeful motion to random effects; motion should encode logic progression.

## Frame Fit and Spacing Priority

- Treat frame fit as a hard requirement: no critical graph/text should leave visible bounds.
- Keep the principal composition centered unless there is an intentional side-by-side design.
- Before introducing new objects, create room via reflow (shift/scale/rearrange existing groups).

## Reading-Time Priority for Text

- Do not remove paragraph text immediately after writing.
- Use a dwell-time estimate based on reading speed:
- `seconds = (word_count / wpm) * 60 + 1`
- Default `wpm = 180`; reduce to `140-160` for dense technical text.

## Preview-First Export Policy

- Always produce and show a low-res preview first (`-ql` 480p-equivalent workflow).
- Ask for user confirmation.
- Only after confirmation, run full-quality export.

## Process Logic Guard (Neural nets, pipelines, staged systems)

- Animate stages in causal order.
- Example feed-forward sequence:
1. layer `L1 -> L2` edges
2. `L2` activation
3. layer `L2 -> L3` edges
4. `L3` activation
- Do not animate downstream flow before upstream state is visible.

## Source Notes

- Manim animation API: https://docs.manim.community/en/stable/reference/manim.animation.animation.Animation.html
- Manim `ValueTracker`: https://docs.manim.community/en/stable/reference/manim.mobject.value_tracker.ValueTracker.html
- Manim updaters: https://docs.manim.community/en/stable/reference/manim.animation.updaters.mobject_update_utils.html
- Reading-speed meta-analysis (silent reading baseline context): https://www.sciencedirect.com/science/article/abs/pii/S0749596X19300786
