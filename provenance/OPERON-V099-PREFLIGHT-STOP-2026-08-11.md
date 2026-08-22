# Operon v0.9.9 preflight stop — tool vocabulary insufficient

## Classification

The detached trace audit for protocol revision `v0.9.9-r1` stopped during the
Phase 4 preflight, before the immutable raw tree was assembled and before the
raw validator was invoked. This is a `tooling-insufficient preflight stop`.

It is **not** a failed review, a failed validator attempt, a consumed one-shot
validator budget, or a voided raw epoch. No `operon-v099/` raw tree was
created, no `operon-certification-v099/` directory was created, no
`VALIDATOR-INVOCATION.json` was written, and no producer bytes were ingested
into this repository.

Both Claude Science producer sessions completed and were exported by the owner.
Those exports remain private, outside Git, and were not modified. Only digests,
byte counts, export metadata, frame identifiers, and path-free derived counts
appear below.

## Preflight conditions that passed

At Epistemics `main@baf406da714c2568984f95a2d02f816687f1afd1`, working tree
clean:

1. **Repository state.** Branch `main`, no uncommitted changes, no prior
   v0.9.9 raw or certification path present.
2. **Source projection recomputes exactly.** All 30 file-backed SHA-256 fields
   in `SOURCE-PROJECTION-V099.json` recompute against the authoritative
   field-to-path mapping in `build.py` and `analysis/verify_operon_v099.py`.
   The one remaining digest field, `internal_build_context_sha256`, recomputes
   from the frozen internal build context. All 31 digest fields pass.
3. **No v0.9.8 reuse.** `SOURCE-PROJECTION-V098.json` remains present, intact,
   and distinct. Seven non-protocol source digests are byte-identical to the
   v0.9.8 projection because those source files genuinely did not change
   between candidates; each was independently recomputed from its actual
   on-disk file rather than copied. Every v0.9.9 protocol and toolchain field —
   tool policy, both context prompts, isolation preflight, trace-audit
   contract, all five schemas, trace extractor, raw validator, Operon gate,
   review-pair manifest, PDF, text projection, supplement, and build context —
   differs from v0.9.8.
4. **Reviewed-input identities.** The pinned PDF
   (`d371922d…`, 346,730 bytes), text projection (`fa49b71e…`, 127,579 bytes),
   and supplement (`8edd1803…`, 55,375 bytes) all verify, and
   `REVIEW-PAIR-MANIFEST-V099.json` binds exactly those three identities plus
   the `pdftotext` executable identity and arguments.
5. **Validator interface.** `analysis/validate_operon_raw.py` exposes the
   two-export interface, creates the invocation receipt by exclusive creation
   before semantic parsing, invokes the pinned extractor internally, and
   exposes no caller-supplied trace-audit argument.
6. **Fixture suites pass unchanged.** 44 tests across the trace-extractor,
   raw-validator, v0.9.9 gate, and review-pair modules pass at the committed
   revision, including the required adversarial fixtures for byte-flipped and
   truncated exports, duplicate/orphan/cyclic/nonreciprocal frames, unknown
   tools, ambiguous generic code, path traversal, parent listing, Context B
   network access, Context A request-log mismatch, output re-emission,
   post-receipt events, receipt mismatch, cross-session identifiers, drift, and
   private-export leakage.
7. **Exports hashed before semantic parsing.** Both supplied exports were
   hashed first:

   | Role | SHA-256 | Bytes | Export version | Exported at (UTC) | Root frame |
   | --- | --- | ---: | --- | --- | --- |
   | `context_a` | `4c465a4aa416a62e511689b9d4210812dfef45a29e5f5fd8e3570ead242ea0d1` | 744,798 | `1.0` | `2026-08-12T03:20:13.585Z` | `aa5ed948-8434-4f16-a3a8-b404f4e0ed84` |
   | `context_b` | `ff50bfb886fb1cf5c9fa4a2dc973b3ebee83608b68f46d7b864938497df6f957` | 640,364 | `1.0` | `2026-08-12T05:14:01.224Z` | `c86da210-9442-49c1-8e10-f4740d342205` |

8. **Export structure conforms.** Both exports declare `export_version` `1.0`,
   which the pinned extractor accepts. Both top-level key sets match
   `EXPORT_FIELDS` exactly. Every frame key set matches `FRAME_FIELDS`, every
   message key set matches `MESSAGE_FIELDS`, and every artifact record key set
   matches `ARTIFACT_FIELDS`, with no unknown fields in either export. Content
   blocks are exclusively `text`, `tool_use`, and `tool_result`. Frame counts
   agree with the export summaries: A has 4 frames and 8 artifact records, B
   has 3 frames and 6 artifact records. Both sessions report `completed`.

