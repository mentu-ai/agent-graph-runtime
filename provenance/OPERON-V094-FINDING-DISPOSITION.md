# Operon v0.9.4 finding disposition

## Status and authority boundary

This record dispositions all 23 findings returned by the blind review of
`v0.9.4-internal`. The findings are **advisory review evidence**, not
certifying evidence: the v0.9.4 return failed the frozen raw-return contract
for archive layout, file-open-log schema, and canonical identifier requests.
Nothing in this record changes that verdict, authorizes release, certifies
novelty, or repairs the immutable files under `operon-v094/`.

The dispositions are coordinator judgments on the merits of the findings.
They guide the in-progress `v0.9.5-internal` revision. Because that revision is
not yet frozen, paths named below are remediation targets rather than a
hash-bound reviewed manuscript. A fresh compliant review must bind the final
v0.9.5 PDF and supplement.

## Immutable source bindings

| Artifact | SHA-256 |
| --- | --- |
| Raw-root path-neutral tree | `e99a53c83493f25eeae1ffc2b19239b3e7d5f2ebbb58de321e5e3eda3d3c82b6` |
| Downloaded raw-return tarball | `bf5b13d3fa1b5b61d497a220e753608b71f6cf7b6f69986ff4569011a6cf9fd9` |
| `context-b/blind-review-findings.json` | `634e6adddcbe2d7c0554688a7404a8a326c321022880e340b84c843f364567ff` |
| `context-b/BLIND-REVIEW.md` | `6bc56d791d96eb74c61617bf4773e039fd97a6ba50a205a5be85e39a79c85609` |
| `INDEPENDENCE-ATTESTATION.json` | `136f07d7db214a7d498e935dccc1be0fd9f58bda22869e99449ec100d8f0a8ef` |
| Reviewed `paper-v0.9.4-internal.pdf` | `1852293bcfe338d0b626ad7e7e2b53cd59ae34206cb3869a5450d0b4c0655621` |
| Reviewed v0.9.4 supplement | `7baf01e3ba87492b4ac21448103b375e26d4c6e7d5755ee92add26479782b2a5` |
| Review projection | `b596713e38e10140b12985c8f3569c01816009c4979a818d7b8199b87acd3182` |

The return-audit verdict and contract failures are recorded in
`provenance/OPERON-V094-RETURN-AUDIT-2026-07-30.md` and
`results/operon-v094-return-audit.json`.

## Disposition vocabulary

- **Accepted** — the finding is supported and the v0.9.5 manuscript-level
  repair or explicit limitation is in scope.
- **Partial** — the core concern is supported, but a requested empirical,
  cross-system, generated-artifact, or supplement change remains unfinished.
- **Rejected** — the requested change is not accepted on its merits; the
  reason is recorded rather than silently ignoring the finding.
- **Deferred** — the concern is valid but requires a new actor, authority, or
  future governance decision outside the current paper-only revision.

## Finding-by-finding disposition

