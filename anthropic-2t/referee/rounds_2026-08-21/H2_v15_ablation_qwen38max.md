<!-- model: qwen/qwen3.8-max | prompt_tokens: 18015 | completion_tokens: 7761 | latency_s: 149 | date: 2026-08-22 -->

# Referee Report — Task H2: Engine v1.5 Base, Channel Ablation, Prompt-H Data Return

**Referee stance:** adversarial, quantitative, non-investment-advice. All section references are to the pack as provided.

---

## 1. Base Choice: Should v1.5 Replace v1?

**Verdict: Adopt v1.5 as the pre-registration base, but with two channels quarantined and one disclosure obligation that is non-negotiable.**

### The intercept problem is the whole story

The ridge fit on 12 comps moves the intercept from 1.20 to 0.898 — a shift of −0.302 in log-space, which compresses every exit multiple by a factor of e^(−0.302) ≈ 0.74, i.e. a **26% level cut** applied uniformly across all paths. The slopes are essentially untouched (b: 1.60→1.590, c: 0.90→0.897, d: 0.60→0.593; all within one bootstrap sd of the prior). The LOO RMSE improvement is 0.774 vs 0.773 — **one part in a thousand**. The mean-only benchmark (0.714) beats both. This is not a model that learned anything about the *relationship* between growth, margins, and multiples; it is a model that learned the 12 comps trade at a lower level than the v1 prior assumed, and nothing else.

**Is the 26% cut legitimate?** The bootstrap sd of the intercept is 0.194. The shift is 0.302/0.194 ≈ **1.56 standard errors** — not significant at any conventional threshold. The 90% bootstrap interval for the intercept is [0.578, 1.214], which **includes the v1 prior of 1.20**. You cannot reject the hypothesis that the prior was correct. The comps are pinning the level, but the level they pin is statistically indistinguishable from the prior.

**However**, the prior was a written-down judgment (v1 config, `prior_coef`), not a fit. The comps are real data. The honest position is: the prior was too optimistic about the level, the data says so, but the data is too thin (n=12, cross-sectional, single vintage) to be confident. The ridge shrinkage at λ=1000 is doing exactly what it should — pulling the slopes back to the prior and letting the intercept absorb the level correction. This is defensible *as a Bayesian update*, not as a frequentist estimate.

**Honest disclosure sentence (required in the pre-registration and the article):**

> "The exit-multiple level is anchored to 12 comparable IPOs via a ridge fit that shrinks slopes toward the v1 prior (λ=1000). The fit moves the intercept from 1.20 to 0.90 (−26% on the multiple), but the LOO RMSE improvement over the fixed prior is <0.1% and the intercept shift is 1.6 bootstrap standard errors — not statistically distinguishable from zero. The level correction is the single largest driver of the v1→v1.5 rating change. We adopt it because the prior was uncalibrated judgment and the comps are data, but we flag that the entire rating is sensitive to this one number."

### Channel-by-channel adoption decision

| Channel | Adopt? | Reason |
|---|---|---|
| Fitted multiple (intercept shift) | **Yes, with disclosure** | See above. It is the dominant channel and must be transparent. |
| Coefficient draw | **Yes** | Bootstrap covariance is correctly specified; the effect is small (ablation: p50 fair value $1,264B→$1,254B, P(loss) 0.49→0.49). It adds honest parameter uncertainty. |
| Restatement | **Yes, but see Q2** | The channel is real; the calibration is judgment. |
| t-copula (ν=4) | **Quarantine** | See below. |
| GM cliff | **Yes** | Evidence D / PitchBook supports the mechanism. The 50% haircut is an estimate but the direction is right. |
| Lockup shock | **Yes** | Self-calibrated from 26 listings (Q8). |
| Price convergence | **Yes** | Mechanically necessary to connect IPO price to model mark. |
| Mix update (CC 17%) | **Yes** | Evidence C supports the shift from 10% to 17%. |
| Calibrated mark noise | **Yes** | The grid calibration to comps drawdown base rates is the right approach. |
| Sector-unwind overlay | **Keep disabled** | Correctly off in base. The hazard rates (6%/5% per year) are pure analogy. Do not enable for pre-registration. |

