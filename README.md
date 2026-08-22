# The Agent Graph Runtime

This repository holds a preprint that defines an execution model for agent
systems, in which "static", "dynamic", and "hybrid" stop being runtime kinds
and become separately specified coordinates: when a graph is constructed, where
it becomes immutable and addressable, how it is authored, and what executes it.
It also holds the full provenance record behind that preprint, including six
attempted external certification epochs, none of which produced a certifiable
review, all of which are preserved here rather than summarized away.

## What is in here

| Path | What it is |
| --- | --- |
| `paper-v0.9.10-internal.pdf` | The paper. 39 pages, 4 figures, 45 references. |
| `paper-v0.9.10-internal.txt` | Deterministic text projection of that exact PDF, produced by `pdftotext -layout -enc UTF-8`. A navigation aid, not a second source. |
| `REPRODUCIBILITY-SUPPLEMENT.md` | Procedures, boundaries, and what each reported number does and does not license. |
| `SOURCE-PROJECTION-V0910.json` | Frozen build projection: the sha256 of every input that produced the PDF. |
| `REVIEW-PAIR-MANIFEST-V0910.json` | The exact byte identities handed to external review, plus the pinned text extractor. |
| `references.bib` | The BibTeX database behind the bibliography. |
| `SHA256SUMS` | Hashes of everything shipped here. |
| `RELEASE-DECISION-2026-08-21.md` | Why these bytes were released, and one open question the author left visible rather than hidden. |
| `VERSION-IDENTITY-RESOLUTION-2026-08-21.md` | How that question was answered, and what the release gate said when it was run through rather than read. |
| `LICENSE` | The single dual grant: MIT for code, CC BY 4.0 for documents, with the full text of both. |
| `RELEASE-CLEARANCE.json` | The author's publication decisions: licence selection bound to `LICENSE` by hash, and scoped consent for the six artifacts it names. |
| `provenance/` | The dated record: every certification epoch, every stop, every void, every finding disposition. |
| `arxiv/` | The LaTeX source that builds the PDF, plus submission notes. |

## Verify it yourself

Nothing here asks you to take a hash on trust. Every claim of identity below is
checkable in a few minutes.

**1. Check the shipped bytes against the manifest.**

```sh
shasum -a 256 -c SHA256SUMS
```

**2. Check that the paper's own frozen projection agrees.**

`SOURCE-PROJECTION-V0910.json` was written at build time and records what the
build consumed. Its `internal_pdf_sha256` field must equal the hash of the PDF
you just checked, and its `review_pair_manifest_sha256` must equal the hash of
`REVIEW-PAIR-MANIFEST-V0910.json`:

```sh
python3 - <<'PY'
import hashlib, json, pathlib
def h(p): return hashlib.sha256(pathlib.Path(p).read_bytes()).hexdigest()
proj = json.load(open("SOURCE-PROJECTION-V0910.json"))
for field, path in [
    ("internal_pdf_sha256", "paper-v0.9.10-internal.pdf"),
    ("paper_text_projection_sha256", "paper-v0.9.10-internal.txt"),
    ("reproducibility_supplement_sha256", "REPRODUCIBILITY-SUPPLEMENT.md"),
    ("review_pair_manifest_sha256", "REVIEW-PAIR-MANIFEST-V0910.json"),
    ("paper_tex_sha256", "arxiv/paper.tex"),
    ("internal_build_context_sha256", "arxiv/build-context.tex"),
    ("references_bib_sha256", "references.bib"),
]:
    print("OK " if proj[field] == h(path) else "MISMATCH ", field, path)
PY
```

**3. Rebuild the PDF and get the same bytes.**

