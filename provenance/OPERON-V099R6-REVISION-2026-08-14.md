# Operon protocol revision v0.9.9-r6 — an input that cannot be judged is not a verdict

## What this document records

Revision `v0.9.9-r6` corrects the defect that produced the nonzero exit recorded
in `OPERON-V099R5-RAW-EPOCH-VOID-2026-08-14.md`. It changes the review protocol
only. No review has been run under it, no producer session has been opened, and
no validator attempt has been made or consumed.

The reviewed manuscript, reproducibility supplement, and deterministic text
projection are the same bytes with the same digests that `r1` through `r5`
reviewed: `d371922d…` (346,730 bytes), `8edd1803…` (55,375 bytes), and
`fa49b71e…` (127,579 bytes). The r6 projection freezer refuses to run if any of
the three moved.

## What happened, in one paragraph

`r5` passed every condition it had. Twenty document bindings agreed, twenty
raw-conformance probes found zero producer deviations, both exports hashed to
their custody digests before semantic parsing, every represented tool name and
every represented envelope field at all five levels resolved, 549 fixtures
passed unmodified, and the eighteen-file raw tree was byte-verified, made
read-only, and refused four write probes. The single validator attempt then
exited `2` with `EXPORT_STRUCTURE_INVALID` before establishing a single check
family, because Session A had been exported while it was still running: root
frame status `processing`, no completion time, summary agreeing, and no
`submit_output` call represented anywhere in the session.

Nothing was wrong with the instrument and nothing was known about the producer's
conduct. There was no finished session to judge. That is the fact this revision
is built around.

## Decision 1 — a third jurisprudence class

`r5` established that the one-shot exists to adjudicate producer conduct, and
that spending it on a defect in the instrument measures nothing. It named that
class `PRODUCER_BLAMELESS_SCHEMA_DEFECT`. The `r5` failure is neither that nor
producer conduct:

- the instrument did not contradict itself — the consistency checker exits `0`
  and every bound value agrees; and
- the producer did not deviate from any document — the raw-conformance preflight
  exits `0` over twenty probes with zero deviations.

What failed is the custody chain between the producer session and the auditor.
It delivered an input that cannot answer the question the attempt asks.

`SUPPLIED_INPUT_CUSTODY_DEFECT` is registered as an epoch-preserving preflight
stop at exit `4`, distinct from the exit `3` blameless class so the two remain
mechanically separable, and declared in
`operon-protocol-v099r6/TOOL-POLICY.json` under `supplied_input_custody_policy`.

| Class | Exit | Attempt | Sessions |
| --- | ---: | --- | --- |
| `SUPPLIED_INPUT_CUSTODY_DEFECT` | 4 | preserved | must be re-run |
| `PRODUCER_BLAMELESS_SCHEMA_DEFECT` | 3 | preserved | must be re-run |
| producer conduct | — | spent | — |

Both preserving classes preserve the attempt and not the sessions. A session
cannot be finished after the fact, so the settlement is the one every preserving
stop in this program has carried since `r1`: two fresh producer sessions, with
the supplied exports and artifacts staying in private owner custody, uningested
and unaudited.

## Decision 2 — the condition, and why it is deliberately shallow

`analysis/preflight_export_custody_v099r6.py` runs after both exports are hashed
and before any validator invocation record exists. It rejects a supplied export
when any of four conditions holds:

| Code | Condition |
| --- | --- |
| `EXPORT_ROOT_FRAME_NOT_COMPLETED` | the root frame's status is not `completed` |
| `EXPORT_SUMMARY_NOT_COMPLETED` | the export summary's status is not `completed` |
| `EXPORT_ROOT_FRAME_COMPLETION_TIME_ABSENT` | the root frame carries no completion time |
| `EXPORT_REPRESENTS_NO_SUBMISSION` | no `submit_output` call is represented in any frame |

Each is a property of the export as a record of a session, never a property of
what the producer decided inside it. Submissions are counted across the whole
exported frame tree rather than the root alone, because the pinned prompts
permit the final submission from the root frame or any descendant.

The shallowness is the point, and it is the hardest line in this revision to
hold. Whether the represented submission carries the receipt-digest marker,
whether that marker binds to the producer's direct outputs, whether the
submission is the final represented event — every one of those is tempting to
add here and every one of them is producer conduct. Moving conduct into
preflight would quietly empty the one-shot of the thing it exists to decide,
which is the boundary `r5` drew and this revision preserves. A fixture,
`test_preflight_does_not_adjudicate_the_submission`, pins the preflight to
proceeding on a submission with no receipt marker, so a later revision that
deepens this check has to delete a test that says why not to.

**Evidence that it works.** Run against the two real `r5` exports, the preflight
exits `4`, reports all four codes on Context A, and reports Context B clean. The
epoch it would have preserved is the one that was spent.

## Decision 3 — the class is bound like every other enumeration

`r5` made documents components of the instrument. The four defect codes and the
class name are declared in
`operon-protocol-v099r6/DOCUMENT-CONSISTENCY-BINDINGS.json` as two new bindings,
each compared across three sources: the preflight's own constants read with
`ast`, a JSON pointer into the tool policy, and the handoff prose the auditor
reads. Twenty bindings become twenty-two.

