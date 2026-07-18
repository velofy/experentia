# External design sources

> Status: primary-source survey. Seven design references scraped and read deeply on 2026-07-18 (with curl_reap for the client-rendered ones). Each entry: what it is, the reusable intelligence, and where its data lives in this repo.

These sources feed the rest of `research/` and the `taste/` profiles. Raw pulls are kept in the research workspace; the distilled taxonomy is in [`ui-patterns.json`](ui-patterns.json), the surface techniques in [`techniques.md`](techniques.md), and the token system in [`tokens-geist.json`](tokens-geist.json).

## 1. refero.design  (UI/UX reference library)
A React SPA over a public JSON API (`api.refero.design/v1/*`). It indexes real, shipped product screens three ways at once: **what the screen does** (87 design patterns, 8 kinds), **what it is made of** (69 page elements, 6 kinds), and **who it is for** (42 categories). 293 apps + 416 sites + a 5,635-screenshot search, each screenshot carrying an extracted 5-color palette and detected fonts.
- **Takeaway:** good reference is real screens, queryable by the problem they solve, mineable for layout, color, and type. This is the model for our own taxonomy.
- **Data:** the full pattern/element/category taxonomy is extracted to [`ui-patterns.json`](ui-patterns.json).

## 2. Tooooools.app + effect.app  (creative image-effect labs, by pivosoki)
Browser tools that apply lo-fi image effects: dithering, stippling, halftone, edge, displacement, bevel, cellular automata, CRT, ASCII, RGB shift, grain (14 free / 76 pro GLSL shaders).
- **Takeaway:** distinctiveness without gradients. Every graphic effect maps to a flat, gradient-free web primitive (SVG filter, SVG `<pattern>`, or canvas) applied to solid color and live text.
- **Data:** the technique-to-primitive cookbook + the no-gradient doctrine are in [`techniques.md`](techniques.md).

## 3. Geist  (Vercel's design system + font family)
Swiss-minimalist system: 10 numbered color scales (100 to 1000, fixed semantic roles: 100-400 surfaces, 500-600 borders, 700 brand, 800-1000 text), 6px/12px/16px radii, a hairline-border-plus-layered-soft-shadow elevation model (no harsh drop shadows), and a tight-tracked type scale. Fonts: **Geist Sans** + **Geist Mono** (9 weights, variable) and **Geist Pixel** (bitmap display, 5 shapes: Square, Grid, Circle, Triangle, Line). All SIL OFL.
- **Takeaway:** the token-driven, numbered-scale, hairline-elevation approach is the cleanest flat system going. Geist Pixel is a ship-ready gradient-free display face.
- **Data:** the token system (grays + accents, radii, shadows, type, fonts) is in [`tokens-geist.json`](tokens-geist.json). This is the basis for the velofy stack refresh (flat, amber accent, no blue/purple).

## 4. Zero UI  (zeroui.co teaser + zeroui.vercel.app component library)
Two products, one name. `zeroui.co` is a warm-"paper" teaser for a design toolkit "for AI-centric projects" (palette `#EBE9E6` + `#0D0D0D` + one hot yellow `#FBD437`, hyper-tuned Inter, narrow editorial column, deliberately anti-cold-AI). `zeroui.vercel.app` is a shadcn-style React library whose centerpiece is a first-class **AI Input** component (attach, web-search toggle, mic, submit).
- **Takeaway:** for an AI product, make the **prompt box the hero**, not a form. And a warm palette + one hot accent reads more human than the default cold-AI blue.
- **Applied:** the AI-input-hero pattern shipped as a ui-atlas reference (`landing-pages/clean/31-prompt.html`, warm paper, flat, gradient-free).

## 5. SpiderUI  (spiderui.vercel.app, MIT React component library)
37 animated copy-paste components. The house recipe: a neutral shadcn base + an embossed `surface-inset` shadow system + spring-physics Motion and GSAP SplitText/ScrollTrigger for the wow (CSS keyframes stay minimal). Standouts: cursor image/sticker trails, OPOS hover (word-thumbs to giant headline), self-drawing SVG card strokes, hover-expand accordion reveal, an EQ-bar footer, fan-card stacks, odometer pricing.
- **Takeaway:** interaction, not decoration, is the differentiator. Reserve motion for one or two signature moments; keep the surface flat.

## 6. designindex.xyz  (curated directory, 415 tools/sites)
13 aesthetic categories. Confirmed the current trend cluster: editorial-serif + mono, dark-lab, grain/dither texture, bento grids, retro/ASCII, section-as-set-piece (dedicated galleries for heroes, CTAs, footers, navbars, 404s). Also a map of free type foundries (Fontshare, Uncut, Velvetyne) and flat color tooling.

## 7. getdesign.md  (DESIGN.md collection, 415 systems)
Machine-readable DESIGN.md files for AI coding agents, across 13 categories (editorial-serif, minimal, ai-futuristic, automotive-luxe, crypto, brutalist, terminal, luxe, retro, playful). Confirms the "hand the agent a design contract" model that experentia itself follows.

## Synthesis for our taste layer

- Index by problem (refero), theme by a numbered flat token system (Geist), differentiate the surface with gradient-free processing (Tooooools) and one signature interaction (SpiderUI), and for AI products lead with the prompt and a warm, non-blue palette (Zero UI).
- Everything here obeys the house rules already in this repo: **flat color, no gradients**, accessibility floors first, one signature moment, prototypical structure with a differentiated surface.
