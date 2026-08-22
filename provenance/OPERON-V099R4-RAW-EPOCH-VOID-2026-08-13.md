# Operon v0.9.9-r4 raw epoch void — first validator attempt exited nonzero

## Classification

The detached trace audit for protocol revision `v0.9.9-r4` passed every Phase 4
preflight condition, assembled the immutable raw tree, and consumed its first
and only full validator attempt. The attempt exited `1`. It raised a single
stable failure code, `DIRECT_OUTPUT_RECEIPT_MISMATCH`, and the derived
trace-audit stub carries status `indeterminate`. No raw validation result
document was produced at all.

Under the pinned rule this **voids the raw epoch**. It is not a preflight stop.

This is the second consecutive epoch to reach adjudication and the first to fail
before adjudication could produce any counts. `r3` failed *at* adjudication with
six codes and a complete count table; `r4` failed on a structural precondition
of the producer attestation and never reached the check families at all.

The one-shot validator budget for this epoch is spent. No retry against this raw
tree, no reopened producer session, no modified export, and no tooling repair is
permitted now that a raw failure has been observed. A further attempt requires a
new projected protocol revision, two new producer sessions, two new exports, and
a new raw root.

Only digests, byte counts, export metadata, frame identifiers, field names,
stable codes, and path-free derived counts appear below. No local path, message
content, prompt text, artifact content, envelope-field value, represented URL,
or owner identity is reproduced here or anywhere in the public record.

## Preflight results, condition by condition

At Epistemics `main@b42fe73017c15d0164eec9d3310067503804a087`, working tree
clean, every handoff condition was established before anything ran. Concurrent
unrelated corpus work advanced `main` by one commit during the epoch; it touched
no file in this package, and every projected and toolchain digest recorded below
was recomputed from the on-disk bytes this attempt actually used.

1. **Repository state.** Branch `main`, no uncommitted changes, and neither a
   prior `operon-v099r4` raw path nor a prior `operon-certification-v099r4`
   audit path present.
2. **Source projection recomputes exactly.** The r4 projection freezer reports
   that all 34 fields recompute.
3. **Carry-forward and binding.** Eighteen fields are byte-identical to the r3
   projection and sixteen differ. All sixteen are protocol or toolchain
   identities — both context prompts, the isolation preflight, the tool policy,
   the r4 trace extractor, the r4 raw validator, the r4 gate, the r4 review-pair
   manifest, the trace-audit contract, six protocol schema documents, and the
   revision string — and each was recomputed from its actual on-disk r4 file.
   All four reviewed-input and build identities carry forward unchanged and
   equal their r1 values: manuscript PDF `d371922d…` (346,730 bytes),
   reproducibility supplement `8edd1803…` (55,375 bytes), deterministic text
   projection `fa49b71e…` (127,579 bytes), and the internal build context
   `59e1d0e6…`.
4. **No earlier-lineage reuse.** The v0.9.8, r1, r2, and r3 projections remain
   present, intact, and distinct as whole files, and no r4 protocol or toolchain
   digest equals its v0.9.8, r1, r2, or r3 counterpart.
5. **Reviewed-input identities.** The r4 review-pair manifest `75d2245a…` binds
   exactly the three reviewed identities above plus the `pdftotext` executable
   identity, version, and arguments, and all three recompute from repository
   originals.
6. **Validator interface.** The r4 wrapper exposes the eleven-argument
   two-export interface named in the handoff and exposes no caller-supplied
   trace-audit input.
7. **Fixture suites pass unchanged.** 411 tests across 26 modules pass at the
   committed revision; no test file was modified. The four r4 modules contribute
   103 of them.
8. **Exports hashed before semantic parsing.** Both supplied exports were hashed
   first, and both matched the orchestrator-recorded digests supplied with the
   custody handoff:

   | Role | SHA-256 | Bytes | Export version | Exported at (UTC) | Root frame |
   | --- | --- | ---: | --- | --- | --- |
   | `context_a` | `7e9d121b754b443645c24bab0da1f293221de6c9db0e11870a67ae7c5d1ebce5` | 967,904 | `1.0` | `2026-08-13T17:07:21.787Z` | `6b436838-9369-43fa-a7dc-869ec62e9eb6` |
   | `context_b` | `16fa90e9bec55a9498a0f6bda794ea7cd0294e2d88580e21001ef55802d72b04` | 651,223 | `1.0` | `2026-08-13T17:57:36.675Z` | `6a194365-1dd5-47d9-a584-ea6893ad22af` |

