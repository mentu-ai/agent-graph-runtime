# Operon v0.9.9-r5 raw epoch void — first validator attempt exited nonzero

## Classification

The detached trace audit for protocol revision `v0.9.9-r5` passed every launch
and Phase 4 preflight condition, including both instrument-consistency
conditions this revision added, assembled the immutable raw tree, and consumed
its first and only full validator attempt. The attempt exited `2`. It raised a
single stable failure code, `EXPORT_STRUCTURE_INVALID`, and both the derived
trace-audit stub and the raw validation result carry status `indeterminate`.

Under the pinned rule this **voids the raw epoch**. It is not a preflight stop
and it is not `PRODUCER_BLAMELESS_SCHEMA_DEFECT`.

This is the third consecutive epoch to reach the attempt. `r3` failed *at*
adjudication with six codes and a complete count table. `r4` failed on a
structural precondition of the producer attestation and produced no result
document at all. `r5` failed on a structural precondition of one supplied
export, before any check family was established — but unlike `r4` it reported
that failure in the machine-readable form the protocol requires.

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

At Epistemics `main@c0924dbaafa3ad88190615457b65e4e55ce6e23a`, every handoff
condition was established before anything ran. Concurrent unrelated corpus work
was in progress on `main` during the epoch; it touched no file in this package,
and every projected and toolchain digest recorded below was recomputed from the
on-disk bytes this attempt actually used.

1. **Repository state.** Branch `main`, no uncommitted change in this package,
   and neither a prior `operon-v099r5` raw path nor a prior
   `operon-certification-v099r5` audit path present.
2. **Document consistency — the condition `r4` lacked.** The r5
   document-consistency checker exits `0`: all twenty bound values agree across
   every source that carries them, including the code constants that enforce
   them. The seven-member `unobserved_controls` set that voided `r4` is
   identical in the attestation schema, the isolation-report schema, the tool
   policy, and the extractor constant. No `INSTRUMENT_DOCUMENT_CONTRADICTION`
   exists at audit time.
3. **Raw conformance over the producer files — the condition `r4` lacked.** The
   r5 raw-conformance preflight exits `0` over twenty probes spanning both roles
   and all four producer report files: zero instrument contradictions and zero
   producer schema deviations, disposition
   `proceed_to_single_validator_attempt`. For every bound value the document the
   producer was given, the constant the code enforces, and the value the
   producer wrote were the same. Both producers emitted the seven-member
   attestation set this revision reconciled.
4. **Source projection recomputes exactly.** The r5 projection freezer reports
   that all 37 fields recompute.
5. **Carry-forward and binding.** Twenty-one fields are byte-identical to the r4
   projection, thirteen differ, and three are new. The thirteen changed and
   three new fields are all protocol or toolchain identities — the r5 tool
   policy, trace extractor, raw validator, gate, review-pair manifest and its
   schema, four protocol schema documents, the trace-audit contract, the
   revision string, and the three new instrument-consistency identities
   (bindings, checker, raw-conformance preflight) — and each was recomputed from
   its actual on-disk r5 file. All four reviewed-input and build identities carry
   forward unchanged and equal their r1 values: manuscript PDF `d371922d…`
   (346,730 bytes), reproducibility supplement `8edd1803…` (55,375 bytes),
   deterministic text projection `fa49b71e…` (127,579 bytes), and the internal
   build context `59e1d0e6…`.
6. **No earlier-lineage reuse.** The v0.9.8, r1, r2, r3, and r4 projections
   remain present, intact, and distinct as whole files. The r5 projection is
   `c6f1d213…`; the r4 projection it supersedes is `e23c1495…`.
7. **Reviewed-input identities.** The r5 review-pair manifest `2a460c00…` binds
   exactly the three reviewed identities above plus the `pdftotext` executable
   identity, version, and arguments, and all three recompute from repository
   originals.
8. **Validator interface.** The r5 wrapper exposes the eleven-argument
   two-export interface named in the handoff and exposes no caller-supplied
   trace-audit input; it accepts only a trace-audit *output* path.
9. **Fixture suites pass unchanged.** 549 tests across 32 modules pass at the
   committed revision on the same interpreter the attempt used; no test file was
   modified. One pre-existing module cannot be executed at all on the platform's
   3.9 interpreter, for a language-version reason unrelated to this protocol; on
   the interpreter of record all 549 pass.
10. **Exports hashed before semantic parsing.** Both supplied exports were
    hashed first, and both matched the orchestrator-recorded digests supplied
    with the custody handoff:

    | Role | SHA-256 | Bytes | Export version | Exported at (UTC) | Root frame |
    | --- | --- | ---: | --- | --- | --- |
    | `context_a` | `c115a3e574812b84177f595dadc8bde0f46098598c35e80a38748ab359531ddc` | 356,036 | `1.0` | `2026-08-14T00:20:54.628Z` | `3aa53588-f4f3-4d23-be23-8cbc74a41384` |
    | `context_b` | `c8041c4cdbd29c356f15d024b3c8418c458448d983a30943814cad1c92bf154b` | 851,425 | `1.0` | `2026-08-14T13:13:11.491Z` | `014271c3-06a0-4798-a0dd-99cf10506105` |

