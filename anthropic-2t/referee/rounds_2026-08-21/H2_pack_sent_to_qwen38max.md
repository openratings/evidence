# TASK H2 — Referee: engine v1.5 as the new base, channel ablation, and the Prompt-H data return (2026-08-22)

Context you already refereed (Tasks A–G): METHODOLOGY v3, rating card v2 (grades mapped to S&P Table 26), the SAGA-template article skeleton (5 figures), the path-archetype method spec, the circular-capital figure. This task: (1) is engine v1.5 the right base for pre-registration; (2) is the attribution in the ablation credible and how should it be disclosed; (3) what the Prompt-H data (now in hand) changes in the card, the figures and the archetype method; (4) the exact list of numbers in our text that must change. Deadline logic: pre-registration 3–5 days before the public S-1 (likely September). Be adversarial and specific.

## 1. What v1.5 changes vs v1 (config diff, sim/config/base.yaml; + = v1.5)
```
-# Meter-Trap W2 Monte Carlo — base configuration (PRIVATE; never published)
+# Meter-Trap W2 Monte Carlo — base configuration, ENGINE v1.5 (PRIVATE; never published)
+# v1.5 (2026-08-21): exit multiple fitted on comps (sim/calibrate.py), gross->net restatement scenario,
+# t-copula innovations, entry-price-dependent price path + lockup shock, GM cliff, sector-unwind overlay
+# (disabled here; sim/config/unwind.yaml enables it). The v1 configuration is frozen in sim/config/v1_frozen.yaml.
+  engine_version: "1.5"
+  restatement:                  # Evidence C #1: cloud-reseller flow booked GROSS; a net restatement cuts headline ARR 20-40%
+    prob: 0.35                  #   probability the economic base is 20-40% below the headline (ESTIMATE; referee range 30-50%)
+    factor_low: 0.60            #   ARR multiplied by U(0.60, 0.80) on restated paths — a level shift, not a lognormal shock
+    factor_high: 0.80
-  initial: {api: 0.45, enterprise: 0.35, claude_code: 0.10, consumer: 0.08, other: 0.02}
+  # Evidence C: Claude Code ~$8B ≈ 17% of the $47B run-rate (vs leaked ~10%); API+enterprise ~80% combined; consumer ~5-8%
+  initial: {api: 0.40, enterprise: 0.33, claude_code: 0.17, consumer: 0.08, other: 0.02}
-  mode: prior                           # 'prior' until comps_table1 regression lands (issue #3/#11)
-  # log(EV/NTM) = a + b*growth_ntm + c*gross_margin + d*committed_share + eps
-  prior_coef: {a: 1.20, b: 1.60, c: 0.90, d: 0.60}
+  mode: regression                      # v1.5: coefficients from sim/calibrate.py (comps_table1, n=12, ridge toward the v1 prior, lambda by LOO)
+  # log(EV/NTM) = a + b*min(growth,0.8) + c*gross_margin + d*committed_share + eps
+  # Posterior (prior family, lambda=1000 -> slopes ≈ prior, intercept re-anchored to the comps: 1.20 -> 0.898).
+  # LOO RMSE 0.774 vs 0.773 for the fixed prior, 0.976 OLS, 0.714 mean-only: the 12 comps pin the LEVEL, not the slopes.
+  coef: {a: 0.8981, b: 1.5904, c: 0.8969, d: 0.5933}
+  coef_draw: true                       # per-path coefficient draw from the pairs-bootstrap covariance (intercept sd ≈ 0.19)
+  coef_cov:
+    - [0.03754528, 0.00047078, 0.00143672, 0.00037076]
+    - [0.00047078, 0.00010015, -0.00000631, 0.00001805]
+    - [0.00143672, -0.00000631, 0.00040579, 0.00009258]
+    - [0.00037076, 0.00001805, 0.00009258, 0.00007196]
+  prior_coef: {a: 1.20, b: 1.60, c: 0.90, d: 0.60}    # v1 written-down prior, kept for reference / ablation
-  resid_sd: 0.30
-  mark_noise_sd_per_q: 0.18             # quarterly noise in mark-to-market multiple (AR(1)); stationary sd ≈0.30 (to be calibrated on Table 2, #5)
-  mark_ar1: 0.80
+  resid_sd: 0.86                        # comps cross-sectional residual sd of log multiple (reported; not used by the engine)
+  mark_noise_sd_per_q: 0.30             # v1.5 calibrated (sim/calibrate.py grid, 20k paths): P(>=40% from peak, 8q) 0.84 vs comps 14/14; P(>=40% below IPO price) 0.45 vs comps 5/14;
+  mark_ar1: 0.80                        #   re-rating q1->q8: mean -0.54 log (comps -0.55), sd 0.62 (comps 0.94). Stationary sd ≈ 0.50. Judgment between the two drawdown targets.
+  gm_cliff: {threshold: 0.35, haircut: 0.50}   # Evidence D / PitchBook: GM < 35% compresses fair value 70-81%; we apply -50% on the multiple (ESTIMATE)
+  copula: t                             # v1.5: t-copula, tail dependence between growth and multiple shocks (2022-style joint event)
+  nu: 4
+# ---- Price path (market price vs fundamental mark) ---------------------------
+price:
+  premium_half_life_q: 4                # IPO price starts at `valuation_usd_b`; the premium/discount to the model's mark halves every 4q (ESTIMATE)
+  lockup:                               # lockup-expiry supply shock on the PRICE path only (Quant_Primer §10, report E: 13 comps, mean -8.6%, sd ~13%)
+    quarter: 2
+    mean: -0.086
+    sd: 0.13
+    half_life_q: 2
+
+# ---- Sector unwind (circular-capital) regime — DISABLED in base; sim/config/unwind.yaml enables ----
+unwind:
+  enabled: false
+  hazard_phase1_per_yr: 0.06            # build phase 2026-28 (E2 §3d; ESTIMATE by analogy: telecom 2000-02, 2008, shale 2014-16, crypto 2022)
+  hazard_phase2_per_yr: 0.05            # 2029+
+  phase1_until_q: 8                     # quarter index of 2028Q4 (entry 2026Q4 = 0)
+  multiple_hit_low: 0.45                # multiple compresses by U(45%,65%) (22x -> 8-12x), then mean-reverts
+  multiple_hit_high: 0.65
+  multiple_half_life_q: 6               # 18-month half-life of the compression
+  demand_quarters: 8                    # growth multiplier applies for 2 years
+  demand_growth_mult: 0.5
+
```
Engine code changes (sim/engine.py): t-copula innovations (nu=4); gross->net restatement as a discrete level shift at entry; exit-multiple coefficients from a ridge fit on 12 comps with per-path coefficient draw from the pairs-bootstrap covariance; GM cliff; sector-unwind overlay (off in base); price path anchored at the IPO price converging to the model mark (half-life 4q) with a lockup-expiry shock; mark noise recalibrated to the comps drawdown base rate.

