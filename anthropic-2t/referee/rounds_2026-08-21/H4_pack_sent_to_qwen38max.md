# TASK H4 — Re-rate after the fixes (2026-08-22)

In H3 you rated the analysis 6/10 and listed: headline–table inconsistency on the run-rate multiple; the exit-multiple level carrying two-thirds of the verdict on 12 comps (disclose ±1σ, LOO, comp screen); article and card not yet rewritten on v1.5r; rating mapping presented as calibration (5/10); circular-capital causal step asserted not shown; tornado instead of ablation table; ladder first; grade out of the table; "house" sentence implies information asymmetry; "fair value" should be "median simulated fair value" with quartiles. We did all of it. Below: the rewritten card v3, the rewritten article v3, the intercept LOO/comp screen, and the ablation (tornado data). Goal: reach 9/10 — tell us exactly what still stands between this and a 9, and whether anything should be CUT rather than added.

## Card v3
# OpenRatings Impairment Grades for the Anthropic IPO — card v3 (2026-08-22, engine v1.5r)

*Draft for openratings.ai. Engine v1.5r (seed 20261016, 100k paths, 5-year horizon, Coatue gate passed, 13 tests green). Referee trail: Qwen 3.8 Max Tasks A–H3 (`docs/review_2026-08-21/`). Analytical opinion; not a credit rating; not investment advice. Every identified bias pushes grades DOWN, none up.*

**One line.** At a $2 trillion listing the IPO buyer's median return is zero, the chance of losing money is one in two and the chance of losing more than half is one in six — impairment odds we liken to a B− credit. The fund that entered at $380B in February is marked at 4.8× on the same day and is A-grade almost whatever happens next — not because it knows more, but because it paid one-fifth the price. Two-thirds of the gap between this verdict and a merely mediocre one rests on one calibrated number, the exit-multiple level, and we show what happens if it is wrong.

**Run-rate denominators (never averaged).** Last confirmed print **$65B** (end-July 2026; Bloomberg, CNBC, Reuters 2026-08-17). Engine listing run-rate: lognormal, median **$90B**, log-sd 0.20 (90% interval $61–133B), calibrated to the $19B → $65B March–July trajectory; FT reports investors expect $100–120B exit-2026. At $2T that is **22× the model's listing run-rate, 31× the last print**.

## Panel A — the two-investor ladder (Figure 1)

*Series-G fund = Coatue/GIC round, $380B post-money, 2026-02-12; cannot sell at the IPO (≈180-day lockup). The fund's gain is the buyer's cost basis.*

| IPO valuation | EV / model run-rate ($90B) | EV / last print ($65B) | **buyer** IRR p50 (p25–p75) | P(lose money) | P(lose > half) | P(≥40% below IPO price, 2y) | P(≥40% off peak, 2y) | **fund** MOIC at IPO | at lockup p50 | hold-to-2031 p50 | P(buyer loses & fund > 3×) |
|---|---|---|---|---|---|---|---|---|---|---|---|
| $1.00T | 11× | 15× | 15% (4–28) | 18% | 2.4% | 31% | 78% | 2.4× | 2.9× | 4.8× | 0% |
| $1.25T | 14× | 19× | 10% (−1–22) | 27% | 5.2% | 38% | 81% | 3.0× | 3.4× | 4.8× | 0% |
| $1.50T | 17× | 23× | 6% (−4–18) | 35% | 8.8% | 43% | 84% | 3.6× | 3.9× | 4.8× | 9% |
| $1.75T | 19× | 27× | 3% (−7–15) | 43% | 13.2% | 48% | 86% | 4.2× | 4.3× | 4.8× | 16% |
| **$2.00T** | **22×** | **31×** | **0% (−10–11)** | **50%** | **17.7%** | **53%** | **87%** | **4.8×** | **4.7×** | **4.8×** | **23%** |
| $2.50T | 28× | 38× | −4% (−14–7) | 61% | 26.7% | 60% | 90% | 6.0× | 5.5× | 4.8× | 34% |
| $3.00T | 33× | 46× | −8% (−17–3) | 69% | 35.4% | 66% | 92% | 7.1× | 6.3× | 4.8× | 43% |

