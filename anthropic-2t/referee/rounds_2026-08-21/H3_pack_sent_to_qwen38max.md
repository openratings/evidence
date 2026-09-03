# TASK H3 — Overall soundness rating before pre-registration (2026-08-22)

You refereed this project in Tasks A–H2 (methodology v3, rating card, SAGA-template article skeleton, path-archetype spec, circular-capital figure, engine v1.5 ablation). Since H2 we did what you asked: adopted engine v1.5r (Gaussian copula, staged lockup shocks −6%/0.20 q1 and −10%/0.30 q2 from our 26-listing measurement, arr log_sd 0.20), ran the pairwise/all-off/intercept-sensitivity ablation, ran the 26-listing archetype clustering and the features-only classifier (it is at chance; we say so), and pulled the EDGAR/literature/lockup/market data (below). The article and the rating card have NOT yet been rewritten on v1.5r.

## The headline as it will be published (plain English)
At $2 trillion, Anthropic's IPO buyer is flipping a coin — and the house is the fund that sold to them. Listing ~Oct-2026 at ~$2T, ~31× the $65B July run-rate. 100k-path simulation, 5 years: median IRR ≈0, P(loss) 0.50, P(lose>half) 0.17 (impairment odds like a B− bond), fair value at 10% required return ≈$1.25T. The $380B Feb-2026 investors: 4.8× mark at listing, A-grade whatever happens — their exit is the buyer's entry. Risk framed as circular capital (Amazon/Google/Microsoft fund Anthropic; Anthropic commits >$170B back; hyperscalers now borrow for 56% of capex; a mark-down is a funding event). Caveat printed in full: ~two-thirds of the gap vs a mediocre verdict rests on one calibrated number — the exit-multiple level — and the data behind it (12 comps) is too thin to be certain; if the v1 prior is right, P(loss) ≈ one in three.

## Headline table (v1.5r, 100k)
| metric | value |
|---|---|
| P(IRR ≥ 35% from $2T entry, 5y) | 0.030 |
| P(−40% within 8q \| metered growth <30% two consecutive q) | 0.749 (trigger prob 0.133; unconditional 0.529) |
| $380B entry percentile on fair-value curve (35% hurdle / 20% hurdle) | 0.530 / 0.207 |
| median IRR / MOIC / exit EV ($B) | 0.001 / 1.00 / 2180 |
| P(MOIC < 1) | 0.499 |

seed=20261016 config=34ba266080c76f8c n=100000

Analytical opinion, not investment advice.

## Price ladder (v1.5r)
# Two-investor price ladder — engine v1.5 base

| IPO valuation | EV/run-rate | buyer IRR p50 (p25–p75) | P(lose money) | P(lose > half) | P(≥40% below IPO price, 2y) | P(≥40% off peak, 2y) | grade | fund MOIC at IPO | at lockup p50 | hold-to-2031 p50 | fund grade | P(buyer loses & fund >3×) |
|---|---|---|---|---|---|---|---|---|---|---|---|---|
| $1.00T | 12× | 15% (4–28) | 18% | 2.4% | 31% | 78% | **OR-BBB-** | 2.4× | 2.9× | 4.8× | OR-A or better | 0% |
| $1.25T | 15× | 10% (-1–22) | 27% | 5.2% | 38% | 81% | **OR-BB-** | 3.0× | 3.4× | 4.8× | OR-A or better | 0% |
| $1.50T | 19× | 6% (-4–18) | 35% | 8.8% | 43% | 84% | **OR-B+** | 3.6× | 3.9× | 4.8× | OR-A or better | 9% |
| $1.75T | 22× | 3% (-7–15) | 43% | 13.2% | 48% | 86% | **OR-B** | 4.2× | 4.3× | 4.8× | OR-A or better | 16% |
| $2.00T | 25× | 0% (-10–11) | 50% | 17.7% | 53% | 87% | **OR-B-** | 4.8× | 4.7× | 4.8× | OR-A or better | 23% |
| $2.50T | 31× | -4% (-14–7) | 61% | 26.7% | 60% | 90% | **OR-CCC/C** | 6.0× | 5.5× | 4.8× | OR-A or better | 34% |
| $3.00T | 37× | -8% (-17–3) | 69% | 35.4% | 66% | 92% | **OR-CCC/C** | 7.1× | 6.3× | 4.8× | OR-A or better | 43% |

Analytical opinion, not investment advice.

## Ablation (v1.5r, 30k) incl. pairwise, intercept ±1sd, all-off
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

## Archetypes result
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

## Data pulls completed since H2 (triage §7)
 Follow-up pulls (2026-08-21/22) — what closed, what changed

Four agents + FRED. Files: `H_followup_edgar.md`, `H_followup_literature.md`, `H_followup_lockups.md`, `H_followup_market.md`; CSVs `data/research/H/H7_*.csv`, `H8_*.csv`, `H1_lockup_*.csv`, `H2_macro_at_ipo.csv`.