### The t-copula quarantine

The t-copula with ν=4 introduces tail dependence between growth and multiple shocks. The ablation shows it moves almost nothing on the median (p50 fair value $1,264B→$1,242B, P(loss) 0.49→0.50). But the *purpose* of a t-copula is to fatten the joint tail, and the ablation's P(lose>half) actually goes *up* slightly (0.170→0.172) when you remove it — meaning the t-copula is making the left tail *very slightly thinner*, not fatter. This is counterintuitive and suggests the tail dependence is being absorbed by the mark-noise recalibration. With ν=4 and only two shock dimensions (growth, multiple), the t-copula is adding a parameter you cannot calibrate from the data. **Drop it for pre-registration; re-introduce only if you can show a comps-based calibration of ν.** The Gaussian copula is the simpler, more defensible default.

---

## 2. Restatement Channel

**p=0.35, haircut U(0.60, 0.80).**

### Is p=0.35 too high or too low?

The evidence base is "Evidence C #1: cloud-reseller flow booked GROSS." The question is whether Anthropic's revenue recognition is genuinely at risk of a gross-to-net restatement. Three considerations:

1. **The base rate for revenue restatements at IPO is low.** Among the 12 comps, zero had a gross-to-net restatement within 2 years of listing. The 35% probability is not calibrated from comps; it is a judgment about Anthropic specifically.
2. **The mechanism is plausible.** If a meaningful share of Anthropic's revenue is pass-through (e.g., compute credits resold, or revenue booked on behalf of cloud partners), a restatement is a real risk. The config comment says "cloud-reseller flow booked GROSS" — this needs to be substantiated with a specific revenue line or S-1 disclosure.
3. **The haircut range U(0.60, 0.80) implies a 20–40% ARR cut.** This is consistent with what a gross-to-net restatement would do if 20–40% of headline revenue is pass-through.

**My assessment:** p=0.35 is **too high for a base-case parameter** but **appropriate as a scenario toggle**. The reason: you have no comps base rate, no S-1 disclosure yet, and the probability is doing significant work in the ablation (−6pp on P(loss), −$160B on p50 fair value). Folding it into the base at 35% bakes in a judgment that the reader cannot verify.

**Recommendation:**
- **Pre-registration base:** Run with restatement **enabled** at p=0.35, but **also report the no-restatement scenario** as a named row in the headline table (the ablation already does this).
- **Disclosure:** "The restatement probability (35%) and haircut range (20–40%) are analyst estimates, not calibrated from comparable filings. They reflect the risk that a material share of headline ARR is pass-through revenue that would be reclassified net under ASC 606. The S-1 revenue-recognition footnote and the breakdown of gross vs. net revenue will resolve this."
- **What would change our mind:** The S-1 revenue-recognition policy note, specifically (a) whether Anthropic acts as principal or agent in cloud-compute resale, (b) the share of revenue from contracts where Anthropic does not control the underlying service, (c) any auditor emphasis-of-matter on revenue recognition.

---

## 3. Attribution Credibility

### What the ablation says

| Channel removed | Δ p50 fair value ($B) | Δ P(loss) | Δ P(lose>half) |
|---|---|---|---|
| Fitted multiple (→v1 prior) | +433 | −0.15 | −0.080 |
| Restatement | +160 | −0.06 | −0.051 |
| Calibrated mark noise (→v1 0.18) | −3 | 0.00 | −0.023 |
| Lockup shock | 0 | 0.00 | 0.000 |
| t-copula | −22 | +0.01 | +0.002 |
| GM cliff | +5 | 0.00 | −0.002 |
| Coefficient draw | −10 | 0.00 | −0.008 |
| Mix update | +3 | 0.00 | +0.003 |
| Price convergence | 0 | 0.00 | 0.000 |

