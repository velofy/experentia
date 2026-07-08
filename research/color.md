# Color: what the evidence says

Status: every claim in this file survived 3-vote adversarial verification (see `claims-verified.json` for quotes and votes). Sources are linked inline.

## The theory

Color preference is learned valence, not raw optics. The ecological valence theory holds that people like a color to the degree they like the things it reminds them of, and a single predictor built on that idea (the WAVE score of color-associated objects) explains 80% of the variance in average preference ratings ([Palmer and Schloss, PNAS 2010](https://www.pnas.org/doi/10.1073/pnas.0906172107)). Cross-cultural testing supports several but not all of the theory's predictions ([Yokosawa et al., Cognitive Science](https://onlinelibrary.wiley.com/doi/10.1111/cogs.12291)).

**Engine implication:** palettes should be built from positive object-associations (sky, water, foliage, warm light), not abstract hue math.

## The robust regularities

- Average hue preference peaks broadly at **blue** and dips most sharply at **chartreuse / dark yellow** ([PNAS](https://www.pnas.org/doi/10.1073/pnas.0906172107)); the same peak-blue, trough-dark-yellow structure holds in both U.S. and Japanese samples, along with a general preference for **saturated** colors ([Cognitive Science](https://onlinelibrary.wiley.com/doi/10.1111/cogs.12291)).
- **Blue beats red for trust** across three studies ([Trustworthy Blue or Untrustworthy Red](https://www.researchgate.net/publication/334550253_Trustworthy_Blue_or_Untrustworthy_Red_The_Influence_of_Colors_on_Trust)).
- Website **colour appeal drives trust and satisfaction**, which drive loyalty (all p<0.001), and a **yellow site scheme was disliked in all three cultures tested** (Canada, Germany, Japan) ([Cyr et al., Int. J. Human-Computer Studies](https://www.sciencedirect.com/science/article/abs/pii/S1071581909001116)).

**Engine implications:** blue-family accents are the lowest-risk default for trust surfaces; never build a site's ground or accent on chartreuse/dark-yellow; prefer saturated accents over muddy ones; large pale-yellow grounds are an evidence-backed anti-pattern.

## The caveats that keep us honest

- Blue-preference is NOT a human universal: the remote Yali of Papua most preferred red and yellow, while Poles most preferred blue ([Sorokowski et al.](https://link.springer.com/article/10.3758/s13423-014-0591-8)).
- Sex differences replicate across wildly different cultures (women peak at red 21%, men at blue 19%, contrast correlation r=.93) ([same source](https://link.springer.com/article/10.3758/s13423-014-0591-8)).
- Lightness taste varies by culture: Japanese participants like darker colors less than U.S. participants ([Cognitive Science](https://onlinelibrary.wiley.com/doi/10.1111/cogs.12291)).

**Engine implication:** taste rules are defaults with audience parameters, not laws. A template system should expose light/dark and accent-warmth as first-class audience knobs.

## The hard floors (accessibility, non-negotiable)

- Text contrast at least **4.5:1**; large text (18pt, or 14pt bold) at least **3:1** (WCAG 2.1 AA, SC 1.4.3).
- UI components and meaningful graphics at least **3:1** against adjacent colors (SC 1.4.11).
- Source: [WCAG 2.1](https://www.w3.org/TR/WCAG21/).

**Engine implication:** every generated palette ships with precomputed contrast pairs; a palette that cannot satisfy these floors is rejected before any taste judgment happens.
