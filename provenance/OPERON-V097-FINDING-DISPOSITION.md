# Operon v0.9.7 finding disposition

## Status

The v0.9.7 Operon run is trace-noncompliant and cannot certify literature,
review independence, novelty, or release. Its 21 blind-review findings are
nevertheless retained as advisory peer-review input. This document records the
author-side v0.9.8 candidate response; it does **not** mark any finding
externally resolved. A fresh, sequential, trace-audited v0.9.8 blind review
must assess the exact revised PDF and supplement.

The raw findings remain immutable under `operon-v097/context-b/`. The source
and process defects in the same return are recorded separately in
`OPERON-V097-RETURN-AUDIT-2026-07-31.md`.

## Dispositions

| ID | Severity / lens | Author-side disposition | v0.9.8 candidate response | Remaining gate |
|---|---|---|---|---|
| `BR7-001` | major / formal | accepted | The public replanning lemma now assumes `chi_succ` is not equivalent to `chi_0`; the stronger semantic corollary separately requires `TraceSound_rho(beta)`. A coarse edge-orientation equivalence countermodel is executable in the invariant checker. | Fresh formal review of exact bytes |
| `BR7-002` | major / formal | partial; major conclusion rejected | Denotational `I_rho` and `A_rho` remain definitions rather than decidable algorithms. A finite observation profile `omega=(h,pi,zeta)` now distinguishes bounded witnesses from universal semantic equality. | Fresh reviewer must confirm the denotational/operational boundary is clear |
| `BR7-003` | minor / formal | accepted | Aggregate environment receipts must expose a schema-versioned ordered constituent inventory and address evidence from which the digest is recomputable; opaque aggregates refuse. | Fresh formal review |
| `BR7-004` | minor / formal | partial | The model already required a total disjoint placement map; v0.9.8 makes totality, typing, semantic classification, encoder closure, and refusal fixtures explicit and executable. | Fresh formal review |
| `BR7-005` | note / formal | accepted | `Gamma_E` now includes the I1-eligible population and header-refusal count. Historical C30 is reported as `(3,3,5,3,0,empty,empty)`. | Fresh exact-input review |
| `BR7-006` | major / novelty | accepted | TensorFlow Eager is added as a direct define-by-run and traced executable-graph precedent. The claimed contribution is narrowed to lifecycle-and-admission synthesis. | Fresh Context A must independently verify and reposition the precedent family |
| `BR7-007` | note / novelty | accepted | Generated figure text and final extracted PDF are subject to barred novelty and cross-epoch pooling checks, with seeded failures in the build tests. | Fresh build and blind review |
| `BR7-008` | minor / terminology | accepted | “Frontier planning” becomes “ready-set computation”; any change to graph nodes or edges is construction-lane activity, distinct from ready-node selection. | Fresh terminology review |
| `BR7-009` | minor / terminology | accepted | RFC 8785 is positioned as the JSON serialization baseline; domain equivalence, path/content aliases, placement, and framing are explicit extensions with counterfixtures. | Fresh Context A verification and formal review |
| `BR7-010` | minor / systems | accepted | The seam predicate is uniformly `recipe.auto_mode != true && effective CLI auto == false`; CLI absence and false collapse to one Boolean state, giving a 3-by-2 fixture surface. | Fresh source audit / blind review |
| `BR7-011` | minor / systems | accepted | The unsupported “other legacy branches remain” statement is removed. The table now scopes raw compatibility scheduling to the selected `SequenceRunner` contract and makes no paper-wide convergence claim. | Fresh systems review |
| `BR7-012` | major / empirical | accepted | Figure 4 reports `3/3 historical` and `1/1 current-Core` separately. A generated-text gate rejects the former composite `4/4`. | Rebuilt figure and visual QA |
| `BR7-013` | minor / empirical | accepted | Exact five-saved-plan telemetry is published: 133,022 input, 10,127 output, 143,149 total tokens; 108,874 ms; 490,151 request and 42,930 response bytes. Twelve dispatches are documented, but only five have complete telemetry. | Machine-to-prose gate and fresh review |
| `BR7-014` | major / empirical | accepted | The funnel now states five qualified projections, two pre-execution semantic rejections (v2 and v4), and three saved-plan execution attempts. “Zero exclusions” is restricted to each attempted identity transition. | Fresh empirical review |
| `BR7-015` | major / citation | accepted | AgentSpec, ReAct, DSPy, and AFlow render only verified versioned-preprint metadata; PROV-DM uses a dated locator. A current 45-key source-identity projection is generated without claiming mechanism or novelty certification. | Fresh Context A field-level verification |
| `BR7-016` | minor / citation | accepted | The exact pinned Kubernetes bytes were independently rechecked and are no longer described as inheritance-only. | Fresh Context A verification |
| `BR7-017` | minor / citation | accepted | PROV-DM now uses the dated 2013 Recommendation locator. | Citation gate and fresh Context A verification |
| `BR7-018` | minor / citation | partial | The 34/37 defect is explicitly scoped to v0.9.5; the v0.9.7 43/43 statement is labeled cite-key membership only, not full rendered-metadata certification. | Fresh 45-key v0.9.8 crosswalk |
| `BR7-019` | minor / reproducibility | partial | The exact PDF/supplement pair is bound by one detached canonical review projection and attestation; cyclic mutual hashes are deliberately avoided. | Fresh pair-manifest and release-gate validation |
| `BR7-020` | minor / reproducibility | accepted | The manuscript and supplement now both state the v0.9.6 failed raw gate and the v0.9.7 trace-audit failure. | Cycle-lineage equality gate and fresh review |
| `BR7-021` | note / reproducibility | preserved open boundary | No cross-machine byte identity or pass-equivalence claim is made. A second-machine run remains valuable but is not manufactured as current evidence. | Future independent rerun |

## Major-finding gate

The five accepted major defects (`BR7-001`, `BR7-006`, `BR7-012`, `BR7-014`,
and `BR7-015`) all change the reviewed surface. `BR7-002` is answered by a
clarification rather than replacing the denotational model with a finite test
definition. Consequently the v0.9.7 PDF cannot be released under any v0.9.7
attestation, even if its trace had been compliant. The only coherent release
path is a sealed `v0.9.8-internal` candidate followed by fresh Operon v098.
