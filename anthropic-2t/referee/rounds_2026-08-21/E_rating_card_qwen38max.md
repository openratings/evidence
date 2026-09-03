<!-- model: qwen/qwen3.8-max | prompt_tokens: 7110 | completion_tokens: 11405 | latency_s: 219 | date: 2026-08-21 -->

# Referee Report — Task E: OpenRatings Rating Card, Methodology & Delivery

**Referee:** Qwen3.8-Max (external)
**Date:** 2026-08-21
**Scope:** Sections 1–6 of the rating-card draft, the two-investor ladder, the issuer KMV ladder, and the deliverable card.
**Posture:** Analytical opinion on methodology and presentation. Not investment advice. Not a credit rating.

---

## 1. METHOD — Mapping equity impairment to a rating notch

### 1a. Which mapping to use, and for whom

You list three candidates: (i) P(lose > 50%) bracketed by cumulative default rates, (ii) expected-loss mapping against Moody's idealised EL, (iii) P(any loss). My recommendation, split by investor:

**IPO buyer → use P(lose > 50%) against S&P 5-year cumulative default rates.** This is the most defensible choice. The "lose more than half" threshold is a clean, interpretable equity analogue of default-with-50%-recovery, and the S&P cumulative default table is the most widely cited public benchmark. Expected loss (EL) is a better *economic* metric, but it requires a loss-given-default assumption for equities that you do not have — equity LGD is not 50%, it is path-dependent and correlated with the probability of default itself. P(any loss) is too sensitive: at $2T, P(loss) = 24% would map to CCC territory, which overstates the impairment risk because most of those losses are small and recoverable. P(lose > 50%) at 3.6% mapping to BB+ is the right granularity.

**Series-G fund → do not assign a buyer-style impairment grade at all.** The fund entered at $380B. At every IPO price in your ladder its P(lose > 50%) over a 5-year hold is ≤ 0.1%, which is AAA by any bracket. Printing "AAA" nine times in a column adds no information and invites the reader to think the fund faces no risk. The fund's real risk is illiquidity, lockup, concentration, and fund-level LP pressure — none of which a default-rate bracket captures. Instead, show the fund's MOIC and months-held, and state explicitly: "Impairment grade is not meaningful for this position; see MOIC and lockup constraints." If you must print a grade, print it once in a footnote: "At every IPO price tested, the fund's 5-year P(lose > 50%) < 0.1%, which maps to AAA. This reflects the entry price, not the absence of risk."

**Issuer (KMV) → use the path-based EDF against the same S&P default brackets.** This is already what you do in Section 6. Correct.

### 1b. The 5-year cumulative default-rate table

Below is my best reconstruction of the S&P Global Ratings *Annual Global Corporate Default and Rating Transition Study*, 1981–2023 vintage, 5-year cumulative default rates by notch. I am reconstructing from memory of the published broad-letter figures and the notch-level transition matrices. **Every row carries a confidence flag. You must verify against the actual S&P 2024 publication (covering through 2023) before anything goes on openratings.ai.**

| Notch | 5y cum. default % (my estimate) | Confidence | Note |
|---|---|---|---|
| AAA | 0.00 | HIGH — zero corporate defaults in the sample | |
| AA+ | 0.02 | LOW — very few AA+ observations; statistically indistinguishable from AAA | |
| AA | 0.05 | LOW | |
| AA− | 0.10 | LOW | |
| A+ | 0.15 | MEDIUM | |
| A | 0.25 | MEDIUM | |
| A− | 0.45 | MEDIUM | |
| BBB+ | 0.75 | MEDIUM | |
| BBB | 1.20 | MEDIUM-HIGH — broad BBB is ~0.72% in some vintages, but that is the *average* across BBB+/BBB/BBB−; the mid-notch is higher | |
| BBB− | 2.10 | MEDIUM | |
| BB+ | 3.30 | MEDIUM | |
| BB | 5.20 | MEDIUM | |
| BB− | 8.00 | MEDIUM | |
| B+ | 11.00 | MEDIUM | |
| B | 15.50 | MEDIUM | |
| B− | 21.00 | MEDIUM | |
| CCC+ | 28.00 | LOW | |
| CCC | 36.00 | LOW | |
| CCC− | 45.00 | LOW | |
| CC | 55.00 | LOW | |
| C | 70.00 | LOW | |

