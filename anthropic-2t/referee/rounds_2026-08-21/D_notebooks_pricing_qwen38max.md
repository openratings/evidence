<!-- model: qwen/qwen3.8-max | prompt_tokens: 42288 | completion_tokens: 13147 | latency_s: 150 | date: 2026-08-21 -->

# TASK D — Referee Review

---

## 1. DID WE PRICE IT?

**Short answer: No. You built a probability-of-hurdle machine, not a pricer.**

The engine takes $2T as a fixed input and asks "what happens from here?" It outputs:

- P(IRR ≥ 35% | $2T entry) = 4.4%
- An IRR/MOIC distribution conditional on $2T
- A fair-value CDF (the `fair35_ipo` array in §5 of W2_engine_review)

What it does **not** output:

- A standalone fair-value point estimate with a confidence band that a reader can compare to $2T without first choosing a hurdle rate.
- A market-clearing multiple. The exit multiple is a **prior** (`mode: prior` in base.yaml, coefficients a=1.20, b=1.60, c=0.90, d=0.60, status **P** in the calibration notes). The entire terminal value rests on coefficients you wrote down, not estimated.
- A decomposition of value by driver (how much of the $3,375B median exit EV is growth, how much is multiple, how much is margin).
- Any treatment of what happens if the IPO is repriced, delayed, or pulled.

The fair-value curve in §5 of W2_engine_review is the closest thing to a price. The array `fair35_ipo = exit_ev × dilution / 1.35^5` is, path by path, the entry price that delivers 35% IRR. Its median **is** the model's fair value at that hurdle. But the notebook never prints `np.percentile(fair35_ipo, [5,25,50,75,95])` as a headline. Instead it reports the percentile at which $2T sits (0.956), which is just P(IRR ≥ 35%) restated geometrically.

**The one extra step.** Add one cell after the fair-value chart in §5:

```python
fv = np.percentile(fair35_ipo, [5, 25, 50, 75, 95])
print(f"Fair-value distribution at 35% hurdle: "
      f"${fv[0]:.0f}B / ${fv[1]:.0f}B / ${fv[2]:.0f}B / ${fv[3]:.0f}B / ${fv[4]:.0f}B")
```

Then repeat at 20%, 25%, 30% hurdles. Present the result as: "The model's median fair value for Anthropic at IPO is $X B, with an interquartile band of $Y–$Z B, at a 35% required return. $2T sits at the 95.6th percentile." That is a price with a band. Without it, the reader has to reverse-engineer the CDF plot.

This is not a cosmetic fix. A hedge-fund quant reading the current notebook sees P(IRR ≥ 35%) = 4.4% and asks "so what's it worth?" The notebook does not answer that question directly.

---

## 2. NOTEBOOK AUDIT

### Notebook 1 — W2_engine_review.ipynb (2026-08-16)

**Role:** Author's results-inspection notebook. The primary deliverable. Should be the one that survives to publication.

**Correct and internally consistent:**
- The Coatue gate passes within tolerance. MOIC 4.407 vs 4.400 (+0.16%), IRR 36.6% vs 35% (+4.71%), ARR $224.002B vs $224B, exit EV $1,993.6B vs $1,995B. All within ±5%. The gate is doing its job.
- The shock incidence check (91.8% of paths hit ≥1 shock over 20 quarters, matching 1−e^{−20×0.125}) is correct.
- The drawdown trigger logic (two consecutive quarters of <30% annualised metered growth) matches the config.
- The fair-value curve arithmetic is correct: 5.75 years from 2026Q1 to 2031Q4 for Coatue, 5.0 years for IPO.
- The sensitivity lattice is correctly structured and the readings are honest.

**Concrete errors and issues:**

1. **Dead code in the regime-scaled growth plot (§2).** The expression `((1+gbar)**0.25*0 + (1+((1+gbar)**0.25-1)*m)**4-1)` contains a `*0` term that contributes nothing. Remove it. It makes the formula look wrong to a reviewer.

2. **The "S-1 confidential" row in the funding table (§1)** has confidence = "VERIFIED-PRIMARY" but all values are NaN. If it is confidential, it is not verified-primary. If it is a placeholder, label it as such. An IPO-desk reviewer will ask why a confidential filing is in a public evidence table.

