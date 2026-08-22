# Operon v0.9.5 finding disposition

## Status and authority boundary

This repository-owned record dispositions all 44 findings returned by the
blind review of `v0.9.5-internal`. It does not modify the immutable
`operon-v095/` return, certify novelty, authorize release, or claim that an
accepted remediation is complete. The reviewed manuscript recommended major
revision. `v0.9.6-internal` remains a working revision and requires a fresh
exact-input review after it is frozen.

“Accepted” below means that the criticism is supported on its merits.
“Partial” means that a narrower concern is supported but part of the finding or
recommended test overgeneralizes. “Preserved note” retains a no-defect
observation as a regression condition. No finding is silently discarded.

## Immutable reviewed-input binding

Every row and every machine-readable finding record binds the same two reviewed
inputs:

| Reviewed input | SHA-256 |
| --- | --- |
| `operon-v095/context-b-inputs/paper-v0.9.5-internal.pdf` | `40ed40274c63622ada7dc445187177cf6e44f240f782715e7238fdcc6c51b68d` |
| `operon-v095/context-b-inputs/REPRODUCIBILITY-SUPPLEMENT.md` | `f1921597b79b6de6649fb1b286c0edfac9f72a55003154635f6e7be34310e15a` |

The source review projection is
`operon-v095/context-b/blind-review-findings.json` at
`de63fb92687fbf24d7c424ad15f338273e5c14cb1b8e56cd5f40f727b8328bfa`.
The narrative review is
`operon-v095/context-b/BLIND-REVIEW.md` at
`2074666488c7c234dea8df8cb07289dd8200b7c6348d5fbaf0aecc60075734c7`.

## Finding-by-finding disposition

