# The v1.0 public rendition, 2026-08-22

By author decision during the arXiv submission act: the public
rendition presents as **v1.0, dated 22 August 2026**. It is the same
manuscript as the archived v0.9.10-internal (same sources, same
build-context projection values) with exactly three authored
front-matter changes, none of which touches the gate, the epochs, or
any disclosure:

1. The cover banner's final clause now states the truth post-release:
   the release act occurred on 2026-08-22 under Decision A1 (it
   previously read "has not occurred; not for dissemination", which
   the act itself falsified).
2. Appendix F gains a dated-status paragraph: the eligibility rule is
   recorded as designed; the 2026-08-14 boundary decision and Decision
   A1 govern; the machine gate's refusal is preserved undisturbed.
3. PaperVersion v0.9.10-internal -> v1.0; PaperDate 14 -> 22 August
   2026. The internal lineage remains fully disclosed in the banner
   and Appendix A; provenance/ retains every internal artifact and
   hash unchanged.

paper-v1.0-preprint.pdf sha256 prefix: 1c92f0e9680cf712989b.
This is the v1.0-preprint the version-identity resolution named as the
release target, reached by the author's front-matter act under
Decision A1 rather than by release mode — which remains closed, its
refusal intact.


---

## Addendum, 2026-08-26: build correction v1.0.1

An external citation-integrity audit found the released PDF rendered an
empty References section: 35 pages, zero entries, while this repository's
README described the intended artifact (39 pages, 45 references). Root
cause: the release build ran Tectonic without references.bib beside the
manuscript, so its BibTeX pass produced an empty bibliography; the frozen
paper.bbl (45 entries) was present but is not consumed by Tectonic. The
arXiv source package is unaffected: it ships paper.bbl, which arXiv's
pipeline typesets directly.

Correction: rebuilt from the identical frozen source with references.bib
present (SOURCE_DATE_EPOCH=1785369600, Tectonic). The corrected PDF renders
all 45 references, numbered contiguously 1-45, 39 pages. No word of the
manuscript changed; the only difference is the bibliography now renders.

- superseded artifact sha256 prefix: 1c92f0e9680cf712989b (35 pp, empty References; preserved in git history)
- corrected artifact sha256: beabc9be049c62658b8cb91ce2223a0fe25a8dc3c7def8cac2b9b750ee4c6c81

The release gate remains closed and untouched; this is a build correction
of the rendition artifact, recorded rather than silently swapped.
