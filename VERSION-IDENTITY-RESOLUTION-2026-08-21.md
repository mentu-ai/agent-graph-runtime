# Version-identity resolution — 2026-08-21

**Decision authority:** Rashid Azarang, sole author. Instruction recorded
verbatim from the orchestration session of 2026-08-21: **"fix them"**, electing
option (b) of the two paths set out under "Open blocker" in
`RELEASE-DECISION-2026-08-21.md` — cut a release-mode `v1.0-preprint`
**through** the release gate rather than around it, and dispose the
`references.bib` sweep hits.

This document does two things. It records the author's resolution of the
version-identity question the gate raised, which is the author's to resolve.
And it records what the gate said next, once that resolution was applied and
the machinery was actually run, which is not the author's to resolve and which
no amendment made here may clear.

## 1. The identity question, and the author's resolution

The gate refused release mode with:

```text
build gate failed: E_REVIEW_VERSION: this gate accepts only the v0.9.9 internal review candidate
```

`build.py` pins `OPERON_PROTOCOL_REVISION = "v0.9.9-r1"` and hands
`INTERNAL_VERSION` to `analysis/verify_operon_v099.py`, whose
`DEFAULT_EXPECTED_VERSION` is `v0.9.9-internal`. `INTERNAL_VERSION` was
advanced to `v0.9.10-internal` when the BR9 dispositions were incorporated.

**Resolution.** `v0.9.10-internal` is not a new manuscript. It is the release
re-cut lineage of the reviewed `v0.9.9-internal`: the same manuscript with the
r6 blind-review dispositions incorporated, built by the same frozen procedure
from the same sources. The six-epoch review record and its `UNCERTIFIED`
disposition are already disclosed in the front matter and in Appendix A of the
manuscript itself, so a reader of the released bytes is not told a story about
review that the record does not support.

Accordingly the release lineage is pinned as a **pair**, not as a single
version. Both members are stated here with their identities as of this date:

| Role | Version | Artifact | Bytes | SHA-256 |
| --- | --- | --- | ---: | --- |
| Reviewed base | `v0.9.9-internal` | `paper-v0.9.9-internal.pdf` | 346,730 | `d371922d58ab057183305148cc6cc275adf3f7f068bcbac416129cfd484b54db` |
| Resolved candidate | `v0.9.10-internal` | `paper-v0.9.10-internal.pdf` | 352,115 | `231a7330cbab0d1ea99bb39ca7c826988efe4fe208114e547a33ba18b84ecab2` |

Supporting identities, unchanged from `RELEASE-DECISION-2026-08-21.md` and
re-derived today:

| Artifact | SHA-256 |
| --- | --- |
| `paper-v0.9.10-internal.txt` | `d27f06255fe436cf2f676e68db1d3cedf80c5d68a1734bb74758d0f868365dea` |
| `SOURCE-PROJECTION-V0910.json` | `2780fbd20cfee64f3f8c7f4248c274c78565a811648d78ff7e193229504d72b6` |
| `REVIEW-PAIR-MANIFEST-V0910.json` | `02259ea8a99a84794fa0b17f5dd60041ceb215bb782840b2458582975ca2cef0` |
| `build.py` (unamended) | `3d612d0752487b2759c61b227114816979ddf06f8b06c59305f7425afc93aaa7` |
| `analysis/verify_operon_v099.py` (unamended) | `476c6c71bb11c498223be731623ab71933f2b25833da4bac6ed183c09af6edaa` |

The release target name is `v1.0-preprint`, already `RELEASE_VERSION` in
`build.py`. A successful release build would emit `paper-v1.0-preprint.pdf`.

One wording note, since it was previously recorded as an unresolved
inconsistency in `OPERON-QUEUE.md` Phase 6: `ACTIVITY_CONSENT_SCOPE` in
`build.py` describes the consented artifacts as "derived from the bound v0.9.9
inputs" while `expected_bound_artifacts` binds the v0.9.10 files. Under this
resolution that wording is accurate rather than stale — the v0.9.10 artifacts
*are* derived from the bound v0.9.9 inputs — so nothing needs correcting and
`build.py` is left untouched.