| ID | Severity / lens | Disposition | Rationale | Concrete v0.9.6 remediation or remaining boundary |
| --- | --- | --- | --- | --- |
| `BR5-001` | Note / novelty | **Preserved note** | The reviewed PDF consistently refuses priority, uniqueness, and superiority claims. | Preserve the restraint and add a context-aware prohibited-novelty lexical gate; lexical matching alone must not reject explicit negations or source titles. |
| `BR5-002` | Minor / novelty | **Partial** | The OxyMake sentence implied an unevaluated conjunction, but a full product matrix is not required if no absence claim is made. | Retain the visible no-absence clarification; add conjunct locators only for inspected sources and mark all others `not inspected`. |
| `BR5-003` | Minor / novelty | **Accepted** | Runtime replanning is an analytic scope consequence, not an empirical counterexample. | Keep the visible `scope theorem` / `exclusion lemma` terminology in the contribution list, formal model, claims projection, and figures. |
| `BR5-004` | Minor / terminology | **Accepted** | Four meanings of `profile` create a real construct collision. | Complete the visible migration to authoring method, assurance contract, target contract, and compatibility surface; sweep tables, captions, conclusion, and generated figures for stale bare uses. |
| `BR5-005` | Minor / terminology | **Accepted** | Unqualified `audited` can imply third-party assurance that did not occur. | Use `source-audited` or `source-checked` everywhere and preserve the explicit no-third-party-certification sentence; several stale uses still require a package-wide sweep. |
| `BR5-006` | Minor / terminology | **Partial** | Qualification and scaffold need narrower first-use definitions, but established-neighbour claims require verified sources rather than review assertion alone. | Preserve the visible regulated-qualification disclaimer and authoring-method distinction; add verified terminology anchors before release. |
| `BR5-007` | Minor / terminology | **Accepted** | The paper does not map its receipt/evidence vocabulary to the closest supply-chain terms. | Add a bounded term map for receipt, manifest, activation evidence, and qualification result, while explicitly withholding signature and functionary-authorization properties. |
| `BR5-008` | Major / formal | **Accepted** | The reviewed version left artifact-declared versus externally pinned canonicalizer/schema versions ambiguous. | Preserve the visible payload/header split, external pin, fixed header framing, and pre-effect mismatch refusal; add mismatch and version-sensitivity fixtures. |
| `BR5-009` | Major / formal | **Partial** | Open-world adequacy was not established, but declared closure is mechanically falsifiable and is not true of every implementation. | Keep I5 renamed `declared binding closure`; retain schema adequacy as a separate defeasible property and execute omission-witness probes without treating finite passes as proof. |
| `BR5-010` | Major / formal | **Accepted** | Toolchain/schema versions did not satisfy the paper's trace-semantic placement criterion. | Keep versions in a separately framed identity header and effect-semantic fields in the payload; version changes may change artifact identity without being called trace-semantic. |
| `BR5-011` | Major / formal | **Accepted** | The reviewed lifecycle reused one symbol for unchanged requalification and a changed successor. | Preserve `x_rq` / `q_rq` for requalification and `x_succ` for mutation across manuscript, formal documents, figures, and generated claims. |
| `BR5-012` | Minor / formal | **Accepted** | Operator/domain glyph collisions and the unary-looking lifecycle chain obscured types. | Retain the visible typed operator sequence, add a compact symbol table, and mechanically check unique glyph roles in claim-bearing equations. |
| `BR5-013` | Minor / formal | **Partial** | A dispatch can falsify implementation membership, so I2 is not inherently unfalsifiable; the reviewed wording made reclassification too easy. | Keep I2 as a predeclared entry-path predicate and retain every observed planner dispatch or exclusion in attempt accounting. |
| `BR5-014` | Minor / formal | **Accepted** | The reviewed manuscript did not instantiate `H` or explain displayed digest prefixes. | Preserve the visible full-length SHA-256 definition and prefix disclaimer; add a build assertion that displayed prefixes derive from full result digests. |
| `BR5-015` | Minor / formal | **Accepted** | Projection parity combines lossless projection with deterministic pinned lowering. | Keep the visible conjunction disclaimer and add repeat-lowering plus deliberately lossy-projection controls before attributing a parity pass. |
| `BR5-016` | Major / systems | **Accepted** | The paper's own realization gate required executed equivalent fixtures, while two fixtures were only inspected as test definitions. | **Pending executed-test evidence:** execute origin parity and the admitted vertical slice at the pinned Core commit in external scratch, or demote realization to architecture evidence. |
| `BR5-017` | Major / systems | **Partial** | The conditional projection-to-legacy route does not implement the adoption rule; that fact does not generalize to the admitted Core path. | Preserve the now-explicit route-level nonconformance and profile-scoped Core claim; annotate the lifecycle figure and add a regression test that ordinary dispatch refuses an unadopted generated projection. |
| `BR5-018` | Minor / systems | **Accepted** | The direction of the constructor census matters even without a traffic denominator. | State explicitly that 9 of 10 direct production `SequenceRunner` constructors are raw and one admitted; publish per-site reachability while making no invocation-frequency inference. |
| `BR5-019` | Minor / systems | **Accepted** | The executed runtime-state drift control was not mapped to a declared environment field. | Publish the closed `F_eta` / receipt field map and bind the control to its exact perturbed constituent before citing it for I4 or I5. |
| `BR5-020` | Note / systems | **Preserved note** | Substrate realization, assurance, protocol conformance, and evidence adequacy are kept distinct. | Preserve this separation with a terminology regression check in abstract, conclusion, implementation map, and figures. |
| `BR5-021` | Major / empirical | **Partial** | I1 equality can fail inside the eligible set, so the ratio is not tautological; prior-stage selection still needed disclosure. | Bind the visible attempted/refused/admitted/matched funnel to generated evidence and report `3/3 attempted, 0 excluded` only if mechanically reproduced. |
| `BR5-022` | Major / empirical | **Partial** | The three channels are corroborating but not independent, and the reviewed paper already acknowledged their boundedness. | Replace `triangulated` with `in-system corroboration` and claim zero **recorded** dispatches; add an out-of-band proxy/provider count only if retaining an absolute no-dispatch claim. |
| `BR5-023` | Major / empirical | **Partial** | Equivalence-side and environment-isolation fixtures are absent, but the paper already withheld full I5 conformance. | **Pending executed-test evidence:** run equivalent-encoding, semantic-inequivalence, `F_eta` isolation, and header-mismatch fixtures before any full canonicalizer-conformance claim. |
| `BR5-024` | Minor / empirical | **Accepted** | The size of the mutation-coverage gap is countable and should not remain qualitative. | Regenerate the matrix under the repaired payload/header model, showing witnesses and gaps for every `F_chi` class plus header and partition-isolation controls. |
| `BR5-025` | Minor / empirical | **Accepted** | The stage-to-repository-head clustering needed to interpret 5/5 was withheld. | Publish the five-row stage/head/executable-identity table and state the number of distinct executable identities among projection checks. |
| `BR5-026` | Minor / empirical | **Partial** | Bundle checks are nested and derived, but statistical design-effect language is inapposite to deterministic digest validation. | Report leaf counts per bundle, retain `n=1 objective / 3 bundles`, and state that bundle digests are derived checks rather than independent observations. |
| `BR5-027` | Minor / empirical | **Accepted** | Incomplete telemetry was reported with unsupported precision and no field-level missingness. | Report contributing and missing records for each aggregate, round lower bounds, identify the price basis/date/currency, or remove the dollar estimate. |
| `BR5-028` | Minor / empirical | **Accepted** | The evidence-adequacy vector was defined but not instantiated exactly. | Print separate historical and current `chi_E` vectors and record host-effect dispatch status per admitted attempt; do not replace unknown counts with a lower bound. |
| `BR5-029` | Minor / empirical | **Accepted** | The matched study lacks a primary comparative estimand, multiplicity rule, precision rationale, and unconditional/conditional reuse distinction. | Amend the prospective protocol before any study execution; name the endpoint and estimand, justify the floor, and state whether amortization is conditional on first success. |
| `BR5-030` | Minor / empirical | **Accepted** | Abstract and Figure 4 combine three historical disposable controls with one current-Core execution. | Split the count into `3 at 40bd3f9` and `1 at f3d89e7` at every high-read surface and pin every figure numeral. |
| `BR5-031` | Note / empirical | **Accepted** | Positive seeded controls assess sensitivity only; no innocuous specificity controls exist. | Add negative controls whose expected result is zero detections and report sensitivity and false-positive observations separately. |
| `BR5-032` | Major / citation | **Accepted** | The reviewed surface did not enumerate verification status for its 37 references. | Produce a per-key verification/disposition table bound to independently checked primary records; fail release when a cited claim lacks a verified row. |
| `BR5-033` | Major / citation | **Accepted** | Several close operational analogues were absent from the discriminant positioning. | Independently verify and disposition SLSA, Sigstore, OPA/Gatekeeper, Temporal, asset-versioned orchestrators, and portable workflow standards; add only positive, sourced precedents. |
| `BR5-034` | Minor / citation | **Accepted** | One ICLR source used a third-party index while peer entries used primary venue identifiers. | Replace the DBLP locator with a verified primary identifier and lint claim-bearing bibliography URLs against aggregator-only hosts. |
| `BR5-035` | Minor / citation | **Partial** | A blind packet need not contain every internal control record, but reviewed claims about prior review need an auditable disposition crosswalk. | Bind the repository-owned v0.9.4 disposition from the appendix or public supplement and fail the gate on missing finding IDs without exposing internal reasoning before blind review. |
| `BR5-036` | Note / citation | **Preserved note** | Commit-pinned non-DOI web references are a strong reproducibility practice. | Preserve immutable or version-pinned locators and access dates; verify content digests without making network availability a prerequisite for every offline build. |
| `BR5-037` | Major / reproducibility | **Accepted** | The executed Core control requires Swift, which the reviewed environment omitted. | The working environment now names Swift/Xcode/SDK; still add the exact command/exit receipt to detector results and update the supplement. A second-machine run remains pending. |
| `BR5-038` | Major / reproducibility | **Partial** | Calling a withheld ledger authoritative weakens self-containment, but blind exclusion of internal adjudication metadata is defensible. | Make the manuscript/supplement authoritative for published claims, treat the ledger as control metadata, and enforce a complete manuscript-facing claim projection without giving it to the blind reviewer. |
| `BR5-039` | Major / reproducibility | **Partial** | A combined process exit can remain nonzero without conceptual conflation if typed outcomes are separately reported. | Preserve the visible invariant/baseline/output status split, document it in the supplement, and demonstrate portability behavior separately; do not report baseline drift as invariant failure. |
| `BR5-040` | Minor / reproducibility | **Accepted** | The reviewed surface contains no full result identity digest despite making digest-equality claims. | Add a bounded appendix table of full representative and admitted executable/plan/receipt digests plus the sealed archive digest; keep figures truncated for readability. |
| `BR5-041` | Minor / reproducibility | **Partial** | Public licensing is unresolved, but linking to third-party sources and quoting bounded excerpts does not automatically require redistributing their full snapshots. | Require author/legal clearance for the paper license, excerpt basis, any redistributed third-party bytes, and the stable locator; keep release failed closed meanwhile. |
| `BR5-042` | Minor / reproducibility | **Accepted** | The singular/plural human-participant description and future timed judgments lack a complete consent/ethics path. | State the exact human count, bind consent per retained participant, and record an ethics/exemption determination before the matched study begins. |
| `BR5-043` | Minor / reproducibility | **Accepted** | Unauthorized readers can check projection consistency but cannot independently authenticate private grade-A/B evidence. | Preserve the access limitation and obtain a named independent authorized rerun or equivalent signed/escrowed attestation before strengthening reproducibility rhetoric. |
| `BR5-044` | Note / reproducibility | **Preserved note** | The path-neutral, read-only, output-isolated harness design is strong. | Preserve it and add regression tests for all three forbidden output-root placements, asserting nonzero exit and zero writes. |

## Summary and release state

- Findings dispositioned: **44 / 44**
- Major findings: **14**
- Minor findings: **25**
- Notes: **5**
- Accepted: **27**
- Partial: **13**
- Preserved notes: **4**
- Rejected notes: **0**
- Unresolved majors for release: **14**
- Release authorized: **no**
- Novelty certified: **no**

The machine-readable counterpart is
`results/operon-v095-finding-disposition.json`. All major findings remain
release blockers until the revised manuscript, supplement, generated evidence,
and executed-test receipts are frozen and independently reviewed.
