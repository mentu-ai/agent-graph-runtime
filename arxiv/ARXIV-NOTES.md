# arXiv submission notes

Prepared 2026-08-21 by the release packager. Everything here is ready to paste
or upload. The two outward acts at the end are reserved to the author.

## Source form: TeX, so submit source (not PDF-only)

The PDF is Tectonic-produced LaTeX, so arXiv's source rule applies and a
PDF-only submission would be refused absent a stated exception. The complete
source is in this directory:

| File | Role |
| --- | --- |
| `paper.tex` | The manuscript. `\documentclass[11pt]{article}`. |
| `build-context.tex` | Generated numeric projection, `\input` by `paper.tex`. Required; the manuscript raises a `\PackageError` without it. |
| `paper.bbl` | Rendered bibliography, 45 entries. **Required**: arXiv does not run BibTeX. |
| `figs/fig1-lifecycle.pdf` | Figure 1 |
| `figs/fig2-policy-axes.pdf` | Figure 2 |
| `figs/fig3-runtime-paths.pdf` | Figure 3 |
| `figs/fig4-evidence-boundary.pdf` | Figure 4 |

Upload those seven files preserving the `figs/` subdirectory (arXiv accepts a
`.tar.gz` or `.zip` with structure intact).

Notes that matter at submit time:

- **`references.bib` is deliberately absent from this upload set.** arXiv
  typesets the supplied `paper.bbl` and never invokes BibTeX, so the
  bibliography renders correctly without it. Its de-identification disposition
  was cleared on 2026-08-21 (both hits are cited-author names) and it now ships
  at the top level of the repository for local rebuilds. Adding it to the arXiv
  upload is harmless but unnecessary.
- **`\bibliographystyle{abbrvurl}` needs no `.bst` at submit time.** That
  command only writes a line into the `.aux`; the style file is consumed by
  BibTeX, which arXiv does not run. Do not be alarmed by its absence.
- **Figures are PDF 1.7 inside a PDF 1.5 output.** Tectonic emits a warning per
  figure. It is cosmetic, the figures render, and the released PDF carries the
  same warning in its build log.
- arXiv's TeX Live differs from Tectonic's bundle, so the arXiv-built PDF will
  not be byte-identical to `paper-v0.9.10-internal.pdf`. That is expected and
  does not affect the reproducibility claim, which is stated against Tectonic
  0.16.9 with `SOURCE_DATE_EPOCH=1785369600`. If arXiv's build fails on a
  package version, fall back to requesting a PDF-only submission and cite the
  deterministic-build requirement as the reason.

## Category

**Primary: `cs.SE` (Software Engineering). Cross-list: `cs.AI`.**

The paper's contribution is an architectural and lifecycle model, namely the
separation of construction, lowering, qualification, freezing, requalification,
admission, execution, and evidence, together with a conformance and provenance
regime and a test and pilot record. Agent systems are the subject matter, but
the reasoning is about execution substrates, artifact identity, and assurance
boundaries rather than about learning or inference, so `cs.SE` is the honest
primary and `cs.AI` is where its readers are.

## Abstract for the metadata field

Plain text, no markup, 1,907 characters, within arXiv's 1,920 limit. Also
written to `abstract.txt` in this directory for copy-paste. It is a faithful
condensation of the paper's longer abstract, not a verbatim copy.

```text
Agent systems are classified as static workflows, dynamic planners, or hybrids.
Those labels conflate four separable questions: when a graph is constructed,
where it becomes immutable and addressable, how it is authored, and what
executes it. This paper defines an agent graph runtime model in which they are
separately specified lifecycle coordinates over a constrained feasible region,
sharing one executable representation and execution substrate. Static, dynamic
one-shot, staged-direct, and staged-scaffold configurations become reference
points in that region, not necessarily distinct runtimes, and not every
Cartesian combination is claimed meaningful or implementable.

The model separates construction, lowering, qualification, freezing,
requalification, admission, execution, and evidence. It also separates easily
confused properties: executable graph identity, execution environment identity,
output reproducibility, plan adequacy, and outcome correctness. Mentu is the
paper's author-checked instantiation of the strict-DAG admitted profile, and one
cross-profile boundary is reported as unenforced: a generated persistent
projection can be rediscovered by legacy dispatch without a named adoption
transition, so the product does not yet enforce projection-is-not-adoption. A
targeted suite passes 25 of 25 tests across 13 filters at the current source pin.

A frozen historical pilot is reported as a mechanical invariant exercise, not a
treatment comparison: identity equality for five qualified projections, three
saved-plan transitions that all reached admission and retained identity, zero
planner dispatches, and sealed-manifest integrity. It retains negative evidence:
mechanically qualified plans failed human semantic review. With no matched
observations and no repetition series, comparative superiority, amortization,
and generality claims are excluded; novelty remains uncertified.
```