### Closed with primary sources
| Item | Result | Lands in |
|---|---|---|
| H7-2 CoreWeave debt | **$35,551M principal at 2026-06-30** (Q2-26 10-Q), by tranche; DDTL 4.0 non-recourse SOFR+225 rated A3 = first IG GPU-backed loan; ~$10B notes at 9–9.75% ≈ par in filing FV; wall $4.4B/6.2B/4.4B (26/27/28). Nebius $10B converts + $5B (8/19). | Fig 4 fallback; card Panel G |
| H7-3 Hyperscaler capex/debt | XBRL quarterly FY22–Q2-26. **Aggregate debt/capex 11% FY24 → 32% FY25 → 56% H1-26** (Alphabet 26→71→70, Amazon 6→19→84, Meta 28→43→51, Microsoft ~0). Q2-26 capex: GOOGL $44.9B (37.5% rev), MSFT $35.8B (39.8%), AMZN $54.2B (27%), META $30.1B (49.5%). | Fig 3 caption ("9%→32%" → "11% FY24 → 32% FY25 → 56% H1-26", with CP-roll caveat); Fig 1/2 |
| H7-5 Alphabet raise | **Confirmed $84.75B** (8-K 6/4–6/5/26; 424B5): $18B common + $16.75B 6.25% mandatory convertible pref + $10B Berkshire + $40B ATM (~$30B employee-equity tax); ≈$90B w/ greenshoes; AI capex/GCP. | Fig 3 caption |
| H7-4 Hyperion | Beignet Investor LLC $27.3B 144A sr secured amortising, **6.581% / T+225, 2049, S&P A+**, Blue Owl 80/Meta 20, **unconsolidated VIE** (max exposure ~$46B), 16-yr RVG, DSCR 1.12×; El Paso $12.5B T+287.5. | Fig 3 caption ("SPV" now has terms) |
| H7-13 Neocloud spreads | Point-in-time only: CRWV 5y CDS 670 (Nov-25) → 881 (Dec) → 452 (Jun-26) → **855bp (2026-07-29)**; 9.75% '31 at 89.6 / 12.3% YTW (8/21); DDTL margins +400 → +225 → +450 → +550/OID97; ORCL CDS 105→215. | **Fig 4 = CDS/yield path**, not GPU basis (too thin pre-Jul-25) |
| H7-7 Run-rate | $65B end-July: Bloomberg 8/17 first, CNBC ("told investors"), Reuters; Q2 rev >$11.5B; FT: $100–120B 2026 exit; Reuters: bankers vs $190–200B 2028. Series updated (`run_rate_series.csv`: 2026-03 $19B, 2026-07 $65B). | Engine `arr_usd_b` (median 90 at listing — keep, quote both); card EV/run-rate col |
| H7-6 Commitments | AWS >$100B/10y, Azure $30B, Fluidstack $50B, **TeraWulf ~$19B, Hut 8 ~$7B**; Google "tens of billions" — no $40B primary. | KMV default point: decide what counts; $170B is a floor |
| H7-12 Ramp | Paid-AI adoption 7.5% (Jan-23) → 55.7% (Jul-26); Anthropic share of Ramp AI spend **4.6% → 43.5%** (Jul-26) vs OpenAI 39.7%; "4×" = monthly spend Feb-25→Feb-26. | Demand driver evidence; article §3 |
| H7-14 CoWoS | TSMC transcripts only ("double" 24/25; Jul-26 "limits my customers' growth"); secondary wpm 35–40k → 70–80k → 120–140k. | Capacity-cycle regime priors |
| H7-10 Pipeline | OpenAI S-1 confidential 6/8 but leaning 2027; others not 2026 → **low concurrent mega-IPO supply** for an Oct listing. | H2 feature for Anthropic |
| H1 lockups (26/26) | Float: SPCX 4.9%, HOOD 7, CART 8, CRWV 8.4, FIG 8.7, ARM/ABNB 9.3 …; **9/26 lockups lapsed <180d** (earnings/price triggers); down-round IPOs CART 0.25×, RDDT 0.64×, PLTR 0.81×, ARM 0.85×, CRCL 0.90×. From bars: **full-release ±10d window median −11%, 79% negative (n=24)**; first release −6%, 69% negative. | Archetype features; v3 lockup shock (5–15%) now self-calibrated at the top |
| H2 macro | VIX, 10y, Nasdaq 3m/6m at each IPO date (FRED). | Archetype features |
| H8-5 Lucent | FY2001 10-K405: provision for uncollectibles & customer financings **$2,249M** (FY00 $505M); commitments $5.3B, drawn $3.0B. Nortel FY01 provisions $887M on $1.35B drawn. **"$3.7B" is wrong.** | Article/F §3: use $2.2B |
| H8-6 Railway mania | Odlyzko: 1847 capex £44m = **7.3% of GDP**; miles sanctioned 1845 2,700 / 1846 4,538; index Jul-1845 167.9 → Oct-1849 60.5 (−64%). Campbell & Turner: 1,984 (8 Aug 1845) → 673 (19 Apr 1850) = −66%. | Article history box |
| H8-7 SPACs | Klausner–Ohlrogge–Ruan Yale J.Reg 39(1) 2022: median net cash/share $5.70, dilution 50.4%, 3-mo median −14.5%. Gahng–Ritter–Zhang RFS 2023: 2021 Q1–Q3 de-SPACs −62.1%. **Ritter Table 15c: 2021 mergers 1-yr −64.2%, 3-yr −73.0%** (EW means). **No SEC DERA SPAC staff report exists.** | Article base-rate box (replaces the ESTIMATE) |
| H8-8 Enron/Lehman/AAA | Enron S&P BBB+ → BBB → BBB− → **B− 2001-11-28** (not a one-step cut), Ch.11 12-02; Lehman A2/A/A+ (424B2 7/31/08), Moody's review 9/10, filing 9/15. FCIC: **83% of 2006 Aaa MBS tranches downgraded**; 76%/89% of 2006/07 IG tranches to junk; >80% of Aaa CDO to junk. | Card Panel G "Lehman" line; article §5 |
| H8-1/H3 Ritter | 2025 29.3% / 2024 15.3% / 1980–2025 19.0% confirmed (7 Jul 2026 vintage); 3-yr BHR 2020 cohort −48.1% (mkt-adj −78.6%), 2021 −49.1% (−68.6%); size tables by sales not proceeds (≥$1bn sales mkt-adj −2.1%). Field & Hanka: −1.5% 3-day AR, +40% volume. Renaissance IPO index 2019 +34.8 / 2020 +109.6 / 2021 −11.4 / **2022 −57.0** / 2023 +51.6 / 2024 +16.4 / 2025 +4.5 / 2026 YTD ~+0.7 (8/21). | Base-rate box |
| H8-13 | Minsky WP 74 May 1992 ✓; Kindleberger–Aliber–McCauley 8th ed. 2023; Perez: Project Syndicate 2024-03-11 "key development within the still-unfolding ICT revolution" — no bubble call. | Citations |

