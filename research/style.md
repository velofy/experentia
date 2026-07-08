# Style: what the evidence says

Status: the four claims in "Verified" survived 3-vote adversarial verification. The "Pending verification" set was extracted from primary sources but its verification votes errored on an API limit mid-run; re-verification is queued. See `claims-verified.json`.

## Verified

- First aesthetic impressions of a web page form within **50 milliseconds** ([Lindgaard et al., Behaviour and IT 2006](https://www.tandfonline.com/doi/abs/10.1080/01449290500330448)).
- **Visual complexity (VC) and prototypicality (PT)** shape aesthetic judgment within those first 50ms, tested on 119 real-website screenshots ([Tuch et al., Google Research / IJHCS 2012](https://research.google/pubs/the-role-of-visual-complexity-and-prototypicality-regarding-first-impression-of-websites-working-towards-understanding-aesthetic-judgments/)).
- The winning combination is **low visual complexity plus high prototypicality**: simple layouts that look like what the category is supposed to look like.
- The effect exists even at **17ms**, with complexity mattering more than prototypicality at that speed.

**Engine implications:**

1. The first viewport is the whole game; it must parse instantly. Budget the hero's element count.
2. Novelty spends a limited budget. A page can break ONE convention memorably; a page that breaks three reads as low-prototypicality noise. This is why the "one signature element, everything else disciplined" rule works.
3. Category templates (landing, docs, dashboard, checkout) should be prototypical in structure and differentiated in surface (type, color, texture, one signature moment).

## Pending verification (plausible, primary-sourced, votes errored)

- 50ms ratings correlate highly with 500ms ratings; first impressions are stable (Lindgaard).
- Perceived complexity + colorfulness models plus demographics explain ~48% of appeal variance at 500ms (Reinecke et al., CHI 2013).
- Complexity is the dominant driver, with an asymmetric inverted-U: high complexity hurts sharply, low complexity barely (Reinecke et al.).
- The aesthetic-usability effect: pre-use aesthetics-usability correlation r=.66; after use, perceived usability tracked the interface's aesthetics rather than its actual manipulated usability (r=.71) (Tractinsky et al., "What is beautiful is usable").
- Conclusion of that line of work: aesthetics is treated by users as a usability cue, so it cannot be an afterthought.

**Engine implication (contingent):** if confirmed, aesthetic investment is not decoration; it directly moves perceived usability, which justifies the taste-engine's existence in performance terms.