11. **Tool vocabulary fully declared.** Every represented tool name in both
    exports resolves to a declared class in the r5 registry. No `UNKNOWN_TOOL`
    condition exists.

    | Role | Tool events | Declared names observed |
    | --- | ---: | --- |
    | `context_a` | 65 | `python` 47, `request_network_access` 9, `read_file` 7, `save_artifacts` 2 |
    | `context_b` | 50 | `read_file` 19, `repl` 19, `python` 8, `save_artifacts` 2, `submit_output` 2 |

    Context B represents no `request_network_access` call, so its prohibition is
    satisfied on its face; that was never adjudicated. Context A represents nine,
    whose reconciliation against its identifier log was never adjudicated.
    Context A represents **no `submit_output` call at all** — see below.

12. **Envelope vocabulary fully declared.** Every represented field at all five
    levels resolves to a declared field with a declared class in both exports.
    Top-level, frame, content-block, and artifact-record key sets match their
    pinned sets exactly in both. Observed message-level fields are `role`,
    `content`, `_ts`, `_uuid`, `_response_id`, `_tokens`, `_harness_notice`,
    `_intent_id`, and `_persisted_spills` in Context A, and those less
    `_persisted_spills` plus `_artifact_refs`, `_harness_prompt`, and
    `_system_hint` in Context B. No `UNDECLARED_ENVELOPE_FIELD` condition
    exists. No field was ever *classified*, because the attempt aborted before
    the class model was applied.
13. **Both exports are structurally enumerable.** Read-only enumeration, writing
    no file and performing no adjudication, found Context A with 1 frame, 111
    messages, 161 content blocks, and 8 artifact records; Context B with 3
    frames, 96 messages, 144 content blocks, and 6 artifact records. Every
    message body is a block list; `tool_use` and `tool_result` blocks are
    balanced in both (65/65 and 50/50); every frame is reachable from the
    declared root and parent/child references are reciprocal. Both frame counts
    and both artifact-record counts equal the orchestrator-recorded custody
    metadata.
14. **Raw tree assembled, byte-verified, and read-only.** 18 files, 743,075
    bytes total, tree digest
    `b1d5a51a6c6d85a6be2e94e6039486094a19426ecf8b1a552599f7d746cff28c`, every
    copy byte-identical to its source and the three pinned context-b inputs
    matching their projected digests. Contents were copied without metadata, so
    no `.DS_Store`, AppleDouble file, cache, or derivative entered the tree.
    Directories and files were set read-only and four write probes — create in
    the root, create in a role directory, append to an existing producer file,
    and delete — were each refused before validation.

## The attempt

The first and only full attempt used the handoff's exact command interface with
`--protocol-revision v0.9.9-r5`, the r5 projection and tool policy, both private
exports, and an audit directory outside the raw tree.

- Invocation `ab7e7f42-fdb2-429f-8405-a507b950e2f0`, attempt index 1, exclusive
  creation before semantic parsing, at `2026-08-14T13:37:04.039736Z`.
- Raw tree manifest `6af646c5…`; package manifest `3863f869…`.
- Exit code `2`. Derived trace-audit stub status `indeterminate`, schema
  `agent-graph-runtime.trace-extraction-error.v1`, failure code
  `EXPORT_STRUCTURE_INVALID`, detail *the detached validator failed closed
  before completing the attempt*.
- A raw validation result **does** exist, schema
  `agent-graph-runtime.operon-raw-validation.v4`, status `indeterminate`, failure
  codes `["EXPORT_STRUCTURE_INVALID"]`, empty scope-qualification list, all
  thirteen check families recorded `indeterminate` with the detail *the attempt
  did not establish this check family*. It binds the invocation receipt, both
  export digests, the raw tree manifest, the review-pair manifest, the source
  projection, and the tool policy.
- No check family was established. Nothing about producer conduct was
  adjudicated.

## The failure that fired

The extractor validates the structure of each supplied export before adjudicating
anything. Context A's export does not represent a completed session:

- its single root frame carries `status` `processing` and a null `completed_at`;
- the export summary carries `status` `processing` and a null duration; and
- the session represents zero `submit_output` calls across all 65 tool events,
  its last represented tool events being generic execution and artifact saves.

The extractor requires a parseable frame completion time and a completed root
frame. Context A satisfies neither, so it failed closed on the first export it
was given. Context B is structurally clean on every one of these points: three
frames, all `completed`, summary `completed`, and two represented `submit_output`
calls, the last of them the final represented tool event of the session.

This is a defect in the supplied input, not in the instrument and not in the
protocol's rules. The pinned launch instructions are explicit on both points
that failed: the producer's *final* `submit_output` call must carry the receipt
marker, and the human closes the session and exports it only *after* the session
visibly completes. Neither happened for Context A. The eight Context A artifacts
exist and were saved during the session, but an artifact registry is not a
submission, and a `processing` export is not a closed one.

