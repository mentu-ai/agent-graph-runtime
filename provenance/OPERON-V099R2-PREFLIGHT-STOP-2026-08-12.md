# Operon v0.9.9-r2 preflight stop — export message envelope unparsed

## Classification

The detached trace audit for protocol revision `v0.9.9-r2` stopped during the
Phase 4 preflight, before the immutable raw tree was assembled and before the
raw validator was invoked. This is a `tooling-insufficient preflight stop`.

It is **not** a failed review, a failed validator attempt, a consumed one-shot
validator budget, or a voided raw epoch. No `operon-v099r2/` raw tree was
created, no `operon-certification-v099r2/` directory was created, no
`VALIDATOR-INVOCATION.json` was written, and no producer bytes were ingested
into this repository.

Both Claude Science producer sessions completed and were exported by the owner.
Those exports remain private, outside Git, and were not modified. Only digests,
byte counts, export metadata, frame identifiers, schema field names, and
path-free derived counts appear below.

This is the second consecutive preflight stop on this candidate, and it has the
same shape as the first: a frozen vocabulary in the protocol lacks a term for
something the producing platform actually emitted. In `r1` the missing term was
a tool name. Here it is a message-envelope field.

## Preflight conditions that passed

At Epistemics `main@bf9ccba9be5a2f6a675a8d0318a6b4e0df2df96d`, working tree
clean:

1. **Repository state.** Branch `main`, no uncommitted changes, and neither a
   prior `operon-v099r2/` raw path nor a prior `operon-certification-v099r2/`
   audit path present.
2. **Source projection recomputes exactly.**
   `python3 -I analysis/freeze_source_projection_v099r2.py --check` reports that
   `SOURCE-PROJECTION-V099R2.json` recomputes exactly across all 34 fields.
3. **Carry-forward and binding.** Eighteen fields are byte-identical to the r1
   projection and sixteen differ. All four reviewed-input and build identities
   carry forward unchanged: the manuscript PDF (`d371922d…`, 346,730 bytes), the
   reproducibility supplement (`8edd1803…`, 55,375 bytes), the deterministic
   text projection (`fa49b71e…`, 127,579 bytes), and the internal build context.
   Every one of the sixteen changed fields is a protocol or toolchain identity,
   and each was independently recomputed from its actual on-disk r2 file: tool
   policy, both context prompts, isolation preflight, trace-audit contract, all
   five schemas, r2 trace extractor, r2 raw validator, r2 Operon gate, and the
   r2 review-pair manifest.
4. **No r1 or v0.9.8 reuse.** `SOURCE-PROJECTION-V098.json` and
   `SOURCE-PROJECTION-V099.json` remain present, intact, and distinct from the
   r2 projection as whole files, and every r2 protocol and toolchain digest
   differs from both.
5. **Reviewed-input identities.** `REVIEW-PAIR-MANIFEST-V099R2.json` binds
   exactly the three reviewed identities above plus the `pdftotext` executable
   identity, version, and arguments.
6. **Validator interface.** `analysis/validate_operon_raw_v099r2.py` exposes the
   eleven-argument two-export interface named in the handoff, including
   `--session-export-a`, `--session-export-b`, `--invocation-output`, and
   `--trace-audit-output`. It exposes no caller-supplied trace-audit input.
7. **Fixture suites pass unchanged.** 225 tests across 18 modules pass at the
   committed revision. The four r2 modules contribute 61 of them, including all
   four required network-access-request fixtures — a logged and allowlisted
   Context A request that reconciles bidirectionally, an unlogged Context A
   request, a Context A request to a host outside the pinned set, and a Context B
   request that violates even with no resolvable URL — plus the unresolved-input
   case, reconciliation of a URL outside the declared locator fields, and the
   assertion that the declared class is never reported as an unknown tool. No
   test file was modified.
