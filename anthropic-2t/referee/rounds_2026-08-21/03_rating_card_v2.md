# OpenRatings Impairment Grades for the Anthropic IPO — card v2 (2026-08-21)

*Draft for openratings.ai, grades re-mapped 2026-08-21 to the verified S&P table. Engine v1 (seed 20261016, 100k paths, 5-year horizon). Analytical opinion; not a credit rating; not investment advice. Cells marked ⟲ must be re-run after the three MUST fixes (exit-multiple regression on comps, gross→net revenue restatement, entry-price→multiple link). Every identified bias pushes grades DOWN, none up.*

**One line.** Anthropic the company is OR-A-or-better (top of the scale; AAA through A− are indistinguishable at five years) against the ~$170B of compute it has actually signed for, and OR-B if it signs the trillion. Anthropic the stock at a $2T IPO is OR-BB — junk-grade impairment odds for a median 9% a year — and OR-B− if the sector unwinds. The Series-G fund's exit is the IPO buyer's entry.

## Panel A — the two-investor ladder

*Series-G fund = Coatue/GIC round, $380B post-money, 2026-02-12. The fund cannot sell at the IPO (≈180-day lockup); "MOIC at IPO" is the mark, "at lockup" is the earliest realisable exit. The fund's gain is the buyer's cost basis.*

| IPO valuation | EV / run-rate (@$90B) | **IPO BUYER** median IRR (p25–p75) | P(lose money) | P(lose > half) | P(≥40% under water, yrs 1–2) ⟲ | **OR grade** | sector-unwind stress: P(lose>half) → grade ⟲ | **FUND** MOIC at IPO (mark) | MOIC at lockup, ~14 mo (−5% placeholder) ⟲ | hold to 2031: MOIC / IRR | P(buyer loses money AND fund > 3×) |
|---|---|---|---|---|---|---|---|---|---|---|---|
| $0.75T | 8× | 33% (22–45) | 1% | 0.0% | 36% | OR-A or better | 1.4% → OR-BBB− | 1.8× | 1.7× | 7.5× / 42% | — |
| $1.00T | 11× | 25% (15–37) | 4% | 0.2% | 36% | OR-A or better | 3.3% → OR-BB | 2.4× | 2.3× | 7.5× / 42% | — |
| $1.25T | 14× | 20% (10–31) | 7% | 0.5% | 36% | OR-BBB+ | 5.8% → OR-BB− | 3.0× | 2.8× | 7.5× / 42% | 7% |
| $1.50T | 17× | 16% (6–26) | 12% | 1.2% | 36% | OR-BBB− | 8.6% → OR-B+ | 3.6× | 3.4× | 7.5× / 42% | 12% |
| $1.75T | 19× | 12% (3–22) | 18% | 2.2% | 36% | OR-BBB− | 11.6% → OR-B+ | 4.2× | 4.0× | 7.5× / 42% | 18% |
| **$2.00T** | **22×** | **9% (0–19)** | **24%** | **3.6%** | **36%** | **OR-BB** | **14.9% → OR-B−** | **4.8×** | **4.5×** | **7.5× / 42%** | **24%** |
| $2.50T | 28× | 4% (−4–14) | 36% | 7.3% | 36% | OR-BB− | 21.3% → OR-B− | 6.0× | 5.7× | 7.5× / 42% | 36% |
| $3.00T | 33× | 1% (−7–10) | 48% | 12.3% | 36% | OR-B+ | 27.8% → OR-CCC/C | 7.1× | 6.8× | 7.5× / 42% | 48% |

Fund note: at every price tested the fund's 5-year P(lose > half) is < 0.1% — OR-A or better (top of the scale). That is the $380B entry, not the absence of risk; the fund's risks are lockup, concentration and LP terms, which an impairment grade does not measure. Its top grade assumes a liquid exit — exactly what disappears in a sector unwind; see Panel G. Its sub-year annualised IRR is deliberately not printed (4.8× in ~8 months annualises to ~830%, which overstates a rate of return). Dilution: buyer 0.92 over 5y; fund 0.905 to IPO, 0.84 to 2031.

