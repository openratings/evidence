# SWE-bench Verified Error-Correlation Matrix (2026-04-22)

## Overview

- **Models**: 17
- **Instances**: 117 (complete task overlap)
- **Note**: Absolute f2p_passed counts are unreliable pending #549 rescore. Correlation patterns are the useful signal.

## Model Performance Summary

| Model | correct | f2p_passed | solve rate |
|-------|--------:|-----------:|-----------:|
| claude-sonnet-4 | 1 | 1 | 1/117 |
| deepseek-v3 | 1 | 1 | 1/117 |
| gemini-3-flash | 2 | 2 | 2/117 |
| gemma-3n-e4b | 0 | 0 | 0/117 |
| glm-5 | 6 | 8 | 6/117 |
| gpt-4.1 | 1 | 1 | 1/117 |
| gpt-oss-120b-fw | 11 | 13 | 11/117 |
| kimi-k2.5 | 0 | 0 | 0/117 |
| llama-3.3-70b | 0 | 0 | 0/117 |
| minimax-m2.5 | 0 | 0 | 0/117 |
| qwen-plus | 0 | 0 | 0/117 |
| qwen2.5-vl-72b | 0 | 0 | 0/117 |
| qwen3-max | 13 | 17 | 13/117 |
| qwen3-vl-235b | 1 | 2 | 1/117 |
| qwen3-vl-8b | 1 | 1 | 1/117 |
| qwen3.5-122b | 1 | 2 | 1/117 |
| qwen3.5-397b | 2 | 2 | 2/117 |

### Pearson Correlation (correct)

```
                          claude-son deepseek-v gemini-3-f gemma-3n-e      glm-5    gpt-4.1 gpt-oss-12  kimi-k2.5 llama-3.3- minimax-m2  qwen-plus qwen2.5-vl  qwen3-max qwen3-vl-2 qwen3-vl-8 qwen3.5-12 qwen3.5-39
          claude-sonnet-4      1.000      1.000     -0.012      0.000      0.399      1.000      0.288      0.000      0.000      0.000      0.000      0.000     -0.033     -0.009     -0.009     -0.009     -0.012
              deepseek-v3      1.000      1.000     -0.012      0.000      0.399      1.000      0.288      0.000      0.000      0.000      0.000      0.000     -0.033     -0.009     -0.009     -0.009     -0.012
           gemini-3-flash     -0.012     -0.012      1.000      0.000     -0.031     -0.012      0.183      0.000      0.000      0.000      0.000      0.000      0.163     -0.012     -0.012     -0.012     -0.017
             gemma-3n-e4b      0.000      0.000      0.000      1.000      0.000      0.000      0.000      0.000      0.000      0.000      0.000      0.000      0.000      0.000      0.000      0.000      0.000
                    glm-5      0.399      0.399     -0.031      0.000      1.000      0.399      0.456      0.000      0.000      0.000      0.000      0.000      0.411      0.399     -0.022      0.399      0.268
                  gpt-4.1      1.000      1.000     -0.012      0.000      0.399      1.000      0.288      0.000      0.000      0.000      0.000      0.000     -0.033     -0.009     -0.009     -0.009     -0.012
          gpt-oss-120b-fw      0.288      0.288      0.183      0.000      0.456      0.288      1.000      0.000      0.000      0.000      0.000      0.000      0.445     -0.030      0.288     -0.030      0.183
                kimi-k2.5      0.000      0.000      0.000      0.000      0.000      0.000      0.000      1.000      0.000      0.000      0.000      0.000      0.000      0.000      0.000      0.000      0.000
            llama-3.3-70b      0.000      0.000      0.000      0.000      0.000      0.000      0.000      0.000      1.000      0.000      0.000      0.000      0.000      0.000      0.000      0.000      0.000
             minimax-m2.5      0.000      0.000      0.000      0.000      0.000      0.000      0.000      0.000      0.000      1.000      0.000      0.000      0.000      0.000      0.000      0.000      0.000
                qwen-plus      0.000      0.000      0.000      0.000      0.000      0.000      0.000      0.000      0.000      0.000      1.000      0.000      0.000      0.000      0.000      0.000      0.000
           qwen2.5-vl-72b      0.000      0.000      0.000      0.000      0.000      0.000      0.000      0.000      0.000      0.000      0.000      1.000      0.000      0.000      0.000      0.000      0.000
                qwen3-max     -0.033     -0.033      0.163      0.000      0.411     -0.033      0.445      0.000      0.000      0.000      0.000      0.000      1.000      0.263      0.263      0.263      0.373
            qwen3-vl-235b     -0.009     -0.009     -0.012      0.000      0.399     -0.009     -0.030      0.000      0.000      0.000      0.000      0.000      0.263      1.000     -0.009      1.000     -0.012
              qwen3-vl-8b     -0.009     -0.009     -0.012      0.000     -0.022     -0.009      0.288      0.000      0.000      0.000      0.000      0.000      0.263     -0.009      1.000     -0.009     -0.012
             qwen3.5-122b     -0.009     -0.009     -0.012      0.000      0.399     -0.009     -0.030      0.000      0.000      0.000      0.000      0.000      0.263      1.000     -0.009      1.000     -0.012
             qwen3.5-397b     -0.012     -0.012     -0.017      0.000      0.268     -0.012      0.183      0.000      0.000      0.000      0.000      0.000      0.373     -0.012     -0.012     -0.012      1.000
```

