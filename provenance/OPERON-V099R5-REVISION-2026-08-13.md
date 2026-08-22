# Operon protocol revision v0.9.9-r5 — documents are components, and the one-shot is for producers

## What this document records

Revision `v0.9.9-r5` corrects the defect that produced the nonzero exit recorded
in `OPERON-V099R4-RAW-EPOCH-VOID-2026-08-13.md`, corrects the second defect that
attempt exposed in the validator's own failure path, and changes the
jurisprudence of the one-shot validator attempt. It changes the review protocol
only. No review has been run under it, no producer session has been opened, and
no validator attempt has been made or consumed.

The reviewed manuscript, reproducibility supplement, and deterministic text
projection are the same bytes with the same digests that `r1` through `r4`
reviewed: `d371922d…` (346,730 bytes), `8edd1803…` (55,375 bytes), and
`fa49b71e…` (127,579 bytes). The r5 projection freezer refuses to run if any of
the three moved.

## What happened, in one paragraph

`r4` moved `session_frame_topology` out of the producer claim set and into the
unobserved-control set. It carried that change into the extractor constant and
into `PRODUCER-REPORT-SCHEMAS.md`, which governs the isolation report, and left
`PRODUCER-ATTESTATION-SCHEMA.md`, which governs the attestation, listing six
fields. Both producers wrote seven fields in their isolation reports and six in
their attestations — exactly what the document governing each file specified.
The extractor applied the seven-field rule to both files, the attempt failed on
the difference before adjudicating a single event, and the wrapper then raised
`TypeError` while writing its own failure record, so the spent attempt produced
no machine-readable result at all.

Two producers followed their instructions perfectly and an epoch was destroyed.
That is the fact this revision is built around.

## Decision 1 — the field set is seven, and every source says so

**Registered basis.** `OPERON-V099R4-REVISION-2026-08-12.md`, decision 2d:
"`session_frame_topology` joins the unobserved-control set." The intent is
unambiguous and is preserved rather than reversed. The extractor and the
isolation-report schema already implemented it; the attestation schema did not.

**Change.** `PRODUCER-ATTESTATION-SCHEMA.md` lists seven fields. It also states
plainly why the seventh exists and what happened in `r4`, so a producer reading
only that document understands the field rather than merely obeying it.

**A third spelling, found while fixing the first two.**
`TOOL-POLICY.json`'s `unobservable_host_controls` carried six names in a
different spelling again — `memory_injection`, `background_network`,
`cross_session_cache` without the `host_` prefix. No code compared it to
anything, so it had drifted silently since it was written. It now carries the
canonical seven.

## Decision 2 — documents are components of the instrument

A prose enumeration a producer is told to satisfy has exactly the force of the
constant that enforces it. `r4` treated one as specification and the other as
commentary, and nothing compared them.

`operon-protocol-v099r5/DOCUMENT-CONSISTENCY-BINDINGS.json` declares twenty
bound values — field sets, direct-output file lists, six schema identifiers, the
revision string, and the public claim boundary in both its forms — and, for
each, every source that must carry it:

- markdown enumerations located by anchor;
- markdown fenced blocks;
- markdown blockquotes, whitespace-normalized, so a quoted claim boundary is
  compared to the constant rather than trusted;
- JSON pointers into the tool policy and the bindings file itself; and
- module-level constants in the pinned extractor, validator, and gate.

`analysis/check_document_consistency_v099r5.py` resolves each source
mechanically and compares them. Python sources are read with `ast` and never
imported, so a check cannot be influenced by module side effects. A binding
whose sources disagree raises `INSTRUMENT_DOCUMENT_CONTRADICTION`. A binding
whose source cannot be resolved — an anchor that matches nothing, an absent
constant, an unresolvable pointer — fails closed, because a check that cannot
find its evidence has not passed.

**Evidence that it works.** Run against the sealed `r4` files, with only the
bindings added, the checker raises `INSTRUMENT_DOCUMENT_CONTRADICTION` on:

1. `attestation.unobserved_controls`, reporting all four sources and the
   disputed members — the exact defect that voided the `r4` epoch, and the tool
   policy's third spelling alongside it; and
2. `schema_id.session_trace_audit`, where `r4`'s code wrote
   `agent-graph-runtime.session-trace-audit.v4` while its trace-audit contract
   documented `v3`.

A third divergence of the same shape, `agent-graph-runtime.operon-raw-validation`
`v4` in code against `v3` in `RAW-VALIDATION-SCHEMA.md`, could not be replayed
because `r4` had no module-level constant to bind; it was found by hoisting one.
Both documentation lags are reconciled to the values the code actually shipped.

So `r4` released three document/code divergences. One was fatal, two were
silent, and 411 passing tests could see none of them, because the fixtures built
their attestations programmatically from the same constants the code enforced.

**When it runs.** Before launch, as a condition of a revision being launchable
at all — at that point a contradiction costs no producer session, no export, and
no attempt. Then again at audit time, because freezing and auditing are
separated in time.

## Decision 3 — a producer-blameless schema defect no longer spends the one-shot

The one-shot validator attempt exists to adjudicate producer conduct. Spending
it on a defect in the instrument measures nothing.

`analysis/preflight_raw_conformance_v099r5.py` resolves three values for every
bound field set: `D`, the enumeration in the document the producer was given;
`C`, the constant the pinned code enforces; and `P`, what the producer's own
output carries.

| Case | Disposition | Exit |
| --- | --- | ---: |
| `D == C` and `P == C` | conforming; proceed to the attempt | 0 |
| `D != C` | `INSTRUMENT_DOCUMENT_CONTRADICTION`, epoch disposition `PRODUCER_BLAMELESS_SCHEMA_DEFECT` — preflight stop, validator never invoked | 3 |
| `D == C` and `P != C` | `PRODUCER_SCHEMA_DEVIATION` — not a stop; the single attempt adjudicates it | 0 |

