# Operon v0.9.9-r3 raw epoch void — first validator attempt returned noncompliant

## Classification

The detached trace audit for protocol revision `v0.9.9-r3` passed every Phase 4
preflight condition, assembled the immutable raw tree, and consumed its first
and only full validator attempt. The attempt exited nonzero with status
`noncompliant`.

Under the pinned rule this **voids the raw epoch**. It is not a preflight stop.
It is the first time this candidate has reached adjudication at all: `r1` and
`r2` both died in preflight on a frozen vocabulary that lacked a term for
something the platform emitted, and `r3` closed both of those gaps
successfully — no unknown tool name, no undeclared envelope field, no unparsed
event in either export.

The one-shot validator budget for this epoch is spent. No retry against this
raw tree, no reopened producer session, no modified export, and no tooling
repair is permitted now that a raw failure has been observed. A further attempt
requires a new projected protocol revision, two new producer sessions, two new
exports, and a new raw root.

Only digests, byte counts, export metadata, frame identifiers, field names,
stable codes, and path-free derived counts appear below. No local path, message
content, prompt text, artifact content, envelope-field value, represented URL,
or owner identity is reproduced here or anywhere in the public record.

## Preflight results, condition by condition

At Epistemics `main@8a3c3698150821e8bc1c40ac1d0aae1e0b39cd89`, working tree
clean, every handoff condition was established before anything ran.

1. **Repository state.** Branch `main`, no uncommitted changes, and neither a
   prior `operon-v099r3` raw path nor a prior `operon-certification-v099r3`
   audit path present.
2. **Source projection recomputes exactly.** The r3 projection freezer reports
   that all 34 fields recompute.
3. **Carry-forward and binding.** Twenty-one fields are byte-identical to the
   r2 projection and thirteen differ. All thirteen are protocol or toolchain
   identities — tool policy, r3 trace extractor, r3 raw validator, r3 gate, r3
   review-pair manifest, the trace-audit contract, five protocol schema
   documents, and the revision string — and each was independently recomputed
   from its actual on-disk r3 file. All four reviewed-input and build
   identities carry forward unchanged and equal their r1 values: manuscript PDF
   `d371922d…` (346,730 bytes), reproducibility supplement `8edd1803…` (55,375
   bytes), deterministic text projection `fa49b71e…` (127,579 bytes), and the
   internal build context.
4. **No earlier-lineage reuse.** The v0.9.8, r1, and r2 projections remain
   present, intact, and distinct as whole files, and no r3 protocol or
   toolchain digest equals its r1 or r2 counterpart.
5. **Reviewed-input identities.** The r3 review-pair manifest binds exactly the
   three reviewed identities above plus the `pdftotext` executable identity,
   version, and arguments.
6. **Validator interface.** The r3 wrapper exposes the eleven-argument
   two-export interface named in the handoff and exposes no caller-supplied
   trace-audit input.
7. **Fixture suites pass unchanged.** 308 tests across 22 modules pass at the
   committed revision; no test file was modified. The four r3 modules
   contribute 83 of them, including the four network-access-request fixtures
   and all six envelope-class fixture families: out-of-band pointer qualifying
   without voiding and never publishing its value, undeclared envelope field
   failing closed both with and without a tool result, the
   inert-versus-content-bearing boundary in both directions (URL token,
   absolute path, tool-use-identifier key, out-of-shape value), in-export
   references that resolve and that do not, gate-side boundary discipline in
   four directions, and an undeclared qualification code.
8. **Exports hashed before semantic parsing.** Both supplied exports were
   hashed first:

   | Role | SHA-256 | Bytes | Export version | Exported at (UTC) | Root frame |
   | --- | --- | ---: | --- | --- | --- |
   | `context_a` | `f310245f76ddfa6a66ecec316ba6f3160478c9d6471422b7c80c8c0717197d7c` | 813,547 | `1.0` | `2026-08-12T21:10:35.003Z` | `f94b4abc-52a8-4f75-806b-fe6a2c23fe7b` |
   | `context_b` | `d06456075fbdee62111807061545e1893242386e42fcd45d9e12e35c50ee46b7` | 689,682 | `1.0` | `2026-08-12T21:44:20.646Z` | `6ec600cb-fb14-4767-8c03-01631460bab8` |