**Grade analogy** (P(lose > half in 5 years) bracketed by S&P 5-year cumulative corporate default rates by notch, 2024 study Table 26, verified verbatim — *an analytical analogy for readability, not a calibration against realised default frequencies; the operative numbers are the probabilities*): $1.0T BBB− · $1.25T BB− · $1.5T B+ · $1.75T B · **$2.0T B−** · $2.5T CCC/C · $3.0T CCC/C. Fund at every price: A or better (its P(lose > half) < 0.1%; the top six notches are indistinguishable at five years). Brackets: ≤0.42% A-or-better · BBB+ ≤0.79 · BBB ≤1.09 · BBB− ≤2.40 · BB+ ≤2.90 · BB ≤5.05 · BB− ≤8.28 · B+ ≤12.88 · B ≤14.69 · B− ≤22.03 · CCC/C ≤46.53.

Fund note: the fund's sub-year annualised IRR is deliberately not printed (4.8× in ~8 months annualises to ~830%). Its A-grade assumes a liquid exit — exactly what disappears in a sector unwind (Panel G). Dilution: buyer 0.92 over 5y; fund 0.905 to IPO, 0.84 to 2031.

## Panel B — what moves the verdict (Figure 2, `figures/tornado_v15.png`)

Switching each v1.5r channel off, median fair value at a 10% required return (base $1,245B): **exit-multiple level +$434B**, **restatement scenario +$169B**, every other channel within ±$6B; the two interact by +0.002 on P(loss) (negligible). Intercept ±1 bootstrap sd moves fair value to **$1,040B–$1,499B** and P(loss) at $2T to **0.59–0.40**; the v1 prior gives 0.35; the v1 engine with every channel off gives 0.24.

**Disclosure (required wording).** The exit-multiple level is anchored to 12 comparable IPOs by a ridge fit that shrinks slopes toward the v1 prior (λ=1000 by leave-one-out). The fit moves the intercept from 1.20 to 0.898 (−26% on every multiple); the leave-one-out RMSE improvement over the fixed prior is <0.1% and the shift is 1.6 bootstrap standard errors — not statistically distinguishable from zero. Leave-one-out over the comps moves the intercept between 0.798 (drop ABNB) and 1.040 (drop CRCL); no single comp restores the prior (`figures/multiple_fit_loo.md`, screen disclosed). We adopt the fitted level because the prior was uncalibrated judgment and the comps are data; the headline is conditional on that choice. The restatement probability (35%) and haircut (20–40%) are analyst estimates: the risk that cloud-reseller flow booked gross is reclassified net under ASC 606. The S-1 revenue-recognition note resolves it; the no-restatement row is always shown (P(loss) 0.43).

## Panel C — issuer commitment-coverage grade (KMV-style)

Default point D = debt-like take-or-pay compute commitments. Disclosed as of Aug-2026: AWS >$100B/10y, Azure $30B, Google "tens of billions" (no primary for $40B), Fluidstack $50B, TeraWulf ~$19B, Hut 8 ~$7B. Which are take-or-pay is unknown until the S-1; **$170B (AWS + Google + Azure) is the floor, ~$240B if Fluidstack and TeraWulf are take-or-pay**. Breach = value below D in any quarter within 5 years, 100k paths. Two bases: **marked** (engine value incl. multiple noise) and **stripped** (revenue × gross margin at a steady capitalisation).

| default point D | 5-yr breach, marked | grade | breach, stripped | grade |
|---|---|---|---|---|
| $132B — $170B on the KMV convention | 0.00% | A or better | 0.00% | A or better |
| $170B — disclosed, accelerated | 0.03% | A or better | 0.00% | A or better |
| $250B — incl. Fluidstack/TeraWulf | 0.4% | A or better | 0.00% | A or better |
| $500B | 10.3% | B+ | 0.00% | A or better |
| $625B | 19.7% | B− | 0.02% | A or better |
| $825B | 36.4% | CCC/C | 0.4% | A or better |
| **$1,000B — Amodei's "$1T of compute"** | **49.9%** | **D-range (>46.5%)** | **1.9%** | **BBB−** |
| $1,250B | 65.5% | D-range | 7.6% | BB− |