3. **The comps drawdown comparison in §7 is apples-to-oranges.** The model reports P(≥40% from running peak) = 0.756 and P(≥40% from entry) = 0.357. The comps base rate of 0.86 is from running peak. The notebook then says "mark-noise/regime vol likely too LOW vs comps" but the 0.756 vs 0.86 gap is only 10pp, while the 0.357 vs 0.86 gap is 50pp. The diagnosis should specify which metric is the calibration target. The config comment says "calibrate on Table 2 return paths so that unconditional P(−40% within 8q) matches the comps base rate" — but which P? From entry or from peak? This ambiguity propagates into the mark-noise calibration.

4. **The Coatue gate's g0 = 4.5551 is a curve-fitting artifact, not a growth parameter.** The calibration notes say it was "solved numerically" to hit $224B from $14B in 19 quarters. The notebook presents this without flagging that 455% initial growth is not a meaningful economic quantity. A reader might confuse it with the base-run g0 = 1.50. Add a sentence: "This g0 is a deterministic curve-fit parameter for the gate overlay; it does not represent a growth forecast."

5. **The IRR fan chart (§5) uses `res['VAL']` but the notebook never defines or displays what VAL contains.** Is it the fundamental value (multiple × ARR × NTM adjustment) or the mark-to-market value? The text says "fundamental mark" but the variable name is ambiguous. State the formula.

6. **The sensitivity lattice uses 20k paths vs 100k for the base run.** This is noted in the code but not in the reading. At 20k paths, the standard error on a probability near 0.04 is roughly √(0.04×0.96/20000) ≈ 0.14pp. The difference between P(IRR≥35%) = 0.002 (g0=1, τ=4) and 0.008 (g0=1.5, τ=4) is within noise. Flag this.

7. **No restatement scenario.** Evidence C (§2 below) identifies gross-booking of cloud-reseller flow as the single largest revenue risk (20–40% haircut). The engine has no scenario for this. The entry ARR median of $90B is treated as a lognormal with σ=0.15, but a restatement is not a lognormal shock — it is a discrete reclassification. This is the biggest gap in the notebook.

### Notebook 2 — Engine_v2_Design.ipynb (2026-08-17)

**Role:** Design document. A plan, not a run. Should be kept as a design artefact but clearly labelled "not executed."

**Correct and well-structured:**
- The Mermaid pipeline diagram correctly shows the data flow from inputs through calibration to engine to decision layer to outputs.
- The driver table in §3 correctly maps each driver to its calibration source.
- The decision-layer state diagram (§4) correctly includes the pre-IPO node (on-schedule / repriced / delayed), the lockup, and the Coatue exit policies.
- The "what changes vs v1" table (§7) is honest and well-motivated.

**Issues:**

1. **The LSMC sketch in §4 is too simplified to be useful as a design spec.** It regresses on `[1, price, price², growth, belief, lockup, price×growth]` but does not specify the basis for the continuation value vs the exercise value. In the actual implementation, the choice of basis functions determines whether LSMC converges. The sketch should specify at least the polynomial degree and whether interactions are included.

2. **The MCTS cross-check is listed as a deliverable but the primer (Notebook 3, §3) correctly shows MCTS adds nothing over exact DP for a 4-action, 20-step problem.** The design should either drop MCTS or justify the computational cost. As written, it is a checkbox item that will consume build time for no analytical gain.

3. **The Sobol sensitivity section mentions "the 6 least-identified inputs" but does not name them.** The calibration notes flag g0, τ, the multiple coefficients, the mark noise, the regime transition matrix, and the correlation structure as the least identified. Name them explicitly.

4. **No mention of the gross-booking restatement risk.** Evidence C finding #1 is the single largest tail risk on the revenue line. The v2 design adds substitution, capacity cycles, and token pricing but does not add a revenue-recognition scenario. This is a gap.

5. **The panel section (§5) describes quantile elicitation and log pooling, which directly addresses the pilot diagnosis.** Good. But it does not specify how to prevent the copying behaviour identified in the diagnosis (§7 below). The fix is not just "elicit quantiles over inputs" but "do not include engine outputs in the round-0 evidence pack." The design mentions an "anchoring test = round 0 without model outputs" but does not make this the default.

