# Citation verification — v0.9.8 current source projection

## Outcome

The current `paper.tex` and `references.bib` contain the same 45 citation keys.
The repository-owned machine record maps every key exactly once to a nonempty,
HTTPS-addressable identity and an explicit verification basis.

This is **source-identity and displayed bibliographic-metadata evidence only**.
It does not independently certify the mechanism attributed to a source, any
absence claim, novelty, priority, exhaustive coverage, resolution of a blind
review finding, or release readiness. A fresh independent v0.9.8 literature
run and blind review remain required. `release_authorized` and
`novelty_certified` are both `false`.

## Exact source projection

| Input | SHA-256 | Derived keys |
| --- | --- | ---: |
| `paper.tex` | `df8c9551cc38ce08dff5c58442f7b71504842d8665f6010d2aba22f12a74df6e` | 45 cited |
| `references.bib` | `a8b5bc235be370f805ac37bd8f330e791528c3918e7bc425ef373f53e43a839b` | 45 entries |
| `results/citation-verification-v098.json` | `62a80d37abd695f358a71f347583d056edac24e660019993b811bb135fbfe3c6` | 45 records |

The citation set was derived mechanically from every comma-delimited key in
LaTeX cite commands. The bibliography set was derived from every BibTeX entry
key. After whitespace normalization and unique sorting, the sets are equal:
there are no cited-only or bibliography-only keys, and no machine record is
duplicated.

The build validator binds the machine record to both current source hashes,
exact 45-key membership, nonempty identity bases, and an explicit
pending-fresh-v0.9.8-review status. Any later change to either source file
invalidates this projection and requires regeneration before the internal
build can pass.

## Evidence partition

The 45 records divide without overlap:

- 39 exact source identities inherit from the repository-owned v0.9.7
  citation projection at SHA-256
  `d640f31a2195c54f5fb3b628f1e391e109d29ce8e0a65e3f0ff1357337967e84`;
- six records were reconciled against the exact official arXiv or RFC Editor
  identity named by the current bibliography.

This partition describes provenance, not source quality or proposition-level
support. The trace-noncompliant v0.9.7 Operon return is not a verification
basis for either group.

## v0.9.8 identity reconciliations

| Cite key | Current canonical identity | Canonical URL | Bounded disposition |
| --- | --- | --- | --- |
| `Yao2023ReAct` | `arXiv:2210.03629v3` | `https://arxiv.org/abs/2210.03629v3` | Versioned preprint only; no ICLR publication record certified |
| `Khattab2024DSPy` | `arXiv:2310.03714v1` | `https://arxiv.org/abs/2310.03714v1` | Versioned preprint only; no ICLR publication record certified |
| `Zhang2025AFlow` | `arXiv:2410.10762v3` | `https://arxiv.org/abs/2410.10762v3` | Versioned preprint only; no ICLR publication record certified |
| `Wang2026AgentSpecRuntime` | `arXiv:2503.18666v3` | `https://arxiv.org/abs/2503.18666v3` | Versioned preprint only; its acceptance comment does not certify publisher metadata |
| `Agrawal2019TensorFlowEager` | `arXiv:1903.01855v1` | `https://arxiv.org/abs/1903.01855v1` | Newly added closest-precedent identity; mechanism paraphrase not certified here |
| `Rundgren2020JCS` | `RFC:8785` | `https://www.rfc-editor.org/rfc/rfc8785.html` | Newly added serialization-standard identity; no domain-equivalence or path-alias claim |

The stable cite-key years for ReAct, DSPy, AFlow, and AgentSpec are not treated
as publication-status assertions. Their BibTeX entries now render the years and
metadata of the chosen versioned preprint records.

## Bibliographic corrections and retained boundaries

- `W3C2013PROVDM` retains the dated Recommendation identity
  `W3C:REC-prov-dm-20130430` and dated canonical URL. The mutable
  `/TR/prov-dm/` alias is not the bibliography locator.
- `Crusoe2022CWL` retains `{The CWL Community}`. A fresh Crossref lookup for
  DOI `10.1145/3486897` returns ten named people followed by an eleventh author
  object with `given: "The CWL"` and `family: "Community"`. The contrary
  v0.9.7 Operon discrepancy is false.
- The v0.9.7 raw registry's RFC 2748 entry starts with J. Boyle and places
  D. Durham third, while the official RFC front matter begins
  `D. Durham, Ed.`. RFC 2748 is not a current bibliography key. This projection
  does not use that raw registry to certify `IETF2000RFC2753` or any other RFC.
- The v0.9.7 registry also named RFC front matter it had not fetched. Retrieved
  Datatracker or Crossref identity evidence does not make an unfetched source
  fetched.

## Non-certifying Operon boundary

The v0.9.7 raw files pass their final-byte structural validator, but the
repository-owned trace audit at
`results/operon-v097-return-audit.json` records a certifying failure. Contexts
A and B overlapped, both read undeclared local PDF-text derivatives, automated
reviewers crossed the claimed isolation boundary, and a failed full-validator
result was repaired under the same Context A UUID. Its registry and 21 blind
findings remain advisory discovery and review inputs only.

The older v0.9.5 registry likewise remains non-certifying and is not a source
identity basis. Its five copied RFC author fields, incomplete exact-entity
coverage, and same-work or mutable-locator substitutions remain disqualifying.

## Permitted conclusions

The machine projection permits only these conclusions:

1. the current manuscript and bibliography have symmetric 45-key membership;
2. every key has one bounded, HTTPS-addressable source identity;
3. ReAct, DSPy, AFlow, and AgentSpec no longer render unsupported conference
   metadata as though the publisher record were verified;
4. TensorFlow Eager and RFC 8785 have explicit official identities; and
5. a fresh independent v0.9.8 review is still mandatory.

It does not:

- independently full-text verify any cited mechanism;
- certify that any source lacks a construct or conjunction;
- establish novelty, uniqueness, priority, prevalence, or superiority;
- resolve the v0.9.7 blind-review findings;
- authorize public release.