## The preflight condition that failed

The handoff requires that the extractor "understands the actual export version
and parses every frame, message, content block, artifact record, and tool-use
input."

The version, frame, message, content-block, and artifact-record halves of that
condition hold. The tool-use-input half does not.

The Context A export represents one `tool_use` event whose tool name is
`request_network_access`, emitted in the root frame
`aa5ed948-8434-4f16-a3a8-b404f4e0ed84`. That name is declared neither in the
frozen `operon-protocol-v099/TOOL-POLICY.json` tool registry nor in the pinned
extractor's `EXPECTED_TOOLS` set. Both fix the vocabulary at the same ten
names: `bash`, `edit_file`, `generate_plan`, `python`, `read_file`, `repl`,
`save_artifacts`, `submit_output`, `update_step_status`, and
`wait_for_notification`.

Because no declaration exists, the pinned protocol supplies no `locator_fields`
for that event, so the extractor has no defined way to parse its tool-use
input. Under `"unknown_tool_policy": "fail_closed"` it would classify the event
as `UNKNOWN_TOOL` rather than parse it.

Represented tool-use counts, path-free:

| Role | Tool events | Declared names observed | Undeclared names observed |
| --- | ---: | --- | --- |
| `context_a` | 86 | `read_file` 33, `python` 35, `repl` 9, `wait_for_notification` 3, `save_artifacts` 3, `submit_output` 2 | `request_network_access` 1 |
| `context_b` | 50 | `read_file` 20, `repl` 19, `python` 6, `save_artifacts` 3, `submit_output` 2 | none |

Context B's vocabulary is fully covered. The gap is confined to a single
Context A event.

The raw-tree read-only condition was not reached, because the handoff directs a
stop "without touching the raw tree" and the failure is establishable without
assembling it.

## Protocol defect

This is a defect in the frozen v0.9.9 protocol, not a producer violation.

Context A's domain policy explicitly permits network activity: its
`network_mode` is `represented_https_requests_to_allowed_hosts_only`, it pins a
fourteen-host allowlist, and it requires bidirectional reconciliation against
the identifier log. The protocol therefore authorizes an activity while
declaring no tool through which the host performs it. The extractor recognizes
network activity only as URLs inspected inside `generic_execution` code; it has
no term for a platform-level network-access request.

A producer session following the Context A instructions as written, on a host
that mediates network access through a request tool, necessarily emits an event
the frozen vocabulary cannot name. The single observed event is consistent with
that reading. Whether the surrounding Context A network behaviour actually
conformed is **undetermined** — that question belongs to a validator run that
has deliberately not occurred, and nothing in this note should be read as
adjudicating it.

Had the validator been invoked, the attempt would have been spent adjudicating
a known gap in the protocol's own vocabulary rather than a genuine question
about producer behaviour, and the epoch would have been voided under a rule
that also forbids repairing the tooling afterwards. Stopping here preserves the
one-shot budget for a protocol revision that can actually decide the question.

Per the epoch rule, no extractor, tool policy, validator, or projection was
modified after this failure was observed.

## Disposition

`v0.9.9-internal` remains a valid internal manuscript candidate. Its
review-certification path is not executable under revision `v0.9.9-r1`.

The next protocol revision must, before any producer session runs:

- enumerate the producing platform's actual tool vocabulary and reconcile it
  against `TOOL-POLICY.json` and the extractor's `EXPECTED_TOOLS`, rather than
  assuming the vocabulary;
- declare an explicit policy class for platform-mediated network-access
  requests in Context A, with `locator_fields` sufficient to reconcile such an
  event bidirectionally against the identifier log, and an explicit
  prohibition of the same class in Context B;
- add adversarial fixtures for a represented network-access request that is
  logged and allowlisted, one that is unlogged, one to a disallowed host, and
  one appearing in Context B;
- re-freeze a new source projection over the corrected policy, extractor, and
  validator; and
- obtain two new producer sessions and two new exports under that revision.

The two supplied exports and the fourteen downloaded producer artifacts remain
in private owner custody. They were read and hashed for this preflight only,
were not ingested, and are not certified by this note.

## What remains with the author

Licence, stable locator, and activity-data decisions remain solely with Rashid
Azarang and are untouched by this stop. No release decision was made or
implied.