## 2. Multiple fit (sim/calibrate.py output, truncated)
```
multiple_fit:
  n: 12
  tickers:
  - SNOW
  - ARM
  - PLTR
  - META
  - BABA
  - UBER
  - ABNB
  - DASH
  - RDDT
  - CRCL
  - FIG
  - KLAR
  shrink: prior
  lambda_: 1000.0
  loo:
  - family: zero
    lam: 0.0
    loo_rmse: 0.9756993816941175
  - family: prior
    lam: 0.0
    loo_rmse: 0.9756993816941175
  - family: zero
    lam: 0.1
    loo_rmse: 0.9710218546713744
  - family: prior
    lam: 0.1
    loo_rmse: 0.9711664143816339
  - family: zero
    lam: 0.3
    loo_rmse: 0.9622573909051734
  - family: prior
    lam: 0.3
    loo_rmse: 0.9628094530980297
  - family: zero
    lam: 1.0
    loo_rmse: 0.9364662811234397
  - family: prior
    lam: 1.0
    loo_rmse: 0.9392249326062324
  - family: zero
    lam: 2.0
    loo_rmse: 0.9085883688717067
  - family: prior
    lam: 2.0
    loo_rmse: 0.9153103000441862
  - family: zero
    lam: 3.0
    loo_rmse: 0.8873557663434488
  - family: prior
    lam: 3.0
    loo_rmse: 0.8980664781393861
  - family: zero
    lam: 5.0
    loo_rmse: 0.8567040460302643
  - family: prior
    lam: 5.0
    loo_rmse: 0.8743983979576447
  - family: zero
    lam: 10.0
    loo_rmse: 0.8132837289660598
  - family: prior
    lam: 10.0
    loo_rmse: 0.8426897267930167
  - family: zero
    lam: 20.0
    loo_rmse: 0.7757411825252392
  - family: prior
    lam: 20.0
    loo_rmse: 0.816245403604249
  - family: zero
    lam: 50.0
    loo_rmse: 0.7428367622036092
  - family: prior
    lam: 50.0
    loo_rmse: 0.7931723847898188
  - family: zero
    lam: 100.0
    loo_rmse: 0.729209232757177
  - family: prior
    lam: 100.0
    loo_rmse: 0.7834839207485045
  - family: zero
    lam: 1000.0
    loo_rmse: 0.7154738582486376
  - family: prior
    lam: 1000.0
    loo_rmse: 0.7735467835617538
  loo_best:
    family: prior
    lam: 1000.0
    loo_rmse: 0.7735467835617538
  loo_benchmarks:
    prior_fixed: 0.7728165411769083
    ols: 0.9756993816941175
    mean_only: 0.7138517839318533
  prior:
    a: 1.2
    b: 1.6
    c: 0.9
    d: 0.6
  coef:
    a: 0.8981225440632676
    b: 1.5903590493777822
    c: 0.8969279086179559
    d: 0.5932841232011019
  ols:
    a: 1.5291042497180107
    b: 0.7453685465109364
    c: 0.6921185779515383
    d: 0.05596534407780338
  coef_boot_sd:
    a: 0.193766045233182
    b: 0.010007537167074596
    c: 0.02014411775280843
    d: 0.008482690360950649
  coef_boot_p05:
    a: 0.5782621878556828
    b: 1.5757281499443159
    c: 0.8591876982625025
    d: 0.5816762948190641
  coef_boot_p95:
    a: 1.2137634955500496
    b: 1.6085644541209847
    c: 0.923322180237432
    d: 0.6045631013715448
  coef_cov:
  - - 0.03754528028530753
    - 0.0004707774681341738
    - 0.00143672390086431
    - 0.0003707606136609539
  - - 0.0004707774681341738
    - 0.0001001508001503796
    - -6.314740748831003e-06
    - 1.804726841497487e-05
  - - 0.00143672390086431
    - -6.314740748831003e-06
    - 0.00040578548003901264
    - 9.258234922595791e-05
  - - 0.0003707606136609539
    - 1.804726841497487e-05
    - 9.258234922595791e-05
    - 7.195603575976501e-05
  resid_sd: 0.864743508319451
  fitted:
  - 2.768034975532703
  - 2.292550301962981
  - 2.5963639181102733
  - 2.471098298320708
  - 2.364468419462141
  - 2.063829780833847
  - 1.1564957143166568
  - 2.663720133305369
  - 2.0034559458440437
  - 3.093821309709421
  - 2.9168468465992836
  - 1.644468768099023
  resid:
  - 0.73451490038974
  - 0.5347633199660464
  - 0.18864732412806484
  - 0.4680636237448885
  - 0.27458891015311737
  - -0.45439186839974677
  - 1.0842139749593016
  - -0.6
```