### Jaccard Index (f2p_passed > 0)

```
                          claude-son deepseek-v gemini-3-f gemma-3n-e      glm-5    gpt-4.1 gpt-oss-12  kimi-k2.5 llama-3.3- minimax-m2  qwen-plus qwen2.5-vl  qwen3-max qwen3-vl-2 qwen3-vl-8 qwen3.5-12 qwen3.5-39
          claude-sonnet-4      1.000      1.000      0.000      0.000      0.167      1.000      0.091      0.000      0.000      0.000      0.000      0.000      0.000      0.000      0.000      0.000      0.000
              deepseek-v3      1.000      1.000      0.000      0.000      0.167      1.000      0.091      0.000      0.000      0.000      0.000      0.000      0.000      0.000      0.000      0.000      0.000
           gemini-3-flash      0.000      0.000      1.000      0.000      0.000      0.000      0.083      0.000      0.000      0.000      0.000      0.000      0.067      0.000      0.000      0.000      0.000
             gemma-3n-e4b      0.000      0.000      0.000      0.000      0.000      0.000      0.000      0.000      0.000      0.000      0.000      0.000      0.000      0.000      0.000      0.000      0.000
                    glm-5      0.167      0.167      0.000      0.000      1.000      0.167      0.308      0.000      0.000      0.000      0.000      0.000      0.250      0.167      0.000      0.167      0.143
                  gpt-4.1      1.000      1.000      0.000      0.000      0.167      1.000      0.091      0.000      0.000      0.000      0.000      0.000      0.000      0.000      0.000      0.000      0.000
          gpt-oss-120b-fw      0.091      0.091      0.083      0.000      0.308      0.091      1.000      0.000      0.000      0.000      0.000      0.000      0.316      0.000      0.091      0.000      0.083
                kimi-k2.5      0.000      0.000      0.000      0.000      0.000      0.000      0.000      0.000      0.000      0.000      0.000      0.000      0.000      0.000      0.000      0.000      0.000
            llama-3.3-70b      0.000      0.000      0.000      0.000      0.000      0.000      0.000      0.000      0.000      0.000      0.000      0.000      0.000      0.000      0.000      0.000      0.000
             minimax-m2.5      0.000      0.000      0.000      0.000      0.000      0.000      0.000      0.000      0.000      0.000      0.000      0.000      0.000      0.000      0.000      0.000      0.000
                qwen-plus      0.000      0.000      0.000      0.000      0.000      0.000      0.000      0.000      0.000      0.000      0.000      0.000      0.000      0.000      0.000      0.000      0.000
           qwen2.5-vl-72b      0.000      0.000      0.000      0.000      0.000      0.000      0.000      0.000      0.000      0.000      0.000      0.000      0.000      0.000      0.000      0.000      0.000
                qwen3-max      0.000      0.000      0.067      0.000      0.250      0.000      0.316      0.000      0.000      0.000      0.000      0.000      1.000      0.071      0.071      0.071      0.143
            qwen3-vl-235b      0.000      0.000      0.000      0.000      0.167      0.000      0.000      0.000      0.000      0.000      0.000      0.000      0.071      1.000      0.000      1.000      0.000
              qwen3-vl-8b      0.000      0.000      0.000      0.000      0.000      0.000      0.091      0.000      0.000      0.000      0.000      0.000      0.071      0.000      1.000      0.000      0.000
             qwen3.5-122b      0.000      0.000      0.000      0.000      0.167      0.000      0.000      0.000      0.000      0.000      0.000      0.000      0.071      1.000      0.000      1.000      0.000
             qwen3.5-397b      0.000      0.000      0.000      0.000      0.143      0.000      0.083      0.000      0.000      0.000      0.000      0.000      0.143      0.000      0.000      0.000      1.000
```

### Phi Coefficient (correct > 0)

```
                          claude-son deepseek-v gemini-3-f gemma-3n-e      glm-5    gpt-4.1 gpt-oss-12  kimi-k2.5 llama-3.3- minimax-m2  qwen-plus qwen2.5-vl  qwen3-max qwen3-vl-2 qwen3-vl-8 qwen3.5-12 qwen3.5-39
          claude-sonnet-4      1.000      1.000     -0.007      0.000      0.399      1.000      0.288      0.000      0.000      0.000      0.000      0.000     -0.022     -0.004     -0.004     -0.004     -0.007
              deepseek-v3      1.000      1.000     -0.007      0.000      0.399      1.000      0.288      0.000      0.000      0.000      0.000      0.000     -0.022     -0.004     -0.004     -0.004     -0.007
           gemini-3-flash     -0.005     -0.005      1.000      0.000     -0.019     -0.005      0.143      0.000      0.000      0.000      0.000      0.000      0.128     -0.005     -0.005     -0.005     -0.009
             gemma-3n-e4b      0.000      0.000      0.000      1.000      0.000      0.000      0.000      0.000      0.000      0.000      0.000      0.000      0.000      0.000      0.000      0.000      0.000
                    glm-5      0.120      0.120     -0.011      0.000      1.000      0.120      0.363      0.000      0.000      0.000      0.000      0.000      0.331      0.120     -0.006      0.120      0.106
                  gpt-4.1      1.000      1.000     -0.007      0.000      0.399      1.000      0.288      0.000      0.000      0.000      0.000      0.000     -0.022     -0.004     -0.004     -0.004     -0.007
          gpt-oss-120b-fw      0.063      0.063      0.054      0.000      0.242      0.063      1.000      0.000      0.000      0.000      0.000      0.000      0.314     -0.006      0.063     -0.006      0.054
                kimi-k2.5      0.000      0.000      0.000      0.000      0.000      0.000      0.000      1.000      0.000      0.000      0.000      0.000      0.000      0.000      0.000      0.000      0.000
            llama-3.3-70b      0.000      0.000      0.000      0.000      0.000      0.000      0.000      0.000      1.000      0.000      0.000      0.000      0.000      0.000      0.000      0.000      0.000
             minimax-m2.5      0.000      0.000      0.000      0.000      0.000      0.000      0.000      0.000      0.000      1.000      0.000      0.000      0.000      0.000      0.000      0.000      0.000
                qwen-plus      0.000      0.000      0.000      0.000      0.000      0.000      0.000      0.000      0.000      0.000      1.000      0.000      0.000      0.000      0.000      0.000      0.000
           qwen2.5-vl-72b      0.000      0.000      0.000      0.000      0.000      0.000      0.000      0.000      0.000      0.000      0.000      1.000      0.000      0.000      0.000      0.000      0.000
                qwen3-max     -0.006     -0.006      0.044      0.000      0.200     -0.006      0.281      0.000      0.000      0.000      0.000      0.000      1.000      0.053      0.053      0.053      0.108
            qwen3-vl-235b     -0.004     -0.004     -0.007      0.000      0.399     -0.004     -0.020      0.000      0.000      0.000      0.000      0.000      0.263      1.000     -0.004      1.000     -0.007
              qwen3-vl-8b     -0.004     -0.004     -0.007      0.000     -0.014     -0.004      0.288      0.000      0.000      0.000      0.000      0.000      0.263     -0.004      1.000     -0.004     -0.007
             qwen3.5-122b     -0.004     -0.004     -0.007      0.000      0.399     -0.004     -0.020      0.000      0.000      0.000      0.000      0.000      0.263      1.000     -0.004      1.000     -0.007
             qwen3.5-397b     -0.005     -0.005     -0.009      0.000      0.203     -0.005      0.143      0.000      0.000      0.000      0.000      0.000      0.373     -0.005     -0.005     -0.005      1.000
```

## Oracle Pairs (Lowest Correlation)

Low-correlation pairs fail on different instances — most valuable for ensemble voting.

### By Pearson (correct)

| Rank | Model A | Model B | Pearson |
|-----:|---------|---------|--------:|
| 1 | claude-sonnet-4 | qwen3-max | -0.0328 |
| 2 | deepseek-v3 | qwen3-max | -0.0328 |
| 3 | gpt-4.1 | qwen3-max | -0.0328 |
| 4 | gemini-3-flash | glm-5 | -0.0307 |
| 5 | gpt-oss-120b-fw | qwen3-vl-235b | -0.0299 |

### By Jaccard (f2p_passed > 0)

| Rank | Model A | Model B | Jaccard |
|-----:|---------|---------|--------:|
| 1 | claude-sonnet-4 | gemini-3-flash | 0.0000 |
| 2 | claude-sonnet-4 | qwen3-max | 0.0000 |
| 3 | claude-sonnet-4 | qwen3-vl-235b | 0.0000 |
| 4 | claude-sonnet-4 | qwen3-vl-8b | 0.0000 |
| 5 | claude-sonnet-4 | qwen3.5-122b | 0.0000 |

## Redundant Pairs (Highest Correlation)

High-correlation pairs fail on the same instances — redundant for ensembles.

### By Pearson (correct)

| Rank | Model A | Model B | Pearson |
|-----:|---------|---------|--------:|
| 1 | glm-5 | gpt-oss-120b-fw | 0.4562 |
| 2 | claude-sonnet-4 | deepseek-v3 | 1.0000 |
| 3 | claude-sonnet-4 | gpt-4.1 | 1.0000 |
| 4 | deepseek-v3 | gpt-4.1 | 1.0000 |
| 5 | qwen3-vl-235b | qwen3.5-122b | 1.0000 |

### By Jaccard (f2p_passed > 0)

| Rank | Model A | Model B | Jaccard |
|-----:|---------|---------|--------:|
| 1 | gpt-oss-120b-fw | qwen3-max | 0.3158 |
| 2 | claude-sonnet-4 | deepseek-v3 | 1.0000 |
| 3 | claude-sonnet-4 | gpt-4.1 | 1.0000 |
| 4 | deepseek-v3 | gpt-4.1 | 1.0000 |
| 5 | qwen3-vl-235b | qwen3.5-122b | 1.0000 |

## 3-Model Ensemble Recommendation

Optimal trios for 2/3 majority voting (#370) — lowest average pairwise Pearson correlation.

### #1: claude-sonnet-4 + qwen3-vl-235b + qwen3-vl-8b

- Avg pairwise Pearson: 0.0086
- Max pairwise Pearson: 0.0086
  - claude-sonnet-4-qwen3-vl-235b: -0.0086
  - claude-sonnet-4-qwen3-vl-8b: -0.0086
  - qwen3-vl-235b-qwen3-vl-8b: -0.0086

### #2: claude-sonnet-4 + qwen3-vl-8b + qwen3.5-122b

- Avg pairwise Pearson: 0.0086
- Max pairwise Pearson: 0.0086
  - claude-sonnet-4-qwen3-vl-8b: -0.0086
  - claude-sonnet-4-qwen3.5-122b: -0.0086
  - qwen3-vl-8b-qwen3.5-122b: -0.0086

### #3: deepseek-v3 + qwen3-vl-235b + qwen3-vl-8b

- Avg pairwise Pearson: 0.0086
- Max pairwise Pearson: 0.0086
  - deepseek-v3-qwen3-vl-235b: -0.0086
  - deepseek-v3-qwen3-vl-8b: -0.0086
  - qwen3-vl-235b-qwen3-vl-8b: -0.0086

### #4: deepseek-v3 + qwen3-vl-8b + qwen3.5-122b

- Avg pairwise Pearson: 0.0086
- Max pairwise Pearson: 0.0086
  - deepseek-v3-qwen3-vl-8b: -0.0086
  - deepseek-v3-qwen3.5-122b: -0.0086
  - qwen3-vl-8b-qwen3.5-122b: -0.0086

### #5: gpt-4.1 + qwen3-vl-235b + qwen3-vl-8b

- Avg pairwise Pearson: 0.0086
- Max pairwise Pearson: 0.0086
  - gpt-4.1-qwen3-vl-235b: -0.0086
  - gpt-4.1-qwen3-vl-8b: -0.0086
  - qwen3-vl-235b-qwen3-vl-8b: -0.0086

## Methodology

- **Pearson**: correlation of binary `correct` (0/1) vectors across 117 instances
- **Jaccard**: |A∩B| / |A∪B| where A,B = sets of instances with `f2p_passed > 0`
- **Phi**: Matthews phi coefficient on 2×2 contingency table of `correct > 0`
- **Oracle pairs**: lowest correlation → models fail on different instances
- **Redundant pairs**: highest correlation → models fail on same instances
- **Ensemble selection**: minimize avg pairwise Pearson across all 3-choose combinations

## Dependencies

- #549 — R0 rescore (improves absolute numbers; doesn't block this)
- #370 — HLE + APEX HRP clustering + 2/3 voting (this feeds that)
