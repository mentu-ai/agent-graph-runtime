# Operon v0.9.7 return audit — 2026-07-31

## Verdict

The returned `v0.9.7-internal` bundle is **non-certifying advisory evidence**.
The closed 16-file tree and the independent raw-validator reproduction are
preserved unchanged, but the private execution trace disproves the process
attestation on which the green mechanical result depends. The return is not a
release input, does not certify novelty, and cannot authorize `v1.0-preprint`.

This is not a claim that the literature registry or blind-review findings are
substantively worthless. The 21 findings remain a useful exact-input review
agenda, and the 104-record registry remains a discovery set. A fresh v0.9.8
run is required for certification because the defects are process defects, not
fields that Codex may repair in the sealed return.

`release_authorized` remains `false`; `novelty_certified` remains `false`.

## Two different validation layers

The frozen raw validator succeeds when it is run only over the final files and
self-reported logs:

| Surface | Result |
| --- | --- |
| raw validator status | `compliant` (exit 0) |
| raw file count | 16 |
| raw-tree SHA-256 | `fab39ec135dca85778fa1d6f9f71320d7efe8c4db972834ac0ac828a610921ab` |
| attestation SHA-256 | `0b22516185b3dadbf765faf213bc17af69784db7ad99bbd2b2f81669d8d02a86` |
| review-projection SHA-256 | `a5e0b18624bb9294b07ed2f3027011714fa99ea7c7b16fbd6dc3e446887bf146` |
| validator-result SHA-256 | `0f855ee14ae40c1942b4e3c986ca8ac9251177d7b5ff1b3f80eeae4fed21c383` |
| preserved tarball SHA-256 | `00a3f2ec12d3d709ce5ac088fc56438df9fe6ac7c8f57fb244ccc2d23707ad7f` |

The private 17-frame session export is independently bound by SHA-256
`c8f2464763f8bd7656f535adb2cab62c46a69517727cd5b6ae0ad6027718a27c`.
Unlike the raw validator, that trace records actual frame lifetimes, local
derivative creation and reads, automated reviewer frames, feedback delivered
to the contexts, and the first validator failure. On that evidence the
certifying verdict is `fail`.

The mismatch is diagnostic: the v0.9.7 validator checks declared logs and
final bytes, but it cannot establish that those logs exhaust the actual tool
trace.

## Trace failures

### 1. Context B ran before Context A closed

The frozen queue requires: “Start Context B fresh only after Context A is
closed.” The trace instead records:

| Context | Protocol UUID | Frame id | Started | Closed |
| --- | --- | --- | --- | --- |
| A | `9f547e8b-6e9b-468a-93f5-37d41d81350f` | `67b2672f-1fd8-42d5-b34c-e10ba662067d` | `2026-07-31T07:44:47.148Z` | `2026-07-31T08:43:26.003Z` |
| B | `16518113-5c50-4edd-b361-761280b6f858` | `455489b5-2fde-455f-8107-56b63eb0bbcd` | `2026-07-31T07:44:47.149Z` | `2026-07-31T08:03:49.852Z` |

Context B began one millisecond after Context A began and completed while A
was still open. Distinct UUIDs do not cure the violated sequencing contract.

### 2. Both contexts used undeclared local derivatives

Both direct context frames extracted the reviewed PDF into
`work/paper.txt` and subsequently read that file. Context A created the file
in its message 10 and read it beginning in message 12. Context B created the
same session-local derivative in its message 10 and read it beginning in
message 12. Reviewer children later read those derivative paths as well.

The queue and both context prompts explicitly forbid reading a session or
local derivative. Neither final `FILE-OPEN-LOG.json` declares the derivative.
The final logs are therefore valid against their schemas but incomplete as
records of actual reads.

### 3. Automated reviewer contexts broke the claimed isolation

Context A spawned seven reviewer children; Context B spawned two:

- Context A: `a92da8fb-aa5b-4352-aedf-dd98604740e6`,
  `c496b46d-be2a-4670-83be-fe7e63ceee68`,
  `46c20522-8289-4d9e-9eaf-b68fd7f332c5`,
  `32d7a3cf-bb37-4efe-8099-eb5985e89834`,
  `d455d2b0-48c0-4940-90d3-c20f3eb8d193`,
  `da5137b8-856e-4a08-ba77-067a93364818`, and
  `ec023fa2-f2ab-4362-8873-af385bd59a14`;
