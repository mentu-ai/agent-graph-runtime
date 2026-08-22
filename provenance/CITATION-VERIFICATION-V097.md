# Citation verification — v0.9.7 current source projection

## Outcome

The current `paper.tex` and `references.bib` contain the same 43 citation keys.
The repository-owned machine record maps every key exactly once and records a
bounded source identity for each one.

This is source-identity evidence only. It does not independently certify the
mechanism attributed to any source, any absence claim, novelty, priority, or
release readiness. No external source was fetched or full-text reviewed while
creating this v0.9.7 projection. A fresh exact-input v0.9.7 external literature
review and blind review remain required. `release_authorized` and
`novelty_certified` are both `false`.

## Exact source projection

| Input | SHA-256 | Derived keys |
| --- | --- | ---: |
| `paper.tex` | `e3d0cd48b8adf91e85fe541d5d3726f7c7062377e0a00e00fe5bb76e5a918d2c` | 43 cited |
| `references.bib` | `195bb158edec379a1acf0d6ee8437cdf827a6b3a35059858320a974c8218e4e0` | 43 entries |
| `results/citation-verification-v097.json` | `d640f31a2195c54f5fb3b628f1e391e109d29ce8e0a65e3f0ff1357337967e84` | 43 records |

The citation set was derived mechanically from every comma-delimited key in
LaTeX cite commands. The bibliography set was derived from every BibTeX entry
key. After whitespace normalization and unique sorting, the sets are equal:
there are no cited-only or bibliography-only keys, and no machine record is
duplicated.

The repository build validator accepts the machine record for
`v0.9.7-internal`, including its current source hashes, exact 43-key membership,
nonempty identity bases, and explicit pending-fresh-review status.

## v0.9.6 ancestry

The immediate ancestry is preserved rather than rewritten:

| Artifact | SHA-256 | Use |
| --- | --- | --- |
| `results/citation-verification-v096.json` | `6662b35c4d4ea60acd7bb52e5b0dcbd6c03c49a1c37d92271a56ce3fc2f9bdce` | Repository-owned identity ancestry for seven exact v0.9.6 records |
| `operon-certification-v093/CODEX-SOURCE-VERIFICATION.json` | `d5f8c32b008dde7ee1e897a03989aa3f1baa7a5ef68e238fff80ff34dc4b5b3c` | Version-bound identity and bibliographic metadata for 25 unchanged current records |

The v0.9.6 file retains the mutable LangGraph locators and shortened arXiv
labels that BR5-104 and BR5-113 identified. Those fields are superseded in the
v0.9.7 record; the ancestry artifact itself is unchanged.

The current 43 records divide without overlap:

- 25 unchanged identities bound to the v0.9.3 repository verification;
- 7 exact identities inherited from the v0.9.6 repository-owned record;
- 8 exact arXiv version identities bound by the current bibliography and
  supplement table;
- 3 LangGraph commit/path/raw-byte identities.

These counts sum to 43. The tier split is an evidence-provenance partition, not
a ranking of source quality or mechanism support.

## Exact arXiv version identities

The current bibliography and the v0.9.7 repair table agree on these versioned
identities:

| Cite key | v0.9.7 canonical identity | Canonical URL |
| --- | --- | --- |
| `Wang2026AgentSpecRuntime` | `arXiv:2503.18666v3` | `https://arxiv.org/abs/2503.18666v3` |
| `Wang2025MI9` | `arXiv:2508.03858v4` | `https://arxiv.org/abs/2508.03858v4` |
| `Wang2026AgentTraces` | `arXiv:2606.04990v4` | `https://arxiv.org/abs/2606.04990v4` |
| `Amini2025OpenAgentSpec` | `arXiv:2510.04173v4` | `https://arxiv.org/abs/2510.04173v4` |
| `Trooskens2026CompiledAI` | `arXiv:2604.05150v1` | `https://arxiv.org/abs/2604.05150v1` |
| `Serie2026OxyMake` | `arXiv:2606.20989v2` | `https://arxiv.org/abs/2606.20989v2` |
| `Besanson2026SARC` | `arXiv:2605.07728v1` | `https://arxiv.org/abs/2605.07728v1` |
| `Xu2026EvoMAS` | `arXiv:2605.08769v1` | `https://arxiv.org/abs/2605.08769v1` |