The build is deterministic. With [Tectonic](https://tectonic-typesetting.github.io)
0.16.9 installed, the source in `arxiv/` reproduces the shipped PDF exactly:

```sh
cd arxiv
SOURCE_DATE_EPOCH=1785369600 tectonic -X compile -C --reruns 2 \
  --keep-intermediates --keep-logs --outdir ../rebuild paper.tex
shasum -a 256 ../rebuild/paper.pdf
# expect 231a7330cbab0d1ea99bb39ca7c826988efe4fe208114e547a33ba18b84ecab2
```

This was confirmed on 2026-08-21: 352,115 bytes, byte-identical to the released
PDF. The fixed `SOURCE_DATE_EPOCH` is what makes the output stable across
machines and dates.

One caveat about the bibliography. Tectonic re-runs BibTeX on every build and
rewrites `paper.bbl` in place, so the rebuild needs `references.bib` beside
`paper.tex`. It ships here, at the top level, so copy it into `arxiv/` before
rebuilding. This is a Tectonic behaviour, not an arXiv one: arXiv does not run
BibTeX and typesets the supplied `paper.bbl` directly.

**4. Reproduce the text projection.**

```sh
pdftotext -layout -enc UTF-8 paper-v0.9.10-internal.pdf - | shasum -a 256
```

The extractor version pinned in `REVIEW-PAIR-MANIFEST-V0910.json` is
`pdftotext version 26.03.0`. Other versions may differ in whitespace, which is
exactly why the version is pinned rather than assumed.

## What this record does and does not establish

Read `provenance/RELEASE-BOUNDARY-DECISION-2026-08-14.md` before drawing
conclusions from the certification record. In short:

- Six external certification epochs (`r1` through `r6`) were attempted. None
  produced a certifiable review. The two that reached adjudication (`r3` and
  `r6`) returned `noncompliant` on producer conduct, principally because
  producer self-reports diverged from the platform-represented trace. In `r6`,
  57 logged network requests appeared against zero represented network events.
- That is a result about the review instrument and the producing platform. It
  is not a result about this manuscript, which no epoch ever judged.
- **Novelty, correctness, and comparative rank are uncertified.** The paper is
  released with that stated plainly rather than waiting for a certificate the
  platform twice demonstrated it could not produce.
- The paper's own reported numbers are bounded by the supplement. The frozen
  C30 pilot is a mechanical invariant exercise, not a treatment comparison, and
  the paper excludes comparative superiority, amortization, and generality
  claims on that basis.

The PDF's cover carries an internal preprint notice, including the words "not
for dissemination". That text is a preserved artifact of the build that
produced these bytes, and it is superseded by `RELEASE-DECISION-2026-08-21.md`,
which records the author's decision to release them. It was left in place
rather than quietly edited, because editing it would have changed every hash on
this page.

Removing that notice honestly would have meant building in release mode, and
that was attempted on 2026-08-21 rather than assumed.
`VERSION-IDENTITY-RESOLUTION-2026-08-21.md` records what happened. Release mode
requires an external review bundle at the frozen protocol revision with a green
validation result. No such bundle exists: the four raw trees that have the
required layout declare later protocol revisions, and the validations that were
produced returned `noncompliant` twice, `indeterminate` once, and nothing once.
The gate was therefore left closed and unamended rather than widened to let
these bytes through, which is the same reason the notice was left in the PDF.

## What is withheld

This repository is a subtree of a larger private research repository. The
following are deliberately not here:

- **The raw certification trees** (`operon-v099r*/`,
  `operon-certification-v099r*/`) and the two private Claude Science session
  exports they audit. The voided epochs are in private owner custody by design,
  and the exports were never platform-signed. `provenance/` carries the dated
  record of each one, which is the part that carries evidential weight.
- **Internal audit metadata**: `CLAIMS-LEDGER.md`, `spec-map.json`,
  `SOURCE-MAP.md`, and the internal build and release runbooks.
- **Client-identifying material** from the surrounding private repository,
  which is permanently unpublishable. Everything shipped here passed a
  de-identification sweep with zero hits.

## Citing

Rashid Azarang. *The Agent Graph Runtime: A Unified Model for Static, Dynamic,
and Hybrid Execution*. Preprint, 2026.

An arXiv identifier will be added here once the submission is processed. The
same identifier is owed to `RELEASE-CLEARANCE.json`, whose release locator is
recorded as pending and is bound by a dated addendum within 72 hours of the
identifier being assigned.

## Licence

`LICENSE` is the authoritative file and carries the full official text of both
grants. (c) 2026 Rashid Azarang.

- Source code is MIT.
- The paper, documentation, provenance records, and data files are CC BY 4.0.

`LICENSE-CODE` and `LICENSE-DOCS` are the same grant split in two, kept for
readers who want one licence at a time. `RELEASE-CLEARANCE.json` records the
selection as `MIT AND CC-BY-4.0` and binds it to `LICENSE` by sha256.