8. **Exports hashed before semantic parsing.** Both supplied exports were hashed
   first:

   | Role | SHA-256 | Bytes | Export version | Exported at (UTC) | Root frame |
   | --- | --- | ---: | --- | --- | --- |
   | `context_a` | `a36c8c56f0848fc4fed6858ad257d5b535fa19b45030d20f4fdff3313a4e4a9c` | 760,472 | `1.0` | `2026-08-12T17:24:45.640Z` | `ccdf214a-c3dc-4324-8ec0-4c30e4ddfa72` |
   | `context_b` | `ddbaed31cc7561f5fd6f45596b519b5c9a07d822c468efb9a13da371cf6977dd` | 679,173 | `1.0` | `2026-08-12T18:07:00.368Z` | `45c9a20e-bcc2-4380-99c8-7c45dde30e37` |

9. **Tool vocabulary fully declared — the r1 gap is closed.** Every represented
   tool name in both exports resolves to a declared class in the r2 registry.
   No undeclared name appears in either export, and no `UNKNOWN_TOOL` condition
   exists:

   | Role | Tool events | Declared names observed | Undeclared names observed |
   | --- | ---: | --- | --- |
   | `context_a` | 70 | `python` 34, `repl` 19, `read_file` 11, `submit_output` 4, `save_artifacts` 2 | none |
   | `context_b` | 60 | `read_file` 27, `repl` 21, `python` 7, `save_artifacts` 3, `submit_output` 2 | none |

   Neither export represents a `request_network_access` call at all. The r2
   declaration was therefore necessary to reach this preflight cleanly, but the
   class went unexercised in these two sessions. Whether Context A's network
   behaviour conformed remains undetermined and is not adjudicated here.

10. **Export skeletons conform.** Both exports declare `export_version` `1.0`,
    which the pinned extractor accepts. Both top-level key sets match
    `EXPORT_FIELDS` exactly. Every frame key set matches `FRAME_FIELDS`, every
    artifact record key set matches `ARTIFACT_FIELDS`, and content blocks are
    exclusively `text`, `tool_use`, and `tool_result`, each conforming to its
    pinned block shape. Frame counts agree with the export summaries: A has 5
    frames (4 descendants) and 8 artifact records, B has 3 frames (2
    descendants) and 6 artifact records. Every frame in both exports reports
    `completed`, and agent names are confined to `OPERON` and `REVIEWER`.

## The preflight condition that failed

The handoff requires that the pinned r2 extractor parse both exports' actual
export version, including every tool-use input, under the declared vocabulary.

The tool-vocabulary half of that condition holds, as recorded above. The
complete-parse half does not.

The Context B export contains one message that carries an envelope field named
`_persisted_spills`. It appears in B's root frame
`45c9a20e-bcc2-4380-99c8-7c45dde30e37`, at message index 10, on a `user`-role
message whose only content block is a `tool_result`. It is the single such
occurrence across both exports; Context A's envelopes are fully covered.

That field is not declared in the pinned extractor's `MESSAGE_FIELDS` set, which
fixes the message envelope at fourteen names: `role`, `content`, `_ts`, `_uuid`,
`_harness_notice`, `_intent_id`, `_response_id`, `_tokens`, `_system_hint`,
`_async_exec`, `_artifact_refs`, `_harness_prompt`, and `_from_agent`.

The extractor's message check requires the envelope key set to be a subset of
that fixed set and raises `EXPORT_EVENT_UNPARSED` — "message schema contains an
unparsed field" — otherwise. The condition was confirmed two ways: by evaluating
the pinned predicate against the actual export bytes, and by invoking the
extractor's own `load_export` function on each export as a read-only diagnostic
that wrote no file and performed no adjudication. That diagnostic accepts the
Context A export (5 frames, 147 messages, 172 content blocks, 70 tool events)
and rejects the Context B export with `EXPORT_EVENT_UNPARSED`.