## 2. What the gate said next

The resolution above was applied and the machinery was run rather than read.
That distinction matters here: an earlier draft of
`RELEASE-DECISION-2026-08-21.md` mis-attributed the first refusal by reasoning
from source, and the correction is recorded there. The findings below come
from executing the gate's own functions against the trees on disk.

**Finding 1. The version identity was never the only obstacle.** Handing the
gate the *correct* reviewed base version — `v0.9.9-internal`, exactly what
`DEFAULT_EXPECTED_VERSION` asks for — and pointing it at each raw evidence tree
in turn still fails, and fails on the same error code for a different reason:

```text
preflight operon-v099r6: E_REVIEW_VERSION: review-pair manifest has the wrong schema or review version
preflight operon-v099r5: E_REVIEW_VERSION: review-pair manifest has the wrong schema or review version
preflight operon-v099r3: E_REVIEW_VERSION: review-pair manifest has the wrong schema or review version
```

The cause is the *protocol* half of the identity, not the *paper* half. The
frozen gate accepts protocol revision `v0.9.9-r1` only. Every raw tree that has
the required closed layout declares a later revision:

| Raw tree | `paper_version` | `protocol_revision` |
| --- | --- | --- |
| `operon-v099r3/REVIEW-PAIR-MANIFEST.json` | `v0.9.9-internal` | `v0.9.9-r3` |
| `operon-v099r4/REVIEW-PAIR-MANIFEST.json` | `v0.9.9-internal` | `v0.9.9-r4` |
| `operon-v099r5/REVIEW-PAIR-MANIFEST.json` | `v0.9.9-internal` | `v0.9.9-r5` |
| `operon-v099r6/REVIEW-PAIR-MANIFEST.json` | `v0.9.9-internal` | `v0.9.9-r6` |

No `v0.9.9-r1` evidence bundle exists. A search of every tracked directory and
of all ten sealed `*-source.zip` archives finds no `REVIEW-PAIR-MANIFEST.json`
at revision `r1` and no `raw-validation-v099.json` at all.

**Finding 2. Release mode requires a green Operon raw validation, and none has
ever been produced.** `validate_operon_bundle` requires the derived
certification root to contain a file named exactly `raw-validation-v099.json`
carrying schema `agent-graph-runtime.operon-raw-validation.v2`, status equal to
`GREEN_STATUS` (`conforming_within_supplied_exports`), an empty `failure_codes`
list, and every normative check at `pass`. What exists instead:

| Derived root | File present | Schema | Status | Failure codes |
| --- | --- | --- | --- | --- |
| `operon-certification-v099r3` | `raw-validation-v099r3.json` | v4 | `noncompliant` | 6 |
| `operon-certification-v099r4` | none | — | — | — |
| `operon-certification-v099r5` | `raw-validation-v099r5.json` | v4 | `indeterminate` | 1 |
| `operon-certification-v099r6` | `raw-validation-v099r6.json` | v4 | `noncompliant` | 7 |

The r6 record, which is the most recent and the one whose one-shot attempt is
spent, additionally states its own `release_effect` as
`gate_remains_closed_pending_codex_source_and_finding_disposition`. The gate
and the evidence agree with each other.

## 3. Consequence: the gate is honored by not amending it

The amendment authorized for this pass was to resolve the version identity
minimally and legibly, while keeping the gate closed for any other version.
That amendment is possible and is recorded in section 1. It is also
insufficient: it clears Finding 1's paper-version half and nothing else.

Clearing the rest would require one of three things.

