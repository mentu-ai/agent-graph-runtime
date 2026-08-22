# Operon protocol revision v0.9.9-r2 — declared network-access-request class

## What this document records

Revision `v0.9.9-r2` corrects the defect that stopped the `v0.9.9-r1` detached
preflight, recorded in `OPERON-V099-PREFLIGHT-STOP-2026-08-11.md`. It changes
the review protocol only. No review has been run under it, no producer session
has been opened, and no validator attempt has been made or consumed.

The reviewed manuscript, reproducibility supplement, and deterministic text
projection are the same bytes with the same digests that `r1` reviewed:
`d371922d…` (346,730 bytes), `8edd1803…` (55,375 bytes), and `fa49b71e…`
(127,579 bytes). A protocol revision may not silently re-cut the artefacts under
review, and the r2 projection freezer refuses to run if any of the three moved.

## The defect

`r1` pinned a ten-name tool registry in both `TOOL-POLICY.json` and the
extractor's `EXPECTED_TOOLS`. The Context A profile simultaneously granted
HTTPS access to a fourteen-host allowlist and required bidirectional
reconciliation against the identifier log, while declaring no tool through
which a host performs a network request. The extractor recognized network
activity only as URLs inspected inside `generic_execution` code.

A producer following the Context A instructions as written, on a host that
mediates network access through a request tool, therefore necessarily emits an
event the frozen vocabulary cannot name. The protocol authorized an activity
while lacking a term for the mechanism that performs it.

## The correction

1. **Declared class.** `request_network_access` is declared as the
   `network_access_request` class. It is adjudicated on its declared kind and
   is never reported as an unknown tool.

2. **Honest vocabulary statement.** The policy now states explicitly that the
   registry is closed for adjudication but is *not* a claim that the producing
   platform exposes only those names. The platform's vocabulary is not fixed by
   this protocol and may change between sessions. A name outside the registry
   remains `UNKNOWN_TOOL` and fails closed, but the policy now records what that
   means: a coverage gap in the protocol revision, not a demonstrated producer
   violation. It is resolved only by a new projected revision that declares the
   name, never by editing the policy after an attempt has seen the event.

3. **Domain semantics.** Context A conditionally allows the class, subject to
   the pinned host set and bidirectional reconciliation against
   `identifier-verification-log.json`. Context B prohibits it by name in a new
   per-domain `prohibited_kinds` list rather than by omission, and a represented
   Context B call is `CONTEXT_B_NETWORK_VIOLATION` whether or not a URL resolves
   from its input and whether or not the platform granted the request.

4. **Locator-independent reconciliation.** This protocol does not fix and cannot
   verify the platform's request-tool input schema. Binding reconciliation to
   named fields would fail silently whenever the platform renamed or nested
   them. The extractor therefore scans every string value of the complete
   canonical tool input for HTTPS URL tokens. The declared locator fields
   document the expected shape and never narrow the scan. Over-detection is
   deliberate: a URL mentioned anywhere in a request event must reconcile with
   the log, which can only tighten adjudication.

5. **Unresolved requests are indeterminate.** A request whose complete
   represented input yields no resolvable URL is
   `NETWORK_ACCESS_REQUEST_UNRESOLVED`. Absence of a visible URL is not evidence
   that no request occurred, so the result is indeterminate rather than
   compliant. This is a distinct code from `UNKNOWN_TOOL` and from
   `GENERIC_EXECUTION_UNRESOLVED`.

## Why the r2 toolchain is separate files

The r2 extractor, raw validator, and gate are new pinned files
(`extract_operon_trace_v099r2.py`, `validate_operon_raw_v099r2.py`,
`verify_operon_v099r2.py`) rather than in-place edits.

Editing the r1 tools in place was attempted and reverted. Those three files are
members of the evidence manifest's `analysis_tools` inventory, so changing them
invalidates `results/evidence-manifest.json`, which is itself a byte-comparable
output recorded in `results/reproduction-baseline.json` and the reproduction
receipt. Restoring that chain by hand would have asserted a reproduction result
that was not reproduced, to accommodate a change that has nothing to do with the
scientific evidence pipeline. Versioned tooling avoids the coupling entirely and
follows the existing pattern by which `verify_operon_bundle.py` (v0.9.8) and
`verify_operon_v099.py` (v0.9.9) coexist.

The consequence is that the whole `r1` record stays byte-identical and
independently verifiable: `SOURCE-PROJECTION-V099.json` still recomputes against
its own untouched toolchain, and a guard test asserts it.

## Incidental hardening

The r2 gate's path-neutrality scan previously raised an unhandled `ValueError`
from `urlparse` on any string with a bracketed authority. The pinned URL-token
pattern is itself such a string. An unparseable string is not a URL, so the r2
gate now treats it as ordinary text instead of crashing.

## Verification

- `SOURCE-PROJECTION-V099R2.json` has 34 fields. Sixteen differ from r1 and all
  sixteen are protocol or toolchain identities; eighteen are carried forward,
  including the manuscript, supplement, text projection, and build context.
- `python3 -I analysis/freeze_source_projection_v099r2.py --check` recomputes
  the projection exactly.
- `OPERON-QUEUE.md` binds both the active r2 projection rows and the sealed r1
  rows, so the sealed lineage stays legible and the builder's queue gate holds.
- The test suite is 221 tests across 18 modules, all passing. The 44 r1 protocol
  tests are unmodified. The 57 new tests cover the r2 extractor, gate, raw
  validator, and projection.
- Required r2 fixtures: a Context A request that is logged and allowlisted and
  reconciles; one that is unlogged; one to a host outside the pinned set; and a
  Context B request, including a Context B request carrying no URL at all. The
  suite also pins the unresolved-input case, reconciliation of a URL appearing
  outside the declared locator fields, and that the declared class is never
  reported as unknown.

## Standing limits

This revision does not review anything. It restores the ability to attempt a
review. The strongest available process result remains
`conforming_within_supplied_exports`, which is not an independence,
platform-completeness, scholarly-correctness, novelty, or release certificate.

Whether the `r1` Context A network behaviour actually conformed remains
undetermined and is not settled by this revision. The `r1` exports and producer
artifacts stay in private owner custody, uningested.

Licence, stable locator, and activity-data decisions remain solely with Rashid
Azarang and are untouched.