## 3. Headline v1 (committed, in article/card) vs v1.5 (working tree), $2T entry, 100k paths, 5y
v1: P(IRR≥35%) 0.044; P(−40% in 8q | growth<30% two q) 0.631 (uncond 0.357); $380B entry percentile (35%/20% hurdle) 0.274/0.047; median IRR/MOIC/exit EV 0.092/1.55/$3,375B; P(MOIC<1) 0.241.
v1.5:
| metric | value |
|---|---|
| P(IRR ≥ 35% from $2T entry, 5y) | 0.028 |
| P(−40% within 8q \| metered growth <30% two consecutive q) | 0.712 (trigger prob 0.136; unconditional 0.454) |
| $380B entry percentile on fair-value curve (35% hurdle / 20% hurdle) | 0.531 / 0.201 |
| median IRR / MOIC / exit EV ($B) | 0.001 / 1.00 / 2185 |
| P(MOIC < 1) | 0.497 |

seed=20261016 config=2132e84b0a8608a8 n=100000

Analytical opinion, not investment advice.


## 4. Ablation (v1.5, 30k paths)
# Engine v1.5 — value decomposition by channel ($2T entry, 30k paths, seed from base.yaml)

Each row switches ONE v1.5 channel off (so the gap to the first row is what that channel is worth). 'fitted multiple (v1 prior)' is the level channel.