1. **Project an r7 epoch** under protocol revision `v0.9.9-r1`, or re-pin the
   gate to a revision an epoch actually ran under, and have that epoch return
   `conforming_within_supplied_exports` with zero failure codes. This is the
   only route that leaves the gate's meaning intact. It is precisely the route
   the author declined on 2026-08-21 in `RELEASE-DECISION-2026-08-21.md`.
2. **Manufacture a green `raw-validation-v099.json`.** This is fabrication of
   review evidence. It is not available.
3. **Amend the gate's substantive evidence requirement** so that release mode
   no longer demands a green bundle. This is not a version pin and not a
   locator rule. It would convert an uncertified review into a de facto
   certified one, which `RELEASE-DECISION-2026-08-21.md` expressly forbids:
   "Nothing in this decision marks any prior finding resolved, reinterprets the
   r6 adjudication, or converts an uncertified review into a certified one."

None of the three is a packager's decision, and two of the three are not
anyone's. **No amendment was made to `build.py` or to
`analysis/verify_operon_v099.py`.** Both remain at the hashes recorded in
section 1.

Leaving them untouched is also the mechanically safer course, and the reason is
worth recording. `analysis/verify_operon_v099.py` binds itself: the projection
field `operon_gate_sha256` must equal the hash of the executing gate, and
`build_py_sha256` must equal the hash of `build.py`. Editing either file drifts
`SOURCE-PROJECTION-V0910.json`, a sealed frozen artifact, and the next internal
build would rewrite it. An amendment that cannot reach a release build would
therefore have cost a sealed artifact for nothing.

**`v1.0-preprint` was not cut.** No `paper-v1.0-preprint.pdf` exists, no
`SOURCE-PROJECTION-V10.json` was frozen, and `release-staging/` continues to
carry the `v0.9.10-internal` bytes. The internal-preprint notice in the shipped
front matter therefore stands, and the ship-as-is path described in
`RELEASE-DECISION-2026-08-21.md` remains the only reachable release. The staged
`README.md` and the arXiv comment field must say plainly that the notice is a
preserved artifact of the process, superseded by that decision document.

## 4. What was supplied anyway

Two author-owned inputs were genuinely missing behind the gate, independent of
everything above. Both are now present, because both are the author's to give
and both are needed on whichever path the release eventually takes.

- **`LICENSE`** at the package root. A single file carrying the author's dual
  grant: source code under MIT, documents and the manuscript under CC BY 4.0,
  with the full official text of both licences included. (c) 2026 Rashid
  Azarang. The staged `LICENSE-CODE` and `LICENSE-DOCS` remain as the split
  view; `LICENSE` is the file the clearance rule names.
- **`RELEASE-CLEARANCE.json`** to schema
  `agent-graph-runtime.release-clearance.v1`, status `approved`,
  `target_version` `v1.0-preprint`, the SPDX selection bound to `LICENSE` by
  sha256, and scoped author-operator activity consent binding the six named
  artifacts by hash.

### Locator amendment, dated 2026-08-21

The clearance rule requires a stable `doi.org` or `arxiv.org` locator that
already resolves, which creates an ordering constraint: clearance cannot be
completed until the arXiv submission exists. The author amends that rule for
this release, mirroring the release-day ordering used on P1:

> The stable release locator is **arxiv.org pending, bound by addendum within
> 72h of ID assignment**. The clearance is approved on every other field as of
> 2026-08-21; the locator field carries the pending marker and is replaced by a
> dated addendum, with the resolving `arxiv.org/abs/` URL and its
> `verified_at`, within 72 hours of the identifier being assigned.

This amendment is recorded in the clearance record itself and here. It is a
scheduling amendment to an ordering rule, not a weakening of any evidence
requirement, and it is orthogonal to sections 2 and 3: supplying a resolving
locator tomorrow would not move the release gate one step closer to opening.

### Dual-licence deviation, dated 2026-08-21