Grades: P(lose > half in 5 years) bracketed by 5-year cumulative corporate default rates by notch (equity analogue of default with ~50% recovery). **Brackets verified against S&P Global Ratings, 2024 Annual Global Corporate Default And Rating Transition Study, Table 26 (1981–2024, published 2025-03-27; see `04_sp_default_rates_verified.md`):** the top six notches are non-monotone and statistically indistinguishable at 5 years (AAA 0.34, AA+ 0.13, AA 0.33, AA− 0.27, A+ 0.35, A 0.39, A− 0.42%), so anything ≤0.42% is reported as **OR-A or better**; then BBB+ ≤0.79 · BBB ≤1.09 · BBB− ≤2.40 · BB+ ≤2.90 · BB ≤5.05 · BB− ≤8.28 · B+ ≤12.88 · B ≤14.69 · B− ≤22.03 · CCC/C ≤46.53 (%). Qwen's reconstructed table was wrong at several notches; the corrected grades are in the ladder above.

## Panel B — issuer commitment-coverage grade (KMV-style)

Default point D = debt-like take-or-pay compute commitments; KMV convention = due within 12 months + ½ of the rest. Disclosed: >$100B AWS/10y, ~$40B Google TPU, ~$30B Azure ≈ $170B nominal, ~$24B/yr → D ≈ $132B; $170B = all accelerated. Breach = fundamental value below D at any quarter within 5 years, counted over 100k paths. Two volatility bases: **marked** (engine value incl. multiple noise, 64%/yr) and **stripped** (revenue × gross margin at a steady capitalisation, 17%/yr).

| default point D | 5-yr breach, marked | grade | 5-yr breach, stripped | grade |
|---|---|---|---|---|
| **$132B — disclosed, KMV convention** | **0.00%** | **OR-A or better** | **0.00%** | **OR-A or better** |
| $170B — disclosed, accelerated | 0.00% | OR-A or better | 0.00% | OR-A or better |
| $250B | 0.00% | OR-A or better | 0.00% | OR-A or better |
| $500B | 0.76% | OR-BBB+ | 0.00% | OR-A or better |
| $625B | 2.4% | OR-BBB− | 0.00% | OR-A or better |
| $825B | 7.5% | OR-BB− | 0.00% | OR-A or better |
| **$1,000B — Amodei's "$1T of compute"** | **14.5%** | **OR-B** | **0.00%** | **OR-A or better** |
| $1,250B | 26.7% | OR-CCC/C | 0.00% | OR-A or better |
| $1,500B | 39.4% | OR-CCC/C | 0.00% | OR-A or better |

Reading: on the business alone (stripped), Anthropic out-earns any plausible commitment — gross profit median $75B in year 1 → $171B in year 5 — so breach never happens below a $1.25T default point. **Every breach in the marked column is a mark-to-market event: the value falls because the multiple falls, not because the business stops paying.** That is exactly the channel that matters in a circular-capital sector (Panel G): when marks are the funding, a mark event is a funding event. Coverage lens: against $100B/yr of commitments, gross profit is short in 86% of paths in year 1 (funded from the IPO raise) and 14% by year 5; against $200B/yr, 63% still short in year 5.

Downgrade schedule (marked, verified brackets): A-or-better up to ~$450B · BBB+ ~$500B · BBB− ~$625B · BB− ~$750–825B · B ~$1,000B · CCC/C from ~$1,200B — roughly one notch per $100B of new take-or-pay. Closed-form Merton is not used: with σ = 64% it gives DD ≈ 1 and ~16% at D = $170B, contradicted by the path count (0%) and by the fact that value would have to fall 92% — the process is mean-reverting and the 64% is mark noise, not business risk.

## Panel C — the ride (any entry price) ⟲
P(≥40% below the IPO price at some point in years 1–2) 36% · P(≥40% fall from a peak) 76% · median worst drawdown −27% (p25 −49%, p75 −1%) · price-path vol 62%/yr · if growth prints <30% annualised two quarters running (13% chance): P(≥40% drawdown) 63%. *Engine v1 is scale-free here (same at $1T and $3T — wrong; MUST fix).*

