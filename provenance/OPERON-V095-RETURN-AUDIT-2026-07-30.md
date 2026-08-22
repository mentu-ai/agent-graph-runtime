# Operon v0.9.5 return audit — 2026-07-30

## Verdict

The `v0.9.5-internal` raw return passes the repository's frozen mechanical
raw-return contract. It contains exactly the expected 16 regular files, the
protocol and staged-input bytes are frozen correctly, the attestation binds the
returned outputs, and the raw-side schema checks pass.

That mechanical result is not a scientific certification. Independent
repository review found bibliographic defects and an incomplete citation
binding that prevent an honest release crosswalk. The return is therefore
usable as immutable advisory evidence, but it does not authorize release.
`release_authorized` remains `false`, and `novelty_certified` remains `false`.

The raw evidence under `operon-v095/` was not rewritten. This audit and the
machine-readable companion are repository-owned interpretations outside that
sealed root.

## Provenance bindings

The return was preserved at repository head
`075868cdbe8def24a4e843d8ad2e7d068de873b4`.

| Artifact | SHA-256 |
| --- | --- |
| Closed `operon-v095/` tree | `93a08053a70c4781aa63573945540e6af3835f8ef278e3fbe6a141cf1f1b870b` |
| `INDEPENDENCE-ATTESTATION.json` | `0d3b61813d5135013eced789ee33ba3a876d81c6d3aaaaf5a2e9e6bee5e21b5c` |
| `context-a/prior-art-verified.json` | `8482018e0d92c82562abaf4bd4bbe82eae1ea9e57ca4ed89e40f47cc9c53a4a3` |
| `context-b/blind-review-findings.json` | `de63fb92687fbf24d7c424ad15f338273e5c14cb1b8e56cd5f40f727b8328bfa` |
| `context-b/BLIND-REVIEW.md` | `2074666488c7c234dea8df8cb07289dd8200b7c6348d5fbaf0aecc60075734c7` |
| Reviewed PDF | `40ed40274c63622ada7dc445187177cf6e44f240f782715e7238fdcc6c51b68d` |
| Reviewed supplement | `f1921597b79b6de6649fb1b286c0edfac9f72a55003154635f6e7be34310e15a` |
| Frozen review projection | `74967307f452bde4b4003da42916246cde129a49421b53d13c6c1e24c657f6bb` |

The literature context is
`f8104a23-911f-4c39-a554-cfdcfe423778`; the blind-review context is
`f25afa36-f85c-498f-8281-855ec17b25b3`. Their identifiers are distinct and
both isolation reports satisfy the frozen structured preflight.

## Mechanical raw-return result

The following claims are mechanical and accepted:

- the raw root has 16 files, zero symlinks, and the exact closed path set;
- all three returned protocol files match `operon-protocol-v095/`;
- the staged PDF and supplement match the attested inputs;
- the attestation binds every returned context output by byte count and hash;
- the literature registry has 95 unique records and the identifier log has 95
  corresponding attempts;
- the dispositions are 59 retain, 30 background, three counterexample, and
  three exclude;
- the 92 non-excluded identifier records report resolved attempts, while SLSA,
  Temporal, and OPA/Rego are retained only as explicit blocked exclusions;
- all eight required literature families have records;
- the literature matrix contains exactly the registry's 95 raw cite keys;
- the blind review contains 44 findings: 14 major, 25 minor, and five notes.

These checks prove byte binding, schema conformance, and internal consistency.
They do not prove that an externally observed author, mechanism description,
negative claim, or citation mapping is correct.

## Scientific nonconformance

### 1. Five RFC author fields are wrong

The following registry rows all name `The Bazel Authors`:

```text
yavatkar2000rfc2753
durham2000rfc2748
rfc8785_jcs
rfc6920_ni
rfc3198_policy
```

That value is false for all five RFCs and appears to be copied from the
adjacent Bazel primary-source record. The coordinator replay noted that its
IETF endpoint did not expose author fields, so it did not independently test
this required field. A non-empty array satisfies the mechanical schema, but it
does not satisfy the Context A requirement to verify authors at a primary or
registration-authority source.

