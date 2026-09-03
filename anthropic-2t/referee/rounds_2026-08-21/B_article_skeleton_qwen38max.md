<!-- model: qwen/qwen3.8-max | prompt_tokens: 11489 | completion_tokens: 8896 | latency_s: 177 | date: 2026-08-21 -->

# TASK B — Publication Skeleton (Referee Draft)

Author: Luis M. Sánchez (Toryx / SGX Analytics / OpenRatings). Venue: openratings.ai. Every artifact carries "Analytical opinion, not investment advice."

---

## 1. Section-by-Section Article Skeleton

### §0 — Masthead and Disclosure Block (new; does not exist in v2)

- **First sentence, before the title:** "The author's firm, SGX Analytics, is a paying customer of Anthropic's API. Every growth and margin estimate in this piece should be read as potentially 20% too optimistic because of that relationship. Section §X shows what happens to the conclusions under that haircut." This is not a footnote. It is paragraph one, sentence one. The prior critique (point 1) is unambiguous: bury this and the piece is dead on arrival.
- Byline: Luis M. Sánchez, Toryx / SGX Analytics / OpenRatings. Date. Version hash. Link to GitHub repo, dashboard, SSRN copy.
- Standing disclaimer: "Analytical opinion, not investment advice. No position in Anthropic securities or derivatives. No compensation from Anthropic for this analysis."
- **Missing:** The 20%-too-bullish sensitivity run does not exist yet. It must be computed before publication. If it is not computed, the disclosure is an empty gesture and the reader will notice.

### §1 — The Correction Ledger (replaces v2's opening three paragraphs)

- Keep the three corrections from v2 (Coatue $380B not $360B; leaked underwriting is single-source; "80% metered" is a simplification) but restructure them as a numbered list with a source citation for each, not as narrative prose. The reader needs to see the corrections as a credibility signal, not as a throat-clearing.
- **Update the mix estimate.** v2 says "~45% API, ~35% enterprise, ~10% Claude Code, ~8% consumer." Evidence C (Key Finding 1) says ~80% of the $47B run-rate is API + enterprise, with Claude Code alone at ~$8B (~17%). These are not the same decomposition and the article must say so. State the Sacra/valueaddvc sourcing, flag the Claude Code $8B vs. "~10%" conflict explicitly, and do not resolve it — mark it "unreconciled, see Evidence C."
- **Add the gross-booking risk.** Evidence C Key Finding 1: Anthropic books cloud-reseller (Bedrock/Vertex) end-customer spend on a gross basis; a restatement to net could cut headline ARR 20–40%. This is the single largest restatement risk to every revenue number in the article and v2 does not mention it. It must appear here, before any model output is shown, because every downstream number inherits this uncertainty.
- **Add the Ramp methodology caveat.** Evidence C flags that the "43.5%" figure is not comparable to older "~42% any-AI" numbers because Ramp changed methodology and per-vendor share ≠ total adoption. v2 cites Ramp uncritically ("corporate AI spend up ~4×"). Add the caveat or cut the Ramp citation.
- **Still missing / unverified:** The leaked Coatue underwriting (~$1,995B exit, ~35% IRR, ~$224B 2030 ARR). v2 correctly calls it single-source. Keep that label. Do not promote it to an assumption. The article should say: "We use this only as a gate-check for the Monte Carlo, not as an input."

### §2 — What a $2 Trillion Entry Requires (keep v2 structure, tighten)

