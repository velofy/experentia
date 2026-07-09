# experentia: the build contract for agents

You are an AI agent about to build a web frontend. experentia is the taste layer
that tells you what good looks like and why, backed by evidence. Read this file
first, then follow the flow. Do not skip the verification step.

## What you have access to

| Source | Repo | What it gives you |
| --- | --- | --- |
| summit.js | velofy/summitjs | The performant component and technique runtime: tokens, components, loaders. Read its CSS before writing a component's markup, since components have real markup contracts. |
| ui-atlas | velofy/ui-atlas | Reference landing pages and templates you can read for layout precedent. |
| experentia | this repo | Why a design is good (research/), the distilled rules per genre (taste/), the reference implementations (templates/), and the defects to never ship (checklists/). |

## The flow

1. **Pick the genre.** A genre is an audience choice, not a universal. Read
   `research/color.md` and `research/style.md` for the axes that matter
   (light/dark, accent warmth, visual complexity, prototypicality). Choose the
   `taste/<genre>.json` profile whose audience matches the brief. Available
   profiles are listed below.

2. **Load the taste profile.** It is machine-readable on purpose. It gives you a
   token set with precomputed contrast pairs, type roles, a layout grammar
   (ordered slots with contracts), and a set of assertions phrased as pass/fail
   tests. The tokens already satisfy the WCAG floors; do not retune them without
   re-checking contrast.

3. **Assemble from summit and ui-atlas.** Pull components and loaders from
   summit.js rather than hand-rolling them, and read a ui-atlas template in the
   same category for layout precedent. Keep the page prototypical in structure
   and differentiated only in surface (type, color, one signature moment). Spend
   novelty once; a page that breaks three conventions reads as noise
   (`research/style.md`).

4. **Build nav to footer, mobile first.** Navigation is visible by default, five
   or fewer primary destinations, no hamburger on desktop and only as a last
   resort at phone widths. Every page carries a centered page-transition loader
   that appears only after a 300ms delay threshold, shows a single indeterminate
   ring on the page ground, and degrades to a static mark under
   `prefers-reduced-motion`. Ship as self-contained HTML with system fonts and
   no blocking third-party requests so LCP stays under 2.5s on a mid-range phone.

5. **Verify before you call it done.** Run every assertion in the genre profile,
   then walk `checklists/pre-ship.md` item by item. These are real defects found
   in shipped templates, not hypotheticals. In particular: probe
   `document.scrollingElement.scrollWidth` at a true 390px rendered inside a
   390px iframe host, never a naive headless window (headless Chrome clamps to a
   500px minimum and will lie to you). Confirm every `var(--x)` resolves, every
   `<a>` has an explicit color, and the em-dash count is zero.

## Available genres

| Profile | Template | Audience |
| --- | --- | --- |
| `taste/dark-cinematic-lab.json` | `templates/dark-cinematic-lab.html` | Developer-facing AI or infrastructure product. Dark ground, typographic UI, one cinematic image, terminal affordances. Trades broad warmth for in-group credibility. |
| `taste/warm-light-editorial.json` | `templates/warm-light-editorial.html` | A design-led publication or studio journal. Light warm ground, serif voice, one restrained accent. The light and warm counterpoint to the lab genre. |
| `taste/app-dashboard.json` | `templates/app-dashboard.html` | A data-dense operator product. Information design leads: sidebar nav, KPI cards with sparklines, a scrolling data table, semantic status colors distinct from the accent, skeleton loaders. |
| `taste/developer-docs.json` | `templates/developer-docs.html` | Product documentation. High prototypicality: top nav, persistent sidebar, a 65ch prose column, anchored headings, and code blocks that wrap or scroll. |
| `taste/commerce-marketing.json` | `templates/commerce-marketing.html` | A conversion-focused storefront or landing page. The CTA wins on contrast, not hue; product grid, trust signals, pricing, mobile first. |

More genres are added over time. Each ships as a profile plus a verified
reference template, and every profile carries its own assertions.

## The non-negotiables

- Accessibility floors are checked before any taste judgment: 4.5:1 for text,
  3:1 for large text and interactive borders. A palette that cannot meet them is
  rejected, not shipped with a note.
- A rule with no citation is experience and says so. A claim carries its
  verification status. Unverified means unverified.
- No em-dash characters anywhere, in copy or code or comments.