Reading: on the business alone Anthropic out-earns any commitment it has disclosed; **every breach in the marked column is a mark-to-market event** — the value falls because the multiple falls, not because the business stops paying. That is the circular-capital channel (Panel G). Coverage lens: against $100B/yr of commitments, gross profit is short in most paths in year 1 (funded from the IPO raise) and in a minority by year 5. Closed-form Merton is not used (mark noise is not business risk). Change vs v2: the marked ladder is roughly one notch harsher at every D ≥ $500B because v1.5r values are lower (level) and noisier (calibrated marks); the stripped ladder is unchanged.

## Panel D — the ride, any entry

At $2T: P(≥40% below the IPO price at some point in years 1–2) **53%**; P(≥40% fall from a peak) **87%**; if metered growth prints <30% annualised two quarters running (13% chance): P(≥40% drawdown) **75%**. Price path: IPO price converging to the model mark (half-life 4q) with staged lockup shocks — first release q1 (−6%, sd 0.20), full release q2 (−10%, sd 0.30) — from our own 26-listing measurement (full-release ±10-day window median −11%, 79% negative, n=24; first release −6%, 69%). Path archetypes (26 listings, `07_path_archetypes_26.md`): 24/26 closed below first close within six months; week-26 median −7% vs first close (p10 −66%, p90 +71%); the pre-listing hype features we can measure do not separate the paths (classifier at chance), so the archetype prior is the base rate — wobble 40% / slow slide 28% / straight slide 20% / moonshot 12%.

## Panel E — what should I pay?

Median simulated fair value (p25–p75): require 8%/yr → **$1.37T** ($0.82–2.34T; 32% of futures make $2T cheap) · 10% → **$1.25T** ($0.75–2.14T; 28%) · 12% → $1.14T (24%) · 15% → $1.00T (19%) · 20% → $0.81T (13%) · 35% → $0.45T (3%). Under the sector-unwind overlay: 10% → $1.09T.

## Panel F — pre-registered downgrade triggers (scored the week the S-1 is public, and at lockup)

| trigger | effect |
|---|---|
| S-1 revenue-recognition note shows Anthropic as agent on cloud-resold revenue (gross → net, 20–40% of ARR) | restatement branch becomes the base: buyer −1 notch at every price |
| S-1 listing run-rate below $72B (engine p25) | buyer −1 notch; above $112B (p75) +1 |
| two consecutive quarterly prints of metered growth < 30% annualised | 75% drawdown branch; buyer −1 to −2 notches |
| gross margin prints < 35% | GM cliff: −1 notch |
| float at IPO < 5% | price declared uninformative for 2 quarters; no upgrade on price |
| new take-or-pay commitment > $100B, or S-1 shows Fluidstack/TeraWulf as take-or-pay | issuer −1 notch per ~$100B of D above $250B |
| second export-control episode within 12 months of listing | −1 notch, buyer and issuer |
| CoreWeave 5y CDS > 1,200bp (≈855bp at pre-registration), or a neocloud misses debt service | sector-linked grade −1 notch |
| two of MSFT/GOOGL/AMZN/META cut capex guidance >15% in the same quarter | sector-linked grade −1 notch |
| Ramp AI-adoption share falls two consecutive months AND two frontier releases < 5% gain on enterprise benchmarks | capability-plateau flag, −1 notch |

## Panel G — sector-linked grade: circular capital (the "Lehman" term, stated carefully)

