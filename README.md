# experentia

A taste-engine for frontends. It answers two questions an AI agent cannot answer
from a component library alone: what does good look like for this audience, and
why. The answers are backed by empirical research, distilled into machine-
readable profiles, and proven with reference templates that pass their own tests.

**Live site:** [velofy.github.io/experentia](https://velofy.github.io/experentia/) (landing page and browsable reference templates).

experentia is one of three layers a velofy agent builds with:

- **summit.js** (velofy/summitjs) is the runtime: performant components, tokens,
  loaders.
- **ui-atlas** (velofy/ui-atlas) is the precedent: reference landing pages and
  templates.
- **experentia** (here) is the taste: the evidence, the rules, and the verified
  references that tell an agent which choices are good and which are defects.

If you are an agent, start with [AGENTS.md](AGENTS.md). It is the build contract.

## Layout

| Directory | What it holds |
| --- | --- |
| `research/` | The evidence base. Color, style, and pattern doctrine with citations, plus the raw and verified claim sets from a deep-research pass. Every rule downstream traces back here. |
| `samples/` | Deconstructions of real, well-made pages, read for the reusable rules of their genre. |
| `taste/` | The machine layer. One JSON profile per genre: tokens with precomputed contrast pairs, type roles, layout grammar, and assertions phrased as pass/fail tests. |
| `templates/` | A verified reference implementation per genre, nav to footer, mobile-friendly at a true 390px, self-contained, with a centered page-transition loader. |
| `checklists/` | `pre-ship.md`: the defect classes found in real shipped templates. An agent walks this before calling any build done. |

## Principles

- **Taste is defaults with audience knobs, not laws.** Blue is the lowest-risk
  trust accent, but blue-preference is not a human universal; light or dark and
  accent warmth are first-class choices, not accidents. See `research/color.md`.
- **The first viewport is the whole game.** Aesthetic impressions form in about
  50ms, and the winning combination is low visual complexity with high
  prototypicality. Be prototypical in structure, differentiated in surface. See
  `research/style.md`.
- **Accessibility is a floor, not a garnish.** Contrast is checked before any
  taste judgment. A palette that cannot meet the floors is rejected.
- **Every claim carries its status.** Verified is verified, pending is pending,
  and a rule with no citation says it is experience. The research README records
  exactly what survived adversarial verification and what is still queued.

## Status

The research layer is complete and committed. Five genres ship so far, each as a
profile plus a verified reference template that passes its own assertions:
dark-cinematic-lab, warm-light-editorial, app-dashboard, developer-docs, and
commerce-marketing. More genres follow.

Alongside them, `templates/supply-chain.html` is the one template wired live on
[summit.js](https://velofy.github.io/summitjs/): a neutral operations control tower
whose shipments table, KPIs, low-stock alerts, and carrier bars all react from a
single `s-data` source. It shows the same taste rules driving a reactive interface
rather than a static page. The summit.js runtime is inlined, so the file stays
self-contained with no external requests.
