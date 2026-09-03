# OpenRatings Impairment Grades for the Anthropic IPO — card v3 (2026-08-22, engine v1.5r)

*Draft for openratings.ai. Engine v1.5r (seed 20261016, 100k paths, 5-year horizon, Coatue gate passed, 13 tests green). Referee trail: Qwen 3.8 Max Tasks A–H3 (`docs/review_2026-08-21/`). Analytical opinion; not a credit rating; not investment advice. Every identified bias pushes grades DOWN, none up.*

**One line.** At a $2 trillion listing the IPO buyer's median return is zero, the chance of losing money is one in two and the chance of losing more than half is one in six — impairment odds we liken to a B− credit. The fund that entered at $380B in February is marked at 4.8× on the same day (dilution-adjusted, ×0.905; raw $2T/$380B = 5.3×) and is A-grade almost whatever happens next — not because it knows more, but because it paid roughly a fifth of the price. Two-thirds of the gap between this verdict and a merely mediocre one rests on one number — the exit-multiple level, fitted to twelve comparable IPOs with a standard error a fifth its size (±1σ band in Panel B) — and we show what happens if it is wrong.

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
| **$1,000B — Amodei's "$1T of compute"** *(marked: D-range because the multiple can fall below 1× the commitment; stripped: BBB− because the business out-earns it — the disagreement between the columns is the point)* | **49.9%** | **D-range (>46.5%)** | **1.9%** | **BBB−** |
| $1,250B | 65.5% | D-range | 7.6% | BB− |

Reading: on the business alone Anthropic out-earns any commitment it has disclosed; **every breach in the marked column is a mark-to-market event** — the value falls because the multiple falls, not because the business stops paying. That is the circular-capital channel (Panel G). Coverage lens: against $100B/yr of commitments, gross profit is short in most paths in year 1 (funded from the IPO raise) and in a minority by year 5. Closed-form Merton is not used (mark noise is not business risk). Change vs v2: the marked ladder is roughly one notch harsher at every D ≥ $500B because v1.5r values are lower (level) and noisier (calibrated marks); the stripped ladder is unchanged.

## Panel D — the ride, any entry

At $2T: P(≥40% below the IPO price at some point in years 1–2) **53%**; P(≥40% fall from a peak) **87%**; if metered growth prints <30% annualised two quarters running (13% chance): P(≥40% drawdown) **75%**. Price path: IPO price converging to the model mark (half-life 4q) with staged lockup shocks — first release q1 (−6%, sd 0.20), full release q2 (−10%, sd 0.30) — from our own 26-listing measurement (full-release ±10-day window median −11%, 79% negative, n=24; first release −6%, 69%). Path archetypes (26 listings, `07_path_archetypes_26.md`): 24/26 closed below first close within six months; week-26 median −7% vs first close (p10 −66%, p90 +71%); the pre-listing hype features we can measure do not separate the paths (classifier at chance), so the archetype prior is the base rate — wobble 40% / slow slide 28% / straight slide 20% / moonshot 12%. With 26 listings and four archetypes the test has low power (<30% to detect a medium effect); the base-rate prior is a conservative default, not a proof of unpredictability.

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
| CoreWeave 5y CDS > 1,200bp (≈855bp at pre-registration), or any GPU-collateralised borrower with > $5B of debt (CoreWeave, Nebius, Lambda, Crusoe, Applied Digital, IREN) misses a debt-service payment | sector-linked grade −1 notch |
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