9. **Tool vocabulary fully declared.** Every represented tool name in both
   exports resolves to a declared class in the r3 registry. No `UNKNOWN_TOOL`
   condition exists.

   | Role | Tool events | Declared names observed |
   | --- | ---: | --- |
   | `context_a` | 72 | `python` 35, `repl` 20, `read_file` 9, `save_artifacts` 3, `submit_output` 3, `request_network_access` 2 |
   | `context_b` | 49 | `repl` 19, `read_file` 17, `python` 7, `save_artifacts` 3, `submit_output` 3 |

   Context A represents two `request_network_access` calls. The class that r2
   declared but never exercised is exercised here. Context B represents none,
   as its domain requires.

10. **Envelope vocabulary fully declared — the r2 gap is closed.** Every
    represented field at all five levels resolves to a declared field with a
    declared class in both exports. Top-level, frame, and artifact-record key
    sets match their pinned sets exactly. Observed message-level fields are
    `role`, `content`, `_ts`, `_uuid`, `_response_id`, `_tokens`,
    `_harness_notice`, `_harness_prompt`, `_intent_id`, `_artifact_refs`, and
    `_system_hint`; observed content-block fields are `type`, `text`, `id`,
    `name`, `input`, `caller`, `tool_use_id`, `content`, `is_error`, and
    `_viewport_stub`. No `UNDECLARED_ENVELOPE_FIELD`, no
    `ENVELOPE_FIELD_CLASS_VIOLATION`, and no `ENVELOPE_REFERENCE_UNRESOLVED`
    arose. `_persisted_spills`, the field that stopped r2, does not occur in
    either of these exports.
11. **Both exports parse completely.** Invoking the pinned extractor's export
    loader on each export as a read-only diagnostic — writing no file and
    performing no adjudication — accepted both: Context A with 4 frames and 151
    messages, Context B with 4 frames and 104 messages.
12. **Raw tree assembled, byte-verified, and read-only.** 18 files, 731,522
    bytes total, every copy byte-identical to its source and the three pinned
    context-b inputs matching their projected digests. No `.DS_Store`,
    AppleDouble file, cache, or derivative entered the tree. Directories and
    files were set read-only and a write probe was refused before validation.

## The attempt

The first and only full attempt used the handoff's exact command interface with
`--protocol-revision v0.9.9-r3`, the r3 projection and tool policy, both
private exports, and an audit directory outside the raw tree.

- Invocation `36bc0438-7061-4a8b-a371-b38626da53e1`, attempt index 1, exclusive
  creation before semantic parsing, at `2026-08-12T21:52:25.329622Z`.
- Raw tree manifest `33a1c82bc8d650b1f0e86811dc7bcfecef7d160bf804dc870fd7df3ef25ce9d2`.
- Exit code `2`; derived audit and raw validation status `noncompliant`.
- All thirteen check families are recorded `indeterminate` — the attempt
  established none of them.

Six stable failure codes were raised:

`CONTEXT_A_REQUEST_LOG_MISMATCH`, `DIRECT_OUTPUT_RECEIPT_MISMATCH`,
`GENERIC_EXECUTION_UNRESOLVED`, `PRODUCER_CLAIM_CONTRADICTION`,
`PROHIBITED_TOOL`, `UNDECLARED_LOCAL_ACCESS`.

Five scope qualifications were derived, all `PLATFORM_CONTENT_ANNOTATION` from
the `_system_hint` message field — two in Context A, three in Context B, each
naming one tool-use identifier, values recorded by digest only and never
published. No `OUT_OF_BAND_CONTENT_POINTER` occurred. The r3 qualification
machinery therefore worked as designed and is not what voided the epoch; the
qualifications are recorded here for completeness and carry no claim, because a
noncompliant result publishes no claim boundary at all.

## What the derived audit counted

Across both exports: 2 exports, 8 frames, 6 descendants, 255 messages, 300
content blocks, 121 tool calls, 0 internal orchestration artifacts.

| Count | Value |
| --- | ---: |
| unknown tool calls | 0 |
| unparsed tool calls | 0 |
| envelope scope qualifications | 5 |
| prohibited tool calls | 10 |
| generic-execution calls inspected | 81 |
| generic-execution calls unresolved | 15 |
| undeclared local reads | 26 |
| undeclared local writes | 0 |
| declared local reads | 3 |
| parent-directory or filesystem-discovery events | 0 |
| Context A represented network requests | 4 |
| Context A allowlisted requests | 4 |
| Context A unmatched represented requests | 0 |
| Context A unmatched request-log entries | 118 |
| Context B represented network requests | 0 |
| receipt submissions | 0 |
| receipt mismatches | 4 |
| post-receipt events | 0 |
| output re-emissions | 0 |
| producer raw-validator calls | 0 |
| producer-authored trace-audit events | 0 |
| cross-session inheritance events | 0 |