## Comments field

```text
39 pages, 4 figures. Reproducibility supplement, frozen build projection, and
the full provenance record of six attempted external certification epochs are
at https://github.com/mentu-ai/agent-graph-runtime
```

Replace the URL with the real one once the repository exists. If the repository
is not public at submit time, drop the URL and add it in a v2 rather than
pointing at a 404.

## Licence

**arXiv.org perpetual, non-exclusive licence to distribute this article.**

This is the default and it is the right choice: it keeps the repository's
CC BY 4.0 grant, carried in `LICENSE` and mirrored in `LICENSE-DOCS`, as the
operative permissive licence while avoiding a second, stricter grant on the
arXiv copy. Do not select a CC licence
in the arXiv form; the two would then have to be reconciled, and arXiv licence
selections cannot be changed after announcement.

## Metadata summary

| Field | Value |
| --- | --- |
| Title | The Agent Graph Runtime: A Unified Model for Static, Dynamic, and Hybrid Execution |
| Authors | Rashid Azarang |
| Primary category | cs.SE |
| Cross-list | cs.AI |
| Comments | see above |
| Licence | arXiv non-exclusive |
| MSC / ACM class | leave blank |
| Journal ref | leave blank |

## Submit-day checklist

Steps 1 through 7 are preparation and are already done or are the author's
desk work. Steps 8 and 9 are the outward acts.

1. **Done.** Candidate hashes verified against `OPERON-QUEUE.md` and the frozen
   projection. PDF, text projection, and supplement all match.
2. **Done.** PDF independently rebuilt from frozen source, byte-identical
   (`231a7330...`, 352,115 bytes, Tectonic 0.16.9).
3. **Done.** De-identification sweep over every shipped file: zero hits.
4. **Done.** Source package staged here, complete and self-sufficient for
   arXiv's pipeline.
5. **Done, and the answer is ship as-is.** The author elected on 2026-08-21 to
   cut a release-mode `v1.0-preprint` through the gate. The attempt is recorded
   in `../VERSION-IDENTITY-RESOLUTION-2026-08-21.md`: release mode requires an
   external review bundle at the frozen protocol revision with a green
   validation, no such bundle exists, and the gate was left closed rather than
   widened. No hash on this page changed and no restaging of the source package
   was needed. The internal-preprint notice on the PDF cover therefore stands,
   explained in the repository README rather than edited away.
6. **Done.** `references.bib` disposed on 2026-08-21: both sweep hits are cited
   authors in bibliography entries, no client identifier, no redaction needed.
   It ships at the repository top level. Never blocking for arXiv.
7. **Author.** Confirm the repository name and that arXiv account endorsement
   for `cs.SE` is in place. A prior `cs.SE` submission satisfies this.
8. **OUTWARD ACT, author or orchestrator.**
   `gh repo create mentu-ai/agent-graph-runtime --public`, then push the
   contents of `release-staging/` as a fresh single-commit repository, sole
   author and committer Rashid Azarang <rashid.azarang.eg@gmail.com>. Do not
   push the surrounding private repository or its history.
9. **OUTWARD ACT, author.** Submit to arXiv: upload the source package, paste
   the abstract, comments, and category above, select the arXiv non-exclusive
   licence, and submit. Record the `submit/NNNNNNN` identifier in the registry
   ledger, and add the arXiv ID to the repository README once announced.