| ID | Severity / lens | Disposition | v0.9.5 remediation and remaining boundary |
| --- | --- | --- | --- |
| `BR4-001` | Major / formal | **Accepted** | Shared-substrate realization is now an explicit if-and-only-if definition with four conjuncts. Missing evidence for any conjunct means realization is not established. |
| `BR4-002` | Major / formal | **Partial** | The binding schema now declares per-field equivalence, executable equivalence, a biconditional canonicalizer contract, and trace-changing same-byte witnesses as failures. One executable-bound mutation control exists, but the complete mandatory-field I5 matrix remains unrun; full I5 conformance is therefore withheld. |
| `BR4-003` | Major / formal | **Accepted** | The model now separates logical implication from evidence adequacy through a non-vacuity vector covering admitted effects, distinct executables, projections, drift categories, and mutation categories. C30 is explicitly non-vacuous only for I1--I3. |
| `BR4-004` | Minor / formal | **Partial** | The formal model defines `P`, `x`, `xi`, schema field domains, and mandatory version fields. The canonical manuscript still needs an explicit first-use definition of `P` and a final one-to-one field-path presentation before freeze. |
| `BR4-005` | Major / systems | **Accepted** | A current committed-source audit independently confirms the conditional projection-to-legacy re-entry path. v0.9.5 names projection versus adoption, discloses the reachable seam, and limits strong admission to the qualified invocation path. Closing the Mentu implementation seam is outside this paper-only change. |
| `BR4-006` | Major / systems | **Partial** | v0.9.5 publishes a current constructor census, defines the audited strict-DAG admitted profile, names compatibility profiles, and expressly refuses to treat constructor counts as a product-wide denominator. An exhaustive denominator of every effectful product entry point is not established. |
| `BR4-007` | Major / empirical | **Accepted** | Three disposable paper-local controls detect an executable-bound mutation, planner-lane injection, and manifest-byte flip; one independently executed current-Core test detects admission-state drift. All are labeled detector-sensitivity evidence, not instrument validation or new C30 observations. |
| `BR4-008` | Minor / empirical | **Accepted** | The result now reports 54 expected, 54 actual, zero missing, zero extra, and zero mismatched manifest leaves. The three bundle checks are explicitly labeled aggregates derived from those leaves, not independent observations. |
| `BR4-009` | Minor / empirical | **Accepted** | v0.9.5 states in one inferential boundary that no aggregate environment identity and no unchanged-executable output-reproducibility series were observed. No synthetic `h_eta` result is manufactured. |
| `BR4-010` | Minor / empirical | **Accepted** | The conclusion now reports the current Core realization separately from historical observed C30 transitions, removes “validates,” and withholds full I5, environment-identity, repeatability, and comparative claims. |
| `BR4-011` | Major / citation | **Partial** | `abbrvurl` makes DOI, URL, RFC/W3C, and arXiv identifiers visible; AgentSpec uses verified arXiv metadata rather than its unresolved printed DOI; mutable Kubernetes and LangGraph pages are commit-pinned. A fresh compliant identifier verification and visual build of the frozen v0.9.5 PDF remain required. |
| `BR4-012` | Minor / citation | **Partial** | The advisory v0.9.4 return is now reconciled as 53 records: 33 retained, 17 background, one counterexample, and two exclusions. Because that return failed its contract, a certified cited/background/excluded crosswalk and post-resolution query-family disposition remain for the next compliant review. |
| `BR4-013` | Minor / citation | **Accepted** | The asymmetric N/E cell matrix is withdrawn. A positive-only precedent map cites established mechanisms and includes a scoped Mentu realization row, so no unlocated absence cell remains to audit. |
| `BR4-014` | Major / novelty | **Accepted** | The structure that implied uncontested uniqueness is removed. Mentu is described as an author-proposed, source-audited reference realization for the named strict-DAG admitted profile, never as a comparative rank, unique implementation, or externally certified standard. |
| `BR4-015` | Note / novelty | **Rejected** | The demand to make a definition itself empirically falsifiable is not adopted. Coordinate separability remains explicitly classified as a specification claim over a constrained feasible region, not an empirical result or causal-independence claim. Empirical witnesses belong to the future matched study. |
| `BR4-016` | Minor / terminology | **Partial** | Durable replay remains positioned as a distinct precedent and the comparative N/E scoring table is gone. Receipt deconfliction and a verified data-orchestration or asset-version nearest-neighbour treatment still require fresh literature work and are not inferred from the failed return. |
| `BR4-017` | Minor / terminology | **Partial** | The manuscript and research contract use “mechanical invariant exercise” and report four sensitivity controls. The supplement and any generated labels must be swept to remove the stale “instrument validation” phrase before v0.9.5 freezes. |
| `BR4-018` | Minor / terminology | **Partial** | The manuscript defines normative coordinate values and defines the plan container `z` as binding, but not equaling, `x`. Figure 2 and appendix vocabulary still require regeneration and a final crosswalk check against those canonical terms. |
| `BR4-019` | Major / reproducibility | **Deferred** | No independent holder of the sealed workspace has completed an authorized rerun. Until one does, the private tier must be described as a single-party deterministic regression check, and baseline-generating run/date provenance must be added. This cannot be upgraded by prose alone. |
| `BR4-020` | Minor / reproducibility | **Partial** | The manuscript replaces “preregistered” with “prospectively committed in the author-controlled repository before the pilot evidence commit.” The supplement and generated package still require the same wording; no external timestamp priority is claimed. |
| `BR4-021` | Minor / reproducibility | **Partial** | The source verifier now targets commit, path, line, and full source-blob digest rather than guessable short-line hashes. Results and the supplement must be regenerated and checked to ensure no `needle_sha256` or equivalent short-string confirmation survives. |
| `BR4-022` | Note / reproducibility | **Deferred** | The release clearance correctly remains author-owned, but an internal-disclosure and retention rule for timestamp-bearing telemetry still requires an explicit author governance decision. It is not invented by Codex. |
| `BR4-023` | Note / formal | **Accepted** | The four-way distinction among executable identity, environment identity, output reproducibility, and semantic correctness is preserved and strengthened. It remains a regression condition for the final integrity sweep. |

## Summary

- Accepted: 10
- Partial: 10
- Rejected: 1
- Deferred: 2
- Total: 23
- Release authorized: **no**
- Novelty certified: **no**

The machine-readable counterpart is
`results/operon-v094-finding-disposition.json`. The final v0.9.5 integrity
sweep must re-evaluate every partial and deferred item against the frozen
manuscript, supplement, generated results, and exact-input review packet.
