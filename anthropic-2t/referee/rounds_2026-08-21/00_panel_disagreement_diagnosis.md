# Why pilot_s1 and pilot_s2 disagree — diagnostic extracted from the run logs (2026-08-21)

Same protocol, same evidence pack, same four analyst models, same judge (gpt-oss-120b), run back-to-back on 2026-08-17 (04:13–04:48Z and 04:48–05:18Z). Differences: seed (20261016 vs 8675309), round-0 model→seat assignment (Latin-square offset), and pilot_s2 added parameter bounds on simulation requests.

Headline: terminal "all-seat" median P(IRR≥35% @ $2T) = 0.145 (s1) vs 0.045 (s2).

## 1. Every seat starts at the engine's base number
Round-0 p35 by seat: s1 = 0.045, 0.044, 0.146, 0.044, 0.045, 0.044, 0.04, 0.044, 0.044, 0.044, 0.04, 0.044. s2 nearly identical. The evidence pack contains E139 = "W2 base run: P(IRR≥35%) = 0.044". The analysts copy it. No seat formed an independent prior; bulls and bears alike report 4.4%.

## 2. Every later value is a copy of a simulation-request output
Distinct sim results (p35) in s1: S-0-2 (tau=8) = 0.1452; S-1-5 = 0.2823; ... Terminal seats: bulls 0.282 (=S-1-5), neutrals 0.145 (=S-0-2 / S-2-9), bears 0.000–0.044.
In s2: S-0-1/S-0-2 (g0=2, tau=8) = 0.3885; S-0-3 = 0.4309; S-0-4 = 0.1777; S-3-12 = 0.0453. Terminal seats: bulls 0.431 / 0.508 / 0.389 / 0.178, neutrals 0.045, bears ≤0.008.
Each number an analyst reports is, to three decimals, a number the engine printed. The panel is relaying engine outputs, not forming beliefs.

## 3. The "all" consensus is structurally the neutral median
12 seats = 4 bull + 4 bear + 4 neutral. Bulls sit above, bears below, so the median of 12 is always inside the neutral group. "All" = "neutral". The by-model table is also uninformative for the same reason: each model holds one bull, one bear, one neutral seat each round, so its median is its neutral seat.

## 4. So the 3x gap is: did the neutrals adopt a tau=8 run or not
s1 neutral trajectories (p35): all four at 0.044 through round 2; neutral-B moves to 0.145 in round 3 citing S-2-9 (tau=8 alone, result 0.1452); neutral-A follows round 4, neutral-D round 5, neutral-C round 6 — all citing S-2-9, all classified "evidence" by the judge. All four neutral seats were held by the qwen model in the round they moved (seats rotate; the revision log shows model=qwen for every neutral move).
s2 neutral trajectories: all four stay at 0.044–0.045 for seven rounds. No tau=8-alone simulation was ever requested in s2; the bulls requested g0=2.0+tau=8 (0.389–0.431), which the neutrals did not adopt. The only neutral-side sim (S-3-12) returned 0.0453 ≈ base.

## 5. What the judge counted as "evidence"
"S-2-9 reports 0.145, I now say 0.145" was classified as an evidence-driven revision. It is a copy of a requested-and-run number; it did not weigh base vs tau=8, it replaced one with the other. The anti-sycophancy rule as implemented checks *citation*, not *reasoning*.

## 6. Convergence did not happen; the stopping rule fired on stasis
Dispersion across seats (sd of p35) rose every round in both runs (s1: 0.030 → 0.107; s2: 0.040 → 0.194). The runs stopped at the round cap with persona groups farther apart than at the start. "Converged" in FINAL.md means "deltas below threshold two rounds in a row", which stasis also satisfies.

## 7. Other facts relevant to interpretation
- Sim requests are the only new information entering the rounds; facts do not change. So the trajectories are a function of which deltas got requested in which order, which depends on seed and seat assignment.
- s1 had one absurd run (S-0-1, g_term=1.8 → p35=1.0) which bounds later prevented in s2.
- The judge for both pilots was gpt-oss-120b. models.yaml now points the judge at qwen/qwen3.8-max (same family as the qwen analyst) — flagged in the file, not yet resolved.
- Revision counts: s1 36 evidence / 3 conformity / 1 rejected; s2 29 / 9 / 3.