`yavatkar2000rfc2753` is already mapped conceptually to the manuscript's RFC
2753 citation. None of these five rows may be treated as fully verified until
its exact author list is independently observed and recorded in a fresh return.

### 2. Only 34 of 37 cited entities have honest registry matches

The manuscript and bibliography contain the same 37 citation keys. Thirty-four
have an identifiable same-work or same-document registry row. Three do not:

```text
Torres2019inToto
LangChain2026LangGraphPersistence
LangChain2026LangGraphCompatibility
```

The raw registry contains `intoto_spec`, a 2026 specification on the mutable
`main` branch, rather than the cited Torres et al. 2019 USENIX paper. It also
contains only `langgraph_pregel`, which honestly maps to
`LangChain2026LangGraphRuntime`; it has no separate records for the persistence
and backward-compatibility documents.

The v3 citation crosswalk requires every manuscript citation to map to a unique
non-excluded raw record. Reusing one LangGraph row for three references or
substituting a companion specification for the cited paper would be
scientifically false even if a looser machine representation could be made to
accept it. No such crosswalk may be created for v0.9.5.

### 3. Kubernetes binds the wrong source bytes

`Kubernetes2026Admission` and `k8s_admission` refer to the same documentation
subject, but not the same immutable source:

- the bibliography pins commit
  `65a8302b72fc82fe7c15829462b2ac31891813ea`;
- the raw registry verifies the mutable
  `kubernetes.io/docs/reference/access-authn-authz/admission-controllers/`
  page.

This is an entity match with locator drift, not exact citation verification.
The manuscript's pinned blob must remain authoritative and must be verified
directly in the next certifying pass.

### 4. Publication/preprint mappings require explicit treatment

Several honest entity matches use an arXiv record where the manuscript cites a
later conference or proceedings record:

```text
Yao2023ReAct -> yao2023react
Kim2024LLMCompiler -> kim2024llmcompiler
Zhang2025AFlow -> zhang2025aflow
Prasad2024ADaPT -> prasad2024adapt
Khattab2024DSPy -> khattab2024dspy
Wang2026AgentSpecRuntime -> wang2026agentspec
Zhuge2024GPTSwarm -> zhuge2024gptswarm
```

Other bibliography entries pin explicit arXiv versions while the registry uses
an unversioned arXiv locator. These mappings may support discovery and
same-work identity, but their year, venue, and source locator must not replace
the manuscript's published or version-pinned metadata without an explicit,
independently verified disposition.

### 5. The return does not certify novelty or mechanism absence

The registry explicitly sets `novelty_certified` to `false`. The literature
report also states that discovery was bounded and that candidate mechanism
coding was based on titles, abstracts, venue metadata, and prior knowledge
rather than close reading of all 95 works. Accordingly, statements such as
“does not emit,” “has no authority construct,” or “no work combines” remain
hypotheses for source-level verification, not certified negative facts.

## Permitted use

The v0.9.5 return may be used as:

- a bounded literature-discovery set;
- a source of candidate identifiers for independent source reading;
- an exact-input blind review of the v0.9.5 PDF and supplement;
- a major-revision agenda;
- evidence that the frozen raw-return protocol can be executed mechanically.

It may not be used as:

- a complete citation crosswalk;
- source verification for the five defective RFC rows;
- exact verification of the Kubernetes, in-toto, or two absent LangGraph
  citations;
- novelty, priority, uniqueness, exhaustive-coverage, or correctness
  certification;
- authorization for public release.

## Fresh v0.9.6 review requirement

The blind review reports 14 major findings, and the citation defects require
changes either to the manuscript, bibliography, or review protocol. Any such
change alters the exact input projection. A certifying path therefore requires
a fresh `v0.9.6-internal` PDF and supplement followed by new isolated Context A
and Context B runs.

The next Context A contract must require one dedicated registry row for every
manuscript bibliography key, exact cited locator or version, separate rows for
the three LangGraph documents, the exact Torres et al. 2019 source, the pinned
Kubernetes blob, and source-observed RFC authors. It must reject placeholder
authors and companion-source substitution. Codex must then independently
verify every retained citation proposition before any release gate can open.