| channel | fair value p50 @10% ($B) | @35% ($B) | P(loss) | P(lose>half) | P(≥40% below entry, 2y) | buyer IRR p50 | exit EV p50 ($B) |
|---|---|---|---|---|---|---|---|
| v1.5 base | 1264 | 454 | 0.49 | 0.170 | 0.45 | 0.4% | 2213 |
| - restatement | 1424 | 512 | 0.43 | 0.119 | 0.41 | 2.8% | 2493 |
| - fitted multiple (v1 prior) | 1697 | 609 | 0.34 | 0.090 | 0.35 | 6.4% | 2970 |
| - coefficient draw | 1254 | 450 | 0.49 | 0.162 | 0.45 | 0.2% | 2194 |
| - t-copula (Gaussian) | 1242 | 446 | 0.50 | 0.172 | 0.46 | 0.0% | 2174 |
| - GM cliff | 1269 | 456 | 0.49 | 0.168 | 0.45 | 0.4% | 2222 |
| - lockup shock | 1264 | 454 | 0.49 | 0.170 | 0.42 | 0.4% | 2213 |
| - price convergence (scale-free) | 1264 | 454 | 0.49 | 0.170 | 0.45 | 0.4% | 2213 |
| - mix update (CC 10%) | 1267 | 455 | 0.49 | 0.173 | 0.45 | 0.4% | 2218 |
| - calibrated mark noise (v1 0.18) | 1261 | 453 | 0.49 | 0.147 | 0.37 | 0.3% | 2208 |

Analytical opinion, not investment advice.


## 5. Price ladder and fair value by hurdle (v1.5)
# Two-investor price ladder — engine v1.5 base

| IPO valuation | EV/run-rate | buyer IRR p50 (p25–p75) | P(lose money) | P(lose > half) | P(≥40% below IPO price, 2y) | P(≥40% off peak, 2y) | grade | fund MOIC at IPO | at lockup p50 | hold-to-2031 p50 | fund grade | P(buyer loses & fund >3×) |
|---|---|---|---|---|---|---|---|---|---|---|---|---|
| $1.00T | 12× | 15% (4–28) | 17% | 2.2% | 24% | 74% | **OR-BBB-** | 2.4× | 3.3× | 4.8× | OR-A or better | 0% |
| $1.25T | 15× | 10% (-0–22) | 26% | 4.9% | 30% | 77% | **OR-BB** | 3.0× | 3.8× | 4.8× | OR-A or better | 0% |
| $1.50T | 18× | 6% (-4–18) | 35% | 8.4% | 35% | 80% | **OR-B+** | 3.6× | 4.3× | 4.8× | OR-A or better | 9% |
| $1.75T | 21× | 3% (-7–14) | 43% | 12.5% | 41% | 82% | **OR-B+** | 4.2× | 4.8× | 4.8× | OR-A or better | 17% |
| $2.00T | 24× | 0% (-9–11) | 50% | 17.0% | 45% | 84% | **OR-B-** | 4.8× | 5.3× | 4.8× | OR-A or better | 24% |
| $2.50T | 31× | -4% (-13–6) | 61% | 26.1% | 53% | 87% | **OR-CCC/C** | 6.0× | 6.2× | 4.8× | OR-A or better | 35% |
| $3.00T | 37× | -8% (-16–3) | 70% | 34.8% | 60% | 89% | **OR-CCC/C** | 7.1× | 7.1× | 4.8× | OR-A or better | 43% |

Analytical opinion, not investment advice.

# Fair value by required return — engine v1.5 base

| required return | p5 | p25 | **p50** | p75 | p95 | share of paths where fair value > $2.0T |
|---|---|---|---|---|---|---|
| 8% | 428 | 830 | **1368** | 2311 | 4934 | 0.31 |
| 10% | 391 | 757 | **1248** | 2108 | 4502 | 0.27 |
| 12% | 357 | 692 | **1141** | 1927 | 4114 | 0.23 |
| 15% | 313 | 606 | **999** | 1688 | 3605 | 0.19 |
| 20% | 253 | 490 | **808** | 1365 | 2914 | 0.12 |
| 25% | 206 | 399 | **659** | 1113 | 2376 | 0.08 |
| 35% | 140 | 272 | **448** | 757 | 1617 | 0.03 |

($B) Analytical opinion, not investment advice.


## 6. Prompt-H data return — what we verified and what changed (triage §3 and §7)
## 3. New facts that change our documents

