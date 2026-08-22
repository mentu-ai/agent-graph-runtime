# Operon protocol revision v0.9.9-r3 — export envelope class model

## What this document records

Revision `v0.9.9-r3` corrects the defect that stopped the `v0.9.9-r2` detached
preflight, recorded in `OPERON-V099R2-PREFLIGHT-STOP-2026-08-12.md`. It changes
the review protocol only. No review has been run under it, no producer session
has been opened, and no validator attempt has been made or consumed.

The reviewed manuscript, reproducibility supplement, and deterministic text
projection are the same bytes with the same digests that `r1` and `r2` reviewed:
`d371922d…` (346,730 bytes), `8edd1803…` (55,375 bytes), and `fa49b71e…`
(127,579 bytes). A protocol revision may not silently re-cut the artefacts under
review, and the r3 projection freezer refuses to run if any of the three moved.

## The defect, and why it is the same defect twice

`r1` froze a ten-name tool registry and met a platform tool it could not name.
`r2` declared that tool, then froze the export message envelope as a single
closed field set — fourteen names, subset-checked — and met a platform field it
could not name. Both stops consumed two producer sessions before the mismatch
was visible.

The common cause is not either missing term. It is that the protocol freezes a
closed vocabulary over a platform surface that publishes no stable contract, and
has no way to distinguish "this field is bookkeeping I can ignore" from "this
field is something I must adjudicate". Under r2 both cases produced the same
outcome: `EXPORT_EVENT_UNPARSED`, epoch over.

The specific field that stopped r2, `_persisted_spills`, made the cost concrete.
It records that the platform persisted part of a tool result to host-local
storage outside the export and kept a locator for it. Ignoring it would have
hidden a real completeness gap; hard-failing on it spends an epoch on platform
behaviour no producer controls.

## The correction

1. **Enumerated, not assumed.** The declared envelope field sets at all five
   levels — top-level, frame, message, content block, and artifact record —
   were derived from four real human-exported sessions in private owner custody:
   the r1 and r2 Context A and Context B exports. Only field names, value
   shapes, and occurrence counts were derived; no value, path, or message
   content left the private audit workspace.

2. **Every field carries a class.** `parsed`, `inert_metadata`,
   `in_export_reference`, or `content_bearing_reference`. The class is verified
   against the represented value, never trusted from the declaration.

3. **The ignorable class is mechanical.** `inert_metadata` is the
   ignorable-metadata class Rashid asked for. A field may hold it only if its
   value matches its declared shape and contains no URL token, no absolute
   filesystem path, and no tool-use-identifier key. A field declared ignorable
   whose value is not in fact inert is `ENVELOPE_FIELD_CLASS_VIOLATION` and
   fails closed. A declaration alone never makes a value ignorable.

4. **In-export references are resolved, not ignored.** `_artifact_refs` names
   artifact and version identifiers that must appear in the export's own
   registry. An unresolvable reference is `ENVELOPE_REFERENCE_UNRESOLVED`.

5. **Out-of-band references are named, not silenced.**
   `content_bearing_reference` fields raise an explicit named indeterminate
   condition with its own stable code: `OUT_OF_BAND_CONTENT_POINTER` for a
   reference to content or execution state held outside the export, and
   `PLATFORM_CONTENT_ANNOTATION` for platform-authored text attached to an event
   whose semantics this protocol does not fix. Neither voids the epoch and
   neither passes silently.

6. **Undeclared fields still fail closed.** `UNDECLARED_ENVELOPE_FIELD` records
   a coverage gap in this revision, not a producer violation, and is resolved
   only by a new projected revision — never by editing the policy after an
   attempt has seen the field.

## What the enumeration found beyond the stopping field

Enumerating all four exports surfaced two fields `r2` already declared and
therefore admitted without inspection, both of which bear on completeness:

- `_async_exec` maps a tool-use identifier to an execution record holding an
  out-of-band execution id, a status, and an `interrupted` flag. It references
  execution state the export does not contain, and the interrupted flag speaks
  directly to whether the represented result is whole.
- `_system_hint` maps a tool-use identifier to platform-authored text attached
  to that event, between 59 and 332 characters in the observed sessions.

Under r2 both would have passed silently in a compliant run. Under r3 both are
`content_bearing_reference` and raise their qualification codes. Applying the r3
extractor to the four private exports as a read-only diagnostic accepts all four
and names three qualifying conditions in the r1 Context A export, five in r1
Context B, one in r2 Context A, and eight in r2 Context B. The r2 stop note's
finding therefore understated the situation: `_persisted_spills` was the field
that stopped the epoch, but it was not the only field carrying an unexamined
completeness question.