- Context B: `39994e47-dbc9-4a7d-8829-e99ff0d45208` and
  `59fa0838-e24d-49fa-ad80-56903e8f887b`.

Those reviewers used artifact and execution-log query surfaces, including
`host.artifact_path`, `host.artifacts`, and `host.query`, and read the
undeclared derivative. More importantly, Context A received two blocking
review findings in its own frame, had its previously submitted output
invalidated, and revised the registry and report in direct response. The final
Context A artifacts therefore incorporate cross-context reviewer feedback
while the isolation report and submitted payload state zero cross-context
artifacts and zero memory-tool calls.

### 4. A failed raw validation was repaired in the same Context A

The first full validation stopped at `ctxA-attempt-001` with
`E_IDENTIFIER_LOG_INVALID`: all 104 attempt objects used `cite_key` where the
frozen schema required `raw_cite_key`. The launch instruction required a
`noncompliant` result and prohibited repair of raw outputs in place after any
full-validator failure.

The coordinator instead returned a correction request to the still-open
Context A. The same frame and protocol UUID re-emitted the identifier log as a
new artifact version after a pure field-name rewrite. The coordinator then
assembled the final tree and reran the validator to green. The rewrite may be
semantically innocuous, but it violates the frozen stop condition; a fresh
context pair was required.

## Independent bibliographic corrections

The trace failure is sufficient to void certification. Independent source
checks also found defects that the raw validator cannot detect:

1. **CWL Community was not absent from Crossref.** A fresh retrieval of DOI
   `10.1145/3486897` returns 11 author objects: ten named people followed by an
   object whose `given` and `family` values are `The CWL` and `Community`.
   The bibliography is correct to retain `{The CWL Community}`. Context A's
   report, registry prose, and the coordinator note incorrectly claim that
   Crossref omits it or carries eleven named authors instead.
2. **RFC 2748's first-author order is wrong in the registry.** The official
   RFC front matter begins with `D. Durham, Ed.`, followed by J. Boyle,
   R. Cohen, S. Herzog, R. Rajan, and A. Sastry. The raw registry begins with
   J. Boyle and places Durham third. This fails the declared first-author
   match against the named primary source.
3. **Three RFC front-matter attributions were unsupported inside Context A.**
   The final registry names published RFC front matter as its ordering source
   for RFC 2753, RFC 3198, or RFC 2748 even though the context's only declared
   RFC Editor retrieval was blocked. The retrieved Datatracker and Crossref
   records remain useful, but they do not make an unfetched source fetched.

Raw Context A files remain immutable. These corrections are repository-owned
dispositions and must not be written back into `operon-v097/`.

## Substantive return retained as advisory evidence

Context A records 104 works: 51 retain, 38 background, five counterexamples,
and ten exclusions; 94 works have a resolved identifier attempt. Context B
records 21 findings: six major, 12 minor, and three notes, with a recommendation
of major revision. The finding set may guide v0.9.8 repairs, but no finding is
resolved merely because an author changed the manuscript. Fresh exact-input
review is still required.

## Permitted use

The v0.9.7 return may be used as:

- a bounded literature-discovery set whose identifiers are independently
  rechecked before citation;
- a substantive blind review of the exact v0.9.7 PDF and supplement;
- a repair agenda for the v0.9.8 candidate; and
- a regression fixture for strengthening the Operon trace gate.

It may not be used as:

- a compliant release-evidence bundle;
- proof of independent or memory-isolated review;
- a release bibliography or certification root;
- novelty, correctness, exhaustive-coverage, or release certification.

## Fresh v0.9.8 requirement

The next certifying attempt requires new Context A and Context B UUIDs, strict
non-overlap, zero local derivatives, reviewer/critic automation disabled, no
artifact-store or trace-query access from either context or its children, and
a fail-closed first-attempt validator record. Repository-owned trace
validation must accompany final-byte validation. A first validation failure
voids the attempt; it cannot be repaired under the same UUIDs.
