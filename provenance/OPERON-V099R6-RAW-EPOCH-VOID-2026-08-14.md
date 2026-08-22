# Operon v0.9.9-r6 raw epoch void — second adjudication in six epochs, noncompliant on seven codes

## Classification

The detached trace audit for protocol revision `v0.9.9-r6` passed every
handoff preflight condition — including the two conditions this revision
added after `r5` — assembled the immutable raw tree, and consumed its first
and only full validator attempt. The wrapper completed and adjudicated:
status **`noncompliant`**, seven failure codes.

Under the pinned rule this **voids the raw epoch**. It is not a preflight
stop; the attempt is spent. This is only the second time in six epochs that a
candidate reached adjudication at all (`r3` was the first, with six codes).
`r6`'s two new custody instruments did exactly what they were built to do:
the export-custody preflight confirmed both supplied exports represent
completed sessions with represented submissions before any invocation record
existed, and the adjudication that followed is therefore about producer
conduct, not the instrument, the custody chain, or the protocol's vocabulary.

No retry against this raw tree, no reopened producer session, no modified
export, and no tooling repair is permitted now that a raw failure has been
observed. A further attempt requires a new projected protocol revision
(`r7`), two new producer sessions, two new exports, and a new raw root.

Only digests, byte counts, export metadata, frame identifiers, field names,
stable codes, and path-free derived counts appear below.

## Preflight results

At Epistemics `main@5038e7f2c9242aca928a298e887f33a5d6a8292f`, all conditions
were established before anything ran, in the handoff's order:

1. **Document consistency**: `check_document_consistency_v099r6.py` exit 0 —
   all 22 bindings agree, including the four r6 custody-defect codes.
2. **Export custody preflight**: exit 0 — both supplied exports represent
   completed sessions with a represented submission. (The condition `r5`
   died on. Both root frames report `completed`.)
3. **Raw conformance preflight**: exit 0 on the assembled tree — 20 probes,
   22 bindings consistent.
4. **Source projection**: `SOURCE-PROJECTION-V099R6.json` recomputes exactly,
   all 38 fields (projection sha256 `f5b66a08…`).
5. **Vocabulary closure, both exports**: every represented tool name resolves
   to a declared class (observed in both sessions: `python`, `read_file`,
   `repl`, `save_artifacts`, `submit_output`; `request_network_access` was
   never called by either), and every envelope field at all five levels —
   top, frame, message, content-block, artifact-record — resolves to a
   declared field. Zero unknown tools, zero undeclared fields, zero unparsed
   events. (The conditions `r1` and `r2` died on.)
6. **Fixture suite**: 705 tests across the full `tests/` tree, all passing,
   unchanged.
7. **Raw tree**: assembled from the two human-supplied artifact sets and the
   pinned context-b inputs, made read-only before any validator invocation;
   manifest sha256 `2a813c05…`. No prior r6 raw or certification path
   existed. No earlier-lineage projection digest is reused.

## The attempt

Invocation `a5273671-b861-4cfb-bb14-149e07fafa2e`, attempt index 1,
exclusive-create, extractor sha256 `e935710d…`. Inputs hashed before semantic
parsing: Session A export 1,178,605 bytes, sha256 `0ad9e0a1…`; Session B
export 960,634 bytes, sha256 `b19d3502…`; package-root manifest `ee2745fd…`;
review-pair manifest `765242e1…`.

Scale of the derived audit: 2 exports, 12 frames, 355 messages, 484 content
blocks, 167 tool calls (163 conditionally allowed), 10 descendant frames,
14 direct-output saves, 38 attachment reads (all carrying the expected
`ATTACHMENT_READ_UNRESOLVED` qualification), 25
`GENERIC_PATH_NOT_STATICALLY_RESOLVED` qualifications, 2
`OUT_OF_BAND_CONTENT_POINTER` and 12 `PLATFORM_CONTENT_ANNOTATION`
occurrences.

## Adjudication — seven codes

1. **`CONTEXT_A_REQUEST_LOG_MISMATCH`.** Session A's
   `identifier-verification-log.json` carries **57 request entries**; the
   export represents **zero network requests** and zero
   `request_network_access` calls. Under the strict two-direction
   reconciliation rule, 57 unmatched log entries. The log describes network
   activity the session's own trace does not represent.
2. **`PRODUCER_CLAIM_CONTRADICTION`.** 104 producer claims classified
   `contradicted` against the represented event scan, concentrated in
   Session A's `FILE-OPEN-LOG.json` entries.
3. **`DIRECT_OUTPUT_RECEIPT_MISMATCH`.** 2 receipt mismatches;
   `receipt_match` is **false for Session A** and true for Session B.
4. **`PROHIBITED_TOOL`.** 4 prohibited tool calls under the pinned
   domain-conditional rules.
5. **`CROSS_SESSION_INHERITANCE`.** 1 cross-session inheritance event.
6. **`UNDECLARED_LOCAL_ACCESS`.** 2 undeclared local reads and 1 undeclared
   local write beyond the declared boundary.
7. **`GENERIC_EXECUTION_UNRESOLVED`.** 4 of 104 inspected generic-execution
   calls unresolved under the reconciled profile.

Session B's distinguishing constraints held: zero represented network events
under its prohibition and a matching receipt. The concentration of findings
in Session A's self-describing logs — a verification log describing requests
the trace does not represent, and an open log contradicted by the event
scan — is the substantive result of this epoch: the producer's account of its
own activity and the platform's represented record of that activity are not
the same document, and the pinned rules charge that difference to the
producer.

## Disposition

- The raw tree `operon-v099r6/` and audit directory
  `operon-certification-v099r6/` are preserved read-only as the record.
- The one-shot budget for `v0.9.9-r6` is spent. The epoch is void as a
  certification; the adjudication stands as a finding.
- The manuscript, supplement, and text projection digests carried through
  all six revisions remain unchanged and unjudged by this outcome; nothing
  in this epoch bears on scholarly correctness either way.
- Whether to project an `r7` — and whether the r7 design should treat
  producer self-describing logs (`FILE-OPEN-LOG`,
  `identifier-verification-log`) as adversarial inputs to be reconciled
  event-by-event at generation time rather than audit time — is an author
  decision, not a standing obligation.
