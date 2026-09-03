# OR-2026-001 — Anthropic expected IPO — evidence

> **Analytical opinion, not investment advice.** See `DISCLOSURES.md`.

The frozen evidence for Open Ratings' first rating action: *Priced as if the Meter Never
Slows* — the expected Anthropic IPO, rated OR-B− at a $2 trillion entry, from a 100,000-path
Monte Carlo engine (v1.5r), with ten pre-registered predictions on the not-yet-filed S-1.

## Authoritative artifacts

The authoritative frozen record is: `article/` (the report source and its typeset PDF),
`predictions/` (the machine-readable calls and resolution rules), `data/` (the exact data the
report's exhibits are built from — byte-identical to what the live page serves), `figures/`,
`referee/` (every pre-publication review, in full), `scoring_protocol.md`, `DISCLOSURES.md`,
and `SHA256SUMS` covering every file here except itself. The live page at
https://openratings.ai/ratings/anthropic-2t/ is **presentation only** — it renders these
artifacts and may evolve cosmetically; the hashes below do not cover it.

## Verify

```
sha256sum -c SHA256SUMS
git tag -v freeze-anthropic-2t-v1.0.0   # if you verify signatures
```

The freeze is fixed by the git tag `freeze-anthropic-2t-v1.0.0`, its full commit SHA, and the
Zenodo deposit (DOI in `FREEZE.md`, written at freeze). The Zenodo record archives this entire
directory, so verification does not depend on this hosting.

## The methodology hash is a commitment, not a disclosure

`predictions/methodology_hash.txt` is the SHA-256 of the private engine methodology file. The
engine is the commercial asset of this practice and is not published. The hash therefore does
not let you verify the methodology today — it lets you verify, when Part 2 is scored, that the
methodology did not move in between. Techniques are named, with update-rule sketches, in the
report's appendix.

## What is deliberately not here

Engine code, calibrations, prompts-as-run for the analyst passes, and model weights (private,
commercial). The Monte Carlo run is characterized by the report's appendix and the exported
aggregates in `data/`; it is a hypothetical scenario analysis, not a reproducible-from-code
artifact in this repository.

## Errata and versioning

The frozen artifacts in this directory are never edited. A material error is handled by a new
dated rating action (an erratum or a superseding version) listed in the top-level Rating
Actions table, leaving this record intact. Scorecards land the same way. If a rating is
withdrawn, the withdrawal is itself a dated action; nothing is deleted.
