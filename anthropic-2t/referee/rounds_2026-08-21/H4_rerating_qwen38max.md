<!-- model: qwen/qwen3.8-max | prompt_tokens: 10706 | completion_tokens: 5021 | latency_s: 90 | date: 2026-08-22 -->

# H4 Re-rate — 2026-08-22

## 1. Overall and sub-ratings

| dimension | H3 | H4 | comment |
|---|---|---|---|
| **Overall** | **6** | **8.5** | Every H3 item is addressed; remaining gaps are clarity and one numerical footnote, not substance |
| Engine / calibration | 6 | 8.5 | Ablation clean, LOO disclosed, interaction negligible, seed/tests green. Docked for n=12 not surfaced in the one-liner |
| Rating mapping & KMV | 5 | 8 | "Analogy" framing correct; brackets sourced; both columns printed with reading note. Docked for the $1T row wording (see Q5) |
| Circular-capital framing | 6 | 9 | "Structural fragility, documented, not a forecast" is the right epistemic status. Lucent analogy precise. No remaining issue |
| Archetype evidence | 7 | 8 | Base-rate prior honest; classifier-at-chance disclosed. Needs a power caveat (see below) |
| Evidence & sourcing | 7 | 9 | Traceability appendix, correction ledger, artifact paths — exemplary |
| Disclosure | 6 | 9 | Panel B required wording, Panel H caveats, bias-direction claim all present and defensible |

---

## 2. Remaining gaps to 9, ranked by points-per-hour

| # | item | action | pts | effort |
|---|---|---|---|---|
| 1 | **4.8× dilution footnote at first mention.** A reader doing $2T ÷ $380B gets 5.26×, not 4.8×. The dilution factor (0.905) is buried in the fund note three paragraphs below the ladder. | **REWORD** — add "(dilution-adjusted; raw = 5.3×)" in parentheses at first use in both card and article | +0.2 | 5 min |
| 2 | **"one-fifth the price" is 0.19, not 0.20.** Trivial, but you asked me to check. | **REWORD** → "one-fifth" is acceptable as rounding; alternatively "a fifth" or "roughly one-fifth." No change needed if you accept 19% ≈ 20%. | +0.0 | 0 |
| 3 | **Correction ledger "20×" reference.** The article says the fund's entry was "richer than the '20×' now claimed for the IPO." The card's own multiples are 22× (model) and 31× (last print). The "20×" is an external claim not sourced in the piece. | **REWORD** — either source the 20× claim ("some commentators cite ~20×") or replace with the card's own numbers | +0.15 | 5 min |
| 4 | **Archetype classifier power caveat.** "The classifier does no better than chance" with n=26 and 4 classes has very low power to detect a real signal. A reader could misread this as "we proved predictability is zero." | **ADD** one sentence: "With 26 listings and four archetypes the test has <30% power to detect a medium effect; the base-rate prior is a conservative default, not a proof of unpredictability." | +0.15 | 5 min |
| 5 | **n=12 in the one-liner.** Panel B discloses it, but the one-liner says "two-thirds of the gap… rests on one calibrated number" without flagging that the calibration set is a dozen comps. A reader who stops at the one-liner misses the fragility. | **REWORD** one-liner: append "…anchored to twelve comparable IPOs (±1σ band in Panel B)" | +0.1 | 2 min |
| 6 | **Panel C $1T row wording** (see Q5 below) | **REWORD** | +0.1 | 10 min |
| 7 | **Headline tone.** "The House Is the Fund That Sold to Them" is now immediately defused in the body. For the article it works. For the *card* one-liner, "house" still carries a connotation of information asymmetry that the body explicitly denies. | **REWORD** card one-liner only: "…and the fund that sold to them is A-grade almost whatever happens next — not because it knows more, but because it paid a fifth of the price." (Already present in the card; the issue is only the article headline.) Acceptable as-is for the article; flag for the card if it ever gets a separate headline. | +0.05 | 0 |

**Total recoverable: ~0.75 points → 9.25 if all done.** Nothing should be CUT; the piece is already tight. The only candidate for cutting is the "correction ledger" section of the article if you want to shorten it for a general audience, but for the openratings.ai audience it's a strength.

---

## 3. Things I would not let print as written

**3a.** Card one-liner, final sentence:

