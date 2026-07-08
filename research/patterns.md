# Patterns: famous sites, navigation, loading, performance

Status: claims here were extracted from the cited sources by the research harness but sit BELOW the adversarial-verification bar unless marked verified (the verification budget ran out mid-run; see `claims-raw.json` for the full 118-claim extraction). Treat as strongly sourced working knowledge.

## Performance budgets (source: [web.dev Core Web Vitals thresholds](https://web.dev/articles/defining-core-web-vitals-thresholds))

- Largest Contentful Paint: good at or under **2.5s**, poor above **4s**.
- Core Web Vitals thresholds are set at the 75th percentile of page loads, so budgets must hold on mid-range mobile hardware, not on a developer laptop.

**Engine rule:** every experentia template targets LCP under 2.5s on a mid-range phone; since templates ship as single self-contained HTML with system fonts and no blocking third-party requests, the practical budget is file weight and first-viewport work.

## Mobile navigation (source: [NN/g hamburger study](https://www.nngroup.com/articles/hamburger-menus/), [NN/g mobile nav patterns](https://www.nngroup.com/articles/mobile-navigation-patterns/))

- Hidden (hamburger) navigation halves engagement on desktop: used in ~27% of cases vs ~50% for visible or combo navigation (179-participant quantitative study).
- Tab bars and top nav bars should carry **at most 5 items** to preserve touch-target size; tab bars stay persistent across screens.

**Engine rules:** navigation is visible by default; hamburgers are a last resort at phone widths only, never on desktop. Five or fewer primary destinations. Touch targets never shrink below comfortable size to fit more items.

## Loading states (sources: [Kraft and Hurtienne, ECCE 2018](https://dl.acm.org/doi/10.1145/3232078.3232086); [Viget, n=136](https://www.viget.com/articles/a-bone-to-pick-with-skeleton-screens); [uxdesign.cc, n=80](https://uxdesign.cc/what-you-should-know-about-skeleton-screens-a820c45a571a))

The evidence on skeletons vs spinners is genuinely mixed, and experentia records it as mixed:

- FOR skeletons: a fictional-news-site test found skeleton screens scored higher than spinners on perceived speed and ease of navigation (ECCE 2018). A separate n=80 study found skeleton splash screens perceived as shorter than blank screens or spinners.
- AGAINST skeletons: a controlled n=136 test of three equal-duration animations found the skeleton produced the LONGEST perceived wait (2.82s) vs spinner (2.41s) and blank (2.29s).

**Engine rules distilled from the conflict:**

1. The best loading state is not needing one; under ~300ms show nothing.
2. For content whose shape is known (lists, cards), use skeletons that exactly mirror final layout so nothing jumps (layout stability is the part nobody disputes).
3. For full page transitions of unknown duration, use a single centered indeterminate loader (spinner or logo mark) on the page ground, appearing only after a delay threshold, with `prefers-reduced-motion` yielding a static mark.
4. Never let a decorative loader block content that is already renderable.

## Famous-site convergences (sources: [Web Design Museum](https://www.webdesignmuseum.org/web-design-history), [Version Museum](https://www.versionmuseum.com/), [Fast Company on Google's 41 blues](https://www.fastcompany.com/1403230/googles-marissa-mayer-assaults-designers-data), [CXL on CTA color](https://cxl.com/blog/which-color-converts-the-best/))

- Long-lived giants (Google, Wikipedia, Amazon) evolved by continuous small revisions rather than dramatic reinventions; their layouts are the definition of prototypicality for their categories.
- Google really did A/B test ~41 shades of blue to standardize its link color (confirmed by Marissa Mayer, 2009); the durable lesson is that even micro color decisions were settled by measurement, and the winner was a mid blue, "not too green, not too red".
- There is no universally best-converting CTA color: button performance tracks CONTRAST against the surrounding page, not hue (the isolation effect). The famous red-vs-green tests measured visual hierarchy, not color psychology.

**Engine rules:** category layouts stay prototypical; the CTA is the highest-contrast element in its viewport regardless of hue; brand accent and CTA emphasis are separate decisions.