6. **The Gantt chart (§8) allocates 3 days for "Drivers + t-copula + gate diag."** This is aggressive given that the t-copula requires re-deriving the Cholesky decomposition for the correlated draws and the gate diagnostic needs to be re-run with the new driver set. Budget 5 days.

### Notebook 3 — Quant_Primer.ipynb (2026-08-17)

**Role:** Teaching. Should be kept as a companion document but is not a deliverable for the S-1 pre-registration.

**Correct and well-executed:**
- The backward-induction toy (§1) is clean and the reading is honest about the positive-drift case.
- The American put LSMC (§2, Toy 1) matches the binomial benchmark within 0.7%.
- The particle filter (§4) correctly shows belief lagging the regime switch.
- The Bayesian shrinkage section (§5) uses actual comps_table1.csv and the LOO-RMSE selection is the right method.
- The Gamma-Poisson hazard (§8) correctly shows the posterior is wide after one observation.
- The t-copula section (§9) correctly demonstrates the tail-dependence gap.
- The IPO-desk base rates (§10) are the most valuable section: 100% of 14 comps had ≥40% peak-to-trough drawdown within 8 quarters, yet the median return at last observation was +40.9%. This is the single most important fact for the article.

**Concrete errors:**

1. **The European price print in §2 Toy 1 is wrong.** The line `print(f'European (BS) ≈ {price - (price-bench):.3f}')` computes `price - price + bench = bench`, which is just the binomial American price again. It does not compute the European Black-Scholes price. Either compute it properly with the BS formula or remove the label.

2. **The MCTS toy in §3 has a genuine bug.** The rollout function says `if not bought: entry = S_lat[t,i]`, meaning the rollout after a "wait" action immediately buys at the current node. The rollout cannot distinguish "wait then buy later" from "buy now." This is why the MCTS "wait" value is −16.0 vs the DP value of +19.34 — a 35-point error that the text dismisses as "the rarely-visited 'wait' branch is noisier." It is not noise. The rollout policy is wrong. Fix: the rollout after "wait" should continue with the option to buy at subsequent nodes, not buy immediately. Since this is a teaching notebook, the bug is pedagogically damaging — it teaches the reader that MCTS is unreliable when the actual problem is the implementation.

3. **The shrinkage section (§5) uses `pct_usage_based_rev/100` as a regressor.** The engine config uses `committed_share` with a positive coefficient (d=0.60). Usage-based share is roughly 1 − committed share. The primer's Anthropic input vector uses 0.60 for this regressor, which would mean 60% usage-based (i.e., 40% committed). The config's blended committed share at entry is roughly 38% (weighted across buckets), so 62% usage-based. The numbers are roughly consistent but the sign convention is inverted between the primer and the config, and neither document calls this out. A reviewer will be confused.

4. **The leakage illustration (§6) uses price_ratio = 6 for most buckets without justification.** Evidence D says self-hosting is 6–17× cheaper above 10–50M tokens/month. The 6× is the low end. Show the range.

### Retirement / merge recommendation

- **W2_engine_review** is the keeper. It should be the single results notebook, updated in place.
- **Engine_v2_Design** should be moved to a `docs/` folder and labelled "design, not executed." It should not sit in `notebooks/` alongside executed code.
- **Quant_Primer** should be moved to `docs/` or a separate `tutorials/` folder. It is teaching material, not a research artefact. The LSMC-on-engine-paths toy (§2, Toy 2) is the only part that touches the actual engine output and should be folded into W2_engine_review as a robustness check once the decision layer is built.

---

## 3. ARE THEY UP TO DATE?

The notebooks are dated 2026-08-16/17. They predate Evidence C–F (dated 2026-08-17, published after the notebooks were frozen) and the panel diagnosis (2026-08-21). The following items are now contradicted or need re-running:

**Contradicted by Evidence C:**
1. **Mix.** The config uses Claude Code at 10% of ARR. Evidence C cites Claude Code at ~$8B ≈ 17% of the $47B run-rate. The initial mix vector `{api: 0.45, enterprise: 0.35, claude_code: 0.10, consumer: 0.08, other: 0.02}` needs updating. This changes the committed-share blend and therefore the multiple.
2. **Gross booking.** Evidence C finding #1: cloud-reseller flow is booked gross; a restatement to net could cut headline ARR 20–40%. The engine has no restatement scenario. The entry ARR distribution (lognormal, median $90B, σ=0.15) does not capture this. A 30% restatement drops the median to $63B, which changes every downstream number.
3. **Growth-decay prior.** Evidence C finding #5: every consumption-SaaS comp decayed to sub-30% YoY within 10–14 quarters of hypergrowth. The config's τ=6q (halving every ~1.2 years) is at the optimistic end. The SNOW analogy (174→106→69→36→33) shows deceleration but SNOW never faced the competitive structure Anthropic faces (open-weight substitution, token-price deflation). The τ prior should be widened.
4. **Pricing power.** Evidence C finding #4: Anthropic cancelled a Sonnet 5 price hike. The config's GM drift (+0.4pp/q scale tailwind minus 0.3pp/q deflation drag) assumes net positive margin expansion. The cancelled hike is evidence that pricing power is weaker than assumed.

**Contradicted by Evidence D:**
5. **Token-price deflation.** Evidence D: OpenAI cut GPT-5.6 Luna by 80%. The config's `deflation_drag_per_q: 0.003` (0.3pp/q) may be too small. The Silicon Data SDLLMTK index is down 20% from its May peak. The GM path needs a stress scenario.
6. **Margin cliff.** Evidence D / PitchBook: if GM prints below 35%, fair value compresses 70–81%. The config's GM floor is 25%, but there is no non-linear multiple compression at 35%. The v2 design mentions a "GM<35% cliff" but v1 does not implement it.

**Contradicted by Evidence F:**
7. **No supply-side driver.** The v1 engine has no capacity-cycle regime. Evidence F shows a bifurcated market (frontier shortage, commodity softening). The v2 design adds this but it is not built.

**Contradicted by the panel diagnosis:**
8. **The panel is not an independent check.** The diagnosis shows every seat starts at the engine's base number (0.044) and every subsequent value is a copy of a simulation-request output. The 3× gap between pilot_s1 and pilot_s2 (0.145 vs 0.045) is entirely due to whether the neutral seats happened to request a τ=8 run. The panel as currently constituted is a relay, not a panel. Any notebook section that cites panel results as independent validation is misleading.

**Needs re-running regardless:**
9. The mark-noise calibration (config: `mark_noise_sd_per_q: 0.18`, `mark_ar1: 0.80`). The comps base rate from running peak is 86% (12 of 14 comps); the model produces 75.6%. The gap is flagged in §7 of W2_engine_review but the calibration has not been done.
10. The multiple regression. The config says `mode: prior` and the calibration notes say "replace with comps_table1 regression (#3, #11)." This has not been done. Every exit-EV number in the notebook is conditional on a prior that has not been tested against data.
11. The W3 similarity model results are available (the JSON is provided) but are not referenced in any notebook. The W3 p_dd40_entry (0.363) agrees with W2 (0.357) to within 0.6pp, and the LOO retrodicts for SNOW and CRWV pass. This agreement should be documented in W2_engine_review as a cross-check.

---

## 4. IMPROVEMENTS — TEN MOST VALUABLE CHANGES, RANKED

**1. Replace the prior multiple with the shrinkage regression on Table 1.**
- Cell/section: base.yaml `multiple:` block; W2_engine_review §2 and §4.
- What: Run the regression `log(EV/NTM) = a + b·growth + c·GM + d·committed_share` on comps_table1.csv with ridge shrinkage (the primer §5 already shows how). Replace `mode: prior` with `mode: regression`. Report the posterior coefficient bands.
- Why: This is the single largest source of model risk. The exit EV distribution, the IRR distribution, the fair-value curve, and every headline probability depend on the terminal multiple. A hedge-fund quant's first question will be "where did you get b=1.60?" and the current answer is "we wrote it down." The primer already demonstrates that OLS extrapolation at Anthropic's growth rate is meaningless without shrinkage; the same logic applies to the prior.

