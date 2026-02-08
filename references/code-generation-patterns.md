# Code Generation Patterns

## Canonical skeleton

```python
from manim import *


class IdeaScene(Scene):
    def construct(self):
        # Beat 1
        ...
        self.play(...)

        # Beat 2
        ...
        self.play(...)
```

## Preferred structure

- `construct()` controls timeline.
- Small helper functions create reusable visual blocks.
- Keep state transitions explicit through `self.play(...)`.
- Add reusable fit/layout helper functions near the top of the file.

## Pattern map

- reveal concept: `FadeIn`, `Write`, `Create`
- focus shift: `Indicate`, `Circumscribe`, subtle scale
- concept morph: `Transform`, `ReplacementTransform`
- remove noise: `FadeOut` and regroup

## Timing guidance

- default beat: 0.6s–1.5s per transition
- dense explanation: add short `wait(0.2-0.4)` pauses for readability

## Readability rule

Never animate every object at once unless intentional; preserve viewer attention hierarchy.

## Formula safety

- Use raw strings for `MathTex` (`r"\\mathcal{L}"`, `r"\\hat{y}"`) to avoid malformed output.
- Compile-check formula scenes early in the loop so broken TeX does not survive to final render.

## Layout safety pattern

```python
def fit_text_in_box(text_mob: Mobject, box: Mobject, width_ratio: float = 0.85):
    max_w = max(0.1, box.width * width_ratio)
    if text_mob.width > max_w:
        text_mob.scale_to_fit_width(max_w)
    text_mob.move_to(box.get_center())
    return text_mob
```

- Use on every boxed text block before `self.play(...)`.
- If text still feels dense after scaling, shorten wording and split into more beats.

## Arrow label pattern

```python
def place_label_for_arrow(label: Mobject, arrow: Arrow, direction=UP, buff: float = 0.15):
    shaft_mid = 0.5 * (arrow.get_start() + arrow.get_end())
    label.move_to(shaft_mid + buff * direction)
    return label
```

- Prefer labels near arrow shafts, not arrowheads.
- Keep label placement consistent across all edges in the same diagram.

## Causal sequence pattern (neural network/process flow)

```python
# Phase 1: L1 -> L2
self.play(LaggedStart(*[Create(e) for e in edges_l1_l2], lag_ratio=0.12), run_time=1.4)
self.play(LaggedStart(*[Indicate(n) for n in layer2_nodes], lag_ratio=0.08), run_time=0.9)

# Phase 2: L2 -> L3 (only after phase 1 completes)
self.play(LaggedStart(*[Create(e) for e in edges_l2_l3], lag_ratio=0.12), run_time=1.4)
self.play(LaggedStart(*[Indicate(n) for n in layer3_nodes], lag_ratio=0.08), run_time=0.9)
```

- Downstream phases must not animate before upstream phases are visible.
- Only use simultaneous phases if the script explicitly says the process is parallel.