9. **Tool vocabulary fully declared.** Every represented tool name in both
   exports resolves to a declared class in the r4 registry. No `UNKNOWN_TOOL`
   condition exists.

   | Role | Tool events | Declared names observed |
   | --- | ---: | --- |
   | `context_a` | 80 | `python` 25, `read_file` 24, `repl` 24, `submit_output` 4, `save_artifacts` 3 |
   | `context_b` | 49 | `repl` 17, `read_file` 15, `python` 12, `save_artifacts` 3, `submit_output` 2 |

   Neither export represents a `request_network_access` call. Context B's
   prohibition is satisfied on its face; whether Context A's identifier log
   reconciles against zero represented requests was never adjudicated.

10. **Envelope vocabulary fully declared.** Every represented field at all five
    levels resolves to a declared field with a declared class in both exports.
    Top-level, frame, content-block, and artifact-record key sets match their
    pinned sets exactly in both. Observed message-level fields are `role`,
    `content`, `_ts`, `_uuid`, `_response_id`, `_tokens`, `_harness_notice`,
    `_harness_prompt`, `_intent_id`, and `_artifact_refs` in Context A, plus
    `_persisted_spills` and `_system_hint` in Context B. No
    `UNDECLARED_ENVELOPE_FIELD`, no `ENVELOPE_FIELD_CLASS_VIOLATION`, and no
    `ENVELOPE_REFERENCE_UNRESOLVED` arose.
11. **Both exports parse completely.** Invoking the pinned extractor's export
    loader on each export as a read-only diagnostic — writing no file and
    performing no adjudication — accepted both: Context A with 6 frames, 158
    messages, 192 content blocks, and 8 artifact records; Context B with 3
    frames, 104 messages, 128 content blocks, and 6 artifact records. Context A
    represents zero envelope-level scope qualifications; Context B represents
    six, one `OUT_OF_BAND_CONTENT_POINTER` from `_persisted_spills` and five
    `PLATFORM_CONTENT_ANNOTATION` from `_system_hint`. Per the handoff a
    qualification is not a reason to stop, and these did not stop anything.
12. **Raw tree assembled, byte-verified, and read-only.** 18 files, 670,173
    bytes total, tree manifest `5d7558a0…`, every copy byte-identical to its
    source and the three pinned context-b inputs matching their projected
    digests. No `.DS_Store`, AppleDouble file, cache, or derivative entered the
    tree. Directories and files were set read-only and both a create probe and
    an overwrite probe were refused before validation.

## The attempt

The first and only full attempt used the handoff's exact command interface with
`--protocol-revision v0.9.9-r4`, the r4 projection and tool policy, both private
exports, and an audit directory outside the raw tree.

- Invocation `d2e38312-0eae-42eb-9dbd-0f8778a0b16d`, attempt index 1, exclusive
  creation before semantic parsing, at `2026-08-13T20:02:22.476039Z`.
- Raw tree manifest `5d7558a0…`; package manifest `ff63271b…`.
- Exit code `1`. Derived trace-audit stub status `indeterminate`, schema
  `agent-graph-runtime.trace-extraction-error.v1`, failure code
  `DIRECT_OUTPUT_RECEIPT_MISMATCH`, detail *the detached validator failed closed
  before completing the attempt*.
- No `raw-validation-v099r4.json` exists. The attempt established no check
  family, no trace counts, no producer claim comparison, and no scope
  qualification set. Nothing about producer conduct was adjudicated.

Two distinct defects are visible in that single run and both are recorded here
as observed, without repair.

## Defect one — the failure that fired

The extractor validates each producer attestation before adjudicating anything.
It requires `unobserved_controls` to be exactly a seven-member set, every value
`unknown`. Both producers supplied a six-member set, every value `unknown`,
omitting exactly `session_frame_topology`. Both supplied the full seven-member
set, every value `unknown`, in their isolation reports.

The reason they did is recorded in the pinned protocol itself. Two r4 schema
documents, both projected and both digest-frozen, disagree with each other:

- `PRODUCER-ATTESTATION-SCHEMA.md`, which governs the attestation, says
  `unobserved_controls` "has exactly these string-valued fields" and lists six,
  not naming `session_frame_topology`.
- `PRODUCER-REPORT-SCHEMAS.md`, which governs the isolation report, lists all
  seven, naming `session_frame_topology` explicitly.

