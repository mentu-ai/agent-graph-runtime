# The Agent Graph Runtime

This repository holds a preprint that defines an execution model for agent
systems, in which "static", "dynamic", and "hybrid" stop being runtime kinds
and become separately specified coordinates: when a graph is constructed, where
it becomes immutable and addressable, how it is authored, and what executes it.
It also holds the full provenance record behind that preprint, including six
attempted external certification epochs, none of which produced a certifiable
review, all of which are preserved here rather than summarized away.

## Versions

The public rendition is **v1.0, dated 22 August 2026**: `paper-v1.0-preprint.pdf`.
Read that one.

It is the same manuscript as the archived `paper-v0.9.10-internal.pdf`, with
three authored front-matter changes and nothing else.
`RENDITION-V1.0-2026-08-22.md` lists them. In short: the cover notice's closing
clause, which previously read "has not occurred; not for dissemination", now
records that the release act occurred on 2026-08-22 under Decision A1; Appendix
F gains a dated status paragraph; the version and date strings change. No
epoch, no gate, no disclosure was touched.

Both PDFs carry the words "Internal preprint" at the top of the cover. That is
accurate and deliberate. The manuscript was written under an internal
certification protocol, six epochs of that protocol ran, and none of them
produced a certifiable review. The cover notice discloses that instead of
hiding it. What changed on 2026-08-22 is the release act, not the
certification status.

v0.9.10-internal remains the internal version identity under the release gate,
and it is the identity every hash and provenance record in this repository is
written against. It is kept here rather than replaced.

## What is in here

| Path | What it is |
| --- | --- |
| `paper-v1.0-preprint.pdf` | The paper as released. 39 pages, 4 figures, 45 references. sha256 `1c92f0e9680cf712989b1542c443dbf032faf74c8a0504133b51527cadf8f218`. |
| `RENDITION-V1.0-2026-08-22.md` | The three front-matter changes that make v1.0, and the decision behind them. |
| `paper-v0.9.10-internal.pdf` | The archived internal build. The bytes every frozen manifest below describes. |
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

**First, one thing to know about the manifests.** `SHA256SUMS` and
`SOURCE-PROJECTION-V0910.json` are frozen records of the v0.9.10-internal
build. They were sealed then and are not rewritten. Four files in the current
tree therefore no longer match `SHA256SUMS`, and are supposed not to:

- `arxiv/paper.tex`, `arxiv/build-context.tex`, `arxiv/abstract.txt`, rewritten
  by the v1.0 rendition.
- `README.md`, this file, which is living documentation rather than a sealed
  record. It is listed in the manifest because the manifest hashes everything
  that shipped on release day, and it has been revised since.

Checking the manifest against the current working tree reports exactly those
four and nothing else. Every sealed artifact still verifies.

To check the manifest against the tree it actually describes, use the release
commit:

```sh
mkdir -p /tmp/agr-v0910
git archive 07f6d98 | tar -x -C /tmp/agr-v0910
cd /tmp/agr-v0910 && shasum -a 256 -c SHA256SUMS
```

One file fails there too: `RELEASE-DECISION-2026-08-21.md`. The manifest was
computed before a closing "Decision A1" section was appended to that document,
and the appended text shipped in the release commit. The section was later
lifted back out, so the file at the current tip does match the manifest again.
The Decision A1 text itself is preserved in git history at commit `07f6d98`,
and the decision it records is restated in `RENDITION-V1.0-2026-08-22.md` and
on the v1.0 cover.

**1. Check the shipped bytes against the manifest.**

```sh
shasum -a 256 -c SHA256SUMS
```

Expect `OK` on 43 of 47 entries, and `FAILED` on the four named above.

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

Two of the seven report `MISMATCH` in the current tree, for the same reason as
above: `paper_tex_sha256` and `internal_build_context_sha256` describe the
v0.9.10 sources, and `arxiv/` now holds the v1.0 ones. Both match at the
release commit:

```sh
git show 07f6d98:arxiv/paper.tex | shasum -a 256
git show 07f6d98:arxiv/build-context.tex | shasum -a 256
```

**3. Rebuild the PDF.**

`arxiv/` holds the v1.0 sources. `arxiv/upload-package-2026-08-22.tar.gz` is the
same set as submitted, and its `paper.tex`, `build-context.tex` and `paper.bbl`
are byte-identical to the loose copies. With
[Tectonic](https://tectonic-typesetting.github.io) 0.16.9:

```sh
mkdir -p rebuild
cp references.bib arxiv/
cd arxiv
SOURCE_DATE_EPOCH=1787356800 tectonic -X compile -C --reruns 2 \
  --keep-intermediates --keep-logs --outdir ../rebuild paper.tex
```

The v0.9.10 sources build the same way from `git archive 07f6d98`, with
`SOURCE_DATE_EPOCH=1785369600`.

On byte identity, read the claim narrowly. The author confirmed on 2026-08-21
that the v0.9.10 sources rebuilt to 352,115 bytes, byte-identical to the
released PDF, on that machine on that date. `SOURCE_DATE_EPOCH` removes the
timestamp, but it does not pin the TeX package set: Tectonic resolves its
support files from a versioned web bundle, and a later bundle typesets to a
different byte stream. Rebuilding the v0.9.10 sources against a 2026 bundle
here produced a well-formed 350,889-byte PDF, not the sealed one. Treat the
`SHA256SUMS` and `SOURCE-PROJECTION-V0910.json` entries as the authority on
what was released, and a rebuild as a check on the source, not as a second
witness to the bytes.

One caveat about the bibliography. Tectonic re-runs BibTeX on every build and
rewrites `paper.bbl` in place, so the rebuild needs `references.bib` beside
`paper.tex`. It ships here, at the top level, which is why the command above
copies it in. This is a Tectonic behaviour, not an arXiv one: arXiv does not
run BibTeX and typesets the supplied `paper.bbl` directly.

**4. Reproduce the text projection.**

```sh
pdftotext -layout -enc UTF-8 paper-v0.9.10-internal.pdf - | shasum -a 256
```

Expect `d27f06255fe436cf2f676e68db1d3cedf80c5d68a1734bb74758d0f868365dea`. The
extractor version pinned in `REVIEW-PAIR-MANIFEST-V0910.json` is `pdftotext
version 26.03.0`. Other versions may differ in whitespace, which is exactly why
the version is pinned rather than assumed.

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

### On the cover notice

Both covers carry an internal preprint notice. The v0.9.10 cover ends "That act
has not occurred; not for dissemination". The v1.0 cover ends by recording that
the act occurred on 2026-08-22 under Decision A1. That is the only substantive
difference between the two notices, and it was made because the release act
falsified the old sentence.

The rest of the notice stands in both, because it is still true. The six-epoch
record is what it is, and the notice is where the paper says so on its own
first page.

Clearing the notice in full would have meant building in release mode, and that
was attempted on 2026-08-21 rather than assumed.
`VERSION-IDENTITY-RESOLUTION-2026-08-21.md` records what happened. Release mode
requires an external review bundle at the frozen protocol revision with a green
validation result. No such bundle exists: the four raw trees that have the
required layout declare later protocol revisions, and the validations that were
produced returned `noncompliant` twice, `indeterminate` once, and nothing once.
The gate was left closed and unamended rather than widened to let these bytes
through. v1.0 is an authored front-matter rendition, not a gate pass, and
`RENDITION-V1.0-2026-08-22.md` says so in those words.

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
and Hybrid Execution*. Preprint v1.0, 22 August 2026.

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