## Panel D — what should I pay? ⟲
Require 8%/yr → median fair value $2.1T (54% of futures make $2T cheap) · 10% → $1.9T (48%) · 12% → $1.8T (42%) · 15% → $1.5T (34%) · 20% → $1.2T (23%) · 35% → $0.7T (4%).

## Panel E — pre-registered downgrade triggers
| trigger | effect |
|---|---|
| two consecutive quarterly prints of metered growth < 30% annualised | 63% drawdown branch; buyer grade −1 to −2 notches |
| S-1 restates cloud-reseller revenue gross → net (20–40% ARR haircut) | every buyer row −1 to −2 notches ⟲ not yet modelled |
| gross margin prints < 35% | ~−1 notch ⟲ not yet modelled |
| second export-control episode within 12 months of listing | −1 notch, buyer and issuer |
| new take-or-pay commitment > $100B | issuer −1 notch per $100B |
| CoreWeave 5y CDS > 400bp, or two neoclouds miss debt service within 90 days | sector-linked grade −1 notch |
| two of MSFT/GOOGL/AMZN/META cut capex guidance >15% in the same quarter | sector-linked grade −1 notch |
| Silicon Data token-spend index (SDLLMTK) −35% from peak AND open-weight gap < 5 ECI points two months running | sector-linked grade −1 notch |
| two consecutive frontier releases < 5% gain on enterprise benchmarks AND Ramp AI adoption growth < 10% QoQ | capability-plateau flag, −1 notch |

## Panel F — caveats
Exit multiple is a written-down prior (MUST: regress on comps) · no gross→net scenario (MUST) · drawdown scale-free in v1 (MUST) · Gaussian correlations, no tail dependence · lockup supply shock is a −5% placeholder · no IPO-process model (delay/reprice/pull) · default-rate brackets reconstructed, verify · dilution factors fixed inputs · the default-rate analogy is a communication device, not a structural equivalence; equity LGD is not 50%.


## Panel G — sector-linked grade: the circular-capital risk (the "Lehman" term)

