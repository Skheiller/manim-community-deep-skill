# Logic and Layout Guardrails

Use these rules to prevent the most common quality failures:

- text spilling outside boxes,
- arrow labels overlapping geometry,
- causal/process animations playing in the wrong order.
- objects appearing on top of each other without intentional layering.
- graphs/labels drifting partially off-screen.

## 1) Container text-fit rules

- For any text inside a box/card, constrain width to at most `0.85 * box.width`.
- If width exceeds budget, apply this order:
1. `scale_to_fit_width(max_width)`
2. reduce text complexity (shorten phrase or split into two lines)
3. only then reduce font size further
- Keep a minimum visual padding of `0.15` scene units from text to container edges.

Example helper:

```python
def fit_text_in_box(text_mob: Mobject, box: Mobject, width_ratio: float = 0.85, padding: float = 0.15):
    max_w = max(0.1, box.width * width_ratio)
    if text_mob.width > max_w:
        text_mob.scale_to_fit_width(max_w)
    text_mob.move_to(box.get_center())
    return text_mob
```

## 2) Arrow and label spacing rules

- Attach labels near the shaft midpoint, not on arrowheads.
- Keep consistent buffer from arrow line (`buff` around `0.12` to `0.2`).
- After placement, run local collision checks with nearby labels and shift slightly along normal direction.

Example helper:

```python
def place_label_for_arrow(label: Mobject, arrow: Arrow, direction=UP, buff: float = 0.15):
    shaft_mid = 0.5 * (arrow.get_start() + arrow.get_end())
    label.move_to(shaft_mid + buff * direction)
    return label
```

## 3) Black background style defaults

- Use pure black or near-black background.
- Use high-contrast text and keep decorative colors muted.
- Keep one accent color per active concept; avoid multiple competing saturated colors.

## 3b) Frame-fit and centering rules

- Keep all critical content inside a safe frame budget (about 90% of frame width/height).
- Center the primary content group unless intentional side-bias is part of the design.
- Before final export, compute each major group's bounds and reflow if any part exits frame margins.

Example helper:

```python
def fit_group_to_frame(group: Mobject, width_ratio: float = 0.9, height_ratio: float = 0.88):
    max_w = config.frame_width * width_ratio
    max_h = config.frame_height * height_ratio
    if group.width > max_w:
        group.scale_to_fit_width(max_w)
    if group.height > max_h:
        group.scale_to_fit_height(max_h)
    group.move_to(ORIGIN)
    return group
```

## 4) Causal ordering for process animations

Do not animate all edges/nodes in a process at once unless intentionally showing parallelism.

For neural-network style flows:

1. `input -> hidden_1`
2. `hidden_1 activation`
3. `hidden_1 -> hidden_2`
4. `hidden_2 activation`
5. `hidden_2 -> output`
6. `output activation`
7. optional backward pass in reverse dependency order

Guardrail:

- A downstream edge animation must not start before the upstream node/state is visibly established.

## 5) Pre-export integrity checks

- No clipped text at frame boundaries.
- No text outside its owning container.
- No overlapping formula/text blocks unless intentional.
- No arrow labels sitting on arrowheads.
- Process beats follow declared dependency order.
- New objects do not spawn on top of active objects without prior reflow.
- Camera framing keeps active content inside safe margins after zoom/pan.
- Main graph/diagram group remains centered or intentionally aligned by design.

If any check fails, re-layout and re-time before final render.

## Source Notes

- Manim mobject geometry and layout methods: https://docs.manim.community/en/stable/reference/manim.mobject.mobject.Mobject.html
- Manim animation parameters (`run_time`, `rate_func`): https://docs.manim.community/en/stable/reference/manim.animation.animation.Animation.html