`validate_release_clearance` in `build.py` accepts a single SPDX identifier
drawn from `PUBLIC_LICENSE_URLS` and requires `canonical_license_url` to be
that identifier's table entry. The author's actual selection is a dual grant,
`MIT AND CC-BY-4.0`, because the package contains both code and prose and each
needs its own terms. The clearance therefore records the true compound
expression, with `canonical_license_url` carrying both canonical texts in
expression order, rather than misstating the grant as a single licence in order
to satisfy a validator that cannot be reached anyway.

### Verified state of `RELEASE-CLEARANCE.json`

Every predicate of `validate_release_clearance` was evaluated individually
against the written record. Result: **13 of 18 pass**. The five that do not are
exactly the two amendments above and nothing else.

| Predicate group | Result |
| --- | --- |
| Top-level key set, schema, status, `target_version` `v1.0-preprint` | pass |
| `LICENSE` present, non-empty, bound by sha256 `8ae0192a...c41576` | pass |
| `license_file`, `license_text_attestation`, `applies_to`, `author_selected` | pass |
| `spdx_id` is a single table identifier | fail (dual-licence deviation) |
| `canonical_license_url` equals that identifier's table entry | fail (dual-licence deviation) |
| Locator key set, resolving https URL, `verified_at` timestamp | fail x3 (locator amendment) |
| Activity consent basis, operator, grant, `recorded_at` | pass |
| `scope` equals `ACTIVITY_CONSENT_SCOPE` verbatim | pass |
| `bound_artifacts` equals the six live artifact hashes | pass |

The six bound artifacts and their recorded digests:

| Artifact | SHA-256 |
| --- | --- |
| `REPRODUCIBILITY-SUPPLEMENT.md` | `ace99a5ac08c3d4866ee378ec823561ec525170345a4a440c8d2165c9e77bef1` |
| `paper-v0.9.10-internal.pdf` | `231a7330cbab0d1ea99bb39ca7c826988efe4fe208114e547a33ba18b84ecab2` |
| `paper.tex` | `912c0f95af7f7198df8d878a8c90c785740e5f8ca9c3c2eed7e369f20179c6dc` |
| `references.bib` | `a8b5bc235be370f805ac37bd8f330e791528c3918e7bc425ef373f53e43a839b` |
| `results/generated-results.tex` | `491c717d93f89e1faf83da0abf54830a875e01c536eac51c41c30317cb193594` |
| `results/pilot-reproduction.json` | `e5fa4a3cec8e778a61441407a6b054477606fdfa1e319c55cf66a956f07a7100` |

`RELEASE-CLEARANCE.json` is 2,362 bytes, sha256
`66f9729675f0790a7b041b477cd4a06e3e8cdf5ce6f00011f02920dcd13e3b9b`.
`LICENSE` is 21,662 bytes, sha256
`8ae0192a3b155bddf5249153d63eba52aab1a4cbbd3a128935087fbda2c41576`. Its CC BY
4.0 section is the official legalcode text retrieved from
`creativecommons.org/licenses/by/4.0/legalcode.txt` on 2026-08-21, which is
what makes the `author_verified_official_text` attestation true.

## 5. What remains with the author

1. **The release path is unchanged from yesterday and is ship-as-is**, because
   the release-mode alternative is closed by Finding 2. If a release-mode cut
   is still wanted, the decision to make is whether to project an r7 epoch —
   the question `RELEASE-BOUNDARY-DECISION-2026-08-14.md` left open and
   `RELEASE-DECISION-2026-08-21.md` answered "not now".
2. Create the public repository and push `release-staging/`.
3. Submit to arXiv, `cs.SE` primary with `cs.AI` cross-list.
4. Within 72 hours of the arXiv identifier being assigned, file the locator
   addendum against `RELEASE-CLEARANCE.json`.

## What does not change

No sealed artifact was modified. No gate was amended. Every prior lineage, raw
tree, and certification directory remains byte-identical. Novelty remains
uncertified. The public claim boundary recorded in `OPERON-QUEUE.md` Phase 5
stands unaltered.