The boundary test is: **does the producer's output conform to the documents the
producer was given?** If it does and the instrument still rejects it, the
instrument is wrong and the epoch survives. The moment adjudicating producer
conduct is required, it is one-shot territory.

An instrument contradiction outranks a simultaneous deviation, because a broken
instrument cannot adjudicate conduct.

The auditor has no discretion in either direction. Stopping on a producer
deviation would suppress evidence about conduct; spending the attempt on an
instrument contradiction would destroy an epoch to learn nothing. An auditor who
believes a stop is unjust records that in the stop note and stops anyway; one
who believes a deviation is excusable records that in the disposition document
and spends the attempt anyway.

**What the class preserves, and what it does not.** It preserves the validator
attempt: no invocation record is created and the raw epoch is not void. It does
not preserve the producer sessions. Correcting the contradiction is a protocol
change authored with knowledge of real producer data, and every such change in
this program since `r1` has required two fresh producer sessions. The supplied
exports and artifacts stay in private owner custody, uningested and unaudited.
This is the settlement `r1` and `r2` received; what is new is that it is now a
named class with a mechanical test rather than a judgement call.

## Decision 4 — a validator that crashes while failing produces no evidence

`r4` added a required keyword-only `scope_qualifications` argument to
`raw_result` and updated the success path only. Both terminal failure paths kept
calling it without that argument, so the wrapper raised `TypeError` while
writing its own failure record, exited 1 instead of the pinned 2, and wrote no
`raw-validation` document.

Both call sites now pass `scope_qualifications=[]`, which is also correct on the
merits: a failed attempt publishes no claim boundary and carries no
qualification. The preservation blocks no longer let an exception raised while
writing a failure record change the attempt's exit status.

The deeper defect was in the fixtures. `r4` had fixtures for every condition
that could reach a failure path and none for the failure paths themselves. The
suite passed 411 tests over a wrapper that could not report a failure. `r5`
exercises the paths directly, and all four new fixtures fail against the r4
wrapper with the TypeError the audit observed.

`VALIDATOR_FAILURE_PATH_DEFECT` is declared as a stable code so a recurrence is
named rather than described.

## What r5 does not change

The tool registry is unchanged from `r2`. The envelope class model, its four
classes, its mechanical inertness test, and its two envelope-level qualification
codes are unchanged from `r3`. The four adjudication rules and the two
event-level qualification codes are unchanged from `r4`. The status enum, the
claim boundary and its qualified sentence, the one-attempt rule, the
no-repair-after-failure rule, and the private-custody rules are unchanged.

Both producer prompts and `ISOLATION-PREFLIGHT.md` are byte-identical to `r4` —
their projected digests carry forward unchanged. The only producer-facing change
in this revision is one field name in one schema document.

## Verification

- `SOURCE-PROJECTION-V099R5.json` has 37 fields. Twenty-one carry forward from
  `r4` unchanged, including both producer prompts, the isolation preflight, the
  manuscript, supplement, text projection, and build context, the last four of
  which also equal their `r1` values. Thirteen differ and all thirteen are
  protocol or toolchain identities. Three are new: the document-consistency
  bindings, the consistency checker, and the raw-conformance preflight.
- `python3 -I analysis/freeze_source_projection_v099r5.py --check` recomputes
  the projection exactly.
- `python3 -I analysis/check_document_consistency_v099r5.py` reports all
  twenty bindings in agreement.
- The `r2`, `r3`, and `r4` projections still recompute exactly and still bind
  their own untouched toolchains.
- The suite is 549 tests across 32 modules, all passing. The 411 tests that
  predate this revision are unmodified. The 138 new tests cover the r5
  extractor, gate, raw validator, projection, document-consistency checker, and
  raw-conformance preflight.
- The public claim boundary and its qualified sentence are bound across the
  handoff prose, the raw validator, and the gate, so a paraphrase in any one of
  the three is a contradiction rather than a discrepancy someone must notice.
- Required r5 fixtures: a contradicted document pair, documents agreeing with
  each other but not with the enforcing constant, an anchor that locates
  nothing, an enumeration with no bullets, an absent constant, an absent source
  file, a single-source binding, a repeated binding identifier, a wrong revision
  string, and an escaping source path; the boundary test in both directions
  including the r4 replay, an instrument contradiction outranking a simultaneous
  deviation, and a preflight that writes no record unless asked; and all three
  validator terminal paths writing a schema-valid indeterminate result with the
  pinned nonzero status.
- The r5 extractor, raw validator, gate, and the two new tools are new pinned
  files, following the precedent set in `r2`, `r3`, and `r4`, so every sealed
  `r1` through `r4` artifact stays byte-identical and independently verifiable.
- The two producer attachment sets are staged and byte-verified outside the
  repository at `~/Desktop/operon-v0995-fresh-inputs`, 8 files for A and 10 for
  B, with the asymmetry derived from the tool policy rather than restated, and
  the corrected attestation schema present in both.

## Standing limits

This revision does not review anything. It restores the ability to attempt a
review for the fourth time, and it is the first restoration whose subject is the
instrument's internal consistency rather than its fit to the platform or to
producer behaviour.

The strongest available process result remains
`conforming_within_supplied_exports`, which is not an independence,
platform-completeness, scholarly-correctness, novelty, or release certificate,
and which may carry narrowing qualifications.

No finding from any prior blind review has been dispositioned. The `r1` through
`r4` exports, producer artifacts, and audit outputs stay in private owner
custody, uningested. A voided epoch disposes of nothing, and neither does a
preserved one.

Licence, stable locator, and activity-data decisions remain solely with Rashid
Azarang and are untouched.
