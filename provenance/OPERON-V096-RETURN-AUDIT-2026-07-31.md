# Operon v0.9.6 return audit — 2026-07-31

## Verdict

The returned review is **non-certifying advisory evidence for
`v0.9.6-internal`**. Its 21 blind-review findings are substantive inputs to the
`v0.9.7-internal` repair, but the raw return does not pass the repository's
frozen full validator and is not a release input.

The minimal version preflight accepts the attested paper version. That check is
not the full release-evidence gate. The full raw-side validation reproduces two
independent contract failures:

1. `context-a/prior-art-verified.json` omits
   `search_protocol.project_memory_disabled: true` and
   `search_protocol.memory_isolated: true`, so validation stops with
   `E_ISOLATION_INCOMPLETE`.
2. An in-memory diagnostic replay that supplies only those two missing flags,
   without rewriting the raw artifact, then stops at identifier attempt
   `a-001` with `E_IDENTIFIER_LOG_INVALID`. Under the exact attested v0.9.6
   verifier, 59 of 76 requests are noncanonical. Forty-seven attempts use
   `doi:`-prefixed registry identifiers that the frozen request normalizer does
   not recognize; three of those also have independent request mismatches.
   Normalizing only the DOI prefix in memory still leaves 15 noncanonical
   attempts: `a-045`–`a-053`, `a-064`, `a-068`, `a-069`, `a-071`, `a-073`,
   and `a-075`.

The second failure includes both a raw-contract/verifier DOI-normalization
mismatch and 15 request-shape mismatches that remain after that normalization.
It does not justify repairing the sealed return or its attested verifier in
place. Both issues require a fresh protocol-compatible return. The raw tree
and superseded coordinator notes remain preserved outside the paper package
under the private archive label
`agent-graph-runtime-v096-nonrelease-2026-07-31`. They are excluded from
release inputs and source packaging. Failed or
superseded test logs are likewise not release evidence.

`release_authorized` remains `false`, and `novelty_certified` remains `false`.

## Provenance bindings

| Artifact | Bytes | SHA-256 |
| --- | ---: | --- |
| Closed 16-file raw tree | — | `1bb8f0397080e90785710ee7b9d21dd1b7d253903f36996afce1bca6c374143a` |
| `INDEPENDENCE-ATTESTATION.json` | 4,866 | `fbcab5207a18c000a4d37ed8e4f7b5c9e4073aa10f0f62ef34d6dc8b9297118b` |
| `context-a/prior-art-verified.json` | 60,779 | `e92d1677ccc2e86cfd2145333c39c88fc0e18a4838edddb35835cb8d35c805a5` |
| `context-a/identifier-verification-log.json` | 57,806 | `49af07ef669cd59cfbf7d111061d13fc8c27738a43e3471c99200d21ef901c10` |
| `context-b/blind-review-findings.json` | 42,060 | `616a366221db6ff92d9e8fbd5a869af21c1e16ff4955545f32beb19b385de0c9` |
| `context-b/BLIND-REVIEW.md` | 18,275 | `363bf36be477e20b07515f3e395c5681fbada0a594437e2cda544ec9400f5263` |
| Reviewed PDF | 328,655 | `4080504dc4a650bfce127749737749f85f3cb5b67772b040ad85cad12652e647` |
| Reviewed supplement | 39,954 | `bba768e5a1133b942d817e24138ae003da4a3f9f4a83bb88ae91c12e5acf4a3f` |
| Attested review projection | — | `4134dac8f6d052c56bd9a68982c3de41643723b8a4a92ffde308870ce6ed3730` |

The literature context is
`c8c16c80-2b0b-4339-9ab3-ceb3eac448c9`; the blind-review context is
`d1afd4f3-e9bb-4b97-98c8-2b299c58d5be`. They are distinct. The attestation and
the two isolation reports describe memory-disabled contexts, but the registry
itself lacks the two isolation bindings required by the frozen schema.

## What passed

The exact closed path set, protocol-template bytes, staged PDF and supplement,
attested review projection, ten attested output hashes, distinct context
identifiers, both isolation-report structures, both file-open logs, and the
21-finding blind-review JSON pass their corresponding raw-side checks. Those
facts establish useful provenance and exact-input review identity. They do not
override either full-gate failure above.

## Substantive return

Context A contains 69 works: 49 retained, 14 background, two counterexamples,
and four exclusions. Its log contains 76 attempts: 69 resolved and seven
blocked. The registry states `novelty_certified: false`.

Context B recommends major revision and records 21 findings: six major,
12 minor, and three notes. All are retained below as advisory review input.
None is marked resolved by this audit. A repair can answer a finding, but only
a fresh exact-input review of the repaired `v0.9.7-internal` PDF and supplement
can assess that answer.