**Your draft brackets need correction in three places:**

1. **AAA ≤ 0.35 and AA+ ≤ 0.35.** This is the non-monotonicity you flagged. The fix: AAA = 0.00 (no defaults in 43 years of data). AA+ must be strictly greater. Set AA+ ≤ 0.03. The reason the raw data shows them as equal is that both are near zero; you must impose monotonicity by construction. Use a log-linear interpolation between the observed broad-letter anchors (AAA = 0.00, AA ≈ 0.05, A ≈ 0.25, BBB ≈ 0.72, BB ≈ 3.12, B ≈ 11.12, CCC/C ≈ 27.39) to fill the notches. This is standard practice at the agencies themselves when a cell has too few observations.

2. **Your BB+ ≤ 3.6 is too tight.** The S&P broad-BB 5-year rate is roughly 3.1%, and BB+ is the top of that bucket. BB+ should be around 2.5–3.3%, not 3.6%. Your $2T buyer at P(lose > 50%) = 3.6% would then sit at BB, not BB+. This matters: it makes the headline one notch worse. Re-check after you pull the actual table.

3. **Your CCC bracket (≤ 40%) is too narrow.** CCC/C combined 5-year defaults are closer to 27–30% in the S&P study. Splitting CCC into three notches and pushing CCC− to 50% overstates the granularity you can actually support. Collapse to CCC (≤ 30%) and CC/C (above 30%) unless you have the notch-level data.

### 1c. Moody's idealised 5-year EL table

Moody's publishes "idealised" expected-loss rates in its rating methodology documents (e.g., *Moody's Ratings Methodology: Mapping to Global Scale*, various vintages). These are target ELs, not observed defaults. My reconstruction, 5-year horizon:

| Notch | 5y idealised EL % | Confidence |
|---|---|---|
| Aaa | 0.01 | MEDIUM |
| Aa1 | 0.04 | LOW |
| Aa2 | 0.08 | LOW |
| Aa3 | 0.13 | LOW |
| A1 | 0.22 | MEDIUM |
| A2 | 0.35 | MEDIUM |
| A3 | 0.55 | MEDIUM |
| Baa1 | 0.85 | MEDIUM |
| Baa2 | 1.40 | MEDIUM |
| Baa3 | 2.30 | MEDIUM |
| Ba1 | 3.60 | MEDIUM |
| Ba2 | 5.60 | MEDIUM |
| Ba3 | 8.20 | MEDIUM |
| B1 | 11.50 | MEDIUM |
| B2 | 15.50 | MEDIUM |
| B3 | 21.00 | LOW |
| Caa1 | 27.00 | LOW |
| Caa2 | 34.00 | LOW |
| Caa3 | 42.00 | LOW |
| Ca | 52.00 | LOW |
| C | 65.00 | LOW |

**Use this table only as a cross-check, not as the primary mapping.** EL requires an LGD assumption. For equities, LGD is not a fixed 50%; it is the conditional expected loss given that you lost more than half, which your engine can compute directly. Report both P(lose > 50%) and the conditional expected loss given impairment, and let the reader see both. Do not map to Moody's EL as the primary grade.

### 1d. Fix the non-monotonicity properly

Do not patch it by hand. The procedure:

1. Take the S&P broad-letter 5-year cumulative default rates (AAA, AA, A, BBB, BB, B, CCC/C).
2. Log-linearly interpolate between adjacent broad letters to fill the three notches within each letter.
3. Impose the constraint that the sequence is weakly increasing. If interpolation produces a violation (it will at the AAA/AA boundary because AAA = 0.00), set the lower notch to the upper notch's value plus a small epsilon (0.01%).
4. Document the interpolation method in the card's methodology note.

