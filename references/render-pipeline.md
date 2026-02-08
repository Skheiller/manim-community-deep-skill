# Render Pipeline

## Mental model

A render pass is `Scene` timeline execution over mobject state with animation interpolation, emitted through a renderer and written by file writer utilities.

## Lifecycle

1. CLI/config resolved.
2. Scene module imported.
3. Scene instantiated.
4. Renderer initialized (`cairo` or `opengl`).
5. `construct()` executed.
6. `self.play(...)` calls perform frame stepping over run time.
7. Outputs saved (image/video and caches).

## Mobject lifecycle

- `add`: register for drawing
- `play`: animate state transitions
- `remove`/fade out: visibility and cleanup
- updaters: frame-level mutation callbacks

## Key reliability principle

Prefer explicit state transitions and short updater lifetimes. Long-lived implicit state mutations are the main source of unpredictable scene behavior.
