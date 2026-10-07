# Open Ratings — Evidence

The public evidence archive of **[Open Ratings](https://openratings.ai)**, an analytical
research project of [Toryx Inc.](https://toryx.ai)

Open Ratings publishes analytical calls **before** the evidence arrives. Every rating's
calls and methodology are SHA-256 hash-committed here at publication; when the evidence
lands, a five-model LLM panel scores the calls in public, and every referee report is
published in this repository. The record — right or wrong — is permanent: directories are
added, never edited or removed after their freeze.

## Rating actions

| Date | ID | Subject | Rating | Evidence |
|---|---|---|---|---|
| 2026-09-03 | OR-2026-001 | Anthropic — expected IPO | OR-B− at $2T (frozen v1.0.0) | [`anthropic-2t/`](anthropic-2t/) |

Each rating action gets its own directory: `figures/` (the data behind every chart),
`predictions/` (the pre-registered calls and their hashes), `register/` (the issues register),
`provenance/` (source records), and the referee reports. A frozen rating is fixed by a git tag
(`freeze-<slug>-vX.Y.Z`), its full commit SHA, and a Zenodo DOI, all printed in the report.

## Verify the Anthropic freeze

The original `freeze-anthropic-2t-v1.0.0` annotated tag is retained unchanged as part of the
published record. The SSH-signed `attest-freeze-anthropic-2t-v1.0.0` tag points to the exact
same frozen commit (`c2b222207c86abaa5d3864705f48384240f7fb71`) and supplies the missing
cryptographic signature without rewriting the original tag.

```bash
git -c gpg.ssh.allowedSignersFile=.github/allowed_signers \
  verify-tag attest-freeze-anthropic-2t-v1.0.0
```

## Notices

Analytical opinion, not investment advice. Open Ratings is not a registered rating agency,
NRSRO, investment adviser, or broker-dealer; OR-grades are hypothetical model-implied
loss-frequency estimates, not credit ratings. © 2026 Toryx Inc. Open Ratings™ is a trademark
of Toryx Inc.