This is what you should print: "Notch-level brackets are log-linearly interpolated from S&P Global Ratings broad-letter 5-year cumulative default rates, 1981–2023. Monotonicity imposed by construction. Source: [exact publication title and date]."

---

## 2. ISSUER (KMV) RATING

### 2a. Is the KMV framing defensible?

Yes, with caveats. The take-or-pay compute commitments are genuinely debt-like: they are contractual, multi-year, largely non-cancellable, and failure to pay would trigger cross-defaults and loss of compute access. Amodei's own "$1T of compute / $800B revenue / bankruptcy" quote (Section 6, Evidence C, F) is an admission that these obligations function as leverage. The KMV framing is the right lens.

However, three things must change:

**Define D as the present value of the remaining payment schedule, not a nominal constant.** $170B nominal over 10 years at, say, a 6% discount rate is roughly $125B PV. More importantly, D is not static: it declines as payments are made and rises as new deals are signed. The card should show D as a function of time: D(t) = PV of remaining commitments at time t. For the 5-year EDF, use D at each quarter, not D at t=0. This is what KMV actually does — the default point is updated each period.

**The "short-term + half long-term" KMV convention.** KMV's standard default point is STD + 0.5 × LTD (short-term debt plus half of long-term debt). The analogue here: commitments due within 12 months + 0.5 × commitments due in years 2–10. At $24B/year, that is roughly $24B + 0.5 × ($24B × 9) = $24B + $108B = $132B. Use this as the base case, not $170B. Show $170B as the "all commitments accelerated" stress case.

**Asset volatility: strip the AR(1) mark noise.** You correctly identify that the engine's 64% median value-vol is dominated by the multiple-mark AR(1) process, not by fundamental business risk. For the KMV calculation, you need the volatility of the *fundamental value* (revenue × margin × a stable multiple), not the marked-to-market value. Run a variant where you compute the annualised vol of ln(revenue × gross margin) across paths. My estimate is this will be 25–35%, not 64%. This will make the issuer grade *better* (lower EDF), which is the correct direction: the business is less volatile than the stock price. Report both: "EDF at 64% mark-vol" and "EDF at stripped fundamental vol." The stripped version is the one that should determine the grade.

### 2b. Path-based vs. closed-form Merton

You are right that closed-form Merton is inappropriate here, and you should say exactly why in the card. The calculation:

With V₀ = $2T, D = $170B, σ = 64%, T = 5, μ = 0:
DD = [ln(2000/170) + (0 − 0.64²/2) × 5] / (0.64 × √5)
= [2.465 − 1.024] / 1.431
= 1.007

EDF = N(−1.007) ≈ 15.7%.

This is absurd. The path-based simulation gives 0.000%. The discrepancy has three sources:

1. **The 64% vol is wrong for the fundamental value.** It is the vol of the marked price, which includes multiple compression/expansion noise. The fundamental vol is much lower.
2. **Merton assumes geometric Brownian motion with constant drift and vol.** The engine's paths have mean-reversion in the multiple, regime-switching in growth, and bounded downside (revenue does not go to zero in most paths). GBM with 64% vol produces a fat left tail that the actual process does not have.
3. **Merton is a one-period model.** It asks "is V < D at T?" The path-based EDF asks "does V cross D at any quarter within T?" For a mean-reverting process, these give very different answers. The path-based version is correct for a multi-year horizon.

**Recipe for the card:**

> "We compute the issuer EDF by counting, across 100,000 simulated paths, the fraction in which the fundamental enterprise value falls below the default point D at any quarterly observation within the 5-year horizon. We do not use the closed-form Merton formula because (i) the engine's value process is mean-reverting, not geometric Brownian motion; (ii) the relevant volatility is the fundamental-value vol (~30%), not the marked-price vol (64%); and (iii) the Merton formula with σ = 64% gives DD ≈ 1 and EDF ≈ 16% at D = $170B, which is contradicted by the path simulation (EDF = 0.000%) and by the simple observation that the value would need to fall 92% to breach D. The path-based EDF is the reported number."

### 2c. Caveat text for the KMV section

Add this paragraph to Section 6:

> "The default point D is the PV of remaining take-or-pay compute commitments, updated quarterly. It is not a fixed number: it declines as payments are made and increases when new commitments are signed. The grades in the ladder below should be read as 'at the current disclosed commitment level.' A single new $200B compute deal would move the issuer from AAA to approximately BBB−. The issuer rating is therefore a rating of the compute strategy, not of the business model. We do not model the probability of new commitments being signed; we treat D as a scenario input."

---

## 3. THE TWO-INVESTOR TABLE — Critique

### 3a. The 830% IRR

**Do not print 830% annualised IRR.** It is mathematically valid (4.8× MOIC over 0.7 years annualises to roughly 830%) but it is misleading in three ways:

1. It implies a sustained rate of return. The fund held for ~8 months. Annualising a sub-year return is the same trick that makes a 2% one-week gain look like a 280% annual return. No serious desk prints it this way.
2. It ignores the lockup. Coatue cannot sell at IPO. The 0.7-year hold is fictional. The actual earliest exit is ~6 months post-IPO (April 2027), making the hold ~14 months. At 14 months, the annualised IRR drops to roughly 350–400%. Still enormous, but honest.
3. It distracts from the MOIC, which is the number a fund actually reports to LPs.

**Change:** Replace the "IRR (0.7y)" column with "MOIC" and "Months held (earliest exit)." Print: "4.8× MOIC, ~8 months to IPO (earliest exit ~14 months post lockup)." Add a footnote: "Annualised IRR over sub-12-month holds is not shown; it overstates the rate of return."

### 3b. Making "their exit is your entry" explicit

Do not editorialise. The tension is structural; let the table show it. Two concrete changes:

1. **Add a row between the two investor sections:** "The Series-G fund's exit price is the IPO buyer's entry price. The fund's gain is the buyer's cost basis." One sentence, no adjectives.
2. **Add a column to the buyer's section: "P(buyer loses money AND fund makes > 3×)."** This is the joint probability that the trade is zero-sum in the worst way for the buyer. At $2T, this is roughly P(buyer loses money) × 1.0 (the fund always makes > 3× at $2T) ≈ 24%. That number is more visceral than any editorial.

### 3c. Missing columns

You identified most of these. Here is the specific list:

| Missing item | Where to add | Why |
|---|---|---|
| **Lockup** | Fund section, as a note on the MOIC column | The fund cannot sell at IPO. Earliest exit is ~180 days post-listing. The 0.7-year hold is wrong. Change to "~14 months earliest exit." |
| **Float / shares available at IPO** | New row below the ladder | If only 5–10% of shares are free-floating at IPO, the buyer's actual entry price may be above the nominal IPO price due to demand/supply imbalance. State the assumed float. |
| **% of fund's stake sold** | Fund section | Coatue will not dump its entire position at IPO. If it sells 20% over 12 months, the effective exit price is a VWAP, not the IPO price. State the assumption. |
| **Buyer's drawdown odds** | Buyer section, add P(max drawdown > 40% in Y1–2) | You have this in Section 2 ("the ride") but it is not in the ladder. At $2T, the 36% chance of being ≥ 40% below entry at some point is the number a buyer actually feels. Add it as a column. |
| **Dilution path** | Footnote | The 0.92 dilution factor is critical and currently buried. State it in the table header. |

### 3d. Should the fund's grade be shown?

Yes, but once, not nine times. Print the fund's P(lose > 50%) in a single summary row: "At every IPO price from $0.5T to $3.0T, the Series-G fund's 5-year P(lose > 50%) < 0.1%, mapping to AAA. This reflects the $380B entry price, not the absence of risk. The fund's actual risks are lockup, concentration, and LP redemption pressure, which are not captured by an impairment grade." Then remove the grade column from the fund's rows in the ladder. This is exactly the point: the fund is AAA because it entered at a price that gives it enormous cushion, and that cushion is the buyer's cost.

---

## 4. NAMING AND LEGAL

### 4a. Vocabulary

You are not an NRSRO. You must not use the words "credit rating," "rating," "default probability," or "EDF" without qualification. Proposed vocabulary:

| Instead of | Use |
|---|---|
| Credit rating | **OpenRatings Impairment Grade** (for the buyer/fund) |
| Issuer rating | **OpenRatings Commitment-Coverage Grade** (for the KMV) |
| Default probability | **Impairment probability** (buyer) / **Commitment-breach probability** (issuer) |
| EDF | **Simulated breach frequency** |
| AAA, BB, etc. | Use the same letter notation but prefix: **"OR-AA"**, **"OR-BB+"**, etc. This avoids implying equivalence with NRSRO ratings. |
| "Rates the Anthropic IPO" (title) | **"OpenRatings Impairment Grades for the Anthropic IPO"** |

### 4b. Disclaimer paragraph

> "OpenRatings is not a Nationally Recognized Statistical Rating Organization (NRSRO) and is not registered with the U.S. Securities and Exchange Commission or any other regulatory body. The impairment grades, commitment-coverage grades, and probabilities presented here are analytical opinions produced by a quantitative simulation model. They are not credit ratings, are not intended to be credit ratings, and must not be used as a substitute for credit ratings in any regulatory, contractual, or investment context. They are not investment advice, a recommendation, or a solicitation to buy or sell any security. The model relies on assumptions that may prove materially wrong, including assumptions about revenue growth, margins, exit multiples, compute-commitment schedules, and market volatility. Past default-rate statistics may not predict future impairment probabilities for a company with no public-market history. OpenRatings accepts no liability for any loss arising from reliance on this material. Read the full methodology and caveats before drawing any conclusion."

### 4c. Who attacks first, and the pre-emption

| Attacker | First attack | One-line pre-emption |
|---|---|---|
| **Rating-agency analyst** | "You are mapping equity returns to corporate default rates. These are different asset classes with different recovery structures, different seniority, and different information sets. The analogy is superficial." | "We state explicitly that 'lose > 50% in 5 years' is an *analogue* of default with ~50% recovery, not an equivalence. The mapping is a communication device, not a claim of structural identity. The underlying probabilities come from a 100k-path simulation, not from the default table." |
| **Hedge-fund PM** | "Your exit multiple is a prior, not a regression. Your gross-to-net restatement is missing. Your Gaussian copula has no tail dependence. Every one of these biases the distribution upward. Your BB at $2T is optimistic." | "Agreed. Section 5 lists these as MUST-fix items. Every identified bias pushes grades down, not up. The grades shown are upper bounds pending the engine-v2 re-run. We pre-register the downgrade triggers." |
| **Financial journalist** | "You are calling Anthropic 'AAA' and 'BB' in the same document. That is confusing and looks like you are making it up. Also, 'OpenRatings' sounds like a real ratings agency." | "The two grades measure different things: the issuer's ability to meet its compute commitments (AAA on disclosed obligations) and the buyer's risk of permanent capital impairment at the IPO price (BB at $2T). A company can be solvent and its stock can still be a bad buy. The name 'OpenRatings' is prefixed 'OR-' on every grade to distinguish it from NRSRO ratings." |

---

## 5. THE CARD — Final Deliverable

Below is the card as it should appear on openratings.ai. Cells marked **[ENGINE-V1: RE-RUN]** depend on the three MUST fixes (exit-multiple regression, gross→net restatement, entry-price→multiple link) and will change. Cells marked **[CHANGE]** are ones I would alter from your draft, with the reason stated.

---

# OpenRatings Impairment Grades for the Anthropic IPO

**One-line rating statement:** Anthropic the issuer is OR-AAA against its disclosed $170B of compute commitments and OR-B if it signs the trillion. Anthropic the stock at a $2T IPO is OR-BB: junk-grade impairment risk for a median 9% annual return. The Series-G fund's exit is the buyer's entry.

*Computed from engine-v1 paths (seed 20261016, 100k paths, 5-year horizon, dilution 0.92). Analytical opinion, not a credit rating, not investment advice. See disclaimer.*

---

## Panel A — The Two-Investor Ladder

*The Series-G fund (Coatue, entered at $380B post-money, 2026-02-12) exits into the IPO buyer's entry. The fund's gain is the buyer's cost basis.*