Anthropic has no debt. The sector it sits in runs on circular capital: Amazon invests up to $25B in Anthropic, Anthropic commits >$100B to AWS; Google invests up to $40B, Anthropic commits to 1M TPUs; Nvidia invests in and backstops the neoclouds that buy its GPUs; hyperscaler capex went from 9% debt-funded (FY24) to 32% (mid-2026); Meta's Hyperion SPV is ~90% debt; CoreWeave carries ~$35B of GPU-collateralised debt; MS/JPM put the sector's new-debt need at ~$1.5T; Alphabet raised $85B of equity in June 2026. Valuations fund capex, capex is the revenue of the firms whose valuations fund it. A single-name KMV grade is blind to five channels: asset correlation with the AI-capex factor; wrong-way risk (investors = suppliers = customers' infrastructure); funding that depends on Anthropic's own marks (it is pre-profit and raises equity at marks); a growth ceiling set by whether counterparties can finance capacity; and demand contagion (one enterprise AI budget funds everyone). Panel B shows the mechanism: every breach in the marked column is a mark event, and in a circular structure a mark event is a funding event.

Agencies handle this for banks as stand-alone profile + systemic adjustment, and for sectors with a cap. Applied here:

| | stand-alone (KMV, disclosed $170B) | sector adjustment | **sector-linked** | under unwind ρ=0.45, 2.5σ | under unwind ρ=0.60, 3σ |
|---|---|---|---|---|---|
| issuer | OR-A or better (AAA…A− not resolvable at 5y) | −3 notches (range −2 to −5): correlation 1, wrong-way 1, funding + ceiling + contagion 1 | **OR-BBB+ to A** | OR-BBB+ to A | OR-BBB− to BB+ |
| sector cap | — | sector itself ≈ BBB on its funding structure → Anthropic ≤ A+ while hyperscaler debt/capex > 25% and neocloud CDS > 300bp | | | |

Sector-unwind event (engine overlay spec, E2 §3d): hazard ~6%/yr in the build phase 2026–28, 3–5%/yr after → 27% chance of at least one in 5 years; severity 55–75% value loss for Anthropic; persistence 2–3 years; joint hit to demand (−30–50%), compute-capacity growth (−40–60%), exit multiple (22× → 8–12×), and equity issuance (closed 12–24 months). Calibrated by analogy — telecom/fibre 2000–02 (Lucent/Nortel vendor financing; closest topology), 2008, shale 2014–16, crypto 2022 (FTX/Alameda loop), SaaS 2022 — none a direct analogue; ESTIMATE. ⟲ The overlay has not been run through the engine.

What the overlay does to the two investors (crude version: 27% × uniform 55–75% hit on exit value; the proper number is the engine run):

| IPO valuation | buyer P(lose>½) base → with sector-unwind overlay | grade base → stressed | buyer median IRR stressed | fund P(lose>½) stressed / median MOIC |
|---|---|---|---|---|
| $1.00T | 0.2% → 3.3% | OR-A → **OR-BB** | 20% (was 25%) | 0.17% / 5.9× |
| $1.25T | 0.5% → 5.8% | OR-BBB+ → **OR-BB-** | 14% (was 20%) | 0.17% / 5.9× |
| $1.50T | 1.2% → 8.6% | OR-BBB → **OR-B+** | 10% (was 16%) | 0.17% / 5.9× |
| $1.75T | 2.2% → 11.6% | OR-BB+ → **OR-B** | 7% (was 12%) | 0.17% / 5.9× |
| $2.00T | 3.6% → 14.9% | OR-BB → **OR-B** | 4% (was 9%) | 0.17% / 5.9× |
| $2.50T | 7.3% → 21.3% | OR-BB- → **OR-CCC** | -0% (was 4%) | 0.17% / 5.9× |
| $3.00T | 12.3% → 27.8% | OR-B → **OR-CCC** | -4% (was 1%) | 0.17% / 5.9× |

(overlay: P(≥1 unwind in 5y)=27%, value loss 55–75% uniform, applied to exit value; crude — the proper run is the engine overlay in E2 §3d)

**Reading.** The unwind takes the $2T buyer from OR-BB to OR-B and the median return from 9% to 4% a year; $2.5T and above go to CCC. The fund stays at the top impairment grade — a 65% haircut on a 7.5× is still 2.6× — but its AAA assumes it can sell, and exit liquidity is the first thing a contagion removes; sector-linked it drops with the issuer. That is the whole tension in one row: **the same event that wipes the IPO buyer's equity below half leaves the Series-G fund with a multiple of its money.**

The Lehman comparison, stated precisely: the topology is the same (Lucent 2001, FTX 2022 — a loop in which one party's investment is another's revenue), but Anthropic has no debt, no maturity transformation, no deposits, no margin calls. It would not have a Lehman Saturday; it would have a Lucent 2001 — a slow bleed of growth, multiple compression, a funding drought, and the discovery that the compute commitments are larger than the revenue can carry. Less sudden, not less deep. The leverage is in the sector, not on Anthropic's balance sheet — which is why it does not show up in a single-name KMV, and why this panel exists.

Early-warning indicators already in our SGX series: GPU spot and forward backwardation, token prices, provider list prices, positioning; to add: CoreWeave/neocloud CDS and bond spreads, hyperscaler debt issuance and capex guidance, SPV terms, TSMC/CoWoS lead times, Silicon Data token-spend index. Triggers are in Panel E.

Caveats: the hazard, severity, ρ and notch count are structural judgments with ranges, not estimates; the highest-priority engine change is the *joint* hit (the AR(1) mark noise treats a sector shock as mean-reverting noise; in an unwind it is a regime), which is why ⟲ marks every number here.

## Vocabulary and disclaimer
"OpenRatings impairment grade" (buyer), "commitment-coverage grade" (issuer), "simulated breach frequency" — never "credit rating", never "EDF" unqualified; every grade prefixed OR-.

OpenRatings is not a Nationally Recognized Statistical Rating Organization and is not registered with the SEC or any regulator. The grades and probabilities here are analytical opinions produced by a simulation model. They are not credit ratings, must not be used as a substitute for credit ratings in any regulatory, contractual or investment context, and are not investment advice or a recommendation. The model relies on assumptions that may prove materially wrong. Past default-rate statistics may not predict impairment for a company with no public-market history. OpenRatings accepts no liability for any loss arising from reliance on this material.

