# Release decision — 2026-08-21: the release act, not an r7 epoch

**Decision authority:** Rashid Azarang, sole author. Instruction recorded
verbatim from the orchestration session of 2026-08-21: **"hagamos 1... get it
to release ready"**, where option 1 had been stated as the release act — the
same playbook as P1 (clean subtree repository under `mentu-ai`, arXiv the same
day) — as against option 2, projecting a seventh certification epoch.

This document records the decision and the candidate binding. It does not
itself constitute the outward release act, which remains the author's.

## What was decided

1. **No `r7` review epoch is projected.** The question left open by
   `provenance/RELEASE-BOUNDARY-DECISION-2026-08-14.md` ("Projecting an r7
   remains open as a separate, future author decision") is answered: not now,
   and not as a precondition of this release. The six-epoch record stands as
   the disclosed evidence about the review instrument and the producing
   platform.
2. **`v0.9.10-internal` is the released bytes.** No new candidate is built for
   this release; the bytes verified below are the bytes that ship. See
   "Open blocker" for the one respect in which those bytes describe themselves
   as unreleased.
3. **Provenance narrative is governed by the standing record.** The r6
   `UNCERTIFIED` disposition and the 2026-08-14 boundary decision govern how
   this release describes its own assurance. Nothing in this decision marks any
   prior finding resolved, reinterprets the r6 adjudication, or converts an
   uncertified review into a certified one.

## Candidate binding, verified on disk 2026-08-21

Restated from `OPERON-QUEUE.md` and re-verified byte-for-byte today:

| Artifact | Bytes | SHA-256 | Verified |
| --- | ---: | --- | --- |
| `paper-v0.9.10-internal.pdf` | 352,115 | `231a7330cbab0d1ea99bb39ca7c826988efe4fe208114e547a33ba18b84ecab2` | match |
| `paper-v0.9.10-internal.txt` | 132,307 | `d27f06255fe436cf2f676e68db1d3cedf80c5d68a1734bb74758d0f868365dea` | match |
| `REPRODUCIBILITY-SUPPLEMENT.md` | 59,558 | `ace99a5ac08c3d4866ee378ec823561ec525170345a4a440c8d2165c9e77bef1` | match |
| `SOURCE-PROJECTION-V0910.json` | 3,218 | `2780fbd20cfee64f3f8c7f4248c274c78565a811648d78ff7e193229504d72b6` | present |
| `REVIEW-PAIR-MANIFEST-V0910.json` | 952 | `02259ea8a99a84794fa0b17f5dd60041ceb215bb782840b2458582975ca2cef0` | match |

The manifest hash `02259ea8...` matches the `review_pair_manifest_sha256` field
recorded inside `SOURCE-PROJECTION-V0910.json`, and `paper.tex` on disk hashes
to `912c0f95af7f7198df8d878a8c90c785740e5f8ca9c3c2eed7e369f20179c6dc`, matching
that projection's `paper_tex_sha256`. The projection cannot record its own
hash, so `2780fbd2...` is stated here as the identity of the file as shipped.

## Independent rebuild, 2026-08-21

The released PDF was rebuilt from the frozen source and is **byte-identical**.

Inputs, taken from `agent-graph-runtime-v0.9.10-internal-source.zip`:
`paper.tex` (`912c0f95...`), `build-context.tex` (`6f38afff7646a71626b198558ac7821293908b3a221fcf61e4d2888d17c2e8e6`,
matching the projection's `internal_build_context_sha256`), `references.bib`,
and the four figure PDFs.

Command, as `build.py` issues it:

```sh
SOURCE_DATE_EPOCH=1785369600 tectonic -X compile -C --reruns 2 \
  --keep-intermediates --keep-logs --outdir "${outdir}" paper.tex
```

Toolchain: Tectonic 0.16.9 (homebrew). Result: `paper.pdf`, 352,115 bytes,
sha256 `231a7330cbab0d1ea99bb39ca7c826988efe4fe208114e547a33ba18b84ecab2` —
identical to the sealed candidate. 39 pages, 4 figures, 45 bibliography
entries. The build is therefore independently reproducible by a third party
from the released source, which is the property the arXiv source package and
the public repository both rest on.

## Open blocker carried to the author

The released bytes describe themselves as unreleased. The v0.9.10 cover block
and the closing sentence of the abstract state, in the PDF that would ship:

- "Internal preprint. ... not for dissemination."
- "the author's explicit release act ... That act has not occurred"
- "Fresh review of this exact PDF and supplement, plus a detached
  supplied-export audit, remains a release gate."

These strings are emitted by the `\ifdefined\InternalBuild` branches in
`paper.tex`, switched by the `\def\InternalBuild{1}` line that `build.py`
writes into `build-context.tex` under `--mode internal`. `build.py` also
implements a `--mode release` that omits the internal-preprint notice and instead
requires a *release clearance record* supplying a public licence SPDX id and a
stable release locator.

Release mode was executed to find out what it actually refuses. It fails
closed:

```text
build gate failed: E_REVIEW_VERSION: this gate accepts only the v0.9.9 internal review candidate
```

An earlier draft of this document attributed the refusal to
`preflight_operon_bundle(...)`, reasoning from the code rather than running it.
That is wrong, and the correction matters, because the real gate is saying
something substantive rather than something stale. `build.py` pins
`OPERON_PROTOCOL_REVISION = "v0.9.9-r1"`, which routes release mode through
`analysis/verify_operon_v099.py`, whose `DEFAULT_EXPECTED_VERSION` is
`v0.9.9-internal`; release mode hands it `INTERNAL_VERSION`, now advanced to
`v0.9.10-internal`. The gate is therefore making a true and load-bearing claim:
**the bytes proposed for release are not the bytes any epoch reviewed.** `r6`
reviewed `v0.9.9-internal`. `v0.9.10-internal` is a re-cut of it that
incorporated the r6 dispositions and was itself never seen by any reviewer.

Two author-owned inputs are absent behind that gate and would block release
mode even if the version identity were resolved: `RELEASE-CLEARANCE.json` (an
approved clearance record binding an SPDX licence by hash to a `LICENSE` file
and naming a stable `doi.org` or `arxiv.org` locator) and a single `LICENSE`
file at the package root, which the two-file `LICENSE-CODE` plus `LICENSE-DOCS`
arrangement does not satisfy. The clearance rule also imposes an ordering
constraint worth noting: a stable locator must already resolve, so clearance
cannot be completed until the arXiv submission exists.

Any amendment to these gates changes `build_py_sha256` and every downstream
hash, which means a new candidate version and a new frozen projection, not a
re-release of these bytes.

Releasing `v0.9.10-internal` as-is publishes a document whose own front matter
denies it was released. Both paths are defensible and the choice is not the
packager's:

- **Ship as-is.** Consistent with "disclose the record"; the notice reads as a
  preserved artifact of the process. The README and arXiv comments must then
  say plainly that the internal-preprint notice is intentional and superseded by this
  decision document, or every reader will take it at face value.
- **Cut a release-mode version.** Resolve the version identity the gate
  raised, supply `RELEASE-CLEARANCE.json` and a single `LICENSE`, freeze a new
  projection, and release bytes that describe themselves accurately. Note that
  `RELEASE_VERSION` in `build.py` is `v1.0-preprint`, so a successful release
  build emits `paper-v1.0-preprint.pdf` rather than a v0.9.10 artifact. This is
  mechanically cheap now that the build is proven reproducible, but it means a
  new candidate, a new hash set, and a locator that must exist first.

Staging under `release-staging/` is complete for the ship-as-is path. Nothing
in it presumes the answer.

## What does not change

- No sealed artifact is modified. Every prior lineage, raw tree, and
  certification directory remains byte-identical.
- Novelty remains uncertified. No epoch ever judged the manuscript.
- The public claim boundary recorded in `OPERON-QUEUE.md` Phase 5 stands
  unaltered.