| ID | Severity / lens | Retained finding | v0.9.7 repair target |
| --- | --- | --- | --- |
| `BR5-101` | major / formal | The stated payload/environment field criterion collapses because the trace language also depends on the environment. | Separate the quantifiers and justify model, permission, sandbox, and approval placement with witnesses or isolation fixtures. |
| `BR5-102` | major / formal | The historical 3/3 inspection–bundle–receipt equality may compare copied digest fields rather than independently recomputed executable bytes. | Recompute the bundle executable identity independently or demote the claim to recorded-field continuity. |
| `BR5-103` | major / systems | The projection re-entry seam is ordinary no-opt-in routing when `auto_mode` and `--auto` are absent/false, not an exceptional configuration. | Describe reachability accurately while making no traffic-frequency claim. |
| `BR5-104` | major / citation | Three LangGraph table identities point to mutable documentation URLs while the bibliography cites commit-pinned blobs. | Bind the exact commit and three exact paths. |
| `BR5-105` | major / reproducibility | No reader tier explicitly reproduces the 25/25 inventory, and its exact Apple/Swift prerequisites are not tied to that tier. | Add a conformance tier, exact toolchain, separate command, and filter inventory. |
| `BR5-106` | major / empirical | A composite 4/4 sensitivity count pools three historical controls with one current-Core control. | Report 3/3 historical controls and 1/1 current-Core control separately. |
| `BR5-107` | minor / formal | I5 closure is tautological when the declared field set is defined as its own disjoint union. | Compare declared fields with independently observed encoded and bound field sets. |
| `BR5-108` | minor / formal | I2 defines population membership through the absence of the event it measures. | Fix membership by the saved-plan entry route and treat planner dispatch as an outcome. |
| `BR5-109` | minor / formal | `chi` and `chi_E` collide, while `eta_beta` is undefined. | Rename the adequacy vector and define the rendered environment binding. |
| `BR5-110` | minor / terminology | “Source-audited architectural reference realization” implies external audit and normative reference status. | Use “author-checked architectural instantiation.” |
| `BR5-111` | minor / terminology | “Strong” is undefined on runner construction paths. | Use the existing admitted/raw distinction. |
| `BR5-112` | minor / novelty | Closest inspected neighbors are not coded conjunct-by-conjunct against the four-part synthesis. | Add positive/not-determinable coding with locators and no absence inference. |
| `BR5-113` | minor / citation | Six arXiv identities lose version suffixes and AgentSpec uses a local label rather than its registered arXiv identity. | Restore every exact `vN` identity and `arXiv:2503.18666v3`. |
| `BR5-114` | minor / citation | Source identity, mechanism support, and publication status are conflated. | Separate the three fields and do not imply a full-text read from metadata resolution. |
| `BR5-115` | minor / reproducibility | The reviewed artifacts do not enumerate the exact 13 filters or their per-filter counts summing to 25. | Publish the complete machine-derived inventory. |
| `BR5-116` | minor / empirical | `HeaderOK` has no fixture at either source pin. | State the gap explicitly; do not present the gate as empirically exercised. |
| `BR5-117` | minor / empirical | The cost total includes an indeterminate term, and the adequacy vector mixes a lower bound with exact counts. | Report a two-attempt subtotal plus an unknown third; derive and precisely label the exact recorded host-boundary count. |
| `BR5-118` | minor / systems | The 9 raw / 1 admitted constructor census has no static entry-path reachability map. | Add a committed-source reachability map while preserving the no-traffic-inference boundary. |
| `BR5-119` | note / novelty | “Most useful implementation finding” is an unsupported self-ranking. | Remove the ranking. |
| `BR5-120` | note / systems | The no-product-wide-cross-origin-parity boundary is correctly preserved. | Preserve it unchanged. |
| `BR5-121` | note / reproducibility | The consent JSON is a scope/provenance attestation, not authenticated proof of authorship or consent. | Say so directly and preserve the exclusion of bare short-line hashes. |

## Permitted use

The v0.9.6 return may be used as:

- a bounded literature-discovery set;
- a source of candidate identifiers for independent verification;
- an exact-input substantive blind review of the v0.9.6 PDF and supplement;
- a repair agenda for the v0.9.7 candidate.

It may not be used as:

- a compliant release-evidence bundle;
- proof that the full Operon gate passed;
- a release bibliography, citation crosswalk, or derived certification root;
- novelty, correctness, exhaustive-coverage, or release certification.

## Fresh v0.9.7 review requirement

Repairing the six major findings changes the exact reviewed inputs. The next
certifying path therefore requires fresh isolated Context A and Context B runs
against exactly `paper-v0.9.7-internal.pdf` and the matching supplement. The
new return must pass the repository-owned full validator before any
repository-owned citation or finding disposition can authorize release.