| Fact | Status | Where it lands |
|---|---|---|
| **Anthropic run-rate "topped $65B by late July 2026"** (after $47B May) | SECONDARY (Bloomberg/Reuters via Yahoo) — **verify before use** | `data/run_rate_series.csv` stops at $47B May-2026; `sim/config/base.yaml` `arr_usd_b` median 90 at IPO assumes this trajectory. If $65B holds, EV/run-rate at $2T is 31× not 42×; the card's "EV / run-rate (@$90B)" column stays but the S-1-day scorecard needs the July print. |
| **Nvidia → OpenAI/SB Energy Ohio backstop, up to $105B, 2026-08-17** (Nvidia SEC filing via Bloomberg/CNBC/Fortune; Fortune: $145B lower than reported) | VERIFIED-PRIMARY | Fig 3 caption ("Nvidia invests in and backstops neoclouds") — add as the named example; it is the single largest backstop and post-dates our draft. |
| Anthropic → Fluidstack/US DC capex commitment $50B (Nov 2025) | SECONDARY (Fierce) | Card §KMV default point uses $170B disclosed (AWS >$100B, Google ~$40B, Azure ~$30B). If the $50B is take-or-pay-like it belongs in D → re-run the KMV ladder at $220B. Flag, do not change yet. |
| Microsoft → Anthropic $5B / Anthropic → Azure $30B (Nov 2025) | SECONDARY | Already in card Panel G. |
| AMD–OpenAI warrant: 160M shares (~10%) at $0.01, 6GW / ~$90B | SECONDARY | Fig 3 parallel-loop note. |
| First mainstream "circular" label: Forbes, Phoebe Liu, 2025-10-09 | SECONDARY | Article footnote; FT Alphaville/Levine coinage not pinned. |
| H8-1: "34% vs 62%" is **not** in Loughran & Ritter; primary says issuers 5%/yr over 5y, 44% more capital needed for equal wealth; Ritter 1991: 29.1% 3-yr underperformance | corrected | Article base-rate box: use 5%/yr + 44%, drop 34/62. |
| H8-5: Lucent $3.7B FY2001 vendor-financing write-off **unconfirmed**; Nortel $2.1B customer financing end-FY2001 confirmed (SECONDARY) | corrected/partial | F §3 Lehman/Lucent table and card Panel G line "Lucent 2001": keep the topology claim, drop the $3.7B number unless we source it from Lucent's FY2001 10-K ourselves. |
| Cisco: $555.4B 2000-03-27 → $8.60 2002-10-08 → record close 2025-12-10 (~25 years) | VERIFIED-PRIMARY (CNBC) | Article history section. |
| Ritter 2025: avg first-day return 29.3% (2024: 15.3%; 1980–2025: 19.0%); money left on table $13.11bn | PRIMARY/SECONDARY | H2 hot-market indicator for 2025–26 cohort; the "hot market" flag for Anthropic's year. |
| Amodei quote verbatim: "If my revenue is not $1 trillion dollars, if it's even $800 billion, there's no force on earth, there's no hedge on earth that could stop me from going bankrupt if I buy that much compute" — Dwarkesh, "$1 trillion of compute that starts at the end of 2027" | confirmed | Card line 38 label and article epigraph — use this wording. |
| Prince quote confirmed FT July 2007; Guerrera as interviewer unconfirmed. Greenspan AEI 1996-12-05 confirmed. | partial | Article — cite FT, no interviewer name. |


## 7. Follow-up pulls (2026-08-21/22) — what closed, what changed

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


## 7. Path archetypes — prototype (n=15) and new data (n=26 paths from bars; lockup terms and macro features for all 26)
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


