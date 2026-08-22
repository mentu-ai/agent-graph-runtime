# Citation verification — v0.9.6 current source projection

## Outcome

The current `paper.tex` and `references.bib` contain the same 43 citation keys.
All 43 source identities are resolved for scoped internal use. Six newly added
records were checked against exact registration-authority or commit-pinned
primary sources, and the DSPy bibliography locator was reconfirmed as the
official OpenReview record `sY5N0zY5Od`.

This is not a release certificate. Thirty-six pre-existing records inherit
source-identity verification from a repository-owned v0.9.3/v0.9.4 artifact;
they were not silently promoted into fresh v0.9.6 full-text checks. A fresh
exact-input external literature review and blind review remain required.
`release_authorized` and `novelty_certified` are both `false`.

## Exact source projection

| Input | SHA-256 | Derived keys |
| --- | --- | ---: |
| `paper.tex` | `4ebb9fc971b1e98dc0f2269b7c89d21ba5cf409434fced9a3fd4331fc8559bb2` | 43 cited |
| `references.bib` | `195bb158edec379a1acf0d6ee8437cdf827a6b3a35059858320a974c8218e4e0` | 43 entries |
| Prior repository verification | `d5f8c32b008dde7ee1e897a03989aa3f1baa7a5ef68e238fff80ff34dc4b5b3c` | 37 records |

The citation set was derived mechanically from every comma-delimited key in
LaTeX cite commands. The bibliography set was derived from every BibTeX entry
key. After whitespace normalization and unique sorting, both sets are equal:
there are no cited-only or bibliography-only keys.

## Verification tiers

- **T1 registration authority:** exact DOI query with title/subtitle,
  authorship, year, venue, and pagination comparison.
- **T1 commit-pinned primary source:** exact official repository, commit, path,
  and source-content digest.
- **T1 tag-and-commit-pinned primary source:** the above plus independent tag
  or peeled-tag verification.
- **T1 official conference record:** exact official venue identifier and
  canonical URL.
- **T2 version-bound repository verification:** an unchanged source-identity
  record inherited from
  `operon-certification-v093/CODEX-SOURCE-VERIFICATION.json` at the exact hash
  above. This tier is identity/metadata evidence, not a fresh source read.

## Six new exact records

| Key | Source and result | Tier | Scoped claim use |
| --- | --- | --- | --- |
| `Newman2022Sigstore` | Crossref resolved DOI `10.1145/3548606.3560596`; title plus subtitle, three authors, ACM CCS 2022, and pp. 2353–2367 match. | T1 registration authority | Sigstore signing and transparency as supply-chain evidence infrastructure. |
| `Crusoe2022CWL` | Crossref resolved DOI `10.1145/3486897`; title plus subtitle, authors, CACM 65(6), 2022, and pp. 54–63 match. The author-posted arXiv abstract supports portability, explicit runtime environments, and multiple implementations. | T1 registration authority plus primary abstract | Portable declarative workflow and runtime-environment precedent. |
| `SLSA2026Verification` | Official lightweight tag `v1.2` resolves directly to commit `19e4e2f005f871270c4f555fc47afecfb37f3efe`; exact file SHA-256 `acdfe8f67f1f6ebc66094304491dde776fde01e9f5c14568e1f71e199de2c263`. | T1 tag-and-commit-pinned source | Provenance verification against trusted builders and expected parameters. |
| `Sigstore2026PolicyController` | Exact official `sigstore/docs` blob at commit `35180becb3f9c68ef39ccab9b4b4616170b3d237`; file SHA-256 `a233604e313f47764d8199e3ce076c0ebb32c3b04c18e7551dc5c6e2cfb495fa`. | T1 commit-pinned source | Kubernetes admission-time validation of signatures and attestations. |
| `OPA2026GatekeeperOperations` | Official annotated tag `v3.23.0` has tag object `0041ff65743945fe1b20fc6d2957cb7f213519d8` and peels to cited commit `cdf332c3f2762c616d4b6f433712a8d7ed62b3d8`; file SHA-256 `9f0d83bda05acfe1f0074eec888491629aa8a894e1bc041cf87a77af818e7418`. | T1 tag-and-commit-pinned source | Gatekeeper validating and mutating webhook operations around Kubernetes admission. |
| `Temporal2026EventHistory` | Exact official Temporal documentation blob at commit `5bb982c4574fb8bab54d776e5ff3264494d88c4c`; file SHA-256 `b556c461dd239fc6a34e3a59320d6bbf26280c42ada11a62c010c1caae02dd37`. | T1 commit-pinned source | Durable Event History and replay-based state restoration after failure. |

## DSPy locator correction

`Khattab2024DSPy` now cites
`https://openreview.net/forum?id=sY5N0zY5Od`. That exact identifier and URL
already appear in the bound repository-owned source verification, and the
official OpenReview publication index identifies it as the ICLR 2024 DSPy
paper. DBLP is no longer used as the canonical bibliography locator.

OpenReview presented a browser challenge during the live body fetch, so this
pass records no new response-body digest. The source identity remains resolved
through the exact official record id plus the prior repository verification;
the limitation is explicit rather than converted into an absence inference.

## Pre-existing 37-key reconciliation

All 37 prior keys remain present in the current citation and bibliography sets
and reconcile one-to-one against the records in
`operon-certification-v093/CODEX-SOURCE-VERIFICATION.json`. Except for the
freshly reconfirmed DSPy locator, their tier is
`T2_VERSION_BOUND_REPOSITORY_VERIFICATION`.

That tier means:

- the cite key, source class, canonical identifier, canonical URL, and resolved
  status are inherited from a hash-bound repository artifact;
- the record is admissible for its already scoped related-work use;
- it is not represented as a fresh v0.9.6 full-text or exact-locator fetch;
- it cannot support a claim that a neighboring system lacks a mechanism;
- it cannot certify novelty, priority, superiority, or exhaustive coverage.

The machine-readable file enumerates every current key, its source class,
canonical identifier and URL, resolution status, exact basis and tier,
claim-use class, and release status.

## Operon v0.9.5 boundary

The v0.9.5 raw registry at SHA-256
`8482018e0d92c82562abaf4bd4bbe82eae1ea9e57ca4ed89e40f47cc9c53a4a3`
is not used as certifying evidence. It remains a useful discovery artifact,
but its five copied RFC author fields, incomplete 34/37 citation-entity
coverage, and same-work or mutable-locator substitutions prevent it from
certifying the exact manuscript bibliography.

## Release boundary

Every current source identity is resolved, and none of the six new records was
accepted through search absence or a matrix blank. This verification permits
only the scoped positive uses recorded in
`results/citation-verification-v096.json`.

It does not:

- certify that any cited system lacks an Agent Graph Runtime conjunct;
- establish that the paper's conjunction is novel or unique;
- disposition the v0.9.5 blind-review majors;
- authorize a public release.

A fresh external literature and blind-review cycle must bind the final
v0.9.6 PDF and supplement before release can be reconsidered.
