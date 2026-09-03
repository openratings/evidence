# Path archetypes — first-pass prototype (2026-08-21)

Question (Luis): match Anthropic not by sector but by recency and built-in hype — what *path* do shares of this kind of listing follow? Data: Alpaca daily bars, the 14 W3 comps plus SPCX (2026-06-12), CRCL, FIG. Paths normalised to the **first close** (what a day-one buyer pays). Ward clustering on the weekly log path over the first 6 months (26 points). Prototype; n=15; sample-size caveats apply to everything below.

| archetype | members | mean path: wk4 / wk13 / wk26 | peak |
|---|---|---|---|
| 1 straight slide | FIG, KLAR, META, RIVN | −15% / −44% / −68% | none (wk 0) |
| 2 moonshot | CRWV, PLTR | +10% / +206% / +172% | +251% wk 11 |
| 3 wobble, flat | ABNB, ARM, BABA, DASH, RDDT, SNOW, UBER | −9% / +8% / +1% | +10% wk 10 |
| 4 pop and fade | CRCL | +149% / +42% / +4% | +189% wk 2 |

Facts from the same data: **every one of the 15 traded below its first close at some point in the first six months** (100%). Median worst point in the first six months: −33% vs first close (SPCX so far: −33%, last/peak −33%, last/first −15%). SPCX's first ten weeks sit between archetypes 1 and 3 (RMS distance 0.263 vs 0.260) — too early to call; the pre-listing features (step-up, float, EV/revenue, concurrent supply, retail heat) are what the real method must use, per Qwen's spec (F) and the deep-research data request (PROMPT H).

Per-ticker (first 250 trading days vs first close): RIVN −80% at 6m, FIG −77%, KLAR −64%, META −38%, UBER −35%, DASH −24%, SPCX −15% (10 wk), SNOW −9%, BABA −9%, ABNB +3%, CRCL +4%, RDDT +28%, ARM +106%, PLTR +145%, CRWV +201%.

Next: extend to the H1 list (25–35 listings incl. COIN, HOOD, CART, CAVA, BIRK, LYFT, PINS, ZM, PTON, BYND, TWTR, BMBL), add pre-listing hype features, fit archetype membership from features only, validate leave-one-out (does it put SPCX/CRCL in "pop and fade" blind?), then produce Anthropic's archetype probabilities and a conditional path fan for the card.