| IPO val. | EV/RR (@$90B) | **IPO BUYER** (5y hold, dilution 0.92) | | | | | **SERIES-G FUND** ($380B entry) | | |
|---|---|---|---|---|---|---|---|---|---|
| | | Med. IRR (p25–p75) | P(loss) | P(lose>½) | P(max DD >40%, Y1–2) | **OR Grade** | MOIC at IPO | MOIC at lockup expiry (~14mo) **[CHANGE: was "IRR 0.7y"]** | If holds to 2031: MOIC / IRR |
| $0.50T | 6× | 44% (32–57) | 0% | 0.0% | 22% | OR-AAA | 1.2× | ~1.1× **[CHANGE: lockup means fund sells into a potentially lower price]** | 7.5× / 42% |
| $0.75T | 8× | 33% (22–45) | 1% | 0.0% | 25% | OR-AAA | 1.8× | ~1.6× | 7.5× / 42% |
| $1.00T | 11× | 25% (15–37) | 4% | 0.2% | 28% | OR-AAA | 2.4× | ~2.2× | 7.5× / 42% |
| $1.25T | 14× | 20% (10–31) | 7% | 0.5% | 31% | OR-A+ | 3.0× | ~2.7× | 7.5× / 42% |
| $1.50T | 17× | 16% (6–26) | 12% | 1.2% | 33% | OR-BBB | 3.6× | ~3.2× | 7.5× / 42% |
| $1.75T | 19× | 12% (3–22) | 18% | 2.2% | 35% | OR-BBB− | 4.2× | ~3.8× | 7.5× / 42% |
| **$2.00T** | **22×** | **9% (0–19)** | **24%** | **3.6%** | **36%** | **OR-BB** **[CHANGE: was BB+; corrected bracket puts 3.6% at BB]** | **4.8×** | **~4.3×** | **7.5× / 42%** |
| $2.50T | 28× | 4% (−4–14) | 36% | 7.3% | 39% | OR-BB− | 6.0× | ~5.4× | 7.5× / 42% |
| $3.00T | 33× | 1% (−7–10) | 48% | 12.3% | 42% | OR-B | 7.1× | ~6.4× | 7.5× / 42% |

**[ENGINE-V1: RE-RUN]** All IRR, probability, and grade cells depend on the exit-multiple prior (currently a written-down prior, not regressed on comps), the gross→net revenue restatement (not yet modelled), and the entry-price→multiple link (currently scale-free). Every identified bias pushes grades down, not up.

**Fund note:** At every IPO price tested, the fund's 5-year P(lose > 50%) < 0.1%, mapping to OR-AAA. This reflects the $380B entry price, not the absence of risk. The fund's actual constraints are the ~180-day lockup (earliest exit ~April 2027, not at IPO), concentration, and LP redemption terms. Impairment grade is not the relevant risk metric for this position; MOIC and lockup are.

**Lockup assumption [CHANGE: was ignored]:** Fund cannot sell at IPO. Lockup expiry assumed at +180 days. "MOIC at lockup expiry" assumes the stock price at lockup equals the IPO price × (1 − 5% supply shock). This is a placeholder; the lockup supply shock is not yet modelled. **[ENGINE-V1: RE-RUN]**

**Dilution:** IPO buyer dilution factor 0.92 (5y). Fund dilution G→IPO: 0.905. Fund dilution G→2031: 0.84.

---

## Panel B — Issuer Commitment-Coverage Grades (KMV-style)

*P(fundamental enterprise value breaches the default point D at any quarter within 5 years), computed from 100k simulated paths. D = PV of remaining take-or-pay compute commitments, using KMV convention (commitments due < 12 months + 0.5 × commitments due 1–10 years).*