- State the arithmetic: $2T entry, 35% IRR hurdle, ~$9.7T enterprise value by late 2031 after dilution, 4.5× in five years. Cite `sim/out/coatue/gate_report.json`.
- State the current run-rate (~$47B, May 2026) and the listing estimate (~$90B). Flag that the $90B is an estimate, not a disclosure, and will be updated when the S-1 is public.
- **Add from Evidence C:** the leaked internal ~$190–200B 2028 projection (Reuters, 2026-08-14, basis unspecified, no 2027 waypoint). Note the missing 2027 waypoint explicitly — the reader needs to see that the projection skips a year.
- **Add from Evidence F:** Anthropic's cost base is locked on multi-year, non-NVIDIA silicon (up to 1M Google TPUs, up to 5 GW AWS Trainium, >$100B/10-yr AWS). This means cheap NVIDIA spot does not cut Anthropic's costs but does arm competitors. State this as a structural asymmetry, not as a prediction.
- **Add from Evidence C Key Finding 2:** Anthropic's compute commitments to clouds are Anthropic's *costs*, not customer revenue floors. v2 does not make this distinction. The article must, because a careless reader will conflate the $100B AWS commitment with a revenue guarantee.
- Figure: `figures/irr_fan.png` (the fan chart of 100k paths). Table: `figures/headline_table.md`.
- **Missing:** The $90B listing revenue estimate has no cited source. Either cite it or label it "author's estimate" with the reasoning shown.

### §3 — The Monte Carlo Engine (methodology summary; full spec in SSRN appendix)

- Five drivers, listed by name with one sentence each: metered growth (regime-switching), revenue-mix drift, gross-margin path (from ~45%), regulatory-access shock (calibrated to June 2026 export episode, 19 days), valuation multiple (reacts to realised growth).
- State the Coatue gate: the engine reproduces the $380B entry arithmetic (4.4×, ~35% IRR, ~$224B 2030 ARR) before running the $2T paths. Cite `sim/out/coatue/gate_report.json`.
- 100,000 paths, seed 20261016, config hash 4fa7a969365f8505. State these. Reproducibility is the point.
- **Add from Evidence D:** the margin path assumption. Compute cost per revenue dollar fell $0.71 → ~$0.56 (Q1→Q2 2026E), implying ~44% gross margin. PitchBook warning: if margin prints below 35%, fair value compresses 70–81%. This must be stated as the downside anchor for the margin driver.
- **Add from Evidence F:** utilisation as the observable proxy for the capacity-cycle driver. Sequoia thresholds: >70% supports the build-out; <50% risks telecom-style writedowns by late 2026. Silicon Data H100/B200 indices become CME-tradeable 2026-10-05 — name this as the real-time signal the dashboard will track.
- **Missing / unverified:** Engine v2 is designed but not built. The article must say "engine v1" and state what v2 changes, or omit v2 entirely. Do not promise a methodology you have not shipped.

### §4 — Headline Numbers (the core results)

- Present the five headline numbers from the HEADLINE NUMBERS table as a single table, not as bullet points. Each row: metric, value, 95% CI if available.
  - P(IRR ≥ 35% from $2T entry, 5y) = 0.044
  - P(−40% within 8q | metered growth <30% two consecutive q) = 0.631 (trigger prob 0.132; unconditional 0.357)
  - $380B entry percentile on fair-value curve = 0.274 (35% hurdle) / 0.047 (20% hurdle)
  - Median IRR / MOIC / exit EV = 0.092 / 1.55 / $3,375B
  - P(MOIC < 1) = 0.241
- **Frame every number as a distribution, never a point.** "The median path earns ~9% a year" is fine. "The stock will be at $X" is not. The prior critique (point G.4) and the decisions list both require this.
- The conditional drawdown claim (63% given the trigger, 36% unconditional) must be presented as a conditional claim with the trigger probability (13.2%) stated. v2 does this. Keep it.
- **The sensitivity lattice gets its own sub-section or figure.** Present the 3×3 grid (g0 × tau) from the SENSITIVITY LATTICE table. Highlight the two extreme cells: g0=1.0, tau=4.0 → P(IRR≥35%) = 0.002; g0=2.0, tau=8.0 → 0.389. The article's claim "under the gentlest decay, ~40%; under the harshest, zero" maps to these cells. State that the entire answer lives in the growth-decay assumption and everything else moves it by single-digit points. Cite `figures/sensitivity_lattice.md`.
- **Add the 20%-vendor-bias sensitivity run here or in §0.** Shave g0 by 20%, re-run, report whether the headline conclusions survive. If they do, say so. If they don't, say that too. This is the single most important credibility move in the article and it does not exist yet.
- Figure: `figures/irr_fan.png`. Table: `figures/headline_table.md`, sensitivity lattice.

