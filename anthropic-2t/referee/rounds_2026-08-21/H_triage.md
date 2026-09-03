# Prompt H — triage of the deep-research return (2026-08-21)

Source: `H_ipo_paths_circular_capital_deepresearch.md` (verbatim). CSVs: `data/research/H/`. The agent ran out of search budget; roughly half the requested cells came back `unavailable`. Below: what is verified, what changes in our documents, what we filled ourselves, what is still open.

## 1. Verified against our own data

- **H6 S&P Table 26** — all 17 notches × (5y, 10y) and the three summary rows match `04_sp_default_rates_verified.md` exactly. Nothing changes in the card brackets. New: Moody's broad-letter 1983–2024 (Aaa 0.06/0.12 … Caa-C 32.69/47.86, SECONDARY, Moody's doc server) — usable as a cross-agency footnote; alphanumeric Moody's and KMV EDF map remain paywalled → card keeps "S&P only".
- **H1 day-1 open/close** — every row the agent filled (SPCX, CRCL, FIG, KLAR, CRWV, RDDT, ARM, RIVN, COIN, HOOD, BMBL, ABNB, DASH, SNOW, PLTR, UBER, LYFT, PINS, ZM, BYND, PTON, BABA, META) matches our Alpaca bars to the cent. SPCX peak $225.64 intraday 2026-06-16 ✓ (peak *close* $201.80 same day); "traded at $134.00 on 2026-08-21" is the **08-20 close** — 08-21 close was $136.03.

## 2. What we filled ourselves (the agent's biggest gap)

`scripts/fetch_bars_h1.py` pulled the 12 H1 tickers we lacked (CART, BIRK, CAVA, COIN, HOOD, BMBL, LYFT, PINS, ZM, BYND, PTON; **TWTR unavailable** — delisted 2022, neither Alpaca nor Yahoo serves it). `data/research/H/H1_paths_from_bars.csv` now carries, for 26 listings, from bars: day-1 pop, 12-month peak (close and high), drawdown peak→6m/12m, return 6m/1y vs offer, worst 6-month point vs first close, below-offer-within-12m, below-first-close-within-6m.

Headline facts from it (n=26): **24/26 closed below their first close within six months** (exceptions ZM, BYND); **17/26 traded below offer within 12 months**. Agent's TL;DR magnitudes check out: RIVN peak→6m −88%, HOOD −84%, COIN peak→12m −59%.

Still missing in H1 and *not* derivable from bars: lockup-expiry dates (agent gave month-level for ~12), price at lockup ±10d (computable once dates are exact), float %, step-up (agent filled ~15, mixed quality — SPCX step-up uses the $400B Jul-2025 round; the Dec-2025 secondary was ~$800B → step-up ~2.2×, not 4.4×), retail allocation (RDDT ~8, HOOD ~20–35 only), oversubscription (CRCL 25×, KLAR 26× only).

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

## 4. Quality flags on the return

- Wrong/placeholder URLs: ARM, CART, BIRK, CAVA rows cite the Reddit-pricing CNBC article; UBER/LYFT/PINS/BABA/TWTR cite a SpaceX Yahoo piece; DASH/SNOW/PLTR/BYND cite SaaStr. Numbers checked out against bars, but the URLs are not sources — re-cite from our own `comps_ipo_prices*.csv` (EDGAR) before print.
- Weak outlets used for history: Bitget (SNOW/ZM peaks), thebubblebubble, technostatecraft (fiber lit ~10% — contradicts the referee's 2.5–5%; neither is primary → need Odlyzko directly), TIKR.
- SPAC cohort −60 to −75% is an ESTIMATE with no source; do not print. Klausner–Ohlrogge / SEC DERA still needed.
- H7 items 1 (GPU history) and 15 (our 15 tickers) were answered as gaps because the agent saw the pre-`a072532` prompt; we hold both. Not a loss.

## 5. Still open — and who does it

Own pulls (cheap, no deep research):
1. EDGAR: CoreWeave 10-Q debt tranches (H7-2); MSFT/GOOGL/AMZN/META capex and debt by quarter FY22–Q2-26 (H7-3); Alphabet June-2026 raise instrument via 424B (H7-5); Lucent FY2001 10-K write-off (H8-5).
2. Literature: Klausner–Ohlrogge "A Sober Look at SPACs" (SSRN); SEC DERA 2022 SPAC staff report; Odlyzko fibre-lit and railway-mania papers; Campbell & Turner; FCIC 2011 AAA downgrade shares; Field & Hanka 2001 lockup abnormal return; Minsky Levy WP 74 (1992) — all fetchable by URL (H8-6/7/8/13, H3 gap).
3. Lockup dates for the 26 listings (S-1/424B "lock-up" sections) → then compute px_at_lockup / +10d from bars.
4. Verify the $65B July run-rate (Bloomberg/Reuters primary) and append to `run_rate_series.csv`.

Needs a second deep-research pass or a paid terminal: Meta Hyperion SPV terms (H7-4), neocloud bond spreads/CDS (H7-13), TSMC CoWoS lead times (H7-14), Ramp AI-spend series (H7-12), Silicon Data SDLLMTK (H7-11 — not public, declare as gap in the article), Renaissance IPO index returns, H2 per-ticker hype features (Trends, article counts, VIX/UST10Y on the day — VIX/10y we can pull from FRED ourselves).

## 6. Next build steps (unchanged from plan, now unblocked)

1. Re-run the archetype prototype on 26 listings with `H1_paths_from_bars.csv` (was 15); fit archetype membership from pre-trade features where we have them (step-up, float, EV/rev, day-1 pop, hot-market year); leave-one-out on SPCX/CRCL.
2. Fig 3 caption: add the $105B Ohio backstop, AMD warrant; re-source the 9%→32% debt-funded share (H7-3 still open — that number is currently unsourced in our caption).
3. Article/card edits from §3 (base-rate box, Lucent number, Amodei wording, Prince citation).

---

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