`Wang2025MI9` was already version-pinned in v0.9.6. The other seven rows repair
either a version-short identity or, for `Wang2026AgentSpecRuntime`, a local
accepted-manuscript label. This is a repository-owned version-pin
reconciliation. It is not represented as a fresh arXiv fetch or full-text
mechanism check.

## LangGraph commit and byte bindings

All three LangGraph identities now bind the exact official repository commit,
path, raw blob URL, and supplied content digest:

| Cite key | Commit-pinned path | Raw blob URL | SHA-256 |
| --- | --- | --- | --- |
| `LangChain2026LangGraphRuntime` | `langchain-ai/docs@5b042a059975a17e297b1f121e44870df36b61c9:src/oss/langgraph/pregel.mdx` | `https://raw.githubusercontent.com/langchain-ai/docs/5b042a059975a17e297b1f121e44870df36b61c9/src/oss/langgraph/pregel.mdx` | `78653c4e36cc6c4871d56e773b45f8690310554d46435bcd58c34925814a98db` |
| `LangChain2026LangGraphPersistence` | `langchain-ai/docs@5b042a059975a17e297b1f121e44870df36b61c9:src/oss/langgraph/persistence.mdx` | `https://raw.githubusercontent.com/langchain-ai/docs/5b042a059975a17e297b1f121e44870df36b61c9/src/oss/langgraph/persistence.mdx` | `f6cbfadf11648afad412b0bc55ae8f6c0a3dc5082fee2f757cfb490b89fd9770` |
| `LangChain2026LangGraphCompatibility` | `langchain-ai/docs@5b042a059975a17e297b1f121e44870df36b61c9:src/oss/langgraph/backward-compatibility.mdx` | `https://raw.githubusercontent.com/langchain-ai/docs/5b042a059975a17e297b1f121e44870df36b61c9/src/oss/langgraph/backward-compatibility.mdx` | `3309fa9075c01d16cbfd48a5acf5b3c8a60923beecc03d6974e78878f3df8110` |

The three bindings repair the live-documentation identities in v0.9.6. The
content hashes are bounded repository-owned repair evidence supplied for these
exact commit paths. They were not independently refetched in this task, and no
claim is made that their full text independently establishes the manuscript's
mechanism descriptions.

## Scoped-use boundary

Every record retains a scoped-use class so a reader can see why the source is
present in the bibliography. In this artifact those classes are labels only:
they do not themselves certify the proposition, support an absence inference,
or establish that a neighboring system lacks any Agent Graph Runtime conjunct.

The machine record therefore permits only these conclusions:

1. the current manuscript and bibliography have symmetric 43-key membership;
2. each key has a nonempty, HTTPS-addressable source identity and a bounded
   repository-owned evidence basis;
3. the shortened arXiv and mutable LangGraph identities from v0.9.6 are not
   carried forward;
4. a fresh v0.9.7 external review is still mandatory.

## Non-certifying v0.9.5 boundary

The v0.9.5 raw prior-art registry at SHA-256
`8482018e0d92c82562abaf4bd4bbe82eae1ea9e57ca4ed89e40f47cc9c53a4a3`
remains advisory only and is not a verification basis. Its copied RFC author
metadata, incomplete exact-entity coverage, and same-work or mutable-locator
substitutions remain disqualifying.

## Release boundary

This v0.9.7 projection does not:

- independently full-text verify any cited mechanism;
- certify that any source lacks a construct or conjunct;
- establish novelty, uniqueness, priority, or superiority;
- resolve or disposition blind-review findings;
- authorize public release.

A fresh exact-input external literature review and blind review must bind the
final v0.9.7 PDF and supplement before release can be reconsidered.