No new undeclared envelope field exists across the four exports beyond
`_persisted_spills`, so the r3 declared sets cover every field these sessions
actually emitted.

## The scope-qualification decision, stated plainly

Rashid chose the named-indeterminate disposition over treating spills as a hard
failure. This document records how that was implemented, because the phrase
admits two readings and only one of them is coherent with the rest of the
protocol.

The status enum is unchanged: `conforming_within_supplied_exports`,
`noncompliant`, `indeterminate`. A scope qualification does **not** set the
status to `indeterminate`, because the handoff voids the epoch on an
indeterminate result and that would make a qualification indistinguishable from
a hard failure — the outcome Rashid rejected. Instead the qualification is a
first-class record that narrows the claim:

- the audit gains a mandatory `scope_qualifications` field listing every
  occurrence with its code, role, level, field, frame id, occurrence count,
  referenced tool-use identifiers, and a digest of the value;
- when any qualification exists the audit's limitations carry the narrowing
  statement;
- the raw validation result restates the qualifications unchanged and appends
  the qualified sentence to its claim boundary; and
- the gate rejects a qualified result publishing the unqualified boundary, an
  unqualified result borrowing the qualified sentence, and any result that drops
  or invents a qualification relative to the derived audit.

So the condition can neither vanish nor be paraphrased away, and it also cannot
silently consume a review epoch. If this is not the reading Rashid intended, the
alternative is a one-line change to the status mapping and a new projection.

## Privacy hardening

The value of any `content_bearing_reference` field is private by class and never
published: host-local locators and platform-authored annotation text are
recorded by digest only. The extractor additionally refuses to emit an audit
containing the export summary's `user_email`, which the previous revisions
carried in the export without an explicit guard.

## Why the r3 toolchain is separate files

The r3 extractor, raw validator, and gate are new pinned files
(`extract_operon_trace_v099r3.py`, `validate_operon_raw_v099r3.py`,
`verify_operon_v099r3.py`), following the precedent set in r2 for the same
reason: the r1 and r2 tools are members of the evidence manifest's
`analysis_tools` inventory, and editing them in place would invalidate
`results/evidence-manifest.json` and the reproduction receipt that depends on
it. Versioned tooling keeps every sealed record byte-identical and
independently verifiable.

## Verification

- `SOURCE-PROJECTION-V099R3.json` has 34 fields. Thirteen differ from r2 and all
  thirteen are protocol or toolchain identities: the tool policy, trace
  extractor, raw validator, gate, review-pair manifest, the trace-audit
  contract, five protocol schema documents, and the revision string. Twenty-one
  are carried forward, including the manuscript, supplement, text projection,
  and build context, all four of which also equal their r1 values.
- `python3 -I analysis/freeze_source_projection_v099r3.py --check` recomputes
  the projection exactly.
- `python3 -I analysis/freeze_source_projection_v099r2.py --check` still
  recomputes the r2 projection exactly, and a guard test asserts that both the
  r1 and r2 projections still bind their own untouched toolchains.
- The test suite is 308 tests across 22 modules, all passing. The 225 tests that
  predate this revision are unmodified. The 83 new tests cover the r3 extractor,
  gate, raw validator, and projection.
- Required r3 fixtures: an out-of-band content pointer that qualifies without
  voiding and never publishes its value; an undeclared envelope field, both with
  and without a tool result on the message; the ignorable-versus-content-bearing
  boundary in both directions, including declared-inert fields carrying a URL, an
  absolute path, a tool-use-identifier key, and a value outside their shape; an
  in-export reference that resolves and one that does not; and gate-side
  boundary discipline in four directions plus an undeclared qualification code.

Writing the fixtures caught two defects in this revision before launch. The
tool-use-identifier rule initially pinned the platform's identifier alphabet,
which is the same closed-vocabulary mistake r3 exists to correct; it now keys on
the `toolu_` prefix and leaves the alphabet permissive. The extractor also still
pinned the r2 validator filename, which the projection binding caught.

## Standing limits

This revision does not review anything. It restores the ability to attempt a
review, for the second time. The strongest available process result remains
`conforming_within_supplied_exports`, which is not an independence,
platform-completeness, scholarly-correctness, novelty, or release certificate,
and which may now additionally carry a narrowing qualification.

Whether the `r1` or `r2` Context A network behaviour actually conformed remains
undetermined and is not settled by this revision. The `r1` and `r2` exports and
producer artifacts stay in private owner custody, uningested. They were read for
envelope enumeration and read-only diagnostics only.

Licence, stable locator, and activity-data decisions remain solely with Rashid
Azarang and are untouched.
