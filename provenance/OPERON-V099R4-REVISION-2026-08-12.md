# Operon protocol revision v0.9.9-r4 — adjudicating the first real attempt

## What this document records

Revision `v0.9.9-r4` corrects the rules that produced the `noncompliant` result
recorded in `OPERON-V099R3-RAW-EPOCH-VOID-2026-08-12.md`. It changes the review
protocol only. No review has been run under it, no producer session has been
opened, and no validator attempt has been made or consumed.

The reviewed manuscript, reproducibility supplement, and deterministic text
projection are the same bytes with the same digests that `r1`, `r2`, and `r3`
reviewed: `d371922d…` (346,730 bytes), `8edd1803…` (55,375 bytes), and
`fa49b71e…` (127,579 bytes). The r4 projection freezer refuses to run if any of
the three moved.

## Why this revision is different from the last two

`r2` and `r3` each corrected a preflight stop: a frozen vocabulary that had no
term for something the platform emitted. `r3` closed that class of defect
completely — every tool name and every envelope field in both exports resolved,
and both exports parsed — and became the first revision in the program's history
to reach adjudication.

It then failed adjudication, with six codes. That is a different kind of
information, and it is worth more than either preflight stop, because it is the
first time the protocol has been tested against real producer behaviour rather
than against its own vocabulary.

Examining the six codes showed that three of them fired on behaviour the pinned
producer prompts never forbade, and one of those was on a rule no producer on
this platform could have satisfied. A rule that cannot be obeyed does not
measure compliance; it measures nothing.

## The four decisions, with their registered-text basis

### 1. The receipt contract was unsatisfiable

**Registered text.** Both `r3` prompts say the final `submit_output.findings`
list "must **contain** the exact receipt-digest marker". The receipt schema
added that it "must contain exactly one string element" of the marker form.

**What the platform does.** The `findings` argument is a list of structured
objects with keys `claim`, `evidence`, `msg_idx`, `verdict`, and sometimes
`severity` and `artifact_version_id`. It is a verification-findings channel, not
a free-text list. Every `submit_output` event in both `r3` sessions occurred in a
descendant frame; neither root frame called it at all.

**What the r3 rule required.** A `findings` list of length exactly one, whose
single element was a bare string fully matching the marker pattern, in the root
frame. Three of those four conditions are outside producer control on this
platform.

**What the producers did.** Context B placed the marker inside a findings
object's `evidence` field — a good-faith reading of "contain" against the
container the platform actually provides — and was recorded as a receipt
mismatch. Context A emitted the marker token in message text and in code but not
inside a findings element.

**Decision.** The instruction stands as written; the rule is corrected to match
it. `r4` scans every represented string value at any depth of the `findings`
container, matching the marker as a token rather than as the whole string, in
any frame of that session's own reachable tree. This is the same
field-name-independent discipline the network-request scan already used, adopted
for the same reason: the protocol does not fix the platform's container shape
and must not depend on it.

**Non-forgeability.** Widening where the marker may appear does not weaken what
it binds. Exactly one distinct digest may appear across a session; it must equal
the SHA-256 of that context's own downloaded receipt bytes; the receipt carries
`context_role` and `context_id`; and a marker digest matching the other
context's receipt is `CROSS_SESSION_INHERITANCE`, not a receipt.

**Post-receipt.** The prohibition is narrowed to what it was always for: direct
output writes, versioning, re-emission, and further receipt submissions after
the receipt event. Other events are permitted and counted as
`post_receipt_non_write_events`. This matters concretely — the `r3` Context B
producer filed an erratum against one of its own findings after submission,
having correctly declined to edit its sealed outputs. Recording that as a
violation would punish exactly the behaviour this corpus wants.

### 2a. Reads are addressed by an identifier the export cannot resolve

**Registered text.** `read_file` declares `file_path` and `version_id` as
locator fields. Neither prompt asks a producer to read by path.

