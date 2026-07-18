# Flat, gradient-free surface techniques

> Status: experience + tooling survey. Source: a deep read of Tooooools.app and Effect.app (pivosoki), cross-checked against SVG-filter and canvas primitives. Distilled 2026-07-18.

## Doctrine: flat color, no gradients

**Hard rule (velofy house):** frontends use flat, solid color. No `linear-gradient`, `radial-gradient`, or `conic-gradient`, and no blurred-blob "mesh/aurora" fields (`filter: blur()` on colored divs reads as a gradient even though a grep for `gradient(` misses it). The blue-to-purple gradient in particular is an instant tell of AI-generated slop.

Flat does not mean plain. Distinctiveness comes from **texture, pattern, and processing**, not color ramps. The techniques below all produce striking, avant-garde surfaces with zero gradients: they use inline SVG filters, SVG `<pattern>` tiles, and `<canvas>`, applied to solid-color content and live text.

Enforce with a grep gate before shipping:
`grep -oiE '(linear|radial|conic)-gradient' file.html` must return 0, and audit any `filter: blur(` over ~30px used as a background field.

## The cookbook

Each entry: the visual, and the gradient-free web primitive that produces it.

| Technique | Visual | Gradient-free primitive |
| --- | --- | --- |
| **Organic warp** | Solid text/shapes rippled and melted like heat haze. Nothing else on the web looks like it. | `<feTurbulence>` -> `<feDisplacementMap in="SourceGraphic">`. Animate `baseFrequency`/`scale` for motion. |
| **Ordered / Bayer dithering** | 1-bit lo-fi, newsprint, retro screen. | Tile a Bayer matrix as an inline-SVG `<pattern>` of `<rect>`s, or `<feTurbulence>` -> `<feColorMatrix>` (to mono) -> `<feComponentTransfer type="discrete" tableValues="0 1">`. `image-rendering: pixelated` on a downscaled canvas for chunky pixels. |
| **Halftone / Ben-Day / dot-matrix / LED** | Comic-print dots, sized by tone. | Inline SVG `<pattern>` of `<circle>` (vary `r`) used as a `mask` over a solid fill. Do NOT use the `radial-gradient` dot trick (it is a gradient). SVG circles or multi-`box-shadow` dots only. |
| **ASCII** | Terminal / brutalist text render. | Pure monospace text in a `<pre>` or a CSS grid of `<span>`s; pick glyph by density. Selectable, animatable, zero images. |
| **Edge-detection wireframe** | Technical outline / blueprint. | `<feConvolveMatrix>` edge kernel `-1 -1 -1 / -1 8 -1 / -1 -1 -1`, or `<feMorphology operator="dilate">` composited (XOR) against the source. On vector shapes, just `stroke`. |
| **Emboss / bevel** | Tactile relief, letterpress. | `<feConvolveMatrix>` emboss kernel `-2 -1 0 / -1 1 1 / 0 1 2`, or the cheap version: two-tone `text-shadow`/`box-shadow` (light top-left, dark bottom-right). Avoid `feSpecularLighting` if it reads as a smooth ramp. |
| **CRT / scanlines / aperture grille** | Old-monitor, phosphor. | Overlay an SVG stripe `<pattern>` (thin `<rect>` lines, or R/G/B vertical bars) with `mix-blend-mode: multiply`. Curvature via `<feDisplacementMap>` or `transform: perspective()`. Never `repeating-linear-gradient` (it is a gradient function). |
| **Cellular automata** | Living, generative two-color texture. | `<canvas>` 2D grid + `requestAnimationFrame` (Game of Life, or Rule 30 -> Sierpinski). Two flat fills. Precompute one frame into an SVG `<pattern>` for a static version. |
| **Threshold / posterize (1-bit)** | High-contrast poster graphics. | `<feComponentTransfer type="discrete">` or a hard `<feColorMatrix>` snaps any content to 2-3 flat tones. |
| **RGB shift / chromatic aberration** | Glitch punctuation. | Isolate channels with `<feColorMatrix>`, `<feOffset>` each, `<feBlend mode="screen">`; on text, a cyan/magenta offset `text-shadow`. |
| **Grain / noise** | Printed, filmic tooth over flat color. | `<feTurbulence type="fractalNoise">` as a low-opacity overlay with `mix-blend-mode: overlay`. The one texture that rescues any flat color from feeling vector-clean. |
| **Reeded glass** | Fluted, ribbed refraction divider. | `<feDisplacementMap>` driven by a vertical-stripe map. |

## Where to reach for these

- **Hero signature**: organic warp on the wordmark, or a cellular-automata canvas field, or a halftone/dither treatment of a solid shape. One per page.
- **Section texture**: grain overlay, dither background, CRT scanline strip.
- **Type effects**: ASCII render, RGB-shift on hover, emboss on a flat plate.
- **Dividers / accents**: reeded-glass strip, edge-detected outline frames.

## Skip under the no-gradient rule

Anything that is a color ramp or needs a source photo: gradient maps, duotone-by-ramp, color grading / curves / levels / hue-sat, bloom / halation / star-glow / vignette, and all blur families (radial glow is `radial-gradient` territory). Use a flat solid, a hard threshold, or one of the pattern techniques above instead.
