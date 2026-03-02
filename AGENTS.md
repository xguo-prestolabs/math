# Math Learning — Agent Guide

This repo is a collection of self-contained interactive math visualizations. Each file is a single HTML page that requires no build step, no server, and no dependencies — open it directly in a browser.

## Current files

| File | Description |
|------|-------------|
| `index.html` | Parametric Curve Demo — animates Circle, Lissajous, Spiral, and Cycloid curves on an HTML5 Canvas |

## Architecture of index.html

The page is plain HTML + vanilla JS in a single `<script>` block. Key sections:

- **`presets` object** — defines each curve with:
  - `t0`, `t1`: parameter range
  - `paramsUI[4]`: slider config (name, min, max, step, value, disabled)
  - `point(t, P)`: pure function returning `{x, y}` in world coordinates
  - optional `mapParams(raw)`: translates raw slider values to named params when the mapping isn't 1-to-1
- **`viewport`** — `{origin, scale}` used by `worldToScreen()` to map world coords to canvas pixels. Updated by `fitViewportToPoints()` on every render so the curve fills the canvas automatically.
- **`render()`** — samples the full curve (1200 pts), fits the viewport, draws grid/axes, draws the full curve in black, draws the trajectory up to current `t` in red, and draws the current point as a pink dot with a coordinate label.
- **`tick()`** — `requestAnimationFrame` loop; advances `t` when playing.

## How to add a new curve

1. Add an entry to the `presets` object following the existing pattern.
2. Add a `<option>` to `#preset` in the HTML matching the key.
3. The UI, playback, and viewport fitting work automatically — no other changes needed.

## How to add a new visualization file

Create a new `.html` file at the repo root. Follow the same conventions:
- Single-file, no external dependencies
- CSS variables for theming (copy `:root` block from `index.html` for consistency)
- Responsive layout with `@media` query

## Conventions

- World coordinates are math-standard (y increases upward); canvas coordinates are screen-standard (y increases downward). `worldToScreen()` handles the flip.
- Sliders always map to named params through `getParamsForPreset()` / `mapParams()`. Never read slider values directly inside `point()`.
- Disabled parameters use `{ name: "-", disabled: true }` in `paramsUI` — the slider is greyed out and the value label shows `-`.
- No frameworks, no bundlers. Keep it that way.
