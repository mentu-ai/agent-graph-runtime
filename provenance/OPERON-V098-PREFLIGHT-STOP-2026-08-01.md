# Operon v0.9.8 preflight stop — instrument-insufficient

## Classification

The 1 August 2026 Operon session stopped after checking the frozen candidate
identities and before creating either review context. This is an
`instrument-insufficient preflight stop`, not a failed literature review, blind
review, raw-validator attempt, or consumed review epoch.

The external session reported that it could not honestly satisfy the detached
trace-audit contract. It had no facility to export its own terminal session,
no independent Codex auditor, no authenticated lifecycle/control record, and
no way to prove that memory, reviewer, query, artifact, frame, or derivative
surfaces were disabled. It correctly declined to invent an export digest,
zero-valued trace counts, lifecycle timestamps, or the literal auditor role.

The session's downloadable narrative artifact has not been imported into this
repository. This record is based on the user-supplied return text and a separate
repository-side audit. It therefore does not claim an independently verified
external session digest or complete private trace.

## Repository-side verification

At Epistemics `main@965544e70ecb766add1b13ba8fd170fc734e23f5`:

- `operon-v098/` is absent;
- no v0.9.8 raw return has been ingested;
- all 20 SHA-256 fields in `SOURCE-PROJECTION-V098.json` recompute against the
  authoritative field-to-path mapping in `build.py`;
- the 345,829-byte PDF and 53,666-byte supplement match the queue; and
- the preserved v0.9.7 raw tree remains untouched.

The external return said no full validator was invoked. The repository can
verify raw-root absence, but without the private session export it cannot prove
the external invocation count. The one-shot validator budget is therefore
`reported unconsumed`, not mechanically certified.

The return's phrase “all 19 file-backed fields” is imprecise. The source
projection has 22 fields in total: `schema`, `paper_version`, and 20 SHA-256
fields. All 20 digest fields pass repository-side verification.

## P0 protocol defect

The stop exposed a real separation-of-duty and observability defect:

1. `analysis/validate_operon_raw.py` accepts a detached audit JSON, but not the
   private session export from which that audit is said to derive.
2. `analysis/verify_operon_bundle.py` validates the audit's shape, literal
   auditor label, digest syntax, timestamps, claimed zero counts, and claimed
   validator history. It does not open or hash the export, derive events, or
   authenticate a distinct auditor.
3. The positive protocol test constructs a synthetic audit with the digest of
   bytes that are never materialized as an export and expects acceptance. That
   test proves schema consistency only.
4. The queue asks the external coordinator to terminate and export a complete
   session, have Codex audit it, and then continue inside the same session to
   run the first validator. Those events cannot all occur in that order.
5. A direct context cannot know its actual final `closed_at` before producing
   the one-shot output that causes it to close.
6. Prompt-level requests to disable a platform surface are not evidence that
   the host disabled it.

Consequently the v0.9.8 gate could accept internally consistent but fabricated
trace evidence. No such evidence was created in this attempt.

## Scientific disposition

The evidential requirement is retained but decomposed. Cross-model review
independence, observable trace isolation, artifact consistency, source
verification, finding disposition, and author release authority are distinct
properties. A later protocol must not collapse them into one self-authored
receipt.

The next protocol revision must:

- let Operon produce review artifacts and terminate without authoring its own
  certifying audit or running the certifying validator;
- have the user export the terminal session outside Git;
- have a detached Codex process read and hash the actual export, derive the
  observable frame/tool/artifact facts, and state unobservable controls as
  `unknown` rather than zero;
- bind the deterministic audit implementation and exact export digest;
- run the first full validator only after the detached audit exists; and
- retain author-controlled source/finding dispositions and publication
  clearance as separate gates.

Until that protocol is implemented and exercised, `v0.9.8-internal` remains a
valid internal manuscript but its review-certification path is not executable.