Anthropic has no debt. The sector it sits in runs on reciprocal capital: Amazon commits up to $25B to Anthropic, Anthropic >$100B to AWS; Google invests, Anthropic commits to ~1M TPUs; Nvidia invests in and backstops the buyers of its GPUs (up to $100B to OpenAI; a $105B payment backstop for OpenAI's Ohio campus, SEC filing 2026-08-17). Hyperscaler capex was **11% debt-funded in FY24, 32% in FY25, 56% in H1-26** (XBRL; commercial-paper roll inflates the H1-26 figure). Meta's Hyperion campus is financed by a **$27.3B 144A bond at 6.581% (T+225), rated A+, in an unconsolidated vehicle 80% owned by Blue Owl**. CoreWeave carries **$35.6B of GPU-collateralised debt** (Q2-26 10-Q; $4.4B due rest-of-2026, $6.2B 2027); its 5-year CDS went 670bp (Nov-25) → 881 → 452 → **855bp (Jul-26)**, its 2031 notes yield 12.3%. Alphabet raised **$84.75B** of equity-like capital in June 2026. Valuations fund capex; capex is the revenue of the firms whose valuations fund it.

**The claim, downgraded to what we can show.** We do not model the transmission mechanism or a trigger level. We document the structural exposure and note that because labs are pre-profit and raise at marks, a simultaneous mark-down across the complex would tighten the funding conditions that created it — a structural fragility, not a predicted event. Agencies handle this for banks as stand-alone profile + systemic adjustment; applied here the issuer's stand-alone A-or-better carries a sector adjustment of −2 to −5 notches (asset correlation with the AI-capex factor, wrong-way funding, contagion) → **sector-linked OR-BBB+ to A**, capped at A+ while hyperscaler debt/capex > 25% and neocloud CDS > 300bp (both true today).

**Sector-unwind overlay, run through the engine** (`price_ladder_unwind.md`): hazard 6%/yr 2026–28 then 5%/yr → P(≥1 unwind in 5y) = **24%**; multiple compresses 45–65% with an 18-month half-life; demand growth halves for two years. At $2T the buyer's median IRR goes 0% → **−3%**, P(loss) 50% → **56%**, P(lose > half) 17.7% → **23%** (B− → CCC/C); fair value at 10% → $1.09T. The fund's hold-to-2031 MOIC goes 4.8× → 4.2× and its grade does not move. That is the tension in one row: **the event that takes the IPO buyer below half leaves the Series-G fund with four times its money.** Calibrated by analogy (telecom 2000–02, 2008, shale 2014–16, crypto 2022): ESTIMATE.

The Lehman comparison, stated precisely: the topology is the same — Lucent's $2.2B FY2001 customer-financing provision, Nortel's $0.9B, a loop in which one party's investment is another's revenue — but Anthropic has no debt, no maturity transformation, no margin calls. It would not have a Lehman Saturday; it would have a Lucent 2001: slower growth, multiple compression, a funding drought, and the discovery that the compute commitments are larger than the revenue can carry. Less sudden, not less deep.

## Panel H — caveats (what is judgment)

Exit-multiple level: n=12, ±1 sd band printed (Panel B). Restatement: analyst estimate, S-1 resolves. Grade mapping: analogy. KMV default point: floor until S-1. Sector-unwind hazard: analogy. Decision layer (buy at IPO vs wait for the first print vs wait for lockup): not yet built — this card rates a fixed entry, not a policy; it is the S-1-week scorecard's job. Adversarial panel: run on v1 inputs, to be re-run on v1.5r for the scorecard. No IPO-process model (delay/reprice/pull). Equity LGD is not 50%; the default-rate analogy is a communication device.

Analytical opinion, not investment advice.


## Article v3
# At $2 Trillion, Anthropic's IPO Buyer Is Flipping a Coin — and the House Is the Fund That Sold to Them

*OpenRatings rates the Anthropic IPO · Luis M. Sánchez · draft v3, computed on engine v1.5r · 2026-08-22*

> Analytical opinion, not investment advice. Toryx, which I founded, builds on Claude; Anthropic is a vendor. Every number below traces to a file in the evidence repository (appendix), and the methodology was refereed three times by an external model whose reports are published with it.

---

Anthropic is expected to list in October at roughly $2 trillion — 31 times the $65 billion revenue run-rate it reported to investors at the end of July, 22 times the run-rate our model expects it to print at listing. I built a simulation to ask a narrower question than "is it worth it": *what does a buyer at that price actually get, and who is on the other side of the trade?*

The short answer: the median buyer breaks even over five years, has a one-in-two chance of losing money and a one-in-six chance of losing more than half — impairment odds we liken, as an analogy, to a B− credit. The investors who paid $380 billion in February are marked at 4.8× on the same day and stay A-grade almost whatever happens next — not because they know something the buyer doesn't, but because they paid one-fifth the price. Their exit is the buyer's entry.

## The correction ledger

Three versions ago this piece leaned on a leaked deck and a "$360 billion Coatue entry". The model corrected the deck's numbers (the entry was $380 billion post-money; the run-rate at the time was $14 billion, so the entry multiple was ~27×, richer than the "20×" now claimed for the IPO). This version corrects itself again, in the open, because the corrections are the method:

- The exit-multiple level is now fitted to twelve comparable listings instead of written down by me. It cut every multiple by 26% and moved the median buyer from "9% a year" to "zero". The fit is one-and-a-half standard errors from my prior — not statistically distinguishable from it. I adopt it because the prior was judgment and the comps are data, and I print what happens if it is wrong (below).
- An external reviewer's "Lucent wrote off $3.7 billion of vendor financing" was wrong; Lucent's FY2001 10-K shows a $2.2 billion provision. "Odlyzko says only 2.5–5% of long-haul fibre was lit" was a misreading — his figures are link utilisations. The Loughran–Ritter "34% vs 62%" pairing is not in the paper; the paper says IPO issuers earned 5% a year for five years and an investor needed 44% more capital in them to match non-issuers. All fixed, all sourced.
- A run-rate print arrived while I was writing: $65 billion at end-July (Bloomberg, CNBC, Reuters, 17 August). It is in the model as the last print; the model's listing run-rate is a distribution around $90 billion, and I report both multiples and never average them.

## Figure 1 — the two-investor ladder

| IPO valuation | EV / model run-rate ($90B) | EV / last print ($65B) | buyer median IRR (p25–p75) | P(lose money) | P(lose > half) | P(≥40% under water in 2y) | fund MOIC at IPO → hold to 2031 |
|---|---|---|---|---|---|---|---|
| $1.0T | 11× | 15× | 15% (4–28) | 18% | 2.4% | 31% | 2.4× → 4.8× |
| $1.5T | 17× | 23× | 6% (−4–18) | 35% | 8.8% | 43% | 3.6× → 4.8× |
| **$2.0T** | **22×** | **31×** | **0% (−10–11)** | **50%** | **17.7%** | **53%** | **4.8× → 4.8×** |
| $2.5T | 28× | 38× | −4% (−14–7) | 61% | 26.7% | 60% | 6.0× → 4.8× |
| $3.0T | 33× | 46× | −8% (−17–3) | 69% | 35.4% | 66% | 7.1× → 4.8× |

Read it from the right: the fund's mark rises with the price; the buyer's odds fall with it. At every price above $1.5T there is a material probability (9% → 43%) that the buyer loses money *and* the fund makes more than three times its money on the same paths. The grade analogy — P(lose more than half) bracketed by S&P five-year cumulative default rates by notch — reads BBB− at $1T, B+ at $1.5T, **B− at $2T**, CCC at $2.5T and above. It is an analogy for readability; the probabilities are the rating.

## Figure 2 — what moves the verdict

![tornado](../figures/tornado_v15.png)

I switched every piece of the model off one at a time. Two things matter and eight do not. Taking the exit multiple back to my old prior adds $434 billion to the median fair value at a 10% required return (from $1.25 trillion to $1.68 trillion) and takes the chance of loss at $2T from 50% to 35%. Removing the gross-to-net revenue-restatement scenario adds $169 billion. Mark noise, the gross-margin cliff, revenue mix, lockup, the copula — each moves fair value by less than $6 billion. So the honest sentence is: *two-thirds of the distance between "coin flip" and "merely mediocre" is one number, and that number is anchored to twelve comparable IPOs with a standard error a fifth its size.* Move it one standard error either way and the chance of loss at $2T runs from 40% to 59%. I pre-register the fitted number and the band together.

## The machine the price sits on

The sector Anthropic lists into runs on reciprocal capital. Amazon has committed up to $25 billion to Anthropic; Anthropic has committed more than $100 billion to AWS over ten years. Google invests; Anthropic commits to a million TPUs. Microsoft invests $5 billion; Anthropic commits $30 billion to Azure. Nvidia has agreed to invest up to $100 billion in OpenAI as OpenAI buys Nvidia systems, and in August filed a payment backstop of up to $105 billion for OpenAI's Ohio campus. The hyperscalers' capex was 11% debt-funded in fiscal 2024, 32% in 2025 and 56% in the first half of 2026 (SEC filings; commercial-paper roll inflates the last figure). Meta's Hyperion campus is financed by a $27.3 billion bond at 6.58%, rated A+, in a vehicle Meta does not consolidate. CoreWeave, a single neocloud, owes $35.6 billion against its GPUs; its five-year credit-default swap has traded between 450 and 880 basis points this year and its 2031 notes yield 12%. Alphabet raised $84.75 billion of equity-like capital in June.

Valuations fund capex; capex is the revenue of the firms whose valuations fund it. I do not model the transmission mechanism and I do not know the trigger level, so I will not tell you a mark-down "is" a funding event. I will say that because the labs are pre-profit and raise at marks, a simultaneous mark-down across this complex would tighten the funding conditions that created it — a structural fragility, documented, not a forecast. In the model it appears as an optional overlay: a 6%-a-year hazard of a sector unwind (one in four over five years) in which multiples compress by half and demand growth halves for two years. It takes the $2T buyer's median return to −3% a year and the chance of losing more than half to 23%; it takes the fund's hold-to-2031 multiple from 4.8× to 4.2×. The event that puts the buyer under water leaves the fund with four times its money.

The Lehman comparison, stated precisely: the topology is the same as Lucent and Nortel in 2001 — vendor financing in which one party's investment is another's revenue — but Anthropic has no debt, no maturity transformation, no margin calls. It would not have a Lehman Saturday. It would have a Lucent 2001: slower growth, multiple compression, a funding drought, and the discovery that the compute commitments are larger than the revenue can carry. Less sudden, not less deep. Anthropic itself, on the business alone, out-earns every commitment it has disclosed — about $170 billion, perhaps $240 billion — by a wide margin; the issuer is A-grade on its own numbers. Only if it signs the trillion Dario Amodei has spoken of ("*if my revenue is not $1 trillion dollars, if it's even $800 billion, there's no force on earth, there's no hedge on earth that could stop me from going bankrupt if I buy that much compute*") does the marked value stand a coin-flip chance of falling below what it owes.

## What 26 listings say about the first six months

I pulled the daily prices of every large, hyped listing since Facebook — 26 of them, SpaceX included. Twenty-four closed below their first-day close within six months; seventeen traded below the offer price within a year; at week 26 the median listing sat 7% below its first close, the worst tenth 66% below, the best tenth 71% above. The window around the full lockup release was −11% at the median and negative 79% of the time; nine of the 26 lockups lapsed early through earnings or price triggers. I tried to predict which archetype a listing would follow from what is known before it trades — float, step-up, pricing versus range, the hotness of the year, the VIX — and the classifier does no better than chance. So Anthropic's archetype prior is the base rate: four in ten wobble flat, three in ten slide slowly, two in ten slide straight down, one in ten moonshots. SpaceX, ten weeks in, is tracking the straight slide. What will separate the paths is revealed after listing — which is why this rating is a series, not a verdict.

## What would change my mind

The S-1. Specifically: the revenue-recognition note (if Anthropic is principal, not agent, on cloud-resold revenue, the restatement branch dies and the chance of loss at $2T falls to 43%); the listing run-rate (below $72 billion, one notch down; above $112 billion, one up); the float (below 5% and the early price tells you nothing); which compute commitments are take-or-pay. After listing: two quarterly prints of metered growth under 30% annualised (the drawdown branch, 75%), gross margin under 35%, a second export-control episode, CoreWeave's CDS through 1,200 basis points or a neocloud missing a payment, two hyperscalers cutting capex guidance in the same quarter. Each is dated and will be scored the week the S-1 is public and again at lockup expiry.

The headline is the bait. The meter is the trap. And the trap is not that the business fails — it is that the price assumes a multiple the public market has never paid a decelerating consumption business, sold to you by people who paid a fifth of it.

---

### Appendix — traceability

| claim | artifact |
|---|---|
| Ladder, fair value by hurdle, KMV panel | `figures/price_ladder.md`, `figures/fair_value_by_hurdle.md`, `sim/out/valuation.json` |
| What moves the verdict | `figures/tornado_v15.png`, `figures/ablation_v15.md`, `figures/multiple_fit_loo.md` |
| Sector-unwind overlay | `figures/price_ladder_unwind.md`, `sim/config/unwind.yaml` |
| Run-rate series, commitments | `data/run_rate_series.csv`, `data/research/H/H7_7_*.csv`, `H7_6_*.csv` |
| Circular capital: capex/debt, Hyperion, CoreWeave, Alphabet | `data/research/H/H7_3_*.csv`, `H7_4_*.csv`, `H7_2_*.csv`, `H7_5_*.csv`, `H7_13_*.csv` |
| 26 listings: paths, lockups, macro | `data/research/H/H1_paths_from_bars.csv`, `H1_lockup_*.csv`, `H2_macro_at_ipo.csv`, `figures/archetypes_26.md` |
| Default-rate brackets | `docs/review_2026-08-21/04_sp_default_rates_verified.md` |
| Referee reports | `docs/review_2026-08-21/*_qwen38max.md` |
| Corrections | `docs/review_2026-08-21/H_triage.md` §3, §7 |

*Analytical opinion, not investment advice.*


## Intercept leave-one-out and comp screen
# Exit-multiple fit — comp screen and leave-one-out on the intercept (2026-08-22)

Screen (data/comps_table1.csv, W3): US-listed tech/platform IPOs 2012–2025 with a fully-diluted IPO valuation ≥ ~$5B, an NTM revenue estimate at listing, and a disclosed gross margin; growth capped at 80% in the regression. Twelve of the fourteen W3 comps qualify (CRWV and RIVN lack an NTM estimate or margin at listing). No comp was added or removed after the fit was first run.

Model: log(EV/NTM) = a + b·min(growth,0.8) + c·GM + d·committed; ridge toward the v1 prior slopes (λ=1000 by LOO). Full-sample intercept **0.898** (v1 prior 1.20; bootstrap sd 0.202).

| dropped comp | intercept | Δ vs full | multiple ratio |
|---|---|---|---|
| ABNB | 0.798 | -0.100 | 0.90× |
| SNOW | 0.829 | -0.069 | 0.93× |
| ARM | 0.852 | -0.046 | 0.96× |
| META | 0.857 | -0.041 | 0.96× |
| BABA | 0.872 | -0.026 | 0.97× |
| PLTR | 0.881 | -0.017 | 0.98× |
| FIG | 0.903 | +0.005 | 1.00× |
| KLAR | 0.909 | +0.011 | 1.01× |
| RDDT | 0.927 | +0.029 | 1.03× |
| UBER | 0.939 | +0.041 | 1.04× |
| DASH | 0.962 | +0.064 | 1.07× |
| CRCL | 1.040 | +0.142 | 1.15× |

Largest single-comp influence: dropping **CRCL** moves the intercept by +0.142 (1.15× on every multiple). Range across all twelve leave-one-outs: 0.798–1.040; none reaches the v1 prior (1.20). Comp rows: SNOW (g 0.80, GM 0.62, committed 0.07, log EV/NTM 3.50), ARM (g 0.22, GM 0.90, committed 0.40, log EV/NTM 2.83), PLTR (g 0.30, GM 0.70, committed 1.00, log EV/NTM 2.79), META (g 0.45, GM 0.85, committed 0.16, log EV/NTM 2.94), BABA (g 0.46, GM 0.72, committed 0.15, log EV/NTM 2.64), UBER (g 0.31, GM 0.75, committed 0.00, log EV/NTM 1.61), ABNB (g -0.30, GM 0.82, committed 0.00, log EV/NTM 2.24), DASH (g 0.80, GM 0.55, committed 0.00, log EV/NTM 2.03), RDDT (g 0.21, GM 0.86, committed 0.00, log EV/NTM 1.67), CRCL (g 0.50, GM 0.90, committed 1.00, log EV/NTM 1.39), FIG (g 0.40, GM 0.88, committed 1.00, log EV/NTM 2.86), KLAR (g 0.15, GM 0.50, committed 0.10, log EV/NTM 1.55).

Analytical opinion, not investment advice.


## Ablation data behind the tornado (Figure 2)
# Engine v1.5r — value decomposition by channel ($2T entry, 30k paths, seed from base.yaml)

Rows 1–10: each switches ONE v1.5r channel off (gap to row 1 = what that channel is worth; 'fitted multiple (v1 prior)' is the level channel). Then: the pairwise table for the two dominant channels (level × restatement), the intercept sensitivity (fitted 0.898 ± 1 bootstrap sd 0.194, and the v1 prior 1.20), and the all-off row (v1 frozen config). Referee: docs/review_2026-08-21/H2_v15_ablation_qwen38max.md.

| channel | fair value p50 @10% ($B) | @35% ($B) | P(loss) | P(lose>half) | P(≥40% below entry, 2y) | buyer IRR p50 | exit EV p50 ($B) |
|---|---|---|---|---|---|---|---|
| v1.5 base | 1245 | 447 | 0.50 | 0.176 | 0.53 | 0.0% | 2179 |
| - restatement | 1414 | 508 | 0.43 | 0.125 | 0.48 | 2.6% | 2475 |
| - fitted multiple (v1 prior) | 1678 | 603 | 0.35 | 0.099 | 0.43 | 6.2% | 2938 |
| - coefficient draw | 1242 | 446 | 0.50 | 0.173 | 0.53 | 0.0% | 2174 |
| - t-copula (Gaussian) | 1245 | 447 | 0.50 | 0.176 | 0.53 | 0.0% | 2179 |
| - GM cliff | 1251 | 449 | 0.50 | 0.174 | 0.53 | 0.1% | 2189 |
| - lockup shock | 1245 | 447 | 0.50 | 0.176 | 0.43 | 0.0% | 2179 |
| - price convergence (scale-free) | 1245 | 447 | 0.50 | 0.176 | 0.53 | 0.0% | 2179 |
| - mix update (CC 10%) | 1248 | 448 | 0.50 | 0.179 | 0.53 | 0.1% | 2185 |
| - calibrated mark noise (v1 0.18) | 1239 | 445 | 0.50 | 0.151 | 0.45 | -0.0% | 2169 |
| pairwise: v1 prior + no restatement | 1918 | 689 | 0.29 | 0.065 | 0.39 | 9.1% | 3357 |
| pairwise: v1 prior + restatement | 1678 | 603 | 0.35 | 0.099 | 0.43 | 6.2% | 2938 |
| pairwise: fitted + no restatement | 1414 | 508 | 0.43 | 0.125 | 0.48 | 2.6% | 2475 |
| sensitivity: intercept −1 sd (0.704) | 1040 | 374 | 0.59 | 0.232 | 0.59 | -3.5% | 1821 |
| sensitivity: intercept +1 sd (1.092) | 1499 | 538 | 0.40 | 0.123 | 0.46 | 3.8% | 2623 |
| sensitivity: intercept = v1 prior 1.20 (1.200) | 1668 | 599 | 0.35 | 0.100 | 0.43 | 6.1% | 2921 |
| all off: v1 frozen config | 1935 | 695 | 0.24 | 0.036 | 0.35 | 9.3% | 3387 |

Interaction term on P(loss), level × restatement = +0.002 (Qwen H2 §3: disclose if > 0.02).

Analytical opinion, not investment advice.


## Questions (numbers first, then reasons)
1. New overall rating 1–10 and the six sub-ratings (engine/calibration; rating mapping & KMV; circular-capital framing; archetype evidence; evidence & sourcing; disclosure).
2. The exact remaining gaps to 9, ranked by points recovered per hour of work. Mark each CUT / ADD / REWORD.
3. Anything in card v3 or article v3 you would not let us print as written — quote it and rewrite it.
4. Is the headline now internally consistent with every table? Check the 22×/31×, the 4.8×, the 0.50/0.177, the $1.25T (p25–p75), the B−, the "one-fifth the price" ($380B vs $2T = 0.19).
5. The KMV marked column now says $1T → 49.9% breach (D-range) while stripped says 1.9% (BBB−). Is printing both honest and clear, or confusing? How should the $1T row be worded?
6. Panel F trigger on CoreWeave CDS: we moved it from 400bp to 1,200bp because it is already ~855bp. Defensible? Better trigger?
7. Would you pre-register this today as is? If not, the single blocking item.