### §5 — The Market Lens (similarity model)

- State the method in three sentences: standardise 14 large-tech IPOs on at-listing features, kernel-weight by similarity to Anthropic-at-IPO, resample 8-quarter post-IPO paths. Cite `similarity/out/summary.json`.
- Report the effective sample size: n_eff = 7.94 out of 14. Name the weights: BABA 0.148, CRWV 0.132, UBER 0.125, DASH 0.124, META 0.124, ARM 0.121, SNOW 0.113, KLAR 0.113. Note that PLTR, RIVN, ABNB, RDDT, CRCL, FIG got zero weight. This is important: the reader needs to see which comps were excluded and why.
- LOO validation: SNOW retrodicts the 2022 consumption re-rating (pred p_dd40_peak 0.771, real 0.589, 100% quarters inside band). CRWV retrodicts the post-IPO drawdown (pred 0.761, real 0.561, 80% quarters inside band). State both. Cite `figures/loo_validation.png`.
- Agreement zone: W2 p_dd40_entry 0.357 vs W3 0.363; W2 p_dd40_peak 0.756 vs W3 0.752. "Tail agreement, median disagreement." Cite `figures/agreement_zone.png`.
- **State the median disagreement honestly.** The W3 q8 percentiles are shifted upward relative to W2 (W3 median at Q8: +0.426 vs W2: +0.086). The market lens is more optimistic about where the stock sits after two years. Do not smooth this over.
- **Missing:** The IQR overlap by quarter ranges from 0.327 to 0.769. The Q2 overlap (0.327) is weak. Flag this. Do not present the agreement as uniform across the horizon.

### §6 — The Adversarial Panel: What It Did and Did Not Establish (replaces v2's empty §)

This is the section that requires the most surgery. The panel diagnosis is damning and the article must confront it.

- **Do not write "twelve adversarial analysts reviewed this."** The diagnosis shows the panel relayed engine outputs, did not form independent priors, and the 3× gap between pilot_s1 and pilot_s2 is entirely an artifact of which simulation the neutral seats happened to request. The panel is not a review. It is a stress-test of the engine's sensitivity to parameter perturbations, mediated by language models. Say that.
- **Publish the disagreement log.** This is the decisions list and it is the right call. The log is interesting *because* it shows the panel failing to converge, not because it shows agreement. Frame it as: "Here is where the models disagreed, here is what they cited, here is what the judge accepted, and here is why we think the judge's acceptance criterion was too weak."
- **State the structural findings from the diagnosis:**
  - Every seat starts at the engine's base number (0.044). No independent prior was formed.
  - Every later value is a copy of a simulation-request output to three decimals.
  - The "all-seat" median is structurally the neutral median (4+4+4 seats; bulls above, bears below).
  - Convergence did not happen; the stopping rule fired on stasis. Dispersion rose every round.
  - The judge classified "S-2-9 reports 0.145, I now say 0.145" as evidence-driven revision. It is a copy, not a weighing.
- **State what you will change for the production run:** parameter bounds (already added in s2), judge model change (flagged: models.yaml now points judge at qwen/qwen3.8-max, same family as the qwen analyst — this must be resolved before the production run or disclosed as a limitation), independent prior elicitation before the evidence pack is shown.
- **If the production panel is not run before publication, cut this section to a methodology note and publish the pilot logs as a supplementary artifact.** Do not present pilot results as findings.
- **Missing:** The production panel protocol. The judge conflict-of-interest (qwen judging qwen). The resolution of the s1 absurd run (S-0-1, g_term=1.8 → p35=1.0) and whether the parameter bounds in s2 are sufficient.

### §7 — The Regulatory and Structural Tail (expand v2's §)