Under the contract, a "partially unparsed export cannot receive compliant
status." Invoking the validator would therefore have spent the single attempt
producing a `noncompliant` or `indeterminate` result caused by the protocol's own
envelope vocabulary rather than by producer behaviour, and would have voided the
raw epoch under a rule that also forbids repairing the tooling afterwards.

The raw-tree read-only condition was not reached, because the handoff directs a
stop "without touching the raw tree" and the failure is establishable without
assembling it.

## Protocol defect

This is a defect in the frozen `r2` protocol, not a demonstrated producer
violation. Nothing in the Context B prompt asks the producer to emit or suppress
platform envelope metadata, and the producer has no control over it.

The field is not cosmetic, and the next revision must not declare it as
ignorable metadata by reflex. Its represented value is a single object mapping
one `python` tool-use identifier to one string. That string is a host-local
absolute filesystem path of 169 characters. Its value is deliberately not
reproduced here, in this note or anywhere else in the public record.

What that implies is the substantive question. The field records that the
platform persisted — "spilled" — some portion of a generic-execution result to a
host-local file outside the export, and retained a pointer to it. The referenced
`tool_result` still carries 2,796 characters inline, which is above the median
inline result size in that export and ranks twentieth of sixty, so the inline
content is not obviously a stub. But the protocol cannot currently tell whether
the inline content is complete, truncated, or summarized, and the spilled file
itself is outside the supplied export and outside this audit's reach.

This bears directly on the standing limitation the contract already carries.
`host_local_derivatives` and `export_completeness` are both listed in the tool
policy's `unobservable_host_controls`, and the mandatory limitations text
already states that export completeness cannot be independently established.
What is new is that an export now contains positive evidence that out-of-band
persistence occurred for a specific generic-execution event, rather than merely
being unable to exclude it. A revision that silences the field without deciding
its meaning would convert a visible completeness gap into an invisible one.

Per the epoch rule, no extractor, tool policy, validator, gate, or projection
was modified after this failure was observed.

## Disposition

`v0.9.9-internal` remains a valid internal manuscript candidate. Its
review-certification path is not executable under revision `v0.9.9-r2`.

Two consecutive stops have now been caused by the same root cause: the protocol
freezes a closed vocabulary over a platform surface whose vocabulary is not a
published, stable contract, and discovers the mismatch one term at a time, after
two producer sessions have already been spent. The next revision should treat
that pattern itself as the defect. Before any producer session runs, it must:

- enumerate the producing platform's actual export envelope — top-level,
  frame, message, content-block, and artifact-record field sets — from real
  exports, and reconcile it against the extractor's pinned sets, exactly as
  `r2` was required to do for tool names and did successfully;
- decide and declare an explicit policy for `_persisted_spills`, including
  whether a represented out-of-band persistence pointer on a generic-execution
  result is compatible with a scope-qualified compliant status, or whether it
  is an explicit indeterminate condition with its own stable failure code;
- decide, more generally, whether unknown *metadata* envelope fields should
  fail closed as unparsed, as they do today, or be admitted under a declared
  ignorable-metadata class that is separated from fields capable of carrying or
  referencing content — the two cases have different evidential consequences and
  the current single rule conflates them;
- add adversarial fixtures for an envelope field carrying an out-of-band
  content pointer, for an unknown envelope field on a message with no tool
  result, and for the ignorable-versus-content-bearing distinction, whichever
  way it is decided;
- re-freeze a new source projection over the corrected policy, extractor,
  validator, and gate; and
- obtain two new producer sessions and two new exports under that revision.

The two supplied exports and the fourteen downloaded producer artifacts remain
in private owner custody. They were read and hashed for this preflight only,
were not ingested, and are not certified by this note.

The `r1` record and the `r2` protocol files remain sealed and byte-identical.
This note corrects nothing in them; it records a new event.

## What remains with the author

Licence, stable locator, and activity-data decisions remain solely with Rashid
Azarang and are untouched by this stop. No release decision was made or implied.