**2. Add a revenue-restatement scenario (gross → net booking).**
- Cell/section: base.yaml `entry: arr_usd_b`; W2_engine_review §1 and §4.
- What: Add a discrete scenario: with probability p (estimate 30–50% based on Evidence C), ARR is restated by a factor drawn from Uniform(0.6, 0.8). This is not a lognormal perturbation; it is a one-time level shift at or before IPO. Run the engine under both states and report the headline metrics conditional on each.
- Why: Evidence C identifies this as "the single largest restatement risk to the headline number." A 30% haircut to ARR drops the entry multiple from ~22× to ~32× (on the restated base), which changes the entire return distribution. An IPO-desk reviewer will ask about this before anything else.

**3. Calibrate mark noise to the comps drawdown base rate.**
- Cell/section: base.yaml `multiple: mark_noise_sd_per_q, mark_ar1`; W2_engine_review §7.
- What: Search over (σ_ε, φ) so that the model's P(≥40% drawdown from running peak within 8q) matches the comps base rate of 86% (12/14). Currently the model produces 75.6%. The config comment already identifies this as the calibration target for issue #5/#11.
- Why: The drawdown probability is one of the three headline metrics. If the mark noise is too low, the model understates the probability of a post-IPO crash, which directly affects the IPO-buyer decision. The 10pp gap is not trivial.

**4. Fix the panel protocol so it is not a relay.**
- Cell/section: W9 harness config; the evidence-pack builder.
- What: (a) Remove engine outputs from the round-0 evidence pack. The diagnosis shows every seat starts at 0.044 because E139 = "W2 base run: P(IRR≥35%) = 0.044" is in the pack. (b) Require each seat to submit a prior before seeing any sim results. (c) Change the judge's "evidence" classification: a revision that cites a sim-request output without comparing it to the base case should be classified as "conformity," not "evidence." (d) Use a judge from a different model family than any analyst seat (the diagnosis flags that models.yaml currently points the judge at qwen3.8-max, the same family as the qwen analyst).
- Why: The panel is supposed to be the adversarial check on the engine. The diagnosis shows it is not. If the panel cannot form independent priors, the entire W9 workstream is producing false confidence.

**5. Add the fair-value headline (the "one extra step" from §1).**
- Cell/section: W2_engine_review §5, after the fair-value chart.
- What: Compute and print `np.percentile(fair35_ipo, [5,25,50,75,95])` at multiple hurdle rates (20%, 25%, 30%, 35%). Present as "Model fair value: $X B [p25: $Y B, p75: $Z B] at a 35% required return." Add a table showing how the fair value changes with the hurdle rate.
- Why: Without this, the notebook answers "what is the probability of earning 35%?" but not "what is Anthropic worth?" The second question is what the S-1 pre-registration needs.

**6. Widen the sensitivity lattice to include the multiple and GM.**
- Cell/section: W2_engine_review §6.
- What: The current lattice varies g0 × τ (9 cells). Add a second lattice: exit-multiple scale factor ∈ {0.7, 1.0, 1.3} × GM path shift ∈ {−5pp, 0, +5pp}. This is a 3×3×9 = 81-cell lattice at 20k paths each, which is computationally feasible.
- Why: The sensitivity reading says "g0 and τ dominate every headline number," but this is only true conditional on the prior multiple. If the multiple is off by 30%, the g0/τ sensitivity is second-order. A reviewer will ask "what if your multiple is wrong?" and the current notebook cannot answer.

**7. Implement the GM cliff at 35%.**
- Cell/section: base.yaml `gross_margin:` and `multiple:`; engine code.
- What: If GM < 0.35 at any quarter, apply a multiplicative haircut to the exit multiple (the PitchBook estimate is 70–81% fair-value compression). This is a non-linear trigger, not a smooth drift.
- Why: Evidence D / PitchBook explicitly identifies this threshold. The current GM floor is 25%, but the multiple does not respond non-linearly. A path that drifts to 34% GM gets almost the same multiple as one at 45%, which contradicts the PitchBook finding.

**8. Add the lockup and float to the price path.**
- Cell/section: Engine v2 design §3 (price driver); W2_engine_review §5 (drawdown mechanics).
- What: At the lockup-expiry quarter (roughly q2–q3 post-IPO), apply a supply shock drawn from the comps distribution in the primer §10 (mean −8.6%, median −7.3% in the 10-day window). Scale by float: a 10% float means the lockup supply is large relative to the trading volume.
- Why: An IPO-desk reviewer will not take the model seriously without a lockup. The primer already has the data (13 comps with lockup-window returns). The v1 engine's price path is purely fundamental (V_t/V_0), which ignores the single largest predictable supply event in the first year.