Three prohibitions the protocol most cares about held: Context B represents no
network event of any kind, no producer ran a validator or authored a trace
audit, and no A material is detectable in B.

Producer claim comparison classified 133 Context A claims and 27 Context B
claims as `contradicted`, 42 as `corroborated_within_export`, and 4 as
`not_resolvable_from_export`. The contradicted set is dominated by file-open-log
entries, and includes both attestations' claimed descendant-frame count of zero
against three represented descendants each, Context A's claimed external-request
count of 122 against 4 represented requests, and both claimed local-read counts.

## Two readings, and why neither changes the outcome

Reported as-is, per the constitution. The six codes do not all have the same
character, and this note does not pretend otherwise.

Some findings are mismatches between a producer's own written claims and its own
exported trace. Context A's identifier-verification log asserts 122 external
verifications while the export represents 4 network requests reconciling to the
pinned host set, leaving 118 log entries unmatched in the log-to-export
direction. Both attestations claim zero descendants while each export represents
three. Neither producer's `submit_output.findings` carried the pinned
receipt-digest marker in any frame, so no receipt submission was recognized and
both receipt verdicts are `False`. Every `submit_output` event in both sessions
occurred in a descendant frame rather than the session root.

Other findings may instead reflect what this revision's rules can resolve. Of
the 26 undeclared local reads, 25 are `read_file` events that yielded no
resolvable logical path: the platform addresses reads by `version_id` rather
than by `file_path`, and a version identifier for an attached input is not
present in the export's own artifact registry, which contains session-produced
artifacts. Exactly one read — of a self-produced artifact — resolved and was
classified as declared. Similarly, Context A's `request_network_access` inputs
carry a `domain` key rather than any declared locator field; the
field-name-independent URL scan still recovered four request URLs, as the
contract intends, so this did not by itself fail, but it is the same family of
assumption. The 10 prohibited and 15 unresolved generic executions come from
rule findings on represented code — forbidden capability calls, unsupported or
forbidden imports, dunder access, and dynamic local paths — and a next revision
should confirm that the profile matches what the pinned prompts actually ask a
producer to do.

Both readings lead to the same disposition. The adjudication stands exactly as
the validator recorded it, the epoch is void, and the protocol forbids amending
the extractor, policy, validator, gate, or projection now that a raw failure has
been seen. Whichever share of these codes is producer behaviour and whichever is
protocol reach is a question for the next revision's design, not for this note
and not for any edit to the sealed r3 toolchain.

## The Context B erratum

After its receipt submission, Session B emitted a message correcting a
misquotation in one of its own findings, attributing to one comparison row a
phrase that only another row carries; the finding's substance was not withdrawn.
The producer correctly declined to edit any sealed output after submission.

The erratum is producer testimony inside the export, not a trace fact, and it is
recorded here only so it is not lost. It is not adjudicated: Phase 5 was never
reached, no finding was dispositioned, and a voided epoch disposes of nothing.
The extractor counted zero post-receipt events, because no receipt submission
was recognized in the first place.

## Custody and preservation

The invocation receipt, the derived session trace audit, and the raw validation
result were preserved unmodified as the validator wrote them, with owner-only
permissions. Nothing was deleted, re-emitted, or edited.

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

1. Decide, with evidence, which of the six codes reflect producer behaviour and
   which reflect the reach of the r3 rules — in particular whether resolving a
   `read_file` by an attachment `version_id` that the export's artifact registry
   does not contain should be `UNDECLARED_LOCAL_ACCESS`, a declared read against
   the review-pair manifest, or a named qualification.
2. Reconcile the receipt contract with what the platform actually permits: the
   marker rule requires a root-frame `submit_output` whose `findings` list is
   exactly the marker, while both sessions submitted from descendant frames with
   substantive findings lists.
3. Decide whether an attestation's descendant count should be compared against
   represented frames at all, given that both producers were told descendants
   are permitted.
4. Re-freeze a new source projection over whatever changes, add fixtures for
   each decision, and obtain two new producer sessions and two new exports.

None of that may be done inside `r3`. The r1, r2, and r3 records and toolchains
remain sealed and byte-identical; this note corrects nothing in them and records
a new event.

## Standing limits and what remains with the author

`v0.9.9-internal` remains a valid internal manuscript candidate whose
review-certification path is not executable under revision `v0.9.9-r3`. Nothing
here certifies independence, platform completeness, export completeness,
scholarly correctness, novelty, comparative rank, or release readiness, and a
noncompliant result certifies less than that.

Licence, stable locator, and activity-data decisions remain solely with Rashid
Azarang and are untouched by this stop. No release decision was made or implied.