The r4 revision moved frame topology out of the producer claim set and into the
unobserved-control set — decision 2d of the revision record — and carried that
change into the extractor constant and into one of the two schema documents.
Each producer emitted exactly what the document governing that file told it to
emit. The extractor then applied the seven-field rule to both files.

This is the failure shape the r4 handoff warned the next auditor to expect and
to report plainly: a code firing on behaviour the pinned instructions never
forbade. Under the r3 vocabulary it is neither a producer violation nor a
vocabulary gap. It is an internal inconsistency between two pinned documents of
the same revision, and no preflight condition in the handoff inspects one
protocol document against another.

The same six-key attestation shape is present in both contexts, so the attempt
would have failed on Context B for the same reason had it reached it.

## Defect two — the validator's own failure path

After the extractor failed closed, the wrapper attempted to write an
`indeterminate` raw validation result and raised `TypeError: raw_result()
missing 1 required keyword-only argument: 'scope_qualifications'`. The process
therefore exited `1` rather than the intended nonzero status, and the result
document the protocol expects on a failed attempt does not exist.

The invocation receipt and the derived trace-audit stub were written before the
crash and are preserved exactly as the validator left them. This defect is
recorded, not fixed; the no-repair-after-failure rule admits no exception for a
defect in the failure path itself.

## What was and was not established

Established, all before the attempt: the projection, the toolchain bindings, the
fixture suite, the custody digests of both exports, the full tool and envelope
vocabularies, complete parsing of both exports, and an immutable byte-verified
raw tree.

Not established, because the attempt aborted at the first failing check: every
substantive question this protocol exists to answer. Whether Context A's
identifier log reconciles, whether either receipt marker binds, whether generic
executions resolve, whether local access stayed declared, whether Context B
represents any network event, and whether any A material appears in B are all
unadjudicated. The three prohibitions the r3 attempt did confirm are **not**
carried forward; nothing in that record transfers to this one.

No producer conduct is impugned by this note. On the one fact the attempt did
surface, both producers followed their pinned instructions exactly.

## Custody and preservation

The invocation receipt and the derived trace-audit stub were preserved unmodified
as the validator wrote them, with owner-only permissions, alongside a private
failure record holding the verbatim terminal output and the read-only diagnosis.
Nothing was deleted, re-emitted, or edited.

Per the handoff, the raw tree and audit artifacts are committed only on a
conforming result. This epoch did not produce one, so neither the assembled raw
producer tree nor the audit outputs enter Git. Both remain on the owner's disk,
untracked and read-only, in private owner custody, and are ignored by this
repository so that no later session can commit them by accident. The two private
exports and the fourteen downloaded producer artifacts were read and hashed for
this audit only, were not ingested, and are not certified by this note.

No claim boundary is published. The qualified and unqualified boundary sentences
both belong to a conforming result and neither is quoted, paraphrased, or
implied anywhere for this attempt.

## What a further attempt would require

1. Reconcile the two r4 schema documents against each other and against the
   extractor's constants, in a new revision. The narrow defect is one field name
   missing from one document; the general defect is that no preflight condition
   compares a pinned schema document against the pinned code that enforces it,
   and the fixture suite constructs its attestations programmatically, so 411
   passing tests could not see the disagreement.
2. Fix the validator's failure path so that a failed attempt produces the result
   document the protocol requires, and add a fixture that exercises it.
3. Decide whether a schema-conformance defect of this kind should consume a
   one-shot validator attempt at all, or whether the attempt boundary should
   fall after a structural conformance pass over the raw tree that a new
   preflight condition could run without adjudicating conduct.
4. Re-freeze a new source projection over whatever changes, add fixtures for
   each decision, and obtain two new producer sessions and two new exports.

None of that may be done inside `r4`. The r1, r2, r3, and r4 records and
toolchains remain sealed and byte-identical; this note corrects nothing in them
and records a new event.

## Standing limits and what remains with the author

`v0.9.9-internal` remains a valid internal manuscript candidate whose
review-certification path is not executable under revision `v0.9.9-r4`. Nothing
here certifies independence, platform completeness, export completeness,
scholarly correctness, novelty, comparative rank, or release readiness, and an
aborted attempt certifies less than a noncompliant one.

No blind-review finding has been dispositioned. Phase 5 was never reached, and a
voided epoch disposes of nothing.

Licence, stable locator, and activity-data decisions remain solely with Rashid
Azarang and are untouched by this stop. No release decision was made or implied.