**What the platform does.** Every `read_file` event in both `r3` exports carried
`version_id` and none carried `file_path`. A version identifier for a
session-produced artifact resolves in the export's own artifact registry. A
version identifier for a human-attached input does not and cannot, because that
registry holds what the session produced, not what was attached.

**Result under r3.** 26 undeclared local reads, of which 25 resolved to no path
at all. Exactly one read — of a self-produced artifact — resolved. The audit
reported a limit of the protocol's reach as a producer boundary violation.

**Decision.** Three-way resolution. A registry-resolvable `version_id` is a
declared read. An unresolvable one is an `attachment_read` raising the named
qualification `ATTACHMENT_READ_UNRESOLVED`, which records the identifier by
digest and narrows the completeness claim for that event without failing. A
resolvable path outside the domain sets, a read carrying both a path and a
version identifier, and any filesystem-discovery event all still fail closed as
before.

This is honest about what was lost. The protocol can no longer prove from the
export alone that Context B read only its three declared inputs. It could not
prove that under `r3` either — it simply reported the gap as a violation instead
of naming it.

### 2b. The network-request locator field

`request_network_access` inputs carried `domain`, which the `r3` locator list
did not declare. The field-name-independent URL scan recovered the URLs anyway,
exactly as the contract intends, so this never failed. `domain` is now declared
so the documented shape matches the observed one.

### 2c. The generic-execution profile was stricter than its prompts

The prompts forbid "shell execution, subprocesses, dynamic evaluation,
environment inspection, filesystem discovery, or undeclared hosts". Audited
against what actually fired:

| r3 rule finding | Count | Registered basis | Disposition |
| --- | ---: | --- | --- |
| `forbidden_capability_call` | 4 | `os.path.getsize` ×5, used to obtain the positive `bytes` value the receipt schema requires in every `files` entry | rule corrected: `os` capability members forbidden by name, `os.path` and `os.stat` permitted |
| `unsupported_or_forbidden_import` | 5 | `uuid` (the log schema requires a unique id per attempt), `xml.etree.ElementTree` (registry responses), `pypdfium2` (A's only reviewed input is a PDF) | rule corrected: added to the allowlist, `pypdfium2` scoped to Context A only |
| `dunder_access` | 1 | `__name__`, in the standard `if __name__ == "__main__"` idiom | rule corrected: only capability-bearing dunders are reflective access |
| `dynamic_local_path` | 17 | no registered instruction requires output filenames to be literals | qualification `GENERIC_PATH_NOT_STATICALLY_RESOLVED`, not indeterminate |

`subprocess`, `socket`, `ctypes`, `importlib`, filesystem discovery, dynamic
evaluation, and a dynamic *network* target remain forbidden or indeterminate as
before — the network policy turns on which host was contacted, so an unresolved
target still forces indeterminate. Every rule that was kept is now named
explicitly in both producer prompts, including the reflective-attribute
prohibition, which `r3` enforced without ever stating.

### 2d. Producers were asked to certify what they cannot observe

Both `r3` attestations claimed zero descendant frames while their exports
represented three each; both claimed local-read counts that did not match
represented events. The platform decides whether a task runs in descendant
frames — the exports show `OPERON` and `REVIEWER` agents — and a producer cannot
observe its own frame topology or its descendants' reads.

**Decision.** `claimed_local_read_count`, `claimed_external_request_count`,
`claimed_descendant_frame_count`, and `all_reachable_descendants_covered` are
removed. `descendant_claims.claimed_count` and `all_reachable_claimed` must be
exactly `unknown`, and `session_frame_topology` joins the unobserved-control
set. What replaces them is `declared_read_targets`: the logical basenames the
producer believes it opened, reconciled by membership in its declared input set
rather than by count equality. Topology and event counts come from the export
and from nowhere else.

Asking an agent to certify a fact it has no way to know manufactures
contradictions and teaches nothing.

### 3. The Context A verification log stays strict, and stops being ambiguous

This is the one finding that was producer behaviour, and the reconciliation rule
does not move.

The `r3` log declared 122 entries against 4 represented network requests, and
118 were unmatched. That is exactly what the apparatus exists to catch, and
`r4` keeps the bidirectional strict rule and its `CONTEXT_A_REQUEST_LOG_MISMATCH`
code unchanged.

The honest part of the record is that the registered text invited it. The `r3`
prompt asked for "a replayable attempt list covering every represented network
request **as well as every registry work**", and then required bidirectional
matching against represented calls. Those two clauses describe different
populations and cannot both hold when works outnumber requests. A producer
filing one entry per work was following the second clause.

**Decision.** The log becomes v4 with two disjoint sections. `requests` means
represented network verification events and nothing else, and is reconciled
strictly in both directions. `works` records per-work registry coverage, carries
no request identity, makes no network claim, and is never reconciled. A `works`
entry carrying a `request_id` is rejected. The Context A prompt now states the
semantics in one sentence and says plainly that conflating the sections is the
most consequential error available in that file.

The strictness is preserved. The ambiguity that produced the finding is not.

## What r4 does not change

The tool registry is unchanged from `r2`. The envelope class model, its four
classes, its mechanical inertness test, and its two envelope-level qualification
codes are unchanged from `r3`. The status enum is unchanged. The claim boundary
and its qualified sentence are unchanged. The one-attempt rule, the
no-repair-after-failure rule, and the private-custody rules are unchanged.

## Verification

- `SOURCE-PROJECTION-V099R4.json` has 34 fields. Eighteen carry forward from
  `r3` unchanged, including the manuscript, supplement, text projection, and
  build context, all four of which also equal their `r1` values. Sixteen differ
  and all sixteen are protocol or toolchain identities: both context prompts,
  the isolation preflight, the tool policy, the r4 extractor, raw validator, and
  gate, the review-pair manifest, the trace-audit contract, five protocol
  schema documents, and the revision string.
- `python3 -I analysis/freeze_source_projection_v099r4.py --check` recomputes
  the projection exactly.
- The `r2` and `r3` projections still recompute exactly and still bind their own
  untouched toolchains.
- The suite is 411 tests across 26 modules, all passing. The 308 tests that
  predate this revision are unmodified. The 103 new tests cover the r4
  extractor, gate, raw validator, and projection.
- Required r4 fixtures: the receipt marker in a root frame, in a descendant
  frame, inside a structured finding alongside substantive findings, and absent;
  two distinct digests in one session, a digest not matching the saved receipt
  bytes, and a Context B marker carrying Context A's digest; a post-receipt
  direct-output write that fails and a post-receipt erratum that does not; read
  resolution in three directions; `os.path.getsize` and the `uuid`/`xml.etree`
  imports accepted while `os.environ`, `os.listdir`, and `__globals__` are
  rejected; `__name__` accepted; a dynamic local path qualifying while a dynamic
  network target still forces indeterminate; and the identifier log reconciling
  over `requests` only, with a `works` entry never satisfying a represented
  request and a `works` entry carrying a request identity rejected.
- The r4 extractor, raw validator, and gate are new pinned files, following the
  precedent set in `r2` and `r3`, so every sealed `r1`, `r2`, and `r3` artifact
  stays byte-identical and independently verifiable.
- The two producer attachment sets are staged and byte-verified outside the
  repository, 8 files for A and 10 for B, with the deliberate asymmetry derived
  from the tool policy rather than restated.

## Standing limits

This revision does not review anything. It restores the ability to attempt a
review, for the third time, and it is the first restoration based on evidence
about producer behaviour rather than about the protocol's own vocabulary.

The strongest available process result remains
`conforming_within_supplied_exports`, which is not an independence,
platform-completeness, scholarly-correctness, novelty, or release certificate,
and which may carry narrowing qualifications.

Whether the `r3` Context A network behaviour actually conformed remains
undetermined and is not settled by this revision. The `r1`, `r2`, and `r3`
exports, producer artifacts, and audit outputs stay in private owner custody,
uningested. No finding from the `r3` blind review has been dispositioned; a
voided epoch disposes of nothing.

Licence, stable locator, and activity-data decisions remain solely with Rashid
Azarang and are untouched.
