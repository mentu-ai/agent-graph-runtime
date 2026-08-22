# Claude Science return audit — 29 July 2026

## Verdict

The return is authentic provenance for an earlier Claude Science
manuscript-construction session, but it is not the requested Operon literature
certification or blind review of `paper-v0.9.1-internal.pdf`. It must not be
copied into `operon/`, used to open release mode, or treated as authority to
replace the canonical manuscript.

The downloaded files remain in a private, ignored provenance directory. This
audit records only hashes, structural facts, and dispositions; the raw export
and returned bundle are excluded from Git and every public source archive.

## Input identities

| Input | Bytes | SHA-256 |
|---|---:|---|
| Raw Claude Science export | 4,448,126 | `9216bb130380c08ade726286a27acf33be3102881d8f7dc241ba9b1b61639ee3` |
| Returned `PRIOR-ART-VERIFIED.json` | 59,553 | `f475aaa25a034f076f2d67480ca3ca7585f428604e7f601192a8e6a9a8cdcf48` |
| Returned `LITERATURE-MATRIX.md` | 20,462 | `677e4a27efd97349ca06a5d4dfeb76eecde4de62bb987be670f2f88a5121d706` |
| Returned `MANUSCRIPT-v1.md` | 32,596 | `75c9a312e54bf6036861c430c843af239ae16b1ac6704725361e8c3f53ff1c1d` |
| Returned `ADVERSARIAL-REVIEW.md` | 8,251 | `5a4164e2cd9856c614f2e55b91bfd3587eac1249057e3d2e365fc35c4d0ad123` |
| Returned `HANDOFF.md` | 3,599 | `321c51683ada9933a0449ebd6b761232cf99a7efb6e1dab75b186c7059201acd` |

The raw export declares 32 artifact records. The downloaded bundle contains 20
files, all byte-identical to their corresponding final artifact records, but
12 supporting artifacts are absent. Missing items include
`ground_truth.json`, `analyzer_out.json`, `final_verify.json`,
`verification.json`, `review_raw.json`, `srcstat.json`, `pool.json`, and
`arxiv.json`. The returned handoff's full-reconstruction instruction therefore
cannot be satisfied from the download.

## Task-identity failure

The export's root conversation is `Repository Provenance and Source Mapping`,
started on 24 July 2026. Its root prompt is the earlier manuscript-construction
brief. The run did not receive:

- `paper-v0.9.1-internal.pdf`;
- `REPRODUCIBILITY-SUPPLEMENT.md`;
- the current `OPERON-QUEUE.md`;
- the current definitions and formal-model hashes; or
- the required literature and blind-review schemas.

The local target identities at audit intake were:

| Required input | SHA-256 |
|---|---|
| `paper-v0.9.1-internal.pdf` | `899423c1bb4af6c90b3fa760e54d2b7aca983eeb4de53a9ff8a399349d8b747f` |
| `REPRODUCIBILITY-SUPPLEMENT.md` | `341023514390c2021ce613915d48d948384495162fccc87d42f78663c61cf8d1` |
| `OPERON-QUEUE.md` | `e418eade4acd7ffed64ad687b2df3e526680a9a65346d3834f91b5b6d7148dd0` |
| `FORMAL-MODEL.md` | `86c74d9a1d23fda39e44a2c05162b47135e5905122592b1775bda5e8bdd659df` |
| `DEFINITIONS-AND-BOUNDARIES.md` | `4152704cf1c0bcef3c8a3ce0578684bb9b7ade6ab7e68f6833fec3faa56b5b48` |

No returned artifact can attest to reviewing inputs it never received.

## Blind-review failure

`ADVERSARIAL-REVIEW.md` is useful internal red-team material, but it reviewed
an earlier Markdown manuscript inside the same authoring session. It did not
review the target PDF and supplement in a fresh blind context. The return has
no:

- `BLIND-REVIEW.md`;
- `blind-review-findings.json`;
- exact reviewed-artifact allow-list and hashes;
- claims-ledger/spec-map non-access attestation; or
- complete, addressable coverage of the required review lenses.

The export's `REVIEWER` frames are harness reviews of transcript windows, not
blind manuscript reviews. The blind-review gate remains unsatisfied.

## Literature-certification failure

The returned `PRIOR-ART-VERIFIED.json` is a custom top-level array, not an
`agent-graph-runtime.prior-art.v1` object. It lacks the required completion
status, timestamp, search protocol, unverified-candidate register, bounded
novelty field, and claim-specific work contract. `LITERATURE-REPORT.md` is
absent.

All 32 DOI identifiers and 13 arXiv identifiers resolved to matching
title/year records, with no duplicates or fabricated identifiers. That is
metadata validation, not full-text validation of the returned semantic
classifications. A separate repository-owned verification therefore admits
only narrowed propositions from selected primary sources.

## Architectural disposition

| Returned proposal | Disposition | Reason |
|---|---|---|
| Replace the title and canonical manuscript | Reject | The current title and canonical `paper.tex` remain aligned with the research contract. |
| Treat static legacy authority as a disconfirmation of runtime unity | Reject | It confuses shared representation/runner/substrate with identical assurance entry. |
| Define the general agent graph as a strict DAG | Reject | Strict DAG is a property of Mentu's admitted generated-graph v1 IR, not the general construct. |
| Treat runtime adaptation as silent mutation of one admitted artifact | Reject | A changed topology requires a successor epoch, an admitted transition system, or a weaker interpreted-tier claim. |
| Infer novelty from no located exact conjunction | Reject | Search absence is not novelty evidence. |
| State that the three admitted attempts compared outputs of one graph | Reject | They executed three distinct executable identities. |
| Retain semantic plan rejections and post-run correction | Accept | They are bounded negative pilot evidence already preserved canonically. |
| Explicitly say the three executions used different plans | Accept | Mechanically supported by three distinct receipt-bound executable hashes. |
| Use returned sources as discovery seeds | Accept with verification | Each identifier and substantive proposition must be independently checked. |

## Privacy and instruction-safety boundary

No credential or concrete malicious prompt-injection payload was found in the
20 downloaded artifacts. The raw export nevertheless contains private paths,
unrelated recalled operational context, nested instruction-shaped messages,
and transcript-review prompts. It is unsafe for public packaging and should
not be supplied wholesale to another model as authoritative instructions.

## Continuation authorized by this audit

The paper may advance internally with:

1. this provenance record;
2. a bounded, independently checked literature layer;
3. the explicit three-distinct-executables limitation;
4. a fresh Operon prompt bound to the new internal PDF hash; and
5. the release gate still closed.

The return does not authorize `v1.0-preprint`.