**9. Switch the correlation structure to a t-copula.**
- Cell/section: base.yaml `correlation:`; engine code (the Cholesky draw).
- What: Replace the Gaussian Cholesky with a t-copula at ν=4 (the v2 design already specifies this). The primer §9 shows the joint-tail probability at ρ=0.5 goes from 1.2% (Gaussian) to 1.9% (t, ν=3) for the joint 5% event. At the 5-driver level the effect is larger.
- Why: The growth↔multiple correlation is 0.55, the dominant term. In a Gaussian world, a growth shock and a multiple compression almost never coincide. In reality they do (the 2022 SaaS drawdown was exactly this). The drawdown probability and the P(MOIC<1) number are both understated by the Gaussian assumption.

**10. Integrate the W3 similarity cross-check into W2_engine_review.**
- Cell/section: W2_engine_review, new §7.5 or appended to §7.
- What: The W3 similarity model produces p_dd40_entry = 0.363 (vs W2's 0.357) and p_dd40_peak = 0.752 (vs W2's 0.756). The LOO retrodicts for SNOW and CRWV pass. Add a table comparing W2 and W3 outputs, and note the IQR overlap by quarter from the W3 JSON.
- Why: The W3 model is an independent method (kernel-weighted comps, not Monte Carlo). The agreement is reassuring and should be documented. Currently the W3 results sit in a JSON file that no notebook references.

---

## 5. WHAT MUST BE RE-EXECUTED AND RE-COMMITTED BEFORE S-1 PRE-REGISTRATION

Timeline: 3–4 weeks. In priority order:

**Week 1 — Calibration (blocks everything):**
1. Run the shrinkage regression on comps_table1.csv. Replace the prior multiple coefficients. Commit the fitted coefficients, their posterior bands, and the LOO-RMSE. This is issue #3/#11 in the calibration notes.
2. Calibrate mark noise (σ_ε, φ) to match the 86% comps drawdown base rate from running peak. Commit the calibrated values and the diagnostic plot.
3. Update the entry ARR distribution to include the restatement scenario. Update the mix vector (Claude Code 10% → 17%). Re-derive the committed-share blend.

**Week 2 — Engine re-run:**
4. Re-run the full 100k-path simulation with the updated config. New seed, new config hash. Commit headline.json.
5. Re-run the Coatue gate with the updated ARR trajectory. The gate must still pass. If the updated mix or ARR changes the gate parameters, re-solve g0 for the overlay.
6. Re-run the sensitivity lattice (g0 × τ × multiple-scale × GM-shift). Commit the lattice table and heat-maps.
7. Compute and commit the fair-value distribution at 20%, 25%, 30%, 35% hurdles.

**Week 3 — Panel and cross-checks:**
8. Fix the panel protocol per improvement #4. Re-run at least one 7-round pilot with the corrected protocol. Verify that seats form independent priors and that the terminal dispersion is not a function of which sim requests happened to be made.
9. Integrate the W3 similarity cross-check. Document agreement or disagreement.
10. Run the engine under the restatement scenario and the GM-cliff scenario. Commit conditional headline metrics.

**Week 4 — Freeze and pre-register:**
11. Freeze the config. Record the config hash, seed, and n_paths in the pre-registration document.
12. Write the falsifiable predictions with dated outcomes (e.g., "By 2026Q4, Anthropic's reported ARR will be in the range $X–$Y B"; "The IPO price will imply an EV/NTM multiple in the range A–B×").
13. Commit the SHA-256 hash of the private methodology bundle (YAML, prompts, weights, code) to the public repo before the S-1 drops.
14. Re-execute W2_engine_review end-to-end from a clean checkout. Verify that every cell runs, every number matches headline.json, and no cell depends on a stale `sim/out/` file. Commit the executed notebook.

**Do not skip:** The panel fix (#8) and the multiple regression (#1). Without the regression, every number is conditional on an untested prior. Without the panel fix, the adversarial check is theatre. A reviewer who reads the diagnosis and then sees the panel cited as validation will dismiss the entire project.

---

*Analytical opinion, not investment advice.*