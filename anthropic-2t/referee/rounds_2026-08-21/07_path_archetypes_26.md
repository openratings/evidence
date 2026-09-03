# Path archetypes on 26 listings — result and what it licenses (2026-08-22)

Code: `similarity/archetypes.py` → `figures/archetypes_26.md`, `similarity/out/archetypes_26.json`. Inputs: Alpaca bars (26 listings), PROMPT H lockup/IPO terms, FRED macro at IPO. Spec: Qwen F §2, H2 §7.

**Clusters (Ward, k=4, 25 full 26-week paths vs first close; SPCX held out at 10 weeks):**
- straight slide (5): FIG, KLAR, RIVN, HOOD, META — −37% at wk13, −68% at wk26, no peak after wk1.
- slow slide (7): CART, CAVA, COIN, BMBL, DASH, UBER, LYFT — −24% / −25%.
- wobble, flat (10): CRCL, RDDT, ARM, BIRK, ABNB, SNOW, PINS, ZM, PTON, BABA — +22% / +11%, peak +29% wk18.
- moonshot (3): CRWV, PLTR, BYND — +205% / +112%, peak +261% wk12.

**The features-only classifier does not work at n=25 — and we say so.** Multinomial ridge on (float %, log step-up, priced-above-range, Ritter year first-day return, VIX, Nasdaq 3m), LOO-selected C=0.03: LOO accuracy 36% vs 25% chance, achieved by predicting the majority class; adding day-1 pop changes nothing. Qwen's threshold (H2 §7) was 50%. Consequence: **the defensible archetype prior for Anthropic is the base rate, not a feature-conditioned probability** — ≈ wobble 40% / slow slide 28% / straight slide 20% / moonshot 12% — and every scenario row (float 4–8%, $1.5–2.5T, in/above range) returns those base rates within ±3pp. That is the honest statement for the card: pre-listing hype features we can measure do not separate the paths of 25 large listings; what separates them is revealed after listing.

**What the 26 paths do license (empirical, no model):** 24/26 closed below first close within six months; 17/26 traded below offer within 12 months; median worst point in 26 weeks −33% vs first close; at week 26 the median listing is −7% vs first close (p10 −66%, p90 +71%), 56% below. Around the full lockup release the ±10-day window is −11% median, 79% negative (n=24). These are the Fig 5 bands and the base-rate box.

**SPCX as the out-of-sample case:** after 10 weeks its path is closest to "straight slide" (RMS 0.119) then "slow slide" (0.157); the pre-trade model put it at 39% wobble / 29% slow slide / 20% straight slide / 12% moonshot — i.e. the model did not see it coming, which is the point.

**What must not be claimed:** that any of this predicts Anthropic's path; that the four clusters are stable (k=4 on 25 paths is a prototype; two clusters are "slides" of different speed); confidence intervals on the probabilities.

**Next (only if wanted):** add EV/NTM-revenue and concurrent-supply features for the 14 comps that have them (n drops to 14 — likely worse), or accept the base-rate framing and spend the effort on the conditional-on-first-print update (archetype membership after 4/8 weeks of trading is where the separation is).

Analytical opinion, not investment advice.