H1_paths_from_bars.csv (26 listings; from Alpaca bars, normalised to offer and to first close):
```
ticker,first_bar,offer,day1_open,day1_close,day1_pop_pct,peak_close_12m,peak_close_date,peak_high_12m,peak_high_date,px_6m,px_12m,dd_peak_to_6m_pct,dd_peak_to_12m_pct,ret_6m_vs_offer_pct,ret_1y_vs_offer_pct,ret_6m_vs_first_close_pct,worst_6m_vs_first_close_pct,below_offer_within_12m,below_first_close_within_6m,bars_days,source
SPCX,2026-06-12,135.0,150.0,160.95,19.2,201.8,2026-06-16,225.64,2026-06-16,136.03,,-32.6,,0.8,,-15.5,-32.7,True,True,70,alpaca_sip
CRCL,2025-06-05,31.0,69.0,83.23,168.5,263.45,2025-06-23,298.99,2025-06-23,87.46,80.28,-66.8,-69.5,182.1,159.0,5.1,-19.6,False,True,442,alpaca_sip
FIG,2025-07-31,33.0,85.0,115.5,250.0,122.0,2025-08-01,142.92,2025-08-01,27.07,24.32,-77.8,-80.1,-18.0,-26.3,-76.6,-76.6,True,True,386,alpaca_sip
KLAR,2025-09-10,40.0,52.0,45.82,14.5,45.82,2025-09-10,57.2,2025-09-10,16.43,,-64.1,,-58.9,,-64.1,-72.0,True,True,338,alpaca_sip
CRWV,2025-03-28,40.0,39.0,40.0,0.0,183.58,2025-06-20,187.0,2025-06-20,120.34,74.81,-34.4,-59.2,200.9,87.0,200.9,-11.5,True,True,504,alpaca_sip
RDDT,2024-03-21,34.0,47.0,50.44,48.4,225.23,2025-02-07,230.41,2025-02-10,64.56,115.7,,-48.6,89.9,240.3,28.0,-22.3,False,True,729,alpaca_sip
ARM,2023-09-14,51.0,56.1,63.59,24.7,186.46,2024-07-10,188.75,2024-07-09,130.96,147.37,,-21.0,156.8,189.0,105.9,-24.7,True,True,729,alpaca_sip
CART,2023-09-19,30.0,42.0,33.7,12.3,39.87,2024-09-18,42.95,2023-09-19,36.99,39.87,,0.0,23.3,32.9,9.8,-33.4,True,True,730,alpaca_sip
BIRK,2023-10-11,46.0,41.0,40.2,-12.6,63.57,2024-08-23,64.78,2024-08-26,43.42,49.84,,-21.6,-5.6,8.3,8.0,-9.5,True,True,730,alpaca_sip
CAVA,2023-06-15,22.0,42.0,43.78,99.0,93.15,2024-05-30,96.93,2024-05-30,40.62,89.93,,-3.5,84.6,308.8,-7.2,-31.5,False,True,729,alpaca_sip
RIVN,2021-11-10,78.0,106.75,100.73,29.1,172.01,2021-11-16,179.4699,2021-11-16,20.6,32.96,-88.0,-80.8,-73.6,-57.7,-79.5,-79.5,True,True,729,alpaca_sip
COIN,2021-04-14,250.0,381.0,328.28,31.3,357.39,2021-11-09,429.54,2021-04-14,246.78,147.29,,-58.8,-1.3,-41.1,-24.8,-32.8,True,True,729,alpaca_sip
HOOD,2021-07-29,38.0,38.0,34.82,-8.4,70.39,2021-08-04,85.0,2021-08-04,11.61,9.05,-83.5,-87.1,-69.4,-76.2,-66.7,-66.7,True,True,728,alpaca_sip
BMBL,2021-02-11,43.0,76.0,70.31,63.5,78.89,2021-02-16,84.8,2021-02-12,50.83,28.1,-35.6,-64.4,18.2,-34.7,-27.7,-43.7,True,True,729,alpaca_sip
ABNB,2020-12-10,68.0,146.0,144.71,112.8,216.84,2021-02-11,219.94,2021-02-11,146.12,180.42,-32.6,-16.8,114.9,165.3,1.0,-13.8,False,True,729,alpaca_sip
DASH,2020-12-09,102.0,163.8,189.51,85.8,245.97,2021-11-12,257.2499,2021-11-15,136.98,164.86,,-33.0,34.3,61.6,-27.7,-40.4,False,True,729,alpaca_sip
SNOW,2020-09-16,120.0,245.0,253.93,111.6,390.0,2020-12-08,429.0,2020-12-08,230.3,323.52,-40.9,-17.0,91.9,169.6,-9.3,-15.7,False,True,729,alpaca_sip
PLTR,2020-09-30,7.25,10.0,9.5,31.0,39.0,2021-01-27,45.0,2021-01-27,23.29,24.04,-40.3,-38.4,221.2,231.6,145.2,-4.9,False,True,727,alpaca_sip
UBER,2019-05-10,45.0,42.0,41.57,-7.6,46.38,2019-06-28,47.08,2019-06-28,27.01,32.79,-41.8,-29.3,-40.0,-27.1,-35.0,-35.2,True,True,728,alpaca_sip
LYFT,2019-03-29,72.0,87.24,78.29,8.7,78.29,2019-03-29,88.6,2019-03-29,41.35,27.6,-47.2,-64.7,-42.6,-61.7,-47.2,-47.2,True,True,728,alpaca_sip
PINS,2019-04-18,19.0,23.75,24.4,28.4,36.56,2019-08-21,36.83,2019-08-22,25.99,17.45,-28.9,-52.3,36.8,-8.2,6.5,-2.5,True,True,729,alpaca_sip
ZM,2019-04-18,36.0,65.0,62.0,72.2,159.56,2020-03-23,164.94,2020-03-23,67.03,150.06,,-6.0,86.2,316.8,8.1,0.0,False,False,729,alpaca_sip
BYND,2019-05-02,25.0,46.0,65.75,163.0,234.9,2019-07-26,239.71,2019-07-26,84.45,91.53,-64.0,-61.0,237.8,266.1,28.4,0.0,False,False,729,alpaca_sip
PTON,2019-09-26,29.0,27.0,25.76,-11.2,97.73,2020-09-25,100.4399,2020-09-23,25.75,97.73,,0.0,-11.2,237.0,-0.0,-24.3,True,True,729,alpaca_sip
BABA,2014-09-19,68.0,92.6999969482422,93.88999938964844,38.1,119.1500015258789,2014-11-10,120.0,2014-11-13,85.19999694824219,65.75,-28.5,-44.8,25.3,-3.3,-9.3,-13.1,True,True,731,yahoo_chart_api
META,2012-05-18,38.0,42.04999923706055,38.22999954223633,0.6,38.22999954223633,2012-05-18,45.0,2012-05-18,23.559999465942383,26.25,-38.4,-31.3,-38.0,-30.9,-38.4,-53.6,True,True,728,yahoo_chart_api

```
Lockup-window prices from bars (first and full release; ±10 trading days):
```
ticker,lockup_first_release,lockup_first_release_px,lockup_first_release_px_plus10d,lockup_first_release_ret_minus10_to_plus10_pct,lockup_first_release_ret_0_to_plus10_pct,lockup_full_release,lockup_full_release_px,lockup_full_release_px_plus10d,lockup_full_release_ret_minus10_to_plus10_pct,lockup_full_release_ret_0_to_plus10_pct
SPCX,2026-08-06,114.92,134.0,13.3,16.6,2027-06-12,,,,
CRCL,2025-08-15,149.26,131.98,-21.5,-11.6,2025-11-14,81.89,75.94,-40.2,-7.3
FIG,2025-09-05,54.86,56.81,-21.9,3.6,2026-08-31,,,,
KLAR,2026-03-09,14.44,13.04,1.7,-9.7,2026-03-09,14.44,13.04,1.7,-9.7
CRWV,2025-05-19,86.59,150.48,195.0,73.8,2025-08-15,99.97,103.07,-1.0,3.1
RDDT,2024-08-09,52.91,59.21,-5.1,11.9,2024-08-09,52.91,59.21,-5.1,11.9
ARM,2024-03-12,129.5,127.96,-7.2,-1.2,2024-03-12,129.5,127.96,-7.2,-1.2
CART,2024-02-15,26.23,33.17,31.4,26.5,2024-02-15,26.23,33.17,31.4,26.5
BIRK,2024-04-08,44.55,43.9,-6.1,-1.5,2024-04-08,44.55,43.9,-6.1,-1.5
CAVA,2023-12-12,38.87,44.44,32.3,14.3,2023-12-12,38.87,44.44,32.3,14.3
RIVN,2022-05-09,22.78,27.99,-17.4,22.9,2022-05-09,22.78,27.99,-17.4,22.9
COIN,2021-04-14,328.28,298.05,-9.2,-9.2,2021-04-14,328.28,298.05,-9.2,-9.2
HOOD,2021-07-29,34.82,48.1,38.1,38.1,2021-12-01,23.93,19.5,-42.4,-18.5
BMBL,2021-08-09,48.07,51.35,1.4,6.8,2021-08-09,48.07,51.35,1.4,6.8
ABNB,2020-12-10,144.71,154.84,7.0,7.0,2021-05-17,132.5,144.31,-14.2,8.9
DASH,2021-03-09,141.48,131.76,-24.1,-6.9,2021-05-18,138.56,149.83,10.8,8.1
SNOW,2020-12-15,328.61,300.92,-1.5,-8.4,2021-03-05,239.73,220.82,-23.9,-7.9
PLTR,2020-09-30,9.5,9.34,-1.7,-1.7,2021-02-18,25.17,24.73,-22.1,-1.7
UBER,2019-11-06,26.94,28.03,-15.2,4.0,2019-11-06,26.94,28.03,-15.2,4.0
LYFT,2019-08-19,51.68,45.42,-23.7,-12.1,2019-08-19,51.68,45.42,-23.7,-12.1
PINS,2019-10-15,25.57,25.57,-3.3,0.0,2019-10-15,25.57,25.57,-3.3,0.0
ZM,2019-10-15,71.11,65.49,-13.6,-7.9,2019-10-15,71.11,65.49,-13.6,-7.9
BYND,2019-08-01,176.04,144.2,-15.3,-18.1,2019-10-28,105.41,76.79,-39.2,-27.2
PTON,2020-02-24,26.5,23.21,-16.7,-12.4,2020-02-24,26.5,23.21,-16.7,-12.4
BABA,2014-12-18,109.25,101.0,-7.5,-7.6,2015-09-19,65.75,63.2,-4.9,-3.9
META,2012-08-16,19.87,19.09,-4.7,-3.9,2013-05-18,26.25,23.85,-15.8,-9.1

```
Also available per listing: float %, deal size, range and priced-vs-range, step-up vs last private round, staged-lockup provisions (H1_lockup_terms.csv); VIX, 10-y, Nasdaq 3m/6m at IPO (H2_macro_at_ipo.csv); oversubscription/retail allocation mostly unavailable.