> "Two-thirds of the gap between this verdict and a merely mediocre one rests on one calibrated number, the exit-multiple level, and we show what happens if it is wrong."

This is good but the word "calibrated" is doing work that the disclosure later walks back (the fit is 1.6 SE from the prior, LOO RMSE improvement <0.1%). Suggested rewrite:

> "Two-thirds of the gap between this verdict and a merely mediocre one rests on one number — the exit-multiple level, fitted to twelve comps with a standard error a fifth its size — and we show what happens if it is wrong."

**3b.** Article, correction ledger, second bullet:

> "the entry multiple was ~27×, richer than the '20×' now claimed for the IPO"

The "20×" is unsourced and inconsistent with the card's own 22×/31×. Rewrite:

> "the entry multiple was ~27× on the $14B run-rate at the time — richer than the 22× model-run-rate multiple at the $2T IPO price, though below the 31× last-print multiple"

**3c.** Article, final paragraph:

> "The headline is the bait. The meter is the trap."

This is rhetorical and editorial. For the article it's acceptable as a closing line. For the *card* it would not be acceptable. Since it only appears in the article, I'll let it pass — but flag it if the card ever adopts a similar closing.

---

## 4. Internal consistency check

| claim | arithmetic | verdict |
|---|---|---|
| 22× model run-rate | $2,000B ÷ $90B = 22.2× | ✓ |
| 31× last print | $2,000B ÷ $65B = 30.8× ≈ 31× | ✓ |
| 4.8× fund MOIC at IPO | ($2,000B ÷ $380B) × 0.905 dilution = 4.76 ≈ 4.8× | ✓ but needs footnote (see gap #1) |
| P(lose money) = 50% | Table row $2T: 50% | ✓ |
| P(lose > half) = 17.7% | Table row $2T: 17.7% | ✓ |
| Median fair value $1.25T @10% | Ablation: $1,245B; Panel E: $1.25T | ✓ |
| B− at $2T | 17.7% falls in B ≤14.69 / B− ≤22.03 bracket | ✓ |
| "one-fifth the price" | $380B ÷ $2,000B = 0.19 | ≈ one-fifth; acceptable rounding |
| Fund hold-to-2031 = 4.8× | Same as MOIC at IPO (no further appreciation in median path) | ✓ consistent with engine (value converges to model mark) |

**No inconsistency found.** The only item requiring action is the 4.8× dilution footnote.

---

## 5. KMV marked vs stripped: honest or confusing?

Printing both is **honest and correct** — it's the single best way to show that the breach is a mark-to-market event, not a business failure. The reading note ("every breach in the marked column is a mark-to-market event") is well-placed.

**The $1T row wording needs one tweak.** Currently:

> $1,000B — Amodei's "$1T of compute" → 49.9% marked (D-range) / 1.9% stripped (BBB−)

The problem: a reader sees "D-range" and "BBB−" on the same row and may think the panel is self-contradictory. Add a parenthetical to the row label:

> **$1,000B — Amodei's "$1T of compute"** *(marked: D-range because the multiple can fall below 1×; stripped: BBB− because the business out-earns it)*

This makes the two columns' disagreement *the point* rather than a puzzle.

---

## 6. CoreWeave CDS trigger: 1,200bp

**Defensible.** Current 855bp → trigger at 1,200bp is a ~40% widening, roughly analogous to moving from "stressed" to "distressed" in high-yield CDS convention. It avoids triggering on noise (the 452→881 wobble this year would have fired a 400bp trigger twice).

**Better alternative:** a *relative* trigger ("CoreWeave 5y CDS widens ≥50% from its 30-day trailing median") would adapt to regime changes. But this is harder to pre-register unambiguously. The absolute 1,200bp is simpler to score and defensible. Keep it.

One addition: the trigger says "or a neocloud misses debt service." Define "neocloud" — currently only CoreWeave is named. If you mean "any GPU-collateralised borrower with >$5B of debt," say so.

---

## 7. Would I pre-register this today?

**Yes, with one blocking item:** the 4.8× dilution footnote (gap #1). Without it, a reader who checks the arithmetic gets 5.26× and concludes the card is wrong. That's a credibility hit on day one.

Everything else is non-blocking polish. The disclosure is sufficient, the epistemic framing is honest, the ablation is clean, the comp screen is transparent, and the pre-registered triggers are falsifiable. Ship it after the five-minute fix.