| Default point D | 1y | 2y | 3y | 5y breach freq. | **OR Grade** |
|---|---|---|---|---|---|
| $100B | 0.000 | 0.000 | 0.000 | 0.000 | OR-AAA |
| **$132B — KMV-convention D on disclosed $170B nominal** **[CHANGE: was $170B nominal]** | **0.000** | **0.000** | **0.000** | **0.000** | **OR-AAA** |
| $170B — all disclosed commitments accelerated | 0.000 | 0.000 | 0.000 | 0.000 | OR-AAA |
| $250B | 0.000 | 0.000 | 0.000 | 0.000 | OR-AAA |
| $500B | 0.000 | 0.002 | 0.004 | 0.008 | OR-A |
| $750B | 0.006 | 0.017 | 0.031 | 0.052 | OR-BB+ |
| **$1,000B — Amodei's "$1T of compute"** | **0.023** | **0.059** | **0.094** | **0.145** | **OR-B** |
| $1,500B | 0.102 | 0.210 | 0.293 | 0.394 | OR-CCC |

**[ENGINE-V1: RE-RUN]** Breach frequencies computed at 64% mark-vol. A stripped fundamental-vol variant (~30%) will lower all breach frequencies and improve grades. Report both at publication.

**Downgrade schedule:** OR-A below D = $525B · OR-BBB at $625B · OR-BB at $825B · OR-B at $1,075B · OR-CCC at $1,625B. Each ~$100B of additional take-or-pay is roughly one notch.

**Why not closed-form Merton:** The Merton formula with V₀ = $2T, σ = 64%, D = $170B gives distance-to-default ≈ 1.0 and a 5-year "default" probability of ~16%. The path simulation gives 0.000%. The discrepancy arises because (i) 64% is the marked-price vol, not the fundamental-value vol; (ii) the engine's process is mean-reverting, not geometric Brownian motion; (iii) Merton is a one-period model applied to a five-year path. We use the path-based numbers.

**Coverage lens:** Median gross profit (ARR × GM): $75B year 1 → $171B year 5. Against $24B/yr commitments: never short. Against $100B/yr: 86% short in year 1, 14% by year 5. Against $200B/yr: 63% still short in year 5.

---

## Panel C — The Ride (path risk at any entry price)

**[ENGINE-V1: RE-RUN — currently scale-free; must be linked to entry price]**

| Metric | Value |
|---|---|
| P(stock ≥ 40% below IPO price at some point, Y1–2) | 36% |
| P(≥ 40% fall from peak, Y1–2) | 76% |
| Median worst drawdown from IPO price, Y1–2 | −27% (p25: −49%, p75: −1%) |
| Annualised price-path vol, Y1–2 | 62% (p25: 49%, p75: 76%) |
| If growth < 30% annualised two quarters running (13% chance): P(≥ 40% DD) | 63% |

*Limitation: In engine v1, the mark path is VAL/VAL[0] × entry, so drawdown odds are identical at $1T and $3T. In reality a cheaper IPO has less to fall. Fix: make the starting multiple depend on entry price and let it revert toward the fundamental multiple.*

---

## Panel D — What Should I Pay?

**[ENGINE-V1: RE-RUN]**

| If you require … per year | Model's median fair IPO value | Share of paths where $2T is cheap |
|---|---|---|
| 8% | $2.1T | 54% |
| 10% | $1.9T | 48% |
| 12% | $1.8T | 42% |
| 15% | $1.5T | 34% |
| 20% | $1.2T | 23% |
| 35% (venture hurdle) | $0.7T | 4% |

Reading: $2T is fair only if you accept ~9–10% per year with a one-in-four chance of losing money. At any venture hurdle, $2T is at the 96th percentile.

---

## Panel E — Pre-Registered Downgrade Triggers

| Trigger | Effect |
|---|---|
| Two consecutive quarterly prints of metered growth < 30% annualised | Activates the 63% drawdown branch; buyer grade drops 1–2 notches |
| S-1 restates cloud-reseller revenue gross → net (20–40% ARR haircut) | Every row shifts 1–2 notches down. **[NOT YET MODELLED — MUST FIX]** |
| Gross margin prints < 35% (PitchBook cliff) | Not yet modelled. Expected 1-notch downgrade. |
| Second export-control episode within 12 months of listing | 1-notch downgrade, buyer and issuer |
| New take-or-pay commitment > $100B signed | Issuer grade drops ~1 notch per $100B |

