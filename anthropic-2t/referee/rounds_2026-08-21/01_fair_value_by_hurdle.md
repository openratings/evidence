# Did we price it? — fair value from the saved engine paths (2026-08-21)

Computed from `sim/out/base/paths.npz` (engine v1, seed 20261016, 100k paths, config 4fa7a969365f8505).
Fair entry value today = dilution (0.92) × exit EV 2031Q4 / (1 + r)^5, per path, by required return r.

| required return r | p5 | p25 | **p50** | p75 | p95 | share of paths where fair value > $2T |
|---|---|---|---|---|---|---|
| 8%  | 752 | 1387 | **2113** | 3226 | 5867 | 0.54 |
| 10% | 686 | 1265 | **1928** | 2943 | 5353 | 0.48 |
| 12% | 627 | 1156 | **1762** | 2690 | 4892 | 0.42 |
| 15% | 549 | 1013 | **1544** | 2357 | 4286 | 0.34 |
| 20% | 444 |  819 | **1248** | 1905 | 3464 | 0.23 |
| 25% | 362 |  668 | **1018** | 1553 | 2825 | 0.14 |
| 35% | 246 |  454 |  **693** | 1057 | 1923 | 0.04 |

($B. Exit EV 2031Q4 p5/25/50/75/95 = 1200 / 2215 / 3375 / 5152 / 9370. IRR from $2T p5/25/50/75/95 = −11% / 0% / 9% / 19% / 34%.)

Reading: the engine does contain a price, it was never printed. At a public-equity required return (10–12%) the model's median fair value is $1.8–1.9T — the $2T IPO sits near the median, roughly a coin flip. At a venture hurdle (35%) the median is $0.7T and $2T is at the 96th percentile. The article's "4% chance of 35% IRR" is true but is the wrong hurdle for an IPO buyer; the honest headline is "$2T is fair only if you would accept ~9–10% a year with a one-in-four chance of losing money, and is absurd at any venture hurdle." This table must go in W2_engine_review and the article.

Caveats carried from the engine: exit multiple is a written-down prior (not regressed), no gross→net restatement scenario, no lockup/float, Gaussian correlations. All of these push the distribution down, none up.

Analytical opinion, not investment advice.
