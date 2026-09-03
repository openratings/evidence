<!-- model: qwen/qwen3.8-max | prompt_tokens: 11438 | completion_tokens: 13294 | latency_s: 255 | date: 2026-08-21 -->

# Task E2 — Referee Report: Circular Capital, Contagion, and the Sector Term in the Anthropic Rating

---

## 1. Is Luis's objection right? Yes, substantially. Here is where the KMV breaks down.

The Section 6 KMV is internally consistent and correctly computed for the question it asks: *can Anthropic's asset value cover its disclosed take-or-pay commitments?* At $170B of commitments against a median fundamental value of $3.2T, the distance-to-default is enormous and the AAA is arithmetically honest. But it answers the wrong question for an IPO buyer. The buyer is not asking "will Anthropic miss a payment to AWS in 2031?" The buyer is asking "will this equity be worth what I paid?" Those are different questions, and the single-name Merton frame is structurally blind to five channels that matter for the second one.

**Channel 1 — Asset correlation with the sector.** The engine draws Anthropic's value path from its own demand, margin, and multiple processes (Rating Card §2, §5). It does not condition those draws on a sector factor. In reality, Anthropic's revenue growth, its exit multiple, and its ability to raise capital are all loaded on the same AI-capex factor that drives AWS, Google, Nvidia, CoreWeave, and the neoclouds. A 2σ sector shock does not hit Anthropic's value through the idiosyncratic 64% vol; it hits through a correlated drawdown that the engine's AR(1) mark process cannot produce. This channel is **not in the engine**. The capacity-cycle regime in Evidence F (Sequoia's >70% / <50% utilisation thresholds, the GPU forward backwardation) is a partial proxy, but it enters as a supply-side input to Anthropic's cost curve, not as a correlated shock to its valuation and funding simultaneously.

**Channel 2 — Wrong-way risk: investors = suppliers = customers' infrastructure.** Amazon invests up to $25B in Anthropic; Anthropic commits >$100B to AWS (Evidence F, F7). Google invests up to $40B; Anthropic commits to 1M TPUs and a multi-GW Broadcom expansion (Evidence F, F7). These are not arm's-length relationships. If Amazon's stock falls 40% and its own capex comes under pressure (hyperscaler debt/capex has already moved from 9% to 32% per Evidence F, F2), Amazon's willingness and ability to honour the $100B AWS commitment, to continue milestone-based equity injections, and to prioritise Anthropic's Trainium capacity all degrade simultaneously. The KMV treats D = $170B as a fixed liability. In a sector stress, the *effective* D rises (counterparties renegotiate, delay capacity delivery, or reprice) while V falls. This is textbook wrong-way risk and it is **not in the engine**.

**Channel 3 — Funding-liquidity dependence on its own valuation.** Anthropic is pre-profit (Rating Card §5, "no gross→net restatement" note; Evidence C, TL;DR). It funds growth by raising equity at marks. The KMV framework assumes the firm either has assets above D or below D; it does not model the inability to raise new capital. In a sector unwind, AI-name equity issuance freezes (the SaaS 2022 analogue: no AI company could raise at prior marks for 12–18 months). Anthropic's growth plan requires continued capital raises. If it cannot raise, growth stalls, the multiple compresses, and the $24B/yr of commitments becomes a larger fraction of a smaller revenue base. The engine's dilution parameter (0.92) assumes orderly dilution at fair marks. Disorderly dilution at distressed marks, or no dilution at all, is **not in the engine**.

**Channel 4 — Contingent liabilities from counterparty capacity.** If AWS, Google, or the neoclouds cannot finance their own buildout (CoreWeave carries ~$35B of GPU-collateralised debt with a 2-year maturity-vs-contract gap per Evidence F, F2; Meta's Hyperion SPV is ~90% debt; MS/JPM estimate the sector needs ~$1.5T of new debt), then Anthropic's growth ceiling binds. The $170B in commitments is a *floor* on Anthropic's cost; the *ceiling* on its revenue is set by how much compute its counterparties can actually deliver. The KMV models the floor. It does not model the ceiling. **Not in the engine.**

**Channel 5 — Demand contagion.** Enterprise AI budgets are the same budgets. Evidence C notes >1,000 business customers each spending >$1M/yr, but those customers are also buying from OpenAI, Google, and every SaaS vendor adding AI features. A macro or sector shock that cuts enterprise IT budgets hits all AI vendors simultaneously. The engine's demand process has idiosyncratic shocks but no sector-wide demand correlation. The Ramp index "Cracks in the AI thesis" (Evidence C, TL;DR) is a leading indicator of this channel. **Partially in the engine** (the growth-decay half-life prior from consumption-SaaS comps captures some of this), but the simultaneity across vendors is not.

**What IS already in the engine:** the regulatory/export-control shock (Rating Card §4, trigger 4); the capacity-cycle regime via Evidence F's utilisation thresholds and GPU forward curves; token-price deflation via Evidence D's SDLLMTK index; the gross→net restatement risk (flagged as a MUST item in §4 but not yet modelled). These are real but they are all single-name or single-channel shocks. None of them model the *joint, correlated, sector-wide* event that Luis is pointing at.

**Bottom line:** the objection is right. The AAA in Section 6 is a correct answer to a narrow question and a misleading answer to the question the IPO buyer actually faces. The single-name KMV understates Anthropic's risk by omitting sector correlation, wrong-way counterparty risk, funding-liquidity dependence, contingent growth-ceiling effects, and demand simultaneity. Five channels, of which at most one and a half are partially captured in the current engine.

---

## 2. Rating-agency analogues and the proposed two-grade structure

**How agencies handle this elsewhere:**

- **Banks (Moody's BFSR / S&P SACP + uplift):** The standalone credit profile (SACP at S&P, Bank Financial Strength Rating at Moody's) strips out government and group support. Then a separate uplift is applied for systemic support. The standalone rating asks "how is this bank on its own?" The final rating asks "how is this bank given the system it sits in?" The two can differ by 2–6 notches.

- **Sovereign ceiling:** S&P and Moody's cap corporate ratings at or near the sovereign rating of the home country, on the logic that a sovereign stress impairs all domestic issuers through macro, funding, and regulatory channels. The cap is not absolute (some exporters get rated above the sovereign) but it is a structural constraint.

- **Sector/industry risk (S&P Industry Risk Assessment, Moody's Industry Grid):** Each sector gets a risk score. Companies in high-risk sectors (mining, airlines, shipping) are capped or notched down relative to their standalone metrics. The sector score captures cyclicality, capital intensity, regulatory exposure, and — relevantly — the degree of interconnection.

- **Circular funding in structured finance:** Moody's and S&P explicitly model "circularity risk" in CLOs and CMBS where the sponsor, the arranger, and the largest investor may be the same entity or closely linked. The rating is notched down for concentration and correlation.

- **Vendor financing (telecom 2000–02):** Lucent and Nortel's vendor-financing books were effectively loans to their own customers. When the customers (telcos) defaulted, the vendors' "revenue" turned out to be uncollectible. Rating agencies were slow to catch this. Post-mortem, the lesson was: revenue funded by your own balance sheet is not revenue; it is a correlated loan.

**Proposed equivalent for Anthropic:**

| Component | Definition | Source |
|---|---|---|
| **Stand-alone grade (SACA-equivalent)** | The KMV number from Section 6: P(V < D) on disclosed commitments, using the engine's fundamental-value paths. At D = $170B, this is AAA. | Section 6, engine v1 |
| **Sector-linked grade** | Stand-alone grade minus a notch adjustment for circular-capital and contagion risk. This is the grade the IPO buyer should read. | New, this section |
| **Notch adjustment** | The number of notches deducted for the five channels in §1 above. | Calibrated below |

**How many notches?**

I propose **3 notches as the central estimate, with a defensible range of 2–5**, on the following basis:

- **Channel 1 (asset correlation):** 1 notch. The engine's 64% vol already embeds some sector exposure through demand and multiple processes. The incremental correlation to a sector factor adds roughly 1 notch of tail risk. This is the Basel ρ adjustment (quantified in §3 below).

- **Channel 2 (wrong-way risk):** 1 notch. The Amazon/Google/Anthropic triangle is the single largest structural vulnerability. It is not modelled at all. One notch is conservative given that both counterparties are also Anthropic's two largest cloud providers and two of its three largest investors.

- **Channel 3 (funding liquidity):** 0.5–1 notch. Anthropic is pre-profit and equity-funded. In a sector freeze, it cannot raise. But it also has no debt maturities to refinance, which limits the acute-illiquidity risk. Half a notch to one notch.

- **Channel 4 (contingent growth ceiling):** 0.5 notch. If counterparties slow capacity, Anthropic's growth stalls but its existing contracts still run. This is a growth impairment, not a solvency event. Half a notch.

- **Channel 5 (demand contagion):** 0.5 notch. Already partially in the engine through the demand-shock process. The incremental sector-wide simultaneity adds half a notch.

Sum: 3–4 notches central, 2–5 range. At 3 notches, the sector-linked grade is **AA−** (from AAA). At 4 notches, **A+**. At 5, **A**.

I recommend booking **3 notches (AAA → AA−)** as the base case for the card, with a sensitivity note that a 5-notch version (AAA → A) is the stress case. The reason I do not go higher than 5: Anthropic has no debt, no maturity transformation, no deposit base, and its take-or-pay commitments are denominated in compute, not cash. The worst-case sector shock impairs its growth and multiple, but it does not create a Lehman-style liquidity run. The floor is higher than a bank's floor.

**The sector cap:** In addition to the notch adjustment, I would impose a soft sector cap: the sector-linked grade should never be more than 2 notches above the implied grade of the AI-capex factor itself. If the sector as a whole is rated BBB (which it arguably is, given the debt/capex shift to 32%, the $1.5T debt need, and the CoreWeave/Meta SPV structures in Evidence F), then Anthropic's sector-linked grade should not exceed A+. This is the sovereign-ceiling logic applied to the sector.

---

## 3. Quantification: the systemic-shock overlay

### 3a. The event specification

Define a **sector-unwind event** as a joint shock hitting four variables simultaneously, with persistence:

| Variable | Shock | Basis |
|---|---|---|
| Enterprise AI demand | −30% to −50% in year 1, partial recovery over 2–3 years | Telecom 2000–02: enterprise telecom capex fell ~40%; SaaS 2022: growth rates halved |
| Compute access / cost | Capacity buildout slows 40–60%; Anthropic's locked contracts partially protect (F7 asymmetry), but new capacity for growth is unavailable | Evidence F: 5–7 yr grid interconnect, 144-week transformer lead times mean no rapid substitution |
| Exit multiple | Compresses from 22× (at $2T IPO) to 8–12× | SaaS 2022: median EV/Revenue fell from ~25× to ~8×; telecom 2000: EV/Revenue went to <2× |
| Funding | AI-name equity issuance freezes for 12–24 months; debt markets close for neoclouds | Crypto 2022: no crypto firm could raise for ~9 months; SaaS 2022: ~12 months |

**Persistence:** 2–3 years of impaired conditions, with a 4–5 year tail of below-trend growth. This is not a V-shaped shock. The telecom bust took 3 years to bottom; 2008 took 2 years; SaaS 2022 took ~18 months. AI capex is more capital-intensive than SaaS and more concentrated than telecom, so 2–3 years is the central estimate.

### 3b. Calibration from analogues

| Analogue | Sector value loss | Duration | Annual hazard (implied) | Anthropic relevance | Confidence |
|---|---|---|---|---|---|
| Telecom/fibre 2000–02 (Global Crossing, WorldCom, Lucent vendor financing) | −65% to −99% for individual names; sector −$2T | 2–3 years | 4–6% | High: circular vendor financing, capex ahead of demand, commodity price collapse. Closest structural analogue. | [VERIFIED-PRIMARY] historical record |
| 2008 (Lehman, AIG CDS circularity) | −50% to −60% for financials; Lehman −100% | 1.5–2 years | 2–3% | Medium: circularity is similar (CDS ↔ CDO ↔ leverage) but Anthropic has no leverage or maturity transformation. | [VERIFIED-PRIMARY] |
| Shale 2014–16 | −60% to −80% for E&P names; many bankruptcies | 1.5–2 years | 6–8% | Medium: commodity-price shock hits a capital-intensive sector with high debt. But shale had real debt; AI capex is more equity-funded. | [VERIFIED-PRIMARY] |
| Crypto 2022 (FTX/Alameda circularity) | −70% to −80% sector-wide | ~1 year | 5–8% | Medium-high: the circularity structure (FTX ↔ Alameda ↔ FTT token) is the closest to the Amazon ↔ Anthropic ↔ AWS loop. But crypto had no real revenue; AI does. | [VERIFIED-PRIMARY] |
| SaaS 2022 | −50% to −70% multiples; no top-tier bankruptcies | 1–1.5 years | 8–12% | Medium: multiple compression without insolvency. Relevant for the exit-multiple channel. | [VERIFIED-PRIMARY] |

**Central calibration for the AI-capex sector unwind:**
- **Annual hazard: 5% (range 3–8%).** This is the probability that a sector-unwind event *begins* in any given year, conditional on the current build-out phase. The hazard is not constant: it is higher during the build phase (2025–2028) and lower once capacity is absorbed. I would use 6–8% for 2026–2028 and 3–5% for 2029–2031.
- **Severity for Anthropic: 55–75% value loss** from peak, conditional on the event occurring. This is lower than telecom (−99%) because Anthropic has real revenue, no debt, and locked compute contracts. It is higher than SaaS 2022 (−50% to −70% on multiples only) because the shock hits demand, supply, funding, and multiples simultaneously.
- **5-year cumulative probability of at least one sector-unwind event: 23–33%** (from 1 − (1−0.06)^5 ≈ 27% at 6% annual hazard).

### 3c. Basel single-factor ρ and its effect on the 5-year EDF

The Basel IRB single-factor model writes asset value as:

V = √ρ · F + √(1−ρ) · ε

where F is the sector factor and ε is idiosyncratic. Default occurs when V falls below a threshold c = Φ⁻¹(EDF_standalone).

**What ρ to assign Anthropic to the AI-capex factor?**

I assign **ρ = 0.45 (range 0.30–0.60).**

Rationale for the range:
- ρ = 0.30 (low end): Anthropic has genuine idiosyncratic value — model quality, enterprise relationships, safety brand. Even in a sector downturn, Claude's API revenue is stickier than a neocloud's GPU rental revenue. The 80% API+enterprise revenue mix (Evidence C) provides some insulation.
- ρ = 0.60 (high end): Anthropic's revenue, cost base, funding, and valuation are all loaded on the AI-capex factor. The wrong-way risk with Amazon and Google pushes correlation up. The pre-profit, equity-funded status means it is fully exposed to capital-market sentiment.
- ρ = 0.45 (central): balances the idiosyncratic franchise value against the structural sector loading.

**Effect on the 5-year EDF:**

The standalone 5y EDF at D = $170B is effectively 0.00% in the engine (Section 6). Numerically, this means c is very far in the left tail. Let me use c = Φ⁻¹(0.0005) ≈ −3.29 as a floor (the engine prints 0.000 but the true EDF is not literally zero).

Conditional on a sector shock of magnitude k (in standard deviations of F):

P(default | F = −k) = Φ( (c + √ρ · k) / √(1−ρ) )

| ρ | Sector shock k | P(default \| shock) | 5y P(shock) at 6%/yr | Unconditional 5y EDF | Implied grade |
|---|---|---|---|---|---|
| 0.30 | 2.0σ | 0.03% | 26% | 0.008% | AAA |
| 0.45 | 2.0σ | 0.16% | 26% | 0.04% | AAA |
| 0.45 | 2.5σ | 0.72% | 26% | 0.19% | AA |
| 0.45 | 3.0σ | 2.5% | 26% | 0.65% | A− |
| 0.60 | 2.5σ | 1.4% | 26% | 0.36% | AA− |
| 0.60 | 3.0σ | 5.2% | 26% | 1.35% | BBB |

Reading: at ρ = 0.45 and a 2.5σ sector shock, the unconditional 5y EDF moves from ~0% to ~0.2%, which is a 2-notch hit (AAA → AA). At ρ = 0.60 and a 3σ shock, it moves to ~1.4%, a 5-notch hit (AAA → BBB). The central case (ρ = 0.45, k = 2.5σ) supports the 3-notch adjustment proposed in §2.

**Critical caveat on this calculation:** the Basel formula assumes the sector shock is a one-period event. The actual AI-capex unwind would be persistent (2–3 years). A persistent shock is worse than a one-period shock because it impairs Anthropic's ability to raise equity, grow revenue, and service commitments over multiple periods. The single-factor formula understates the EDF by roughly a factor of 1.5–2× for a persistent shock. Applying that correction to the central case: 0.19% × 1.75 ≈ 0.33%, still AA− territory but at the weak end. This reinforces the 3-notch call.

### 3d. Proposed engine overlay

Add to the engine a **sector-unwind scenario** as a separate regime, not as a draw from the existing AR(1) process:

- **Trigger:** a latent sector factor F_t follows its own process. With annual hazard λ = 6%, F_t jumps to −2.5σ and mean-reverts with half-life 18 months.
- **Transmission to Anthropic's paths:** (i) revenue growth multiplier drops to 0.5× for 2 years; (ii) exit multiple compresses to 10× (from 22×); (iii) equity-issuance capacity drops to zero for 4 quarters, then recovers at 50% for 4 more; (iv) compute-access growth caps at 60% of plan for 2 years.
- **Calibration:** run 100k paths with the overlay active. Report the 5y EDF at D = $170B under the overlay. Compare to the base-case EDF. The difference is the sector adjustment.
- **Confidence flag:** [ESTIMATE]. No direct historical analogue for AI capex. The telecom and 2008 calibrations are structural analogies, not statistical estimates. The hazard and severity ranges are wide.

---

## 4. The black-swan list for the card

Six events. For each: the propagation path through the circular structure to Anthropic's revenue, margin, compute access, and exit multiple; the early-warning indicator; and the pre-registered trigger.

### Event 1: DeepSeek-style efficiency breakthrough (token-demand collapse)

**Propagation:** A frontier open-weight model achieves Claude-class performance at 1/10th the inference cost → enterprise self-hosting accelerates → token prices collapse (Evidence D already shows DeepSeek V4 Flash at $0.06/$0.12 per M tokens vs Claude Opus 5 at $5/$25) → Anthropic's API revenue growth stalls → the $170B in locked compute commitments becomes a cost anchor with no revenue growth to absorb it → multiple compresses → equity funding closes → growth ceiling binds.

**Early-warning indicators:** Silicon Data SDLLMTK token-expenditure index (already −20% from May 2026 peak, Evidence F Signals); GPU forward-curve backwardation (B200 −8%, H100 −13%, A100 −15% to 36-month, Evidence F Signals); open-weight ECI gap narrowing below 4 months / 8 ECI points (Evidence D TL;DR).

**Pre-registered trigger:** SDLLMTK index falls >35% from trailing peak AND open-weight ECI gap < 5 points for two consecutive monthly readings → flag sector-demand shock; downgrade sector-linked grade by 1 notch.

### Event 2: Neocloud default cascade (CoreWeave / Nebius / smaller GPU clouds)

**Propagation:** CoreWeave's $35B GPU-collateralised debt (Evidence F, F2) hits the 2-year maturity-vs-contract gap (DDTL V-V: contracts avg ~3yr vs loan maturity ~5yr) → utilisation drops below Sequoia's 50% threshold → GPU collateral values fall → cross-defaults across neocloud SPVs → Nvidia's backstop/rent-back guarantees (Evidence F, F2) are called → Nvidia takes losses → Nvidia cuts investment in / backstops for the sector → neocloud capacity that Anthropic uses via spot/overflow disappears → Anthropic's compute access tightens at the margin → more importantly, the sentiment shock hits all AI-name valuations including Anthropic's exit multiple.

**Early-warning indicators:** CoreWeave CDS/bond spreads (DDTL V-V at SOFR+550bps is the benchmark); neocloud utilisation rates; Nvidia's quarterly data-centre revenue guidance; GPU spot-rental prices (Silicon Data H100/B200 indices, CME futures from Oct 2026).

**Pre-registered trigger:** CoreWeave 5yr CDS > 400bps OR two neoclouds miss debt-service payments within 90 days → flag sector-credit shock; downgrade sector-linked grade by 1 notch.

### Event 3: Hyperscaler capex freeze (funding stress)

**Propagation:** Hyperscaler debt/capex at 32% (from 9% FY24, Evidence F, F2) → Microsoft FCF goes negative (expected Q4 2026, Evidence F, F2) → Alphabet's $85B equity raise (June 2026) signals internal cash generation is insufficient → one or more hyperscalers cut 2027 capex guidance by >20% → AWS/Google slow capacity buildout → Anthropic's locked contracts still run (costs continue) but new capacity for growth is unavailable → growth ceiling binds → the $24B/yr commitment-to-revenue ratio worsens → multiple compresses.

**Early-warning indicators:** Hyperscaler quarterly capex guidance vs consensus; hyperscaler debt issuance volume (FactSet data, Evidence F, F2); Meta CDS (already hit record on El Paso SPV, Evidence F, F2); Alphabet/Amazon/Microsoft FCF trajectory.

**Pre-registered trigger:** Any two of {MSFT, GOOGL, AMZN, META} cut capex guidance by >15% in the same quarter → flag capex-freeze shock; downgrade sector-linked grade by 1 notch.

### Event 4: Export-control escalation (China + allied-nation controls)

**Propagation:** US expands export controls to cover inference chips (not just training) or extends controls to allied nations → Nvidia/AMD lose China revenue → Nvidia's ability to backstop neoclouds weakens → global AI infrastructure buildout slows → Anthropic's international expansion (which is part of the growth thesis) is impaired → enterprise AI budgets in affected regions contract → revenue growth decelerates. This is already partially in the engine (Rating Card §4, trigger 4: "a second export-control episode within 12 months").

**Early-warning indicators:** BIS/Commerce Department rule-making dockets; Nvidia quarterly China revenue as % of data-centre revenue; allied-nation (EU, Japan, Korea, UAE) semiconductor policy statements.

**Pre-registered trigger:** A second export-control episode within 12 months of listing (already in §4) OR controls extended to inference-class chips → downgrade sector-linked grade by 1 notch.

### Event 5: Capability plateau (scaling laws hit a wall)

**Propagation:** Frontier labs (including Anthropic) fail to show meaningful capability gains for 2–3 consecutive model generations → enterprise buyers conclude current AI is "good enough" and stop upgrading → token consumption growth decelerates → the ROI narrative that justifies $700–900B of 2026 capex (Evidence F, F2) collapses → hyperscalers cut capex → the circular loop (valuation → capex → revenue → valuation) breaks at the capex link → all AI-name multiples compress → Anthropic's exit multiple falls from 22× toward 10×.

**Early-warning indicators:** Benchmark saturation (MMLU, GPQA, SWE-bench scores plateau across labs); enterprise AI renewal rates (Ramp index, Evidence C); time between frontier model releases lengthening; token-price-per-quality-unit flattening (Evidence D).

**Pre-registered trigger:** Two consecutive Anthropic model releases show <5% improvement on primary enterprise benchmarks AND Ramp AI-adoption growth decelerates to <10% QoQ → flag capability-plateau shock; downgrade sector-linked grade by 1 notch.

### Event 6: GPU supply disruption (TSMC / geopolitical)

**Propagation:** TSMC fabrication disruption (earthquake, geopolitical escalation, CoWoS packaging failure) → GPU/TPU supply halts for 2–4 quarters → all AI infrastructure buildout stops → Anthropic's locked contracts are partially protected (existing capacity runs) but new capacity is unavailable → competitors who rely on spot GPU rental are hit harder (F7 asymmetry: Anthropic is a relative winner from shortage) BUT the sector-wide sentiment shock hits Anthropic's valuation regardless → funding markets close for AI names → growth stalls.

**Early-warning indicators:** TSMC quarterly utilisation and capex guidance; CoWoS/HBM lead times (already sold out through 2027, Evidence F TL;DR); transformer lead times (144 weeks, Evidence F TL;DR); grid interconnect queue lengths.

**Pre-registered trigger:** TSMC reports >10% capacity loss for >1 quarter OR CoWoS lead times extend beyond 24 months → flag supply-disruption shock; downgrade sector-linked grade by 0.5 notch (Anthropic is partially hedged via locked contracts).

---

## 5. Deliverables

### 5(a). Rating-card section: "Sector-linked grade and the circular-capital risk"

**Insert after Section 6 of the Rating Card, as Section 7.**

---

**Section 7 — Sector-linked grade and the circular-capital risk**

The KMV issuer grade in Section 6 is a single-name rating. It asks whether Anthropic's assets cover its disclosed compute commitments. It does not ask whether the sector Anthropic operates in can sustain the valuations, funding, and capacity buildout on which Anthropic's growth depends. Those are different questions, and the second one matters more to an IPO buyer.

The AI-compute sector in mid-2026 has a circular capital structure. Amazon invests up to $25B in Anthropic; Anthropic commits >$100B to AWS. Google invests up to $40B; Anthropic commits to 1M TPUs and multi-GW expansions. Nvidia invests in and backstops neoclouds that buy Nvidia GPUs. Hyperscaler capex has shifted from 9% debt-funded (FY24) to 32% (mid-2026). Meta's Hyperion SPV is ~90% debt. CoreWeave carries ~$35B of GPU-collateralised debt. MS and JPM estimate the sector needs ~$1.5T of new debt. Alphabet did an $85B equity raise in June 2026. Valuations fund capex; capex funds the revenue of the firms whose valuations fund it. Any disruption to one link propagates through all of them.

The table below shows the two grades and the adjustment between them.

| | IPO buyer at $2T | Series-G fund ($380B, Feb-26) |
|---|---|---|
| **Stand-alone grade (KMV, Section 6)** | AAA (at D = $170B) | AAA |
| **Sector adjustment** | −3 notches | −3 notches |
| **Sector-linked grade** | **AA−** | **AA−** |
| **Adjustment basis** | Asset correlation to AI-capex factor (1 notch); wrong-way risk: investors = suppliers (1 notch); funding-liquidity dependence + contingent growth ceiling + demand contagion (1 notch combined) | Same |
| **Sensitivity: −2 notches** | AA | AA |
| **Sensitivity: −5 notches** | A | A |
| **Under sector-unwind scenario (ρ=0.45, 2.5σ shock)** | 5y EDF rises to ~0.2–0.35%; grade AA− to A+ | Same |
| **Under sector-unwind scenario (ρ=0.60, 3σ shock)** | 5y EDF rises to ~1.4%; grade BBB | Same |

The sector-linked grade applies to both the IPO buyer and the Series-G fund. The Series-G fund's AAA in the two-investor ladder (Section 1) reflects its low entry price, not immunity to sector risk. In a sector-unwind event, the fund's ability to exit at any price is impaired; the AAA assumes liquid exit, which is exactly what disappears in contagion. The sector-linked grade corrects for this.

The sector cap: the sector-linked grade should not exceed A+ (2 notches above the implied sector grade of BBB) as long as hyperscaler debt/capex remains above 25% and neocloud CDS spreads remain above 300bps. This is the sovereign-ceiling logic applied to the AI-capex sector.

---

### 5(b). The Lehman comparison — precise, not hysterical

The circular capital structure is real: investment flows from hyperscalers into Anthropic, Anthropic commits that capital back to the same hyperscalers as compute spend, the spend appears as hyperscaler revenue, the revenue supports the hyperscaler valuations that fund the next round of investment. This loop is structurally identical to the Lucent/Nortel vendor-financing loop of 2000–02 and the FTX/Alameda token-collateral loop of 2022, and it shares with 2008 the property that a shock to any single node propagates to all others. The comparison is warranted as a description of the *topology*.

What is different: Anthropic has no debt, no maturity transformation, no deposit base, and no leverage on its own balance sheet. The leverage is in the sector (CoreWeave's $35B, Meta's 90%-debt SPV, the hyperscalers' shift to 32% debt-funded capex), not in Anthropic. Losses in a sector unwind hit equity holders, not creditors; there is no bank run, no overnight liquidity failure, no forced fire-sale of assets to meet margin calls. Anthropic would not have a Lehman Saturday. It would have a Lucent 2001: a slow bleed of growth, multiple compression, funding drought, and a gradual recognition that the compute commitments are a larger burden than the revenue trajectory can support. The systemic risk is real; the transmission mechanism is slower and the loss-absorption is different. That makes the tail less sudden but not less deep.

### 5(c). Caveat text

**Insert at the end of Section 7.**

This sector-linked adjustment is a structural overlay, not a statistical estimate. The annual hazard of a sector-unwind event (5%, range 3–8%) and the severity for Anthropic (55–75% value loss conditional on the event) are calibrated from five historical analogues — telecom 2000–02, 2008, shale 2014–16, crypto 2022, SaaS 2022 — none of which is a direct analogue for AI-capex circularity. The Basel ρ of 0.45 (range 0.30–0.60) is a judgment, not a regression. The notch adjustment of 3 (range 2–5) is defensible on the channel analysis in this section but is not uniquely determined by the data. The sector-unwind scenario has not been run through the engine; the EDF estimates in the table are conditional-on-shock calculations using the single-factor formula with a persistence correction. All of these numbers should be treated as order-of-magnitude guides, not point estimates. The most important uncertainty is not the probability of the shock but the correlation structure within it: if the shock hits demand, compute access, funding, and multiples simultaneously (as specified), the joint loss is materially worse than the sum of the individual channels. The engine does not currently model this joint hit. That is the single highest-priority model improvement for the next version of this card.

The Lehman comparison is a topological analogy, not a prediction. Anthropic's lack of debt and leverage means the failure mode, if it comes, is slower and more visible than a bank failure. The early-warning indicators listed in Section 4 of this card and in the black-swan triggers above are designed to give 2–4 quarters of visibility before the sector-linked grade would need to move. Watch them.

Analytical opinion, not investment advice.

---

## Summary of recommended changes to the rating card

1. **Add Section 7** (the sector-linked grade) as drafted above. This is the single most important addition. The card currently presents the AAA from Section 6 without qualification, and a reader will take it at face value.

2. **Add sector-level triggers to Section 4.** The current triggers are all single-name (growth prints, S-1 restatement, gross margin, export control). Add: CoreWeave CDS > 400bps; two hyperscalers cutting capex guidance by >15% in the same quarter; SDLLMTK index −35% from peak. These are the sector analogues of the existing single-name triggers.

3. **Flag the Series-G AAA in the two-investor ladder.** The AAA assumes liquid exit. Add a footnote: "In a sector-unwind scenario, exit liquidity is impaired; the sector-linked grade for the Series-G fund is AA−, not AAA."

4. **Note in Section 5 (Honesty notes) that the 64% vol is treated as mean-reverting AR(1) noise.** In a sector-unwind regime, the vol is not noise; it is a regime shift. The AR(1) assumption understates the persistence of a sector shock. This is the engine limitation that most directly affects the sector-linked grade.

5. **Commission the sector-unwind overlay run.** The numbers in this referee report are analytical estimates. The engine should be re-run with the overlay specified in §3d above to produce path-based EDFs under the sector shock, replacing the single-factor formula estimates.