## Questions (answer each, numbered; give numbers and thresholds, not adjectives)
1. **Base choice.** Should v1.5 replace v1 as the pre-registration base? Which of the ten channels would you NOT adopt, and why? Is a 12-comp ridge fit that moves only the intercept (LOO RMSE 0.774 vs 0.773 for the fixed prior) a legitimate reason to cut every exit multiple by ~26%? What is the honest disclosure sentence?
2. **Restatement channel.** p=0.35, haircut U(0.60,0.80). Too high, too low? How should it be exposed (scenario toggle, 'what would change our mind' item, or folded into the base)? What S-1 disclosure would resolve it?
3. **Attribution.** The ablation says level (multiple intercept) ≈ −6pp median IRR and +15pp P(loss); restatement ≈ −2.4pp / +6pp; everything else ≈ 0 on the median but lockup/mark-noise move the drawdown tails. Do you believe it? What interaction or ordering effect could mislead a one-at-a-time ablation here, and what should we add (all-off row, pairwise)?
4. **Run-rate.** Last print $65B (Jul-26); FT: investors expect $100–120B 2026 exit. Our entry ARR at listing is lognormal median $90B, log-sd 0.15. Keep, raise, or widen? How should the card quote EV/run-rate (last print vs at-listing)?
5. **KMV default point.** Disclosed commitments now: AWS >$100B/10y, Azure $30B, Fluidstack $50B, TeraWulf ~$19B, Hut 8 ~$7B, Google 'tens of billions'. What counts as debt-like for the default point — and at what D does the issuer grade leave 'A or better'?
6. **Figures.** Fig 4 (the AI 'spread'): with only point-in-time CoreWeave CDS (670→881→452→855bp) and note yields (12.3% YTW), and a DDTL margin path (+400→+225→+450→+550), what is the defensible chart — and is the Hyperion A+ / T+225 bond the right 'AAA ABS 2006' analogue? Fig 3 caption numbers: debt-funded capex 11% FY24 → 32% FY25 → 56% H1-26 (XBRL, CP-roll caveat), Alphabet $84.75B raise, Nvidia $105B Ohio backstop — anything you would not print?
7. **Archetypes.** With 26 paths, float %, step-up, priced-vs-range, day-1 pop, hot-market year, VIX/10y, concurrent supply: specify the features-only classifier you would actually fit (method, regularisation, validation), what a credible statement about Anthropic's archetype probabilities looks like at n=26, and what must NOT be claimed. SPCX float 4.9%, step-up 2.2×, three-tier lockup with first release at day 55 — how do you use it?
8. **Lockup shock.** Our own 24-listing measurement: full-release ±10d window median −11%, 79% negative; first release −6%/69%; Field & Hanka −1.5% 3-day AR. The engine uses mean −8.6%, sd 13%, quarter 2. Change it? And how to treat Anthropic's likely staged lockup?
9. **Text corrections.** Confirm or extend the seven corrections in triage §7 (Lucent $2.2B; fibre 'lit' misattributed; 34/62 dropped; debt-funded capex; Enron path; SPAC −64.2% Ritter 15c; run-rate $65B). Anything in the article/card that Prompt H now contradicts that we missed?
10. **The sentence.** Give the one-line headline for the card at $2T under v1.5 (median IRR ≈0, P(loss) 0.50, P(lose>half) 0.17, fair value @10% ≈ $1.26T), and the one sentence that tells the reader how much of it is judgment.