The aggregate `CUSTODY_DEFECT_CODES` is spelled as string literals so the
checker can read it without importing the module, with an import-time guard that
raises if it disagrees with the four named constants it aggregates, and a fixture
over that guard. A literal that silently drifts from its members would be the
`r4` defect reintroduced in the file written to prevent its successor.

## What r6 does not change

The tool registry is unchanged from `r2`. The envelope class model, its four
classes, its mechanical inertness test, and its two envelope-level qualification
codes are unchanged from `r3`. The four adjudication rules and the two
event-level qualification codes are unchanged from `r4`. The reconciled
seven-member field set, the document-consistency machinery, and the repaired
validator failure paths are unchanged from `r5`. The status enum, the claim
boundary and its qualified sentence, the one-attempt rule, the
no-repair-after-failure rule, and the private-custody rules are unchanged.

Both producer paste blocks are byte-identical to `r5`, as are
`CONTEXT-A-PROMPT.md`, `CONTEXT-B-PROMPT.md`, and `ISOLATION-PREFLIGHT.md`;
their projected digests carry forward unchanged. The three producer-facing
schema documents and the review-pair manifest differ only in their revision
string. `TOOL-POLICY.json` additionally carries the custody declaration, which
governs the auditor and constrains no producer. **No instruction a producer
receives changes in this revision.**

One step the *human* performs does change, and it is the step `r5` missed: the
launch document now says, in both session sections, that the session must show
its final `submit_output` and read as completed before anything is downloaded or
exported.

## Two documentation defects corrected, both recorded rather than hidden

`OPERON-QUEUE.md` opened by calling `v0.9.9-r5` unlaunchable on the day `r5`
launched, where the launch-surfaces commit intended `r4`. It contradicted the
same document's status table and its live phase sections, bound no producer, no
constant, and no check, and the consistency checker could not see it. The r6
queue states it plainly and corrects it; the sealed r5 document is untouched.

`TOOL-POLICY.json`'s `vocabulary_policy.revision_history` had three entries
describing the `r3`, `r4`, and `r5` changes, each stamped `v0.9.9-r5` because
every revision's copy step rewrote the revision string in every entry. The r6
history names the revision each entry actually describes and records that the
relabelling happened. This is the same class of defect the whole document-
consistency apparatus exists to catch, surviving in a field no binding covers,
found only by diffing the copy against its source.

## Verification

- `SOURCE-PROJECTION-V099R6.json` has 38 fields. Twenty-one carry forward from
  `r5` unchanged, including both producer prompts, the isolation preflight, the
  manuscript, supplement, text projection, and build context, the last four of
  which also equal their `r1` values. Sixteen differ and all sixteen are
  protocol or toolchain identities. One is new: the export-custody preflight.
- `python3 -I analysis/freeze_source_projection_v099r6.py --check` recomputes
  the projection exactly.
- `python3 -I analysis/check_document_consistency_v099r6.py` reports all
  twenty-two bindings in agreement.
- The `r2`, `r3`, `r4`, and `r5` projections still recompute exactly and still
  bind their own untouched toolchains.
- The suite is 705 tests across 39 modules, all passing. The 549 tests that
  predate this revision are unmodified. The 156 new tests cover the r6
  extractor, gate, raw validator, projection, document-consistency checker,
  raw-conformance preflight, and the new export-custody preflight.
- The eighteen export-custody fixtures cover the three cases the handoff names —
  a `processing`-status export, a completed export with no submission, and a
  completed export with a submission as the control — plus each condition firing
  alone, an empty completion time, a defect in B alone, both exports defective,
  a submission in a descendant frame, six fail-closed paths returning exit `2`,
  the record written only when asked, the exit status staying distinct from the
  blameless class, the literal aggregate matching its members, and the
  shallowness boundary.
- The r6 extractor, raw validator, gate, and the three preflight tools are new
  pinned files, following the precedent set in `r2` through `r5`, so every
  sealed `r1` through `r5` artifact stays byte-identical and independently
  verifiable.
- The two producer attachment sets are staged and byte-verified outside the
  repository at `~/Desktop/operon-v0996-fresh-inputs`, 8 files for A and 10 for
  B, with the asymmetry derived from the tool policy rather than restated.

## What this revision cannot claim

Each of the five preceding revisions closed the gap it met and did not
anticipate the next one. `r1` and `r2` lacked a vocabulary, `r4` lacked a way to
compare its own documents, `r5` lacked a way to see that an input was unusable.
There is no argument available here that `r6` is the one that anticipated
everything, and this record does not make it. What can be said is narrower: the
specific failure that ended `r5` would now cost no attempt, and it would be
caught by a condition that runs in under a second on data the auditor already
has in hand.

## Standing limits

This revision does not review anything. It restores the ability to attempt a
review for the fifth time.

The strongest available process result remains
`conforming_within_supplied_exports`, which is not an independence,
platform-completeness, scholarly-correctness, novelty, or release certificate,
and which may carry narrowing qualifications.

No finding from any prior blind review has been dispositioned. The `r1` through
`r5` exports, producer artifacts, and audit outputs stay in private owner
custody, uningested. A voided epoch disposes of nothing, and neither does a
preserved one.

Whether a sixth producer session pair is opened at all is not this document's to
decide. Licence, stable locator, and activity-data decisions remain solely with
Rashid Azarang and are untouched.