### Corrections to our own text (cumulative)
1. Lucent write-off: $2.2B provision, not $3.7B.
2. Fibre "lit" share: Odlyzko's 3–5%/~10% are *link utilisations*, not lit share — reword or drop.
3. Loughran–Ritter "34 vs 62": not in the paper; use 5%/yr + 44%.
4. Debt-funded capex: 11% → 32% → 56% (FY24/25/H1-26), sourced.
5. Enron was not cut from BBB+ to junk in one step.
6. SPAC 12-m "−60 to −75" → cite Ritter 15c −64.2% (2021 mergers, 1-yr EW mean).
7. Run-rate: last print $65B (Jul-26), not $47B.

### Still unavailable after two passes
Weekly neocloud spread series; CoreWeave new-issue spreads; Odlyzko/TeleGeography lit-fibre share; Klausner 6/12-m medians; oversubscription for 22/26 and retail allocation for all 26; SDLLMTK (not public); monthly CoWoS; Google's $40B primary; any run-rate print newer than end-July.

## Your own H2 required-actions list (for reference)
## Summary of Required Actions Before Pre-Registration

| Priority | Action | Deadline |
|---|---|---|
| **P0** | Add the intercept-sensitivity disclosure sentence to the pre-registration and article | Before filing |
| **P0** | Run the pairwise ablation {fitted multiple × restatement} and the all-off row | Before filing |
| **P0** | Quarantine the t-copula (switch to Gaussian) or justify ν=4 with a calibration | Before filing |
| **P1** | Recalibrate lockup sd from 13% to ~30% using the 26-listing data | Before filing |
| **P1** | Widen run-rate log-sd from 0.15 to 0.20 | Before filing |
| **P1** | Update the seven text corrections + the additional items in Q9 | Before filing |
| **P2** | Fit the archetype classifier (LOO, ridge, 9 features, n=25 training + SPCX test) | Before article publication |
| **P2** | Build Fig 4 as a discrete-observation timeline, not a continuous series | Before article publication |
| **P3** | Resolve Fluidstack/TeraWulf contract terms for KMV default point | After S-1 |
| **P3** | Resolve gross-vs-net revenue recognition from S-1 footnote | After S-1 |

## Questions — answer numerically and bluntly
1. Rate the analysis 1–10 on **soundness for a public, pre-registered, dated rating** (10 = you would put your name on it; 5 = publishable with the caveats as written; <4 = do not publish). Give the rating first, then the three things that cost the most points.
2. Rate separately (1–10): (a) the engine and its calibration; (b) the rating mapping (P(lose>half) → S&P notch) and the KMV issuer grade; (c) the circular-capital / Lehman framing; (d) the path-archetype evidence; (e) the evidence base and sourcing discipline; (f) the disclosure of judgment vs data.
3. What analysis is still MISSING that a hostile, competent reader (a Bloomberg reporter with a quant, an Anthropic IR person, a sell-side analyst) would hit first? List the top five attacks and, for each, the cheapest defensible response (data we hold, a sensitivity to run, or a sentence to add).
4. Is there anything in the headline above that you would not let us print as written? Rewrite the sentence if so.
5. Is there a cheaper or better way to get the same credibility — e.g. fewer channels, one clean sensitivity chart instead of the ablation table, a different headline metric than P(loss)?
6. Give the one thing we should do next, and the one thing we should stop doing.
