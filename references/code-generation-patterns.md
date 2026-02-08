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
