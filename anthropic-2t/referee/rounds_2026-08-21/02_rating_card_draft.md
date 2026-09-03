# "OpenRatings rates the Anthropic IPO" — rating-card draft (2026-08-21)

Computed from the saved engine-v1 paths (`sim/out/base/paths.npz`, seed 20261016, 100k paths, 5-year horizon, dilution 0.92).
No new model; this is the same engine read out the way a buyer would want it. Analytical opinion, not investment advice.

## 1. The price ladder — what you get at each IPO price

| IPO valuation | EV / run-rate (@ $90B) | IRR median (p25–p75) | P(earn ≥10%/yr) | P(earn ≥20%/yr) | P(lose money) | P(lose > half) | expected loss | grade* |
|---|---|---|---|---|---|---|---|---|
| $0.75T | 8× | 33% (22–45) | 93% | 79% | 1% | 0.0% | 0.2% | AA |
| $1.00T | 11× | 25% (15–37) | 85% | 64% | 4% | 0.2% | 0.7% | A |
| $1.25T | 14× | 20% (10–31) | 76% | 50% | 7% | 0.5% | 1.6% | A− |
| $1.50T | 17× | 16% (6–26) | 66% | 38% | 12% | 1.2% | 3.0% | BBB |
| $1.75T | 19× | 12% (3–22) | 56% | 29% | 18% | 2.2% | 4.7% | BB+ |
| **$2.00T** | **22×** | **9% (0–19)** | **48%** | **23%** | **24%** | **3.6%** | **6.7%** | **BB** |
| $2.50T | 28× | 4% (−4–14) | 34% | 13% | 36% | 7.3% | 11.5% | BB− |
| $3.00T | 33× | 1% (−7–10) | 24% | 8% | 48% | 12.3% | 16.6% | B |

