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
- state-driven motion: `ValueTracker` + `always_redraw`

## Timing guidance

- default beat: 0.6s–1.5s per transition
- dense explanation: add short `wait(0.2-0.4)` pauses for readability

## Readability rule

Never animate every object at once unless intentional; preserve viewer attention hierarchy.

## Motion richness rule

- Most explanatory beats should include at least one meaningful movement:
- transform/morph
- tracker-driven update
- focus shift
- camera motion
- If adding a new block causes crowding, move existing groups first, then reveal.

## Frame-fit centering pattern

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

- Apply to main graph/diagram groups before reveal and before final export.
- Prevents off-screen charts and de-centered compositions.

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

## Reflow-before-reveal pattern

```python
# Open space before introducing new content
self.play(existing_group.animate.scale(0.92).to_edge(LEFT), run_time=0.8)
self.play(FadeIn(new_panel), run_time=0.8)
```

- Reposition first, reveal second.
- Prevents objects stacking on top of each other.

## Tracker-driven dual-view pattern

```python
t = ValueTracker(0.0)

eq = always_redraw(lambda: MathTex(r"f(t) = \sin(t)").to_edge(LEFT))
dot = always_redraw(lambda: Dot(axes.c2p(t.get_value(), np.sin(t.get_value())), color=YELLOW))

self.add(eq, dot)
self.play(t.animate.set_value(2 * PI), run_time=3.0, rate_func=linear)
```

- Use one driver to synchronize abstract and geometric views.

## Text pacing (reading-time) pattern

```python
def min_read_time_seconds(text: str, wpm: int = 180, extra_seconds: float = 1.0) -> float:
    words = len(text.split())
    return (words / max(1, wpm)) * 60.0 + extra_seconds
```

```python
paragraph = Text(long_text, font_size=34)
self.play(Write(paragraph), run_time=1.2)
self.wait(min_read_time_seconds(long_text, wpm=180, extra_seconds=1.0))
```

- Use this for full sentences/paragraphs so viewers can read before content transitions away.
- For dense technical text, lower `wpm` (for example `140-160`) to extend dwell time.

## Camera emphasis pattern

```python
frame = self.camera.frame
self.play(frame.animate.move_to(detail_group).set(width=detail_group.width * 1.4), run_time=1.0)
self.play(frame.animate.move_to(ORIGIN).set(width=14), run_time=1.0)
```

- Zoom in to inspect detail, zoom out to restore context.

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
