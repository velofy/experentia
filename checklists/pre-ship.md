# Pre-ship checklist: the misses that actually happen

Every item below is a defect class found in real velofy templates during a full visual audit (July 2026). An agent building a frontend with experentia MUST verify each item before calling the work done. None of these are hypothetical.

## Links and color

- [ ] Every `<a>` on the page has an explicit color. An anchor with no color rule renders in the browser's default blue (purple when visited), which will not match any design. Set a global `a { color: ... }` and check footers, inline body links, and FAQ answers specifically.
- [ ] Button-styled anchors (`<a class="btn">`) have `text-decoration: none` explicitly. Browsers underline anchors by default; a CSS reset in one environment can hide this miss until the file is served raw.

## Specificity

- [ ] No container rule outranks a component rule. The recurring shape: `.nav a` or `.window-body a` (0,1,2) silently beats `.btn` (0,1,0), recoloring or underlining every button inside that container. Grep for `a` selectors scoped under containers and check every component that can appear inside them.
- [ ] When vendoring a component library, confirm which CSS custom properties its rules actually read, and that every one resolves. A `var(--foo)` with no definition renders as transparent/nothing: invisible buttons, invisible spinners, invisible skeletons.
- [ ] Custom properties composed inside other values must have the right shape. A `--ring` token holding a full shadow list breaks any rule that writes `box-shadow: 0 0 0 3px var(--ring)`; the computed value is silently `none`, and keyboard focus disappears page-wide.

## Component contracts

- [ ] Vendored components get their real markup contract, not an approximation. A switch that expects `<input type="checkbox"> + .s-track` renders as an unstyled sliver if given a `<button>` with a bare span. Read the component's CSS before writing its HTML.

## Mobile (test at a true 390px)

- [ ] No page-level horizontal scroll at 390px. The recurring causes: `white-space: nowrap` inside flex rows, flex/grid children missing `min-width: 0`, and long unbroken strings (URLs) in code blocks.
- [ ] `overflow-x: clip` on a page container HIDES overflow instead of scrolling it. Never rely on it to contain content that can exceed the viewport; make the content wrap (`overflow-wrap: anywhere`) or scroll inside its own container.
- [ ] Code blocks either soft-wrap (`white-space: pre-wrap; word-break: break-word`) or scroll inside their own `overflow-x: auto` container. A clipped CDN URL is a broken install instruction.
- [ ] Fixed/floating elements (docks, toggles, chat bubbles) never cover content at mobile sizes. Give the page bottom clearance equal to the element's height plus margin, and check the last interactive element on every page (sign-in links, footer text).
- [ ] Wide tables scroll inside their wrapper with a visible affordance (an edge fade mask), never silently.
- [ ] TOOLING TRAP: headless Chrome clamps windows to 500px minimum width. A naive `--window-size=390` screenshot is a crop of a 500px layout and fabricates clipping that does not exist (and hides clipping that does). Render inside a 390px iframe host, and probe `document.scrollingElement.scrollWidth` for the truth.

## States

- [ ] Keyboard focus is visible on every interactive element. Do not trust the framework default; tab through, or probe computed `box-shadow`/`outline` on `:focus-visible`.
- [ ] `prefers-reduced-motion` renders full content with no animation dependencies.
- [ ] No-JS renders all content. If JS adds reveal/pin behavior, gate the hiding CSS behind a JS-added marker class so the default is visible, not the reverse.
- [ ] Dark/light: if the page commits to one look, force EVERY family of tokens in both scheme branches, including semantic colors (success/warn/danger and their soft backgrounds). A light-scheme visitor must not get pastel badges on a dark page.
- [ ] Inputs get autofill styling on dark themes (`input:-webkit-autofill` inset box-shadow), or Chrome paints them pale blue.
- [ ] Programmatic `.focus()` on page load must not paint a focus ring; suppress on the container, keep it for keyboard.

## Semantics of color

- [ ] Status colors are never the same value as the accent within one palette. If a warn gold equals the accent gold, warning state becomes invisible as a category.
- [ ] Loaders and empty states are visibly populated in EVERY animation phase; a loader whose keyframes hold an all-erased frame reads as a broken empty box in screenshots and paused tabs.

## Verification protocol

1. Screenshot desktop (1440) and true-mobile (390 via iframe host), full page height.
2. Probe `scrollWidth` at 390.
3. Render a no-JS copy (strip `<script>`) and confirm all content visible.
4. Force the opposite color scheme and confirm tokens hold.
5. Grep: em-dash count is zero; every `var(--x)` has a definition; no `<a` without a color rule in scope.