The level channel (intercept) accounts for **~73% of the total P(loss) increase** (0.15 out of 0.25 total from v1's 0.24 to v1.5's 0.50). Restatement accounts for **~24%**. Everything else is noise on the median but matters in the drawdown tail (mark noise: P(lose>half) drops from 0.170 to 0.147 when you revert to v1's 0.18).

### Do I believe it?

**Mostly yes, with two caveats.**

**Caveat 1: One-at-a-time ablation misses interactions.** The level channel and the restatement channel are not independent. Restatement cuts ARR by 20–40%, which feeds into the exit-multiple regression (lower growth → lower fitted multiple). The one-at-a-time ablation removes restatement while keeping the fitted multiple, so it **overstates** the restatement effect and **understates** the level effect. The true decomposition requires at minimum:

- **All-off row** (v1 config, v1 engine): this is your v1 baseline. You already have it (v1 headline numbers). Include it explicitly as the last row of the ablation table.
- **Pairwise interaction for the top two channels:** Run (a) restatement off + v1 prior, (b) restatement on + v1 prior, (c) restatement off + fitted multiple, (d) restatement on + fitted multiple (= base). The interaction term is (d) − (c) − (b) + (a). If it is material (>2pp on P(loss)), disclose it.

**Caveat 2: The mark-noise channel is underappreciated.** The ablation shows P(≥40% below entry, 2y) drops from 0.45 to 0.37 when you revert to v1's mark_noise_sd=0.18. That is an 8pp swing in a drawdown metric that the card reports prominently. The mark-noise recalibration is doing real work in the tail, and the one-at-a-time format hides this because the median is insensitive to it. **Add a column for P(≥40% below entry, 2y) to the ablation table** (you already have it — good — but flag it in the text).

### What to add

1. **All-off row** (v1 frozen config). Already available.
2. **Pairwise table** for {fitted multiple, restatement} — 4 cells.
3. **Sensitivity of the intercept:** Re-run the base at intercept = 0.898 ± 1 sd (0.704, 1.092) and report the range of P(loss). This tells the reader how much the rating depends on the one number that is not statistically significant.

---

## 4. Run-Rate

**Last print: $65B (end-Jul-26). FT: investors expect $100–120B 2026 exit. Engine median at listing: $90B, log-sd 0.15.**

### Keep, raise, or widen?

**Keep the median at $90B. Widen the log-sd from 0.15 to 0.20.**

Reasoning:
- The $65B print is 7 weeks old. If the listing is October 2026, that is ~3 months of growth. At the implied trajectory ($47B May → $65B July = ~38% in 2 months), $90B by October is plausible but not certain. The FT's $100–120B exit-run-rate is an *annualized* number for year-end, not a point-in-time ARR at listing.
- The log-sd of 0.15 implies a 90% interval of [$69B, $117B] at listing. This is too tight given (a) the $65B print is secondary-source, (b) the growth rate is decelerating or accelerating (unknown), (c) the S-1 will reveal the actual number and it could be anywhere from $70B to $110B.
- A log-sd of 0.20 gives a 90% interval of [$61B, $133B], which brackets the FT's exit-run-rate range and acknowledges the uncertainty.

**How the card should quote EV/run-rate:**
- **At listing (model input):** EV / median ARR at listing = $2,000B / $90B = **22×**. This is the number the engine uses.
- **Last print (reference):** EV / $65B = **31×**. Report this as "EV / last reported run-rate" in a separate column, flagged as "not the model input."
- **Do not average them.** The card should have two columns: "EV / model ARR at listing" and "EV / last reported run-rate." The reader needs to see both.

---

## 5. KMV Default Point

**Disclosed commitments:** AWS >$100B/10y, Azure $30B, Fluidstack $50B, TeraWulf ~$19B, Hut 8 ~$7B, Google "tens of billions."

### What counts as debt-like?

The KMV default point is the level of debt at which the firm's asset value falls below its obligations. The question is which of these commitments are **debt-like** (i.e., fixed, unavoidable cash outflows) vs. **equity-like** (i.e., discretionary, contingent on revenue or usage).

| Commitment | Debt-like? | Reason |
|---|---|---|
| AWS >$100B/10y | **Partially.** If take-or-pay, yes. If usage-based with minimums, only the minimum is debt-like. The S-1 will clarify. |
| Azure $30B | **Partially.** Same logic. |
| Fluidstack $50B | **Likely yes** if it is a capex commitment (build-out obligation). If it is a revenue commitment (Anthropic pays Fluidstack for compute), it is an operating expense, not debt. |
| TeraWulf ~$19B | **Unknown.** Need contract terms. |
| Hut 8 ~$7B | **Unknown.** Same. |
| Google "tens of billions" | **Unknown.** No primary source. |

**Recommendation:** For the pre-registration, use a **conservative debt-like total of $170B** (the current card number) as the floor. Flag that if Fluidstack and TeraWulf are take-or-pay capex commitments, the number rises to ~$240B. Do not change the KMV ladder until the S-1 discloses the contract terms.

**At what D does the issuer grade leave 'A or better'?** This depends on the asset-value distribution, which is the engine's output. Roughly: if the p5 fair value at 5 years is below D, the issuer is in distress. At $2T entry, p5 fair value is ~$391B (10% hurdle). So D would need to exceed ~$390B to push the issuer below A. At $170B, the issuer is comfortably A. At $240B, still A. **The KMV grade is not sensitive to the commitment number in the current range.** Say so explicitly.

---

## 6. Figures

### Fig 4: The AI "spread"

**What you have:** Point-in-time CoreWeave CDS (670→881→452→855bp), 9.75% '31 note at 89.6 / 12.3% YTW, DDTL margin path (+400→+225→+450→+550/OID97), Hyperion A+ at T+225.

**What is defensible:** A **timeline chart** with three series:
1. CoreWeave 5y CDS (4 points, interpolated or shown as dots).
2. CoreWeave DDTL margin (4 points).
3. Hyperion 144A sr secured at T+225 as a **horizontal reference line** labeled "GPU-backed IG (Aug 2026)."

**What is NOT defensible:**
- A continuous spread series. You have 4 CDS points and 4 DDTL points. Do not interpolate between them as if they are a time series. Show them as discrete observations with dates.
- A "GPU basis" (CDS minus asset-backed spread). The asset side is too thin pre-Jul-25.
- Calling Hyperion the "AAA ABS 2006 analogue." Hyperion is **A+**, not AAA. The 2006 analogue was AAA-rated MBS tranches that were downgraded to junk. The correct analogy is: "Hyperion's A+ rating at T+225 is the *investment-grade* version of what 2006's AAA MBS was before the downgrade cycle. The question is whether the A+ holds." This is a more honest and more interesting framing.

**Fig 3 caption numbers:**
- **Debt-funded capex 11%→32%→56%:** Print it, with the CP-roll caveat. The XBRL sourcing is primary. The caveat is that commercial-paper roll-over inflates the ratio in H1-26. Say: "H1-26 ratio includes ~$XXB of CP that may roll into term debt; the FY25 figure (32%) is the cleaner measure."
- **Alphabet $84.75B raise:** Print it. 8-K and 424B5 are primary.
- **Nvidia $105B Ohio backstop:** Print it, but flag the Fortune discrepancy ($145B lower than reported). Say: "Nvidia SEC filing (8/17/26) discloses up to $105B; Fortune reports the commitment is $145B lower than initially reported. We use the SEC filing number."

---

## 7. Archetypes

### What classifier to fit at n=26

**Method:** Multinomial logistic regression (4 archetypes) on pre-listing features, with **L2 regularization** (ridge) and **leave-one-out cross-validation**.

**Features (from the data you have):**
1. Float % (continuous)
2. Step-up vs last private round (continuous, log-transformed)
3. Day-1 pop % (continuous)
4. Piced-vs-range (binary: above range = 1)
5. Hot-market year (binary: 2020–2021 = 1, else 0; or use Ritter's annual first-day return as a continuous proxy)
6. VIX at IPO (continuous)
7. Nasdaq 3m return at IPO (continuous)
8. Concurrent mega-IPO supply (count of IPOs >$5B in the same quarter)
9. EV/revenue at IPO (continuous, log-transformed)

**Regularization:** Ridge (L2), λ chosen by LOO-CV. With n=26 and 9 features, you are in the regime where regularization is mandatory. Do not use L1 (lasso) — it will zero out features arbitrarily at this sample size.

**Validation:** Leave-one-out. Report the LOO confusion matrix. With 26 observations and 4 classes, the expected accuracy by chance is 25%. If LOO accuracy is below 50%, the classifier is not useful and you should say so.

### What a credible statement looks like

> "At n=26, the archetype classifier achieves LOO accuracy of XX% (chance: 25%). For Anthropic, the predicted probabilities are: straight slide XX%, moonshot XX%, wobble-flat XX%, pop-and-fade XX%. These probabilities are conditional on the pre-listing features and the 26-listing training set; they are not calibrated probabilities and should be read as indicative, not predictive."

### What must NOT be claimed

- Do not claim the classifier "predicts" Anthropic's path. It assigns probabilities based on 26 historical analogues.
- Do not claim the archetypes are stable or exhaustive. Four clusters from 15 (now 26) paths is a prototype.
- Do not report confidence intervals on the archetype probabilities. At n=26, the intervals are meaningless.

### SPCX

SPCX (float 4.9%, step-up 2.2×, three-tier lockup, first release day 55) is the closest current analogue to Anthropic. Use it as a **validation case**: fit the classifier on the other 25 listings, predict SPCX's archetype, and report whether it matches the actual path (currently between archetypes 1 and 3 at week 10). If the classifier puts SPCX in "straight slide" or "wobble-flat," that is informative. If it puts SPCX in "moonshot," the classifier is not working.

**Do not include SPCX in the training set.** It is your out-of-sample test case.

---

## 8. Lockup Shock

### Your measurement vs the engine

| Source | Metric | Value |
|---|---|---|
| Your 26-listing bars, full release ±10d | Median return | **−11%** |
| Your 26-listing bars, full release ±10d | % negative | **79%** (n=24) |
| Your 26-listing bars, first release ±10d | Median return | **−6%** |
| Your 26-listing bars, first release ±10d | % negative | **69%** |
| Field & Hanka (2003) | 3-day AR | **−1.5%** |
| Engine v1.5 | Mean, sd | **−8.6%, 13%** |

**The engine's mean of −8.6% is between your full-release median (−11%) and first-release median (−6%).** This is reasonable if the engine is modeling a blended lockup event. However:

1. **The sd of 13% is too low.** Your 26-listing full-release returns range from +195% (CRWV) to −40.2% (CRCL). The sd of those 24 observations is approximately **45%**, not 13%. The 13% sd comes from the Quant_Primer §10 report (13 comps), which is a smaller and possibly different sample. **Recalibrate the sd to your own 26-listing measurement.** If you keep the 13% sd, you are understating the lockup tail risk by a factor of ~3.

2. **The mean should be updated.** Use your own measurement: mean of the 24 full-release returns ≈ **−8%** (close to the current −8.6%, so the mean is fine). But the sd must change.

3. **Anthropic's staged lockup:** Anthropic will almost certainly have a staged lockup (like SPCX's three-tier structure). The engine currently models a single shock at quarter 2. For Anthropic, model **two shocks**: a first-release shock at quarter 1 (mean −6%, sd from first-release data) and a full-release shock at quarter 2–3 (mean −11%, sd from full-release data). The half-life of 2 quarters is appropriate for the full release.

**Recommendation:** Change sd from 13% to **30%** (a compromise between your 45% sample sd and the recognition that the extreme outliers — CRWV +195%, CRCL −40% — are driven by idiosyncratic factors). Add a first-release shock at quarter 1 with mean −6%, sd 20%.

---

## 9. Text Corrections

### Confirm the seven corrections

| # | Correction | Confirmed? | Note |
|---|---|---|---|
| 1 | Lucent write-off: $2.2B, not $3.7B | **Confirmed.** FY2001 10-K405 shows $2,249M provision. | Use "$2.2B provision for uncollectibles and customer financings (FY2001 10-K)." |
| 2 | Fibre "lit" share: Odlyzko's 3–5% is link utilisation, not lit share | **Confirmed.** Reword to "link utilisation" or drop. | |
| 3 | Loughran–Ritter "34 vs 62": not in the paper | **Confirmed.** Use 5%/yr underperformance + 44% more capital needed. | |
| 4 | Debt-funded capex: 11%→32%→56% | **Confirmed.** XBRL-sourced. Add CP-roll caveat. | |
| 5 | Enron: not a one-step cut | **Confirmed.** BBB+ → BBB → BBB− → B− over 3 months. | |
| 6 | SPAC: cite Ritter Table 15c, −64.2% 1-yr EW mean | **Confirmed.** Drop the "−60 to −75" ESTIMATE. | |
| 7 | Run-rate: $65B, not $47B | **Confirmed.** Update `run_rate_series.csv`. | |

### Additional contradictions found in Prompt H that the seven corrections miss

| Item | What the article/card currently says | What Prompt H says | Action |
|---|---|---|---|
| **Nortel write-off** | Card Panel G may reference Nortel $2.1B | Prompt H: Nortel FY01 provisions $887M on $1.35B drawn | **Correct to $887M** unless the $2.1B refers to a different line item (total customer-financing exposure vs. provision). Verify against Nortel FY2001 10-K. |
| **Ritter 2025 first-day return** | Article may cite a different number | 29.3% (2025), 15.3% (2024), 19.0% (1980–2025) | Update if the article uses a stale figure. |
| **2020 cohort 3-yr BHR** | Unknown if cited | −48.1% (mkt-adj −78.6%) | If the article cites 2020-cohort underperformance, use these numbers. |
| **Renaissance IPO index 2022** | Unknown if cited | −57.0% | Useful for the hot-market indicator. |
| **Hyperion terms** | Fig 3 caption may say "SPV" without terms | Now has terms: $27.3B, 6.581%, T+225, A+, 2049, Blue Owl 80/Meta 20 | Update caption. |
| **CoreWeave debt** | Card Panel G may have a stale number | $35,551M principal at 2026-06-30 (Q2-26 10-Q) | Update. |
| **Alphabet raise** | May not be in the article | $84.75B confirmed | Add to Fig 3 caption. |
| **Amodei quote** | Card line 38 may have a paraphrase | Verbatim: "If my revenue is not $1 trillion dollars, if it's even $800 billion, there's no force on earth, there's no hedge on earth that could stop me from going bankrupt if I buy that much compute" | Use verbatim. |
| **Prince quote** | May attribute interviewer as Guerrera | FT July 2007 confirmed; Guerrera unconfirmed | Cite FT, drop interviewer name. |

---

## 10. The Sentence

### Headline for the card at $2T under v1.5

> **At a $2T entry, the median buyer breaks even (IRR ≈ 0%), has a 50% chance of losing money, a 17% chance of losing more than half, and a fair value at a 10% required return of ~$1.26T — meaning the IPO price embeds a 37% premium over the median fair value.**

### The judgment sentence

> **The rating is driven primarily by one calibrated number — the exit-multiple intercept, which the 12-comp ridge fit moves 26% below the v1 prior but which is not statistically distinguishable from it (1.6 bootstrap SEs). If the prior were correct, P(loss) at $2T would be ~35% instead of 50%, and the grade would be one notch higher. Everything else in v1.5 — restatement, mark noise, lockup, GM cliff — moves the rating by less than one notch individually.**

---

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