- June 2026 export order: 19-day global disablement, calibrated as ~12% per-quarter hazard. Keep. Cite the event.
- EU Cyber Resilience Act SBOM obligations: start September 2026, full bite end-2027. US federal SBOM mandates projected early 2027. Keep.
- **Add from Evidence D:** the substitution threat is real but bounded. Open-weight models lag the closed frontier by ~4 months / 8 ECI points (Epoch AI, Jun-2026; 90% CI 7–11 points). 88% of enterprise LLM API spend still flows to three US vendors. Anthropic at 40% enterprise share (Menlo Ventures, Dec-2025). Anthropic leads coding at 54% vs OpenAI's 21%. State this as the bound on the substitution tail.
- **Add from Evidence D:** token-price deflation is violent and two-sided. OpenAI cut GPT-5.6 Luna 80% (2026-07-30). DeepSeek *raised* V4 prices up to ~1,100% (2026-08-16) under capacity strain. Silicon Data blended SDLLMTK index at 1.62, down ~20% from May-2026 peak. This is not a monotonic deflation story. The article must say so.
- **Add from Evidence C:** pricing power is ambiguous. Anthropic cancelled the Sonnet 5 hike ($2/$10 → $3/$15) on Aug-10-2026 while up-tiering Claude Code out of the $20 Pro plan (Apr-21-2026). A new tokenizer (Opus 4.7+) raises effective prices ~35% independent of sticker rates. This is a genuine insight and v2 misses it entirely.
- **Add from Evidence F:** the capacity cycle is bifurcated. Shortage at the frontier and on power (H100/H200 rentals re-tightened +38–56% since Oct-2025; HBM/CoWoS sold out through 2027; 5–7 yr grid interconnect). Early softening at the commodity edge (GPU forward curves in backwardation). Physical shortage resolves no earlier than 2028 on power, mid-2027 on packaging. Anthropic is hedged against shortage, exposed to glut.
- Figure: none currently exists for this section. **Missing:** a timeline graphic of regulatory milestones and capacity-cycle thresholds would help. Not essential but recommended.

### §8 — What Would Change My Mind (keep, sharpen)

- Keep the three falsifiers from v2: growth half-life of two years instead of eighteen months; majority of revenue under multi-year commitments; gross margin at 60% by 2028.
- **Add a fourth:** S-1 discloses net revenue booking (not gross) for cloud-reseller flow, cutting headline ARR by 20–40%. This is the Evidence C restatement risk and it is falsifiable the day the S-1 drops.
- **Add a fifth:** IPO delayed beyond Q1 2027 or cancelled. This is the decisions list requirement. State what the model says in that scenario: the pre-registered predictions void, the analysis is archived, and a follow-up note is published within 30 days of the delay/cancellation announcement.
- Tie each falsifier to a specific pre-registered prediction in §10 below. The reader should be able to check each one against a dated, sourced resolution.

### §9 — The 20% Vendor-Bias Sensitivity Run (new section; required by decisions list)

- Run the full Monte Carlo with g0 shaved by 20% (to proxy for the possibility that SGX Analytics' operational familiarity with Claude makes growth estimates systematically optimistic).
- Report: does P(IRR ≥ 35%) change materially? Does the conditional drawdown probability change? Does the $380B percentile shift?
- If the conclusions survive: "Our headline findings are robust to a 20% growth haircut, which is our best estimate of the maximum vendor-bias effect." If they don't: say that, and say which conclusions break.
- **This section does not exist yet. It must be computed before publication. It is the single highest-priority missing artifact.**

### §10 — Pre-Registered Predictions (new section; the core of the pre-registration)

- List every prediction from §11 below (this document) as a numbered, dated, sourced item.
- Each prediction: exact phrasing, distribution or range (never a point), resolution date, data source, resolution criterion.
- State: "These predictions were frozen on [date], 3–5 days before the expected public S-1 filing. They will be scored in the week the S-1 is public. The scorecard will be published as a separate artifact on openratings.ai and GitHub."
- **This section is the article's reason to exist.** Without it, the piece is a valuation blog post. With it, the piece is a calibration exercise. The prior critique (point 3) is correct: the pre-registration framing is the headline.

### §11 — Closing

- Two sentences. No new information.
- "The headline is the bait. The meter is the trap."
- Disclaimer: "Analytical opinion, not investment advice."

### Appendix — Traceability Table (keep, expand)

- Keep the v2 table. Add rows for:
  - Evidence C–F sources (Reuters, Sacra, Menlo Ventures, Epoch AI, PitchBook, Silicon Data, Sequoia, Ramp).
  - The sensitivity lattice (`figures/sensitivity_lattice.md`).
  - The panel pilot logs (`deliberation/runs/pilot_s1/`, `deliberation/runs/pilot_s2/` — public copies).
  - The 20% vendor-bias sensitivity run (artifact TBD).
  - The pre-registration file (GitHub, timestamped).
- **Remove:** the row "Panel trajectories, revisions, register — deliberation/runs/pilot_s*/ (private)." The pilots are not private if you are publishing the disagreement log. Either make them public or do not cite them.

---

## 2. SSRN Methodology Appendix Skeleton

**What is disclosed in prose:**

- Full specification of the five Monte Carlo drivers: functional forms, regime-switching rules, parameter distributions, calibration sources. The reader must be able to reproduce the engine from this text plus the GitHub repo.
- The Coatue gate: exact arithmetic, what it checks, what it does not check.
- The similarity model: kernel choice, bandwidth (6.21), feature set, weighting scheme, LOO protocol. State n_eff = 7.94 and which comps got zero weight and why.
- The sensitivity lattice: the 3×3 grid, what g0 and tau mean, why those ranges were chosen.
- The panel protocol: number of models, seats, rounds, judge, scoring rule, stopping rule. State what the pilot revealed (relay, not review; stasis, not convergence). State the judge conflict (qwen judging qwen) and what was done about it.
- The pre-registration protocol: what was predicted, when it was frozen, how it will be scored, what counts as a hit/miss/partial.
- The 20% vendor-bias sensitivity: methodology, result, interpretation.
- All data sources with access dates. The 14-comp table, the funding-rounds CSV, the run-rate series, the GPU anchors.
- The "IPO delayed/cancelled" scenario: how the predictions void, what the follow-up protocol is.

**What is withheld:**

- The exact API endpoints and rate limits of the SGX Analytics live data feed. These are a product asset. State that the data are available via the SGX Analytics API and GitHub CSVs (frozen daily from 2026-08-17), but do not publish the endpoint URLs or authentication scheme.
- The proprietary scoring model used by OpenRatings for the dashboard's live probability updates, if it differs from the Monte Carlo engine. State that it exists, state its inputs, do not publish its weights.
- Any internal Anthropic data that SGX Analytics may have access to as a customer. State explicitly: "No non-public Anthropic data were used in this analysis. All revenue and mix figures are sourced from public reporting, leaks attributed by name, or the company's own disclosures." If this is not true, do not publish.
- The specific open-weight model identifiers used in the panel, beyond what is in `models.yaml`. Name the model families (e.g., "a Qwen-family model," "a GPT-OSS model") but do not publish exact checkpoint hashes if they reveal proprietary fine-tuning.

**What is flagged as a limitation:**

- Engine v2 is designed but not built. All results are engine v1.
- The panel pilots are diagnostic, not confirmatory. They show the protocol's failure modes, not its success.
- The $90B listing revenue estimate is an author's estimate, not a disclosure.
- The leaked Coatue underwriting is single-source and unverified.
- The gross-booking risk (Evidence C) means every revenue number could be 20–40% lower.
- The similarity model's Q2 IQR overlap is 0.327, which is weak.

---

## 3. Pre-Registered Predictions

Each prediction is phrased to resolve unambiguously. All are distributions or ranges, never point targets. All carry "Analytical opinion, not investment advice."

| # | Prediction | Phrasing | Resolution date | Data source | Resolution criterion |
|---|---|---|---|---|---|
| P1 | S-1 revenue (TTM or LTM) | "We predict Anthropic's S-1 will disclose trailing revenue in the range $35B–$60B. We assign 70% probability to this range. If gross-to-net restatement applies, we predict the restated figure will be 60–80% of the gross figure." | Week of public S-1 filing (expected Sep 2026) | SEC EDGAR, S-1 filing | Range check on disclosed revenue. Binary on restatement. |
| P2 | S-1 revenue mix | "We predict the S-1 will disclose that ≥70% of revenue is API + enterprise (broadly defined), and that no single customer exceeds 15% of revenue. We assign 60% probability to both conditions jointly." | Week of public S-1 filing | SEC EDGAR, S-1 filing | Binary on each condition. |
| P3 | S-1 gross margin | "We predict the S-1 will disclose a gross margin between 35% and 55%. We assign 75% probability to this range." | Week of public S-1 filing | SEC EDGAR, S-1 filing | Range check. |
| P4 | Revenue growth at listing | "We predict YoY revenue growth at listing will be between 80% and 200%. We assign 70% probability to this range." | Week of public S-1 filing | SEC EDGAR, S-1 filing; if not disclosed, computed from S-1 revenue figures and prior-year comparables | Range check. |
| P5 | First-day close | "We predict the first-day closing market cap will be between $1.2T and $3.0T. We assign 80% probability to this range. We do not predict a point price." | First trading day | NYSE/NASDAQ closing price, shares outstanding from S-1 | Range check on implied market cap. |
| P6 | 8-quarter drawdown | "We predict a ≥40% peak-to-trough drawdown within 8 quarters of listing with probability 0.75 (±0.10). We predict a ≥40% drawdown from the IPO price within 8 quarters with probability 0.36 (±0.10)." | 8 quarters post-listing (≈Q4 2028) | Daily closing prices from NYSE/NASDAQ via SGX Analytics API | Binary on each threshold. Scored as calibration: was the outcome inside the predicted probability band? |
| P7 | Lockup expiry | "We predict the stock will be within ±25% of its pre-lockup-expiry price on the 10th trading day after lockup expiry. We assign 65% probability to this range." | 10 trading days post-lockup-expiry (expected ~Apr 2027) | NYSE/NASDAQ closing prices; lockup date from S-1 | Range check. |
| P8 | Growth decay | "We predict that Anthropic's YoY revenue growth will fall below 50% within 6 quarters of listing. We assign 65% probability to this." | 6 quarters post-listing | Quarterly earnings reports (10-Q), SEC EDGAR | Binary. |
| P9 | IPO delayed or cancelled | "We assign ≤15% probability that the IPO is delayed beyond Q1 2027 or cancelled entirely. If this occurs, predictions P1–P8 are voided and a follow-up note is published within 30 days." | Q1 2027 | SEC EDGAR (no effective S-1), press reports | Binary. |
| P10 | Gross-to-net restatement | "We assign 30% probability that the S-1 discloses revenue on a net basis for cloud-reseller flow, or includes a risk factor that explicitly quantifies the gross-to-net gap at ≥15%." | Week of public S-1 filing | SEC EDGAR, S-1 filing | Binary. |

**Scoring protocol:** Published the week the S-1 is public (for P1–P4, P10) and at each subsequent resolution date. Scorecard format: prediction, predicted range/probability, realised outcome, hit/partial/miss, Brier score where applicable. Published on openratings.ai, GitHub, and SSRN.

**What is not predicted:** A specific IPO price. A specific first-day return. A buy/sell/hold recommendation. Any prediction phrased as "the stock will be at $X."

---

## 4. What in Draft v2 Must NOT Survive into v3

These are items that are wrong, unsupported, or contradicted by Evidence C–F or the panel diagnosis. Cut them or rewrite them.

**4.1 — The panel section as written.** v2 says "I then handed the identical evidence pack … to a panel of open-weight language models playing bull, bear and neutral, roles rotating each round, judged by a separate open-weight model that accepted a score revision only when it was tied to cited evidence." Then: "[PANEL RESULTS — filled from deliberation/runs/pilot_s1, pilot_s2]." This entire framing must go. The diagnosis shows: (a) no seat formed an independent prior; (b) every reported number is a copy of an engine output; (c) the judge's "evidence" criterion accepted copies as reasoning; (d) convergence was stasis; (e) the 3× gap between pilots is a seed-and-seat-assignment artifact. You cannot present this as adversarial review. You can present it as a diagnostic of a protocol that did not work as intended, and that is genuinely interesting. But the v2 framing is a credibility risk that will be exposed the moment anyone reads the run logs.

**4.2 — "Twelve adversarial analysts."** This phrase appears in the v2 heading. Kill it. The panel is four models in rotating seats, not twelve analysts. The number 12 is seats, not independent agents. The prior critique (point 2) already flagged "reviewed by six models" as misleading. "Twelve adversarial analysts" is worse. Replace with a description of what actually happened: "Four open-weight models, rotating through bull/bear/neutral seats over seven rounds, with a separate judge model."

**4.3 — The mix estimate "~45% API, ~35% enterprise, ~10% Claude Code, ~8% consumer."** Evidence C says ~80% is API + enterprise, with Claude Code at ~$8B (~17%). The v2 decomposition and the Evidence C decomposition are not the same and cannot both be right. The Claude Code figure alone (17%) exceeds the v2 "10%" and the v2 "consumer" bucket (8%) is not clearly defined in any source. Either reconcile these with explicit sourcing or present both and mark the discrepancy. Do not present the v2 numbers as settled.

**4.4 — "Ramp's data show corporate AI spend up ~4× in the year to February 2026."** Evidence C flags that Ramp changed methodology and that per-vendor share ≠ total adoption. The "~4×" figure and the "43.5%" figure are not comparable to earlier Ramp numbers. If you cite Ramp, add the methodology caveat. If you cannot verify the ~4× claim against the post-methodology-change data, cut it.

**4.5 — The implicit treatment of Anthropic's compute commitments as demand-side.** v2 does not explicitly conflate them, but the absence of the distinction is a problem. Evidence C Key Finding 2 is explicit: the >$100B AWS commitment, the Google TPU deal, the ~$30B Azure commitment are Anthropic's *costs*, not customer revenue floors. v3 must state this. If any reader of v2 could interpret these as demand signals, the text is misleading by omission.

**4.6 — The absence of gross-booking risk.** v2 does not mention it. Evidence C identifies it as the single largest restatement risk (20–40% of headline ARR). Every revenue number in the article inherits this uncertainty. Omitting it is not a stylistic choice; it is a material omission that undermines the analysis.

**4.7 — The absence of the capacity-cycle asymmetry.** v2 does not discuss the fact that Anthropic's locked-in non-NVIDIA silicon means cheap GPU spot does not help Anthropic but does help competitors. Evidence F is explicit. This is a structural risk to the margin path and the competitive moat, and v2 ignores it.

**4.8 — The absence of the pricing-power ambiguity.** v2 does not mention the cancelled Sonnet 5 hike, the Claude Code up-tiering, or the Opus 4.7+ tokenizer effect (~35% effective price increase). Evidence C Key Finding 4 documents all three. The article's margin-path assumption depends on pricing power, and the evidence says pricing power is ambiguous. v2 presents it as settled.

**4.9 — The Coatue underwriting leak treated as a calibration anchor.** v2 says the engine "had to reproduce Coatue's own arithmetic from a $380B entry — 4.4×, ~35% IRR, ~$224B 2030 ARR — and it does." This is fine as a gate-check. But the $224B 2030 ARR figure comes from the single-source leaked underwriting. If the gate-check is calibrated to a single-source number, the gate is only as good as the source. v3 must say: "The gate reproduces the leaked underwriting's arithmetic. The underwriting is single-source and unverified. The gate checks internal consistency, not external validity."

**4.10 — The closing line survives.** "The headline is the bait. The meter is the trap." Keep it. It is the best line in the piece and it earns its place. Do not bury it in a paragraph. Let it stand alone.

---

*Analytical opinion, not investment advice.*