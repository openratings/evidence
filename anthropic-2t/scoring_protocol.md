# OR-2026-001 — LLM panel scoring protocol (frozen at publication)

Committed before the S-1 exists, so the scorecard cannot be shaped after the fact.

## Panel
One reviewer per independent model family, same five that refereed the pre-publication text:

| family | model id | access |
|---|---|---|
| xAI | grok-4-3 | Azure AI Foundry |
| DeepSeek | deepseek-v4-pro | Azure AI Foundry |
| Anthropic | claude-opus-5 | AWS Bedrock |
| Google | gemini-3.1-pro-preview | Vertex AI |
| Alibaba | qwen3.8-max | Alibaba Model Studio |

If a listed model is unavailable at scoring time, its family's nearest available successor is
used and the substitution is disclosed on the scorecard.

## Procedure
- Input: the frozen predictions (calls.json) plus the resolving evidence (the filed S-1 text
  for document predictions; pricing/tape data for the market and path predictions).
- Each model scores each prediction independently: right / wrong / unresolvable, with a
  one-paragraph justification citing the evidence location. Temperature 0. No cross-talk;
  no model sees another's output. Single round.
- Aggregation: per prediction, the majority verdict of the five stands; ties or a 2-2-1 split
  resolve to unresolvable. Every individual verdict and justification is published verbatim,
  including dissents.
- Conflict handling: the Anthropic model scores predictions about Anthropic's own listing;
  it is included, its verdicts are published, and the scorecard reports the aggregate both
  with and without it.
- Human role: publication of the panel's output as-is. A human may annotate, never override;
  any annotation is labeled as such.

## Scoring prompt template (frozen)
Each model receives a single message containing, in order: (1) this protocol; (2) calls.json
verbatim; (3) the resolving evidence — the relevant S-1 excerpts with their locations, or the
pricing/tape data; (4) the instruction to return exactly this JSON and nothing else:

    {"scores": [{"id": <n>, "verdict": "right" | "wrong" | "unresolvable",
                 "justification": "<one paragraph>",
                 "evidence_location": "<where in the evidence>"}]}

Temperature 0. No other context, no tools, no cross-talk. Raw replies are published verbatim.

## Reporting
Coverage (share resolvable) and accuracy (share of resolvable scored right) are reported
separately. The scorecard is a new dated rating action; the frozen report is never edited.

## Appendix — the pre-publication review-round protocol (P1, as run)

The five-family panel that refereed the article before publication used this rubric and these instructions, assembled into one pack with the frozen article text appended. Raw per-reviewer replies are published in the referee record.

### Rubric (python literal, verbatim from the runner)

```python
RUBRIC = [
    ("grounding",     "Evidence grounding: does every load-bearing number trace to a named, dated source, and are the unsourced ones labelled as estimates?"),
    ("engine",        "Valuation logic: does the stated method actually produce the OR-B- grade at a $2T entry, and are the branch probabilities defensible?"),
    ("substitution",  "The substitution/headwind argument: is the price-decline evidence sufficient for the weight the argument carries?"),
    ("pentagon",      "The Pentagon episode: is the designation/ChatGPT.mil material handled without overclaiming what it shows?"),
    ("scoreability",  "Pre-registered calls: is each call resolvable to right/wrong/unresolvable against a NAMED S-1 section with no interpretive room?"),
    ("calibration",   "Pre-registered calls: are the bands genuinely at risk -- neither near-certain nor unfalsifiable? Name any call that is a free win."),
    ("independence",  "Conflict handling: is the author's interest disclosed adequately for a reader deciding whether to act on this?"),
    ("overreach",     "Unsupported claims: score HIGH when the piece stays inside its evidence. Name every sentence that outruns it."),
    ("figures",       "Do the figures and tables support the claims they are cited for, and does any caption misstate its own data?"),
    ("clarity",       "Clarity for the stated audience (institutional credit and equity readers) without dumbing down the method."),
]
```

### Instructions (verbatim)

```
\
Score the article below on each of the ten rubric items, 1-10 (integers).

Then answer two questions in prose:

  ATTACK: Quote the SINGLE sentence in this article that a hostile, well-informed
  reader would most effectively attack, and say in two sentences how they would
  attack it. Quote it verbatim.

  KILL: Name the one change that would most raise the article's credibility with a
  sceptical institutional reader. One change, not a list.

Return ONLY a JSON object with this exact shape:

{
  "scores": {"grounding": 0, "engine": 0, "substitution": 0, "pentagon": 0,
             "scoreability": 0, "calibration": 0, "independence": 0,
             "overreach": 0, "figures": 0, "clarity": 0},
  "notes":  {"grounding": "one sentence", ...one per item...},
  "attack_quote": "verbatim sentence from the article",
  "attack_why": "two sentences",
  "kill": "one change",
  "overall": 0.0
}

"overall" is your own holistic 1-10 for the article as a whole. It is NOT required
to equal the mean of the items -- if it differs, say why in notes.clarity.
```