\*Grade = the corporate-bond rating whose 5-year cumulative default rate brackets P(lose > half). Brackets used: AAA ≤0.4%, AA ≤0.5%, A ≤0.8%, BBB ≤2%, BB ≤8%, B ≤20%, CCC above (approximate, S&P long-run corporate history — **verify against the current S&P/Moody's default study before publication**). "Lose more than half in five years" is the equity analogue of a default with ~50% recovery. Expected loss shown alongside because it credits magnitude, not just frequency.

Reading: **at $1.5T the odds of permanent impairment are investment-grade; at $2T they are BB — junk; at $3T, single-B.** The $2T buyer is paid a median 9%/yr for BB-grade impairment risk — roughly what a BB bond paid in 2025 — while taking equity volatility.

## 2. The ride — same at every price (engine-v1 limitation, see §5)

| | value |
|---|---|
| chance the stock is ≥40% below the IPO price at some point in the first 2 years | 36% |
| chance of a ≥40% fall from a peak in the first 2 years | 76% |
| median worst drawdown from IPO price, first 2 years | −27% (p25 −49%, p75 −1%) |
| annualised volatility of the price path, first 2 years | 62% (p25 49%, p75 76%) |
| if growth prints <30% annualised two quarters running (13% chance): P(≥40% drawdown) | 63% |

## 3. "What should I pay?" — the ladder inverted

| if you require … per year | the model's median fair IPO value | share of futures in which $2T is cheap |
|---|---|---|
| 8% | $2.1T | 54% |
| 10% | $1.9T | 48% |
| 12% | $1.8T | 42% |
| 15% | $1.5T | 34% |
| 20% | $1.2T | 23% |
| 35% (venture) | $0.7T | 4% |

## 4. What downgrades it (pre-registered triggers)
- two consecutive quarterly prints of metered growth < 30% annualised → the 63% drawdown branch
- S-1 restates cloud-reseller revenue gross → net (20–40% ARR haircut): every row above shifts one to two notches down (not yet modelled — MUST item)
- gross margin printing < 35% (PitchBook cliff) — not yet modelled
- a second export-control episode within 12 months of listing

## 5. Honesty notes / what to fix before this goes on openratings.ai
- Drawdown and vol are scale-free in engine v1: the mark path is `VAL/VAL[0] × entry`, so a $1T IPO and a $3T IPO have identical drawdown odds. In reality a cheaper IPO has less to fall. Fix: make the starting multiple depend on the entry price and let it revert toward the fundamental multiple — this is the one engine change the rating card needs.
- Exit multiple is a written-down prior, not regressed on comps (Qwen D, improvement #1). Every column moves with it.
- No gross→net restatement, no lockup supply shock, Gaussian tails — all push the grades down, none up.
- The MCTS/decision layer is not needed for this card. It is needed only for the *timing* card — buy at IPO vs wait for the first print vs wait for lockup — which is the natural second exhibit.

---

## 6. KMV-style issuer rating — value of the business vs what it owes (added 2026-08-21, after Luis's note)

Merton/KMV: a firm defaults when the value of the business falls below its obligations; distance-to-default = how many standard deviations of value-volatility separate the two; EDF = probability of crossing within the horizon. Anthropic carries almost no debt, but it carries debt-like take-or-pay compute commitments: >$100B to AWS over 10 years (Apr-2026), Google TPUs "tens of billions" (~$40B), ~$30B Azure — roughly **$170B nominal, ~$24B/yr** (Evidence C, F). Amodei's own framing of the tail: "if I buy ~$1T of compute for 2027 and revenue is $800B, no force on earth stops me going bankrupt."

Computed from the engine's fundamental-value paths (`VAL`, 100k paths): P(value falls below the default point D at any quarter within the horizon). Engine median annualised vol of fundamental value = 64% (equity-like; Anthropic is unlevered so asset vol ≈ equity vol, but most of this is the engine's multiple noise — see caveats).

| default point D (debt-like commitments) | 1y | 2y | 3y | 5y EDF | grade (5y default-rate brackets) |
|---|---|---|---|---|---|
| $100B | 0.000 | 0.000 | 0.000 | 0.000 | AAA |
| **$170B — what is disclosed today** | **0.000** | **0.000** | **0.000** | **0.000** | **AAA** |
| $250B | 0.000 | 0.000 | 0.000 | 0.000 | AAA |
| $500B | 0.000 | 0.002 | 0.004 | 0.008 | A |
| $750B | 0.006 | 0.017 | 0.031 | 0.052 | BB+ |
| **$1,000B — Amodei's "$1T of compute"** | 0.023 | 0.059 | 0.094 | **0.145** | **B+** |
| $1,500B | 0.102 | 0.210 | 0.293 | 0.394 | CCC |

Downgrade schedule — the default point at which the 5-year EDF crosses each grade: A below $525B · BBB at $625B · BB at $825B · B at $1,075B · CCC at $1,625B.

Coverage lens (can operating gross profit pay the commitments, without raising capital): median gross profit (ARR × GM) $75B in year 1 → $171B in year 5. Against $24B/yr of commitments: never short. Against $100B/yr: 86% short in year 1, 14% by year 5. Against $200B/yr: 63% still short in year 5.

**Reading.** Two ratings, two different things:
- **Issuer (KMV): AAA against what Anthropic has actually signed.** Its value would have to fall ~95% to breach $170B. The rating is a function of the compute bet, not of the IPO price: every ~$100B of additional take-or-pay is roughly a notch; at the $1T figure it is single-B; at $1.5T, CCC.
- **Buyer at $2T (section 1): BB.** That is about the price paid, not the company. A sound issuer can still be a junk-grade entry.

The card headline writes itself: *"Anthropic the company: AAA on disclosed commitments, B if it buys the trillion. Anthropic the stock at $2T: BB."*

Caveats before this is published: D should be the PV of the scheduled payments (declining as paid, rising as new deals are signed), not a nominal constant; the engine's fundamental value at entry (median $3.2T) sits above the $2T IPO price because the exit-multiple prior is generous — Qwen's #1 fix (regress on comps) moves both ratings; the 64% value-vol is mostly mark noise, so a "true asset vol" variant (strip the AR(1) mark noise) should be run and will make the issuer grade better, not worse; closed-form Merton with V0 = $2T and σ = 64% gives a meaningless DD ≈ 1 at D = $170B — use the path-based numbers, not the formula, and say why; default-rate brackets are approximate and must be checked against the current S&P/Moody's study.

Analytical opinion, not investment advice.