Whether Session A would have conformed had it been allowed to finish is
unknown and is not knowable from this record. Nothing here should be read as a
finding about the review work Context A performed; the attempt never reached it.

## What r5's two new mechanisms did and did not do

Both mechanisms this revision was built to add functioned exactly as designed,
and neither was capable of catching this.

The document-consistency checker cleared all twenty bindings, and the
raw-conformance preflight cleared all twenty producer probes with zero
deviations. The `r4` defect class is closed: the documents, the code constants,
and both producers' actual output agree on the reconciled field set. The
validator's failure path is also demonstrably repaired — the defect that left
`r4` with a spent attempt and nothing but a stack trace did not recur, and this
epoch has a complete, schema-valid, machine-readable result of its failure.

What no r5 preflight condition tests is whether a supplied export represents a
*completed, closed* session. Every preflight condition in the handoff examines
the protocol's own documents, the toolchain's digests, the raw producer tree, or
the exports' vocabulary. None examines the exports' session state, though it is a
single field on the root frame and the summary carries it too. So the one fact
that ended this epoch was cheaply visible before the attempt and was spendable
only as the attempt.

That is the same shape as `r1`, `r2`, and `r4`, in a fourth place. Each of those
revisions closed the gap it met and did not anticipate the next one, and this
note claims no better foresight — only that this instance is now recorded.

## A documentation defect observed, not repaired

`OPERON-QUEUE.md` opens by stating that `v0.9.9-r5` "is no longer launchable:
its epoch is void and its toolchain is sealed," while its own status table on the
following lines records `r5` as "not yet launched," and its Phase 1 through
Phase 5 sections are live launch instructions. The sentence was introduced in the
r5 launch-surfaces commit, whose message describes the intended edit as "r4 is no
longer launchable." It is a wrong revision string in a status sentence.

It is recorded here rather than corrected in place, per the constitution. It is
neither an `INSTRUMENT_DOCUMENT_CONTRADICTION` — the twenty bound values all
agree and the checker exits `0` — nor a governing instruction: the queue's status
prose binds no producer, no code constant, and no check. The handoff governs
launch, and it, the launch prompt, and the queue's own table and phase sections
all agreed that `r5` was live. The statement was false when written and, as of
this note, has become accidentally true.

## What was and was not established

Established, all before the attempt: the twenty document-consistency bindings,
the twenty raw-conformance probes, the projection, the toolchain bindings, the
fixture suite, the custody digests of both exports, the full tool and envelope
vocabularies, the structural enumerability of both exports, and an immutable
byte-verified raw tree.

Not established, because the attempt aborted at the first failing check: every
substantive question this protocol exists to answer. Whether Context A's
identifier log reconciles against its nine represented requests, whether either
receipt marker binds, whether generic executions resolve, whether local access
stayed declared, whether Context B represents any network event, and whether any
A material appears in B are all unadjudicated. No scope qualification was
derived; the empty list in the result means the classifier never ran, not that
none exist. Nothing in the `r3` or `r4` records carries forward.

## Custody and preservation

The invocation receipt, the derived trace-audit stub, and the raw validation
result were preserved unmodified as the validator wrote them, with owner-only
permissions. Nothing was deleted, re-emitted, edited, or retried.

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

1. Two new producer sessions and two new exports. Session A must be allowed to
   reach its final `submit_output`, and both sessions must be exported only after
   they visibly complete. This is the ordinary cost of a voided epoch and is not
   avoidable by any change to the instrument.
2. A new preflight condition, in a new projected revision, that rejects a
   supplied export whose root frame or summary does not represent a completed
   session, before an invocation record exists. The narrow defect is one frame
   status; the general defect is that the preflight validates the protocol
   against itself and the exports' vocabulary, but not the exports' completeness
   as sessions.
3. A decision on where that condition belongs in the two-class jurisprudence
   `r5` introduced. An unfinished export is neither an instrument contradiction
   nor producer conduct the one-shot should adjudicate; on this record it looks
   like a third class — a custody defect in the supplied input — and the honest
   disposition is a preflight stop that preserves the attempt while still costing
   the sessions.
4. A fixture for each decision, and a re-frozen source projection over whatever
   changes.

None of that may be done inside `r5`. The r1, r2, r3, r4, and r5 records and
toolchains remain sealed and byte-identical; this note corrects nothing in them
and records a new event.

## Standing limits and what remains with the author

`v0.9.9-internal` remains a valid internal manuscript candidate whose
review-certification path is not executable under revision `v0.9.9-r5`. Nothing
here certifies independence, platform completeness, export completeness,
scholarly correctness, novelty, comparative rank, or release readiness, and an
attempt that aborted before adjudication certifies less than a noncompliant one.

No blind-review finding has been dispositioned. Phase 5 was never reached, and a
voided epoch disposes of nothing. Context B's six artifacts and Context A's eight
remain uningested and unaudited in private owner custody.

Licence, stable locator, and activity-data decisions remain solely with Rashid
Azarang and are untouched by this stop. No release decision was made or implied.