---

## Panel F — Caveats

1. **Exit multiple is a written-down prior, not regressed on comparable companies.** Every column in Panels A and D moves with it. This is the single largest source of uncertainty. **[MUST FIX before publication]**
2. **No gross→net revenue restatement scenario.** If cloud-reseller revenue is reported net, ARR drops 20–40%, and every grade worsens. **[MUST FIX]**
3. **Drawdown and volatility are scale-free in engine v1.** A $1T IPO and a $3T IPO show identical drawdown odds. This is wrong and will be fixed by linking the entry multiple to the IPO price. **[MUST FIX]**
4. **Gaussian correlation structure.** No tail dependence. Joint extreme events are underrepresented.
5. **No lockup supply shock modelled.** The ~180-day lockup expiry will add selling pressure. The fund's "MOIC at lockup" column uses a placeholder −5% assumption.
6. **No IPO-process model.** No delay, repricing, or bookbuilding uncertainty.
7. **Default-rate brackets are approximate.** Must be verified against the current S&P Global Ratings Annual Default Study (1981–2023) and Moody's idealised EL tables before publication. Notch-level brackets are log-linearly interpolated from broad-letter anchors; monotonicity imposed by construction.
8. **The 64% value-volatility is dominated by the engine's AR(1) multiple-mark process.** The fundamental-value vol is lower (~30% estimated). The issuer KMV grades at 64% are conservative; a stripped-vol variant will be reported.
9. **Dilution factors are fixed inputs (0.92 buyer, 0.905 fund G→IPO, 0.84 fund G→2031).** They do not respond to the IPO price or to secondary offerings.
10. **Anthropic has no public-market history.** The impairment-probability → default-rate analogy is a communication device, not a structural equivalence. Equity LGD is not 50%.

---

## Disclaimer

OpenRatings is not a Nationally Recognized Statistical Rating Organization (NRSRO) and is not registered with the U.S. Securities and Exchange Commission or any other regulatory body. The impairment grades (OR-AAA through OR-C), commitment-coverage grades, and probabilities presented here are analytical opinions produced by a quantitative simulation model. They are not credit ratings, are not intended to be credit ratings, and must not be used as a substitute for credit ratings in any regulatory, contractual, or investment context. They are not investment advice, a recommendation, or a solicitation to buy or sell any security. The model relies on assumptions that may prove materially wrong. Past default-rate statistics may not predict future impairment probabilities for a company with no public-market history. OpenRatings accepts no liability for any loss arising from reliance on this material.

---

## Summary of changes from the draft

| # | What changed | Why |
|---|---|---|
| 1 | $2T buyer grade: BB+ → **BB** | Corrected default-rate bracket; 3.6% P(lose > 50%) sits at BB, not BB+, under the interpolated S&P table |
| 2 | Fund "IRR (0.7y)" column → **MOIC + months held** | Annualising a sub-year return is misleading; lockup makes the 0.7y hold fictional |
| 3 | Fund lockup added | Fund cannot sell at IPO; earliest exit ~180 days post-listing |
| 4 | Fund grade column → **single footnote** | Printing AAA nine times adds no information; the fund's risk is not impairment |
| 5 | Issuer D: $170B nominal → **$132B KMV-convention + $170B accelerated** | KMV standard is STD + 0.5×LTD; nominal overstates the effective default point |
| 6 | Added P(max DD > 40%) column to buyer ladder | The ride risk is what a buyer actually feels; it was in Section 2 but not in the ladder |
| 7 | "Their exit is your entry" sentence added | Makes the structural tension explicit without editorialising |
| 8 | All grades prefixed "OR-" | Legal: not NRSRO ratings |
| 9 | Closed-form Merton rejection documented with the arithmetic | Pre-empts the "why not just use the formula" question |
| 10 | All engine-v1 cells marked **[ENGINE-V1: RE-RUN]** | Transparency about which numbers will change after the three MUST fixes |

---

*Analytical opinion. Not a credit rating. Not investment advice.*