# Reproducibility supplement

## Scope

This supplement accompanies *The Agent Graph Runtime: A Unified Model for
Static, Dynamic, and Hybrid Execution*. It documents the read-only historical
C30 invariant reproduction and the separate current-Core architecture audit
used for the internal preprint. It does not repackage private sealed run
bundles or turn the C30 exercise into a comparative experiment.

The two source populations are deliberately separate:

- historical C30 evidence is interpreted at Mentu
  `40bd3f90cf4cfd34cdcf3f885018b5096ec28e6f`;
- current architecture evidence is audited at Mentu
  `f3d89e721637f4d1953f14dd4be56dc1e0314f76`.

The current audit cannot rewrite the frozen C30 artifacts or retroactively add
C30 observations.

The reproduction has four purposes:

- rebuild persistent projections from recipes and prompt files instead of
  trusting stored parity booleans;
- verify executable identity across inspected plans, requalified admission
  bundles, and receipts;
- distinguish execution-node calls from graph-planner dispatch; and
- verify historical and current committed implementation facts and sealed
  evidence digests without invoking Mentu CLI or MCP surfaces.

## Access and reproducibility tiers

| Reader | What can be reproduced | Required inputs |
|---|---|---|
| Any source-archive reader | Check internal consistency of published result projections; regenerate figures; audit schemas and dispositions. This tier cannot authenticate the private measurements that produced the projections. | The co-distributed source archive |
| Mentu-source holder | Recompute the historical and current committed-source audits from pinned Git blobs | Public archive plus a Mentu Git repository containing both pinned commits |
| Exact-archive conformance reproducer | Re-execute the committed 13-filter/25-test current-Core inventory and obtain a new typed receipt. This is a separate command, not an implicit part of the historical wrapper. | Public archive, a Mentu Git repository containing `f3d89e7`, and the exact Apple/Swift toolchain declared below |
| Authorized local reproducer | Rebuild persistent projections; verify plan-to-receipt identity; recompute all private sealed-bundle digests; rerun the historical wrapper and bounded current audits | Epistemics evidence worktree, Mentu source containing both pins, and read-only sealed C30 workspace |

The sealed bundles are internally high-assurance but access-restricted
evidence and are intentionally excluded
from the public package. Therefore the public archive is sufficient to inspect
the derivation and rerun public projections, but not to reproduce every private
input digest from first principles. The strongest empirical evidence remains
author-produced; no public reader should interpret its internal grade as an
independent replication grade.

The v0.9.9 internal package is named
`agent-graph-runtime-v0.9.9-internal-source.zip`; its detached byte count and
SHA-256 are recorded in `results/build-manifest.json` and
`INTEGRITY-SWEEP.md` when the package is sealed. At the v0.9.9 freeze, public
retrieval through a stable
locator is pending and the internal package is not licensed for public
redistribution. The author must choose both before v1.0. A successful release
archive co-distributes the resulting clearance record and licence; these are
release blockers, not silently satisfied metadata.

Release mode enforces those author-owned decisions through
`RELEASE-CLEARANCE.json`. The record must bind a nonempty `LICENSE` file, a
canonical DOI or arXiv locator, and explicit scoped author-operator consent for
retained timestamp-bearing activity data. Neither Operon nor Codex may invent
those choices. The file and licence are absent from the internal package by
design. The public source package carries no third-party documentation
snapshot or article full text. Citation verification records contain only
identifiers, metadata, resolution receipts, and short source-checked excerpts;
that bounded use is not itself a legal opinion. Public licensing and
third-party-material review remain author-owned release decisions.

## Required inputs for a full authorized rerun

An authorized reproducer supplies:

- an Epistemics Git worktree containing the frozen C30 pilot;
- a Mentu Git worktree containing both pinned source commits recorded in the
  machine maps;
- a read-only workspace containing the named sealed C30 run bundles; and
- a new output directory outside all measured roots.

## Invocation

The wrapper exposes its exact argument contract through:

```text
python3 reproduce.py --help
```

Its path-neutral invocation form is:

```text
python3 reproduce.py \
  --epistemics-root EPISTEMICS_ROOT \
  --mentu-root MENTU_ROOT \
  --workspace-root SEALED_WORKSPACE_ROOT \
  --output-dir NEW_OUTPUT_ROOT
```

The all-capital values are caller-supplied locations. The wrapper refuses an
output directory inside the frozen pilot, Mentu repository, or measured
workspace, and writes only beneath `NEW_OUTPUT_ROOT`.

The validated analysis/build environment is macOS 26.3 build 25D125 on arm64,
CPython 3.14.6 (standard library only), Swift compiler 6.2.3 with swift-driver
1.127.14.1 targeting `arm64-apple-macosx26.0`, Xcode 26.2 build 17C52, macOS
SDK 26.2, librsvg 2.62.1, Poppler 26.03.0, and Tectonic 0.16.9.
`analysis/environment.json` is the machine-readable form;
`analysis/requirements.lock` records that no PyPI package is required. The
25-test conformance tier additionally binds Swift Argument Parser 1.7.0 at
revision `c5d11a805e765f52ba34ec7284bd4fcd6ba68615` and the committed
`Package.resolved` digest
`9d735dd646fa19a09288611f7032b3d28c4fb4a05d535b7e75e600f3e83f9241`.
These exact prerequisites describe the recorded run; no cross-version
byte-identity or pass-equivalence claim is made. The pilot run environment
\(h_{\eta,\mathrm{run}}\) and this analysis/build environment
\(h_{\eta,\mathrm{repro}}\) are distinct constructs; the pilot computed no
standalone aggregate for either.

## Distributed scripts and produced artifacts

The source archive includes `reproduce.py`, all analysis scripts, and the
canonical `build.py` used to validate and package the manuscript. The
historical C30 wrapper produces:

- `results/pilot-reproduction.json`;
- `results/source-audit.json`;
- `results/invariant-checks.json`;
- `results/evidence-manifest.json`;
- `results/generated-results.tex`;
- four figures in SVG, PNG, and PDF;
- `figs/figure-manifest.json`; and
- `reproduction-run.json`.

`reproduction-run.json` is the caller-facing typed receipt. Version 2 reports
stage execution, invariant outcomes, output completeness, and baseline-byte
identity as four separate status families. It lists and hashes every generated
output, including `results/evidence-manifest.json`.
The evidence manifest binds every measured input by a path relative to its
declared root, committed Mentu blobs, result projections, and the exact
analysis scripts and environment metadata used by the run. This two-level
binding is the analyzer provenance contract; per-result self-description is
not treated as a substitute.

`results/reproduction-baseline.json` declares the expected SHA-256 values for
the byte-comparable result projections and `generated-results.tex`. Rendered
SVG/PNG/PDF figures remain structurally validated and inventoried but are not
asserted byte-identical across untested renderer or operating-system versions.
The receipt distinguishes an invariant failure from a missing output, baseline
drift, an invalid baseline, or a failed analysis stage; the canonical build
still requires all four status families to pass. Distinct exit codes and the
always-written receipt keep environment/output reproducibility from being
misreported as invariant failure.

The current evidence surface also contains three bounded audits that are not
folded into the historical C30 denominators:

- `analysis/verify_current_runtime.py` emits
  `results/current-runtime-audit.json` from committed Mentu
  `f3d89e7` blobs as a `reproduce.py` stage;
- `analysis/detector_sensitivity.py` emits
  `results/detector-sensitivity.json` from three disposable-copy controls and
  one selected current-Core engineering test executed from an exact
  `f3d89e7` archive as a `reproduce.py` stage;
- `analysis/verify_mentu_conformance.py` emits a typed current-epoch test
  receipt from 13 named filters executed against an exact committed archive
  with external scratch and an isolated Mentu home. This third audit is
  executed separately and validated by the paper build rather than regenerated
  by the read-only wrapper.

Their separate result schemas preserve the historical/current population
boundary. A successful full wrapper run includes the current-source and
detector-sensitivity stages but does not imply that the 25-test conformance
inventory ran. None of the three current results modifies
`results/pilot-reproduction.json`.

Path-neutral invocations for the additional audits are:

```text
python3 analysis/verify_current_runtime.py \
  --mentu-root MENTU_ROOT \
  --output NEW_OUTPUT_ROOT/results/current-runtime-audit.json

python3 analysis/detector_sensitivity.py \
  --pilot-root C30_PILOT_ROOT \
  --workspace SEALED_WORKSPACE_ROOT \
  --mentu-root MENTU_ROOT \
  --mentu-commit f3d89e721637f4d1953f14dd4be56dc1e0314f76 \
  --output NEW_OUTPUT_ROOT/results/detector-sensitivity.json

python3 analysis/verify_mentu_conformance.py \
  --mentu-root MENTU_ROOT \
  --commit f3d89e721637f4d1953f14dd4be56dc1e0314f76 \
  --output NEW_OUTPUT_ROOT/results/mentu-conformance-tests.json
```

The last command is the exact-archive conformance tier. It records the
environment commands, creates a temporary Git archive of the pinned commit,
uses external Swift scratch directories and a distinct isolated `MENTU_HOME`
for each command, and removes provider credentials. Its complete denominator
is generated from `results/mentu-conformance-tests.json`:

| Package | Exact `--filter` string | Tests |
| --- | --- | ---: |
| `mentu-execution-graph-core` | `MentuExecutionGraphCoreTests.CanonicalJSONTests` | 7 |
| `mentu-execution-graph-core` | `MentuExecutionGraphCoreTests.AdmissionTests/admissionDrift` | 1 |
| `mentu-execution-graph-core` | `MentuExecutionGraphCoreTests.AdmissionTests/admissionReceipt` | 1 |
| `mentu-execution-graph-core` | `MentuExecutionGraphCoreTests.QualificationTests/authorityCompatibilityAndStrictness` | 1 |
| `mentu-execution-graph-core` | `MentuExecutionGraphCoreTests.LowererTests/hashDrift` | 1 |
| `mentu-engine` | `MentuEngineTests.ExecutionGraphLowererTests/originParity` | 1 |
| `mentu-engine` | `MentuEngineTests.ExecutionGraphCanonicalizerTests` | 7 |
| `mentu-engine` | `MentuEngineTests.AdmittedExecutionGraphE2ETests/acceptedVerticalSlice` | 1 |
| `mentu-engine` | `MentuEngineTests.WorkflowExpertCommandTests/savedPlanExecutesExactly` | 1 |
| `mentu-engine` | `MentuEngineTests.WorkflowExpertCommandTests/persistentProjectionParity` | 1 |
| `mentu-engine` | `MentuEngineTests.GraphLifecycleTests/savedRunOrder` | 1 |
| `mentu-engine` | `MentuEngineTests.GraphLifecycleTests/driftRefusesBeforeRunnerConstruction` | 1 |
| `mentu-engine` | `MentuEngineTests.ExecutionGraphCoreCompatibilityTests/definitionRoundTrip` | 1 |
| **Total** | **13 filters** | **25** |

For any single row, use its exact package and filter in the `swift test`
template recorded under `command_contract.tests` in the machine receipt. A
successful historical wrapper run does not imply that this separate inventory
ran.

The current-source audit reads only pinned Git objects. The sensitivity and
conformance tools mutate only temporary copies, place Swift build scratch
outside the Mentu repository, and require the measured inputs to retain
identical before/after tree fingerprints.

## Release-certification boundary

The received exact-input v0.9.5 Operon return passed its mechanical isolation
and closed-tree gate, but its bibliography was scientifically nonconforming.
The later v0.9.6 return is also non-certifying: the frozen full gate rejects
the registry's missing isolation binding and then exposes a DOI request
normalization mismatch. Its 21 blind-review findings, including six majors,
are retained as advisory repair inputs in
`provenance/OPERON-V096-RETURN-AUDIT-2026-07-31.md`; neither the external raw
tree nor superseded coordinator/test material is a release input.

The v0.9.7 submitted files pass the frozen structural raw validator, but the
private session trace invalidates the run: Contexts A and B overlap, both read
undeclared text derivatives, automated reviewer contexts cross the attested
boundary, and Context A is resumed to repair the first failed full-validator
result. Independent source audit additionally finds that the retained RFC 2748
record fails the declared first-author check. The raw tree is preserved
byte-for-byte as a failed, advisory epoch and is not a release input.

The next v0.9.8 attempt stopped before either review context began. Its source
and input digests matched, but its coordinator was asked to author a detached
trace audit without access to a terminal export or a distinct auditor. It
correctly refused to fabricate that evidence. The episode is classified as an
instrument-insufficient preflight stop, not a failed review or consumed review
epoch.

This v0.9.9 artifact therefore requires fresh literature review and blind
review of exactly `paper-v0.9.9-internal.pdf` and this supplement, with no
additional blind source. Each review runs as a separately closed top-level
session. After both terminate, a Codex-side extractor must read and hash the
two user-exported terminal records and derive a path-neutral audit. No v0.9.7
finding is represented as resolved until that fresh review assesses the
repaired artifact.

The repository-owned citation table below is a repair projection, not a new
literature certificate. “Current identity” means the exact registration,
venue, or commit-pinned identity was checked in the repository-owned v0.9.6
audit. “Inherited identity” means unchanged source-identity metadata inherited
from the hash-bound v0.9.3 verification artifact. The separate mechanism-basis
column says what was actually read; identity resolution never silently becomes
full-text mechanism verification. Publication status is also separate. Every
row permits only the named positive precedent use. No row certifies novelty,
an absence claim, or release.

| Cite key | Canonical identity | Source-identity basis | Mechanism-support basis | Publication status | Scoped positive use |
| --- | --- | --- | --- | --- | --- |
| `Mokhov2018BuildSystems` | `doi:10.1145/3236774` | inherited identity | inherited scoped support; not re-read here | peer-reviewed publication | design space or workflow precedent |
| `Deelman2015Pegasus` | `doi:10.1016/j.future.2014.10.008` | inherited identity | inherited scoped support; not re-read here | peer-reviewed publication | design space or workflow precedent |
| `Yao2023ReAct` | `arXiv:2210.03629v3` | current versioned identity | mechanism scope inherited | versioned preprint | planning or agent control precedent |
| `Kim2024LLMCompiler` | `PMLR:v235/kim24y` | inherited identity | inherited scoped support; not re-read here | peer-reviewed proceedings | planning or agent control precedent |
| `Zhang2025AFlow` | `arXiv:2410.10762v3` | current versioned identity | mechanism scope inherited | versioned preprint | planning or agent control precedent |
| `Prasad2024ADaPT` | `doi:10.18653/v1/2024.findings-naacl.264` | inherited identity | inherited scoped support; not re-read here | peer-reviewed publication | planning or agent control precedent |
| `Khattab2024DSPy` | `arXiv:2310.03714v1` | current versioned identity | mechanism scope inherited | versioned preprint | planning or agent control precedent |
| `Agrawal2019TensorFlowEager` | `arXiv:1903.01855v1` | current versioned identity | primary abstract checked | versioned preprint | define-by-run and traced graph extraction precedent |
| `Ghallab2016PlanningActing` | `doi:10.1017/CBO9781139583923` | inherited identity | inherited scoped support; not re-read here | scholarly monograph | planning or agent control precedent |
| `Georgievski2015HTNOverview` | `doi:10.1016/j.artint.2015.02.002` | inherited identity | inherited scoped support; not re-read here | peer-reviewed publication | planning or agent control precedent |
| `Younes2003VHPOP` | `doi:10.1613/jair.1136` | inherited identity | inherited scoped support; not re-read here | peer-reviewed publication | planning or agent control precedent |
| `Necula1997PCC` | `doi:10.1145/263699.263712` | inherited identity | inherited scoped support; not re-read here | peer-reviewed publication | admission policy or authority precedent |
| `VanDerAalst1998Workflow` | `doi:10.1142/S0218126698000043` | inherited identity | inherited scoped support; not re-read here | peer-reviewed publication | design space or workflow precedent |
| `W3C2013PROVDM` | `W3C:REC-prov-dm-20130430` | inherited identity | inherited scoped support; not re-read here | official standard | provenance or evidence precedent |
| `Rundgren2020JCS` | `RFC:8785` | current official identity | exact RFC abstract and serialization scope checked | official informational RFC | canonical JSON serialization baseline |
| `Dolstra2010NixOS` | `doi:10.1017/S0956796810000195` | inherited identity | inherited scoped support; not re-read here | peer-reviewed publication | stored plan identity or replay precedent |
| `Lamb2022ReproducibleBuilds` | `doi:10.1109/MS.2021.3073045` | inherited identity | inherited scoped support; not re-read here | peer-reviewed publication | stored plan identity or replay precedent |
| `Burckhardt2021DurableFunctions` | `doi:10.1145/3485510` | inherited identity | inherited scoped support; not re-read here | peer-reviewed publication | stored plan identity or replay precedent |
| `IETF2000RFC2753` | `RFC:2753` | inherited identity | inherited scoped support; not re-read here | official standard | admission policy or authority precedent |
| `Torres2019inToto` | `USENIX:security19/torres-arias` | inherited identity | inherited scoped support; not re-read here | peer-reviewed proceedings | provenance or evidence precedent |
| `Park2004UCON` | `doi:10.1145/984334.984339` | inherited identity | inherited scoped support; not re-read here | peer-reviewed publication | admission policy or authority precedent |
| `Schneider2000EnforceablePolicies` | `doi:10.1145/353323.353382` | inherited identity | inherited scoped support; not re-read here | peer-reviewed publication | admission policy or authority precedent |
| `Fikes1972Planex` | `doi:10.1016/0004-3702(72)90051-3` | inherited identity | inherited scoped support; not re-read here | peer-reviewed publication | stored plan identity or replay precedent |
| `Colledanchise2017BehaviorTrees` | `doi:10.1109/TRO.2016.2633567` | inherited identity | inherited scoped support; not re-read here | peer-reviewed publication | data-dependent control precedent |
| `Kubernetes2026Admission` | `git:kubernetes/website@65a8302b72fc82fe7c15829462b2ac31891813ea:content/en/docs/reference/access-authn-authz/admission-controllers.md` | current pinned identity | exact pinned mutating/validating admission passage checked | official documentation snapshot | admission policy or authority precedent |
| `Bazel2026RemoteExecution` | `git:bazelbuild/remote-apis@9e084d0e43e717128ee72b5be584a7ba33e8006b` | inherited pinned identity | inherited scoped support; not re-read here | official version-pinned specification | stored plan identity or replay precedent |
| `Wang2026AgentSpecRuntime` | `arXiv:2503.18666v3` | current versioned identity | mechanism scope inherited | versioned preprint; citation does not claim proceedings metadata | admission policy or authority precedent |
| `Wang2025MI9` | `arXiv:2508.03858v4` | inherited versioned identity | inherited scoped support; not re-read here | versioned preprint | admission policy or authority precedent |
| `Hua2024TrustAgent` | `doi:10.18653/v1/2024.findings-emnlp.585` | inherited identity | inherited scoped support; not re-read here | peer-reviewed publication | admission policy or authority precedent |
| `Wang2026AgentTraces` | `arXiv:2606.04990v4` | inherited versioned identity | inherited scoped support; not re-read here | versioned preprint | provenance or evidence precedent |
| `Amini2025OpenAgentSpec` | `arXiv:2510.04173v4` | inherited versioned identity | inherited scoped support; not re-read here | versioned preprint | planning or agent control precedent |
| `Trooskens2026CompiledAI` | `arXiv:2604.05150v1` | inherited versioned identity | inherited scoped support; not re-read here | versioned preprint | planning or agent control precedent |
| `Serie2026OxyMake` | `arXiv:2606.20989v2` | inherited versioned identity | inherited scoped support; not re-read here | versioned preprint | stored plan identity or replay precedent |
| `Zhuge2024GPTSwarm` | `PMLR:v235/zhuge24a` | inherited identity | inherited scoped support; not re-read here | peer-reviewed proceedings | planning or agent control precedent |
| `Besanson2026SARC` | `arXiv:2605.07728v1` | inherited versioned identity | inherited scoped support; not re-read here | working preprint | admission policy or authority precedent |
| `Xu2026EvoMAS` | `arXiv:2605.08769v1` | inherited versioned identity | inherited scoped support; not re-read here | versioned preprint | runtime replanning scope boundary |
| `LangChain2026LangGraphRuntime` | `git:langchain-ai/docs@5b042a059975a17e297b1f121e44870df36b61c9:src/oss/langgraph/pregel.mdx` | repaired commit/path identity | mechanism not newly verified | official documentation snapshot | graph-runtime precedent |
| `LangChain2026LangGraphPersistence` | `git:langchain-ai/docs@5b042a059975a17e297b1f121e44870df36b61c9:src/oss/langgraph/persistence.mdx` | repaired commit/path identity | mechanism not newly verified | official documentation snapshot | graph persistence precedent |
| `LangChain2026LangGraphCompatibility` | `git:langchain-ai/docs@5b042a059975a17e297b1f121e44870df36b61c9:src/oss/langgraph/backward-compatibility.mdx` | repaired commit/path identity | mechanism not newly verified | official documentation snapshot | graph compatibility precedent |
| `Newman2022Sigstore` | `doi:10.1145/3548606.3560596` | current registration-authority identity | metadata only; mechanism not newly full-text checked | peer-reviewed proceedings | provenance or evidence precedent |
| `SLSA2026Verification` | `git:slsa-framework/slsa@v1.2=19e4e2f005f871270c4f555fc47afecfb37f3efe:docs/spec/v1.2/verifying-artifacts.md` | current tag/commit/path identity | exact pinned official source section checked | official version-pinned specification | admission policy or authority precedent |
| `Sigstore2026PolicyController` | `git:sigstore/docs@35180becb3f9c68ef39ccab9b4b4616170b3d237:content/en/policy-controller/overview.md` | current commit/path identity | exact pinned official source section checked | official documentation snapshot | admission policy or authority precedent |
| `OPA2026GatekeeperOperations` | `git:open-policy-agent/gatekeeper@v3.23.0^{}=cdf332c3f2762c616d4b6f433712a8d7ed62b3d8:website/docs/operations.md` | current tag/commit/path identity | exact pinned official source section checked | official documentation snapshot | admission policy or authority precedent |
| `Crusoe2022CWL` | `doi:10.1145/3486897` | current registration-authority identity | primary abstract only | peer-reviewed publication | design space or workflow precedent |
| `Temporal2026EventHistory` | `git:temporalio/documentation@5bb982c4574fb8bab54d776e5ff3264494d88c4c:docs/encyclopedia/event-history/event-history.mdx` | current commit/path identity | exact pinned official source section checked | official documentation snapshot | stored plan identity or replay precedent |

The current repository-owned identity basis is
`results/citation-verification-v098.json`, with its human audit in
`provenance/CITATION-VERIFICATION-V098.md`. It maps all 45 current cite keys
one-to-one. By the table's own source-identity basis column: twenty-nine
identities retain bounded repository ancestry (`inherited`), thirteen are
established at current identities, and three at repaired commit/path
identities. The sixteen non-inherited rows are `Yao2023ReAct`,
`Zhang2025AFlow`, `Khattab2024DSPy`, `Agrawal2019TensorFlowEager`,
`Rundgren2020JCS`, `Kubernetes2026Admission`, `Wang2026AgentSpecRuntime`, the
three LangGraph documentation pins, `Newman2022Sigstore`,
`SLSA2026Verification`, `Sigstore2026PolicyController`,
`OPA2026GatekeeperOperations`, `Crusoe2022CWL`, and
`Temporal2026EventHistory`. An earlier edition of this paragraph asserted
thirty-nine inherited identities with six named exceptions; that count was
hand-maintained, contradicted the table it summarizes, and is corrected here
from the table itself (finding BR9-002 of the v0.9.9-r6 blind review). This is source-identity and
displayed-metadata evidence only. It does not establish the mechanism
proposition assigned to a source, independent Context A verification, novelty,
or release readiness, and all retained mechanism fields still require fresh
review. The predecessor `results/citation-verification-v097.json` remains
immutable 43-key provenance; its trace-noncompliant Operon return is not a
verification basis. `results/citation-verification-v096.json` likewise remains
immutable provenance with superseded mutable LangGraph identities and
version-short arXiv labels identified by BR5-104 and BR5-113.

The rerun protocol uses canonical, hash-bound Context A, Context B, and
review-domain preflight templates. Its raw return must have the declared closed
file layout; the blind domain may read only the staged PDF and this supplement
and may not open the network or any Context A artifact. Source identity records
retain observed metadata and method-specific resolution receipts. Citation
dispositions bind the exact manuscript line span and a no-more-than-25-word,
human-checked primary-source excerpt. Finding dispositions bind their evidence
to a frozen source-artifact hash.

Producer self-reports are necessary but non-certifying. Context A and Context B
run as two separate top-level sessions and terminate before audit. Each review
domain is the complete frame graph reachable from its exported root. Declared
reviewer or critic descendants may operate inside that closure and are scanned
as part of the same computation; they are not silently ignored and are not, by
their mere existence, contamination. Cross-domain identifiers, artifacts,
reads, or prompt material are disqualifying. Declared deterministic PDF-text
extraction is treated as a provenance-bearing transformation of the staged PDF,
not as an undeclared source.

Only after both sessions close does a detached Codex invocation read the actual
private exports, recompute their byte identities, derive frame/tool/artifact
facts under a pinned extractor and tool policy, and run the first full raw
validator. A caller-supplied trace-audit JSON is not accepted. A failed first
attempt permanently voids that raw epoch. The exports stay outside Git and the
public archive; only their digests, path-neutral frame and event locators,
counts, error codes, limitations, and derived status enter the repository.

That status is `conforming_within_supplied_exports`, never an unqualified
independence certificate. The exports have no platform signature or
cryptographic completeness proof. Host memory configuration, omitted platform
events, and hidden control state therefore remain `unobservable`; zero visible
markers cannot be restated as proof that hidden state was absent. Exact input
binding, supplied-export non-interference, scholarly correctness, novelty, and
publication authority are separate gates.

The release builder copies the complete package and review roots once, then
performs projection validation, the reviewed internal rebuild, and release
packaging from that immutable snapshot. The resulting archive includes the
canonical protocol templates and the returned protocol bytes. The reviewed PDF
and supplement already supply the staged-input bytes; the raw manifest records
their duplicate staged paths and digests. These mechanisms make the review
packet auditable and fail closed on byte drift. They remain provenance and
traceability controls, not mechanical proof that a source proposition is true
or that a human/agent support judgment is semantically correct.

## Persistent-projection derivation

For each frozen plan stage, the analyzer:

1. opens the persistent `recipe.json` and referenced prompts as read-only
   bytes;
2. reconstructs effective policy from the plan snapshot and authority
   contract;
3. applies the pinned persistent-definition normalization rules;
4. rebuilds each step-contract manifest;
5. compares prompt bodies and their digests with the generated bundle;
6. creates the canonical executable payload and recomputes its digest; and
7. only then cross-checks the stored parity record.

The parity record is corroborating evidence, not the source of parity. A
mismatch in an identity-bearing component, reconstructed hash, or stored record
fails the invariant.

## Admission identity and planner separation

For each admitted saved-plan attempt, the analyzer compares:

```text
inspected plan executable
  = independently reconstructed requalified admission bundle executable
  = recorded admission bundle executable
  = receipt executable binding
```

The requalified bundle check does not trust its stored `executableHash`.
It re-hashes every stored prompt body, reconstructs the canonical executable
payload from the admitted definition, recomputed prompt bindings, static
variables, contracts, lowerer version, and effective policy independently
derived from the raw plan plus authority envelope, and then computes SHA-256.
Only after that reconstruction does it compare the recorded bundle and receipt
fields. A separate full-chain check joins the independently reconstructed
persistent projection to the same identity.

The attempt funnel is:

| Transition | Attempted | Refused before next stage | Reached next stage | Identity matched |
|---|---:|---:|---:|---:|
| Persistent projection | 5 | 0 | 5 parity records | 5 |
| Projection-to-execution selection | 5 | 2 semantic rejections (v2, v4) | 3 saved-plan attempts | not an identity transition |
| Saved-plan requalification | 3 | 0 | 3 admission attempts | 3 |
| Artifact admission | 3 | 0 | 3 admitted runs | 3 |

The 5/5 and 3/3 values are conditional transition checks, not pipeline pass
rates. “Zero exclusions” applies only inside the reported attempted identity
transitions; it does not erase the two semantic rejections between projection
and execution selection. The five plan stages map to three source heads: v1 to
`c0adef61dd2a811e07042344ee19500edbe583b6`, v2 to
`37f9f2c7957416898f8e2aac86c00c13be0280ad`, and v3--v5 to
`a828e91c9cd8d693a2cd918afc11460003a60a5e`.

The chronology documents 12 task-planning dispatch attempts. Complete telemetry
exists only for the five saved qualified plans: 133,022 input tokens, 10,127
output tokens, 143,149 total tokens, 108,874 elapsed milliseconds, 490,151
request bytes, and 42,930 response bytes. The other documented attempts lack
complete telemetry. These exact values are therefore lower bounds on the full
planning history; bytes, tokens, and elapsed time are distinct measurements and
are not forced into a dimensional reconciliation.

Full historical identity-bearing SHA-256 values are:

| Stage | Plan container | Executable identity |
|---|---|---|
| v1 | `f83b23b23d4dbcaa699e19b013a5a882dd3713e0f72af7ce6240b24fa88155d3` | `79ac85a26528113cd9d302dd12b5ac976058bcdfd80b3f6dc48236f410334115` |
| v2 | `64fb9cd04e5c240b862af5a9010bc92b1469223341732ed0fb4fdf35b056d864` | `b470c7538a2722917328faafd3bc4525b9532b187ef6554161d87879aca8aec8` |
| v3 | `a1df140f299bce8bea83523b96a51a0a34b98a25160dc035f18fc815fb25a247` | `cb10b4f2f08601292f7cef5106f399c51ce85b980ed3782c3c74de6053fc98cb` |
| v4 | `db93d8650e60396e1bdcb5bfe2561f207f0f49d51069502af875dc8725d1603a` | `e9e9dda87693e4d8a467fcdf52a463d03bd4acf2934a1d3e68c6cfdcd35c9e27` |
| v5 | `330f28ea6c21bfd2d3a0668941702ef0070890deae8f1b8cb3c0612def110efa` | `f0167cf72c04e0af77a844188933f42b1f4302a5e0f2acfad4ded0f7dcc25662` |

| Run stage | Receipt SHA-256 | Sealed-bundle SHA-256 |
|---|---|---|
| v1 | `77731c9399250a8165899d29d140477e800f74910be6b317c8196d2d3b589bca` | `a905202f025d4f9aaff14dfb45fa34ba75baa2d37ccb18b41b1b5c520432f91a` |
| v3 | `6acd0707c11922f1c732287187bd91470eb831df167f9cc3ebbf42c591a40e0b` | `7732b3ac4267b21c653f6dce65590241277f7ed474622dc907a8b5abbbae7a0c` |
| v5 | `501f757e8ce4dc67c7a0086d3af8a2f2c8cce6846d26344ebb34c3492231cbb6` | `813f1ead3062a4755b146abf5ecb94bcdd3f386e844c9af8105d3da075983a42` |

The 54 manifest leaves are nested in three bundles in one pilot corpus. They
are not 54 independent trials. One disposable byte flip invalidates one leaf
and the one derived bundle that contains it.

Planner separation uses three partly shared corroboration channels:

- the planner-dispatch field in each saved-execution record;
- sealed call records, each bound to a step activation and classified by lane
  and kind; and
- a committed-blob lexical check that the pinned `runPlanned` function body
  contains no planner emission.

These channels depend on recorded classification or one named implementation
path and are not independent instrumentation. The source check is deliberately
narrow: it is not a whole-program call-graph proof. Absence from one call lane
is likewise not a universal observability guarantee. The result is zero
recorded graph-planner dispatches; node-level model calls remain execution
calls.

## Committed-source audit

### Historical C30 source at `40bd3f9`

`analysis/verify_source.py` reads the historical Mentu pin through a temporary
Git archive rather than relying on dirty working-tree files. It interprets the
frozen C30 population and covers:

- strict-DAG lowering for admitted generated-graph v1;
- lowering to `SequenceDefinition`, sealed prompts, and contracts;
- executable binding of effective policy and lowerer version;
- shared `SequenceRunner` use and the DAG-shaped scheduler boundary;
- legacy persistent authority versus generated admitted-candidate admission;
- pre-admission dispatch refusal;
- the interpreted `WorkflowRunner` compatibility surface as a separate runner
  outside the audited frozen-graph core population;
- persistent executable parity; and
- direct use of the qualified in-memory executable during execution.

This audit is the source-side companion to the historical C30 reproduction.
Its implementation statements remain fixed at `40bd3f9`.

### Current Core source at `f3d89e7`

`analysis/verify_current_runtime.py` separately reads committed blobs at the
current pin and records:

- ownership by `MentuExecutionGraphCore` of the closed graph definition,
  lowerer, canonicalizer, qualification, admission, lifecycle/activation
  evidence, and graph scheduler;
- a strict-DAG admitted profile, one Core scheduler implementation, and one
  prepared admitted `SequenceRunner` construction site after admission;
- committed positive-execution and drift-refusal test definitions;
- a live generated/saved-plan path that remains prepared and admitted;
- raw recipes and the interpreted `WorkflowRunner` as named compatibility
  profiles;
- a lexical constructor census of 11 persisted recipe types, 10 direct
  production `SequenceRunner` sites (9 raw, 1 admitted), and 2 direct
  `WorkflowRunner` sites.

The source audit checks the presence and content of test definitions. The
separate exact-archive conformance tier above executes 13 named filters against
an exact Git archive: 25/25 targeted tests pass. The complete filter strings
and per-filter counts are published above. They cover Core and engine
canonicalization, admission identity and drift, strict authority decoding,
generated/persistent lowering parity, an admitted three-node vertical slice,
saved-plan exact execution, projection parity, lifecycle ordering,
pre-runner drift refusal, and the Engine--Core round trip. The vertical slice
sealed three activations. Within this recorded invocation, generated,
persistent, and admitted executable identities were all
`d1788ef9b0527ffff6dfd7e46ae0720c7dc6cc48c2109621d0c8f8f46a26ab3f`;
the admission-receipt identity was
`da85cc4e9252d7770e51e662aeeb31da4b896212a7605fe2ba995e5006665945`.
Those values identify this fixture invocation; equality across the three
executable representations, rather than cross-invocation digest constancy, is
the tested property. The canonical machine record is
`results/mentu-conformance-tests.json`.
The constructor census remains lexical, not a denominator for all effectful
product entry points.

The verifier records six exact limitations:

1. The inventory does not execute a conventional static recipe and a generated
   graph through one uniform Core admission route.
2. Persistent/generated parity checks executable identity and saved-plan
   execution, not matched outcome equivalence across both origin classes.
3. The implementation has per-artifact schema guards but no unified (lowerer,
   canonicalizer, artifact-schema) header mismatch fixture.
4. Canonicalization coverage is example-based and same-toolchain; it is not
   property-based, cross-language certification.
5. The inventory has no explicit environment-field isolation fixture covering
   every residual `F_eta` field.
6. All checks are author-side repository tests rather than independent
   black-box replication.

In particular, the unified `HeaderOK` gate is untested at both the historical
and current pins. Per-artifact schema guards do not show that each
lowerer/canonicalizer/schema header mismatch refuses before canonicalization
and host effects.

These current facts support describing Mentu as the paper's **author-checked
architectural instantiation of the strict-DAG admitted Agent Graph Runtime
profile**. Raw recipes and interpreted workflows are compatibility surfaces,
not counterexamples to that profile. No current test executes an ordinary
static recipe and a generated graph through one Core admission route, so
product-wide executed cross-origin parity is not claimed. The designation
does not assert product-wide uniform adoption, external certification, or
comparative rank.

## Projection and assurance-contract adoption

Historical C30 parity establishes that a persistent projection can preserve
canonical executable identity. It does not establish that ordinary recipe
discovery adopts the projection's authority profile.

The current audit identifies one ordinary recipe-dispatch adoption seam. A
generated persistent projection can be materialized below
`.mentu/recipes/generated/recipe.json` and resolved as `generated/recipe`.
Materialization adds no `auto_mode` marker, so the unmodified projection
occupies the recipe-auto-false row. Both CLI-auto Boolean cells construct the
raw `SequenceRunner`, whose compatibility initializer assigns legacy
authority. Across the complete 2×2 recipe-auto/CLI-auto matrix, every dispatch
that passes its applicable precondition constructs that same raw runner. Only
the recipe-auto-true/CLI-auto-false cell checks for a committed-recipe record;
this file-existence gate is neither Core qualification nor admission. The live
`GraphAuthoringCoordinator` path remains prepared and admitted, and
materialization alone does not execute either path. CLI absence and explicit
false collapse to one Boolean input state. Static reachability establishes
neither successful execution nor use frequency in any matrix cell.

Cross-profile reuse therefore requires an explicit target assurance contract,
requalification, and target admission before effects. Executable byte parity
is reuse evidence, not an authority grant. The current source shows that this
adoption transition is not globally enforced on ordinary recipe re-entry.

## Detector sensitivity and evidence non-vacuity

`results/detector-sensitivity.json` records two populations that must never be
pooled into a composite score.

The historical paper-control population detects 3/3 named disposable-copy
faults:

1. an executable-bound contract mutation changes executable identity;
2. injection of one planner-classified call record makes the planner-separation
   check fail;
3. one manifest-listed byte flip produces exactly one leaf-digest mismatch and
   one derived aggregate-digest mismatch.

The separate current-Core population detects 1/1 named engineering control:
one independently executed committed Core test refuses a bound
runtime-state-digest perturbation before execution at `f3d89e7`.

The 3/3 result is paper-control sensitivity over disposable copies; the 1/1
result is current-epoch engineering evidence. Neither is a C30 observation,
and the latter cannot retroactively change C30 P4's status: the historical
exercise challenged zero registered drift categories. These bounded results
establish neither complete mutation coverage, semantic correctness, calibrated
detection rates, nor reliability against unseeded faults.

Evidence non-vacuity is reported separately from logical conformance. The
historical population contains 5 persistent projections, 3 admitted saved-plan
attempts, 3 distinct admitted executable identities, and 3 admitted runs with
recorded host-boundary activity. Historical C30 is
therefore operationally non-vacuous for I1--I3, without supplying a policy
effect estimate. Its explicit evidence-adequacy vector is
\(\Gamma_E=(3,3,5,3,0,\varnothing,\varnothing)\): three admitted runs with
recorded host-boundary activity, three distinct admitted executable
identities, five projections, three invocations in the reported I1 set, and
zero exercised header-refusal fixtures. “Recorded host-boundary activity” is the
mechanical call-lane label; it is not upgraded into a claim about the semantic
success of each effect. Zero C30 drift categories and zero C30
binding/canonicalizer fixture classes were exercised. The
paper-local contract mutation covers one of six mandatory effect-semantic
payload classes; there is no C30 equivalence, environment-isolation,
header-mismatch, or omission-witness fixture.

The recorded model-cost value is a roughly US$1 two-attempt subtotal. A third
admitted attempt contains a recorded zero that cannot be distinguished from
missing telemetry, so its contribution is indeterminate and no three-attempt
total is reported.

The separate current test population contains 25/25 targeted passing tests.
Its admitted vertical slice executes and seals three dependency-ordered
activations, while its negative-path tests refuse declared identity and state
drift before effects. This is author-side engineering-test evidence over fixed
fixtures, not production traffic or an operational conformance rate. The
constructor census is not product-wide coverage, and no ordinary-static versus
generated execution comparison follows.

## Interpretation boundary

Passing the historical reproduction establishes only identity continuity,
observed planner-lane separation, historical committed-source facts, and digest
integrity at `40bd3f9`. Passing the current audit establishes only the named
current committed-source facts at `f3d89e7`. Detecting 3/3 historical
paper-control faults and 1/1 current-Core engineering control establishes
sensitivity only within those separate populations. Neither establishes comparative
superiority, lower total cost or latency, deterministic model outputs,
semantic correctness, or generality beyond Mentu.

The historical exercise challenged zero drift categories and computed no
aggregate environment identity; those properties remain
source/preregistration claims rather than C30 results. The one current-Core
drift test is engineering evidence in a different population.

Negative observations remain part of the result: mechanically qualified plans
failed semantic inspection, and one mechanically successful artifact required
later semantic correction. The comparative-verdict flag must remain false
until the preregistered matched study exists.

## v0.9.5 blind-review disposition

All 44 findings are retained in the reviewed surface: 14 major, 25 minor, and
5 notes. The repository-owned initial disposition classified 26 accepted, 13
partial, 4 preserved-note, and 1 superseded (`BR5-005`, whose v0.9.6
author-side boundary was replaced at v0.9.7) findings; it authorized neither release nor a
novelty claim. “Remediation” below is the v0.9.6 action, while “boundary”
states what the revision still may not infer. The machine record is
`results/operon-v095-finding-disposition.json`.

| ID | Severity / lens | Disposition | v0.9.6 remediation | Remaining boundary |
|---|---|---|---|---|
| `BR5-001` | note / novelty | preserved-note | Preserve restraint and add a context-aware prohibited-novelty lexical gate. | Explicit negations and quoted titles must remain permitted. |
| `BR5-002` | minor / novelty | partial | Add conjunct locators only for inspected sources. | Uninspected cells imply no absence. |
| `BR5-003` | minor / novelty | accepted | Use scope theorem or exclusion lemma consistently. | The lemma is not an empirical product failure. |
| `BR5-004` | minor / terminology | accepted | Use authoring method, assurance contract, target contract, and compatibility surface. | Package-wide stale-term sweep remains required. |
| `BR5-005` | minor / terminology | superseded | The v0.9.6 author-side boundary proved insufficient; v0.9.7 uses “author-checked architectural instantiation.” | No external certification follows. |
| `BR5-006` | minor / terminology | partial | Retain the regulated-qualification and scaffold terminology boundaries. | Established meanings still require verified anchors. |
| `BR5-007` | minor / terminology | accepted | Map receipt and sealed evidence to attestation vocabulary. | Do not inherit signatures or supply-chain guarantees Mentu does not implement. |
| `BR5-008` | major / formal | accepted | Split payload/header, pin externally, frame separately, refuse mismatch. | Complete mismatch/version fixtures remain required. |
| `BR5-009` | major / formal | partial | Make I5 declared closure and adequacy a separate defeasible claim. | Finite probes cannot prove universal adequacy. |
| `BR5-010` | major / formal | accepted | Put effect semantics in payload and toolchain/schema identity in the header. | Version identity is not mislabeled trace semantics. |
| `BR5-011` | major / formal | accepted | Use `x_rq` for requalification and `x_succ` for mutation. | Generated surfaces require collision checks. |
| `BR5-012` | minor / formal | accepted | Use a typed lifecycle and unique symbol roles. | A compact symbol table remains useful. |
| `BR5-013` | minor / formal | partial | Treat I2 as entry-path membership and retain violations in accounting. | Population denominators must remain explicit. |
| `BR5-014` | minor / formal | accepted | Instantiate SHA-256 and publish full source digests. | Figure prefixes are labels only. |
| `BR5-015` | minor / formal | accepted | State parity as a conjunction. | Lowerer-determinism and lossy-projection controls are still absent. |
| `BR5-016` | major / systems | accepted | Execute origin parity and the admitted vertical slice externally. | Ordinary-static versus generated execution through one Core admission route is unclaimed. |
| `BR5-017` | major / systems | partial | State conditional-route nonconformance and annotate the lifecycle figure. | Global adoption enforcement remains an implementation boundary. |
| `BR5-018` | minor / systems | accepted | Publish 9 raw and 1 admitted direct constructors. | Lexical counts do not measure reachability or traffic. |
| `BR5-019` | minor / systems | accepted | Publish runtime-context fields and the perturbed `runtimeStateDigest`. | This remains a bounded engineering control, not complete I5 evidence. |
| `BR5-020` | note / systems | preserved-note | Preserve substrate/assurance separation. | “Implemented” must not collapse distinct decisions. |
| `BR5-021` | major / empirical | partial | Publish attempted, refused, admitted, and matched counts. | Conditional identity ratios are not pipeline pass rates. |
| `BR5-022` | major / empirical | partial | Say bounded corroboration and zero recorded dispatches. | Absolute absence needs independent instrumentation. |
| `BR5-023` | major / empirical | partial | Execute equivalence and inequivalence tests; name missing partition/header fixtures. | Full canonicalizer conformance remains unestablished. |
| `BR5-024` | minor / empirical | accepted | Publish each payload/header/partition witness and gap. | Old 1-of-9 counting is invalid after the field split. |
| `BR5-025` | minor / empirical | accepted | Publish stage-to-head and identity mapping. | Five stages are not five independent source states. |
| `BR5-026` | minor / empirical | partial | Report 54 leaves nested in 3 bundles and 1 corpus. | No effective sample size of 54 is claimed. |
| `BR5-027` | minor / empirical | accepted | Round telemetry and state missingness, currency, and unavailable price basis. | Incomplete telemetry is not a treatment estimate. |
| `BR5-028` | minor / empirical | accepted | Print the historical evidence-adequacy vector. | Unknown effect counts remain lower-bounded. |
| `BR5-029` | minor / empirical | accepted | Add a primary endpoint, multiplicity rule, precision plan, and unconditional repeats. | Pilot data cannot justify prospective design choices. |
| `BR5-030` | minor / empirical | accepted | Separate C30, current-Core, and paper-control populations in high-read surfaces. | Cross-epoch aggregation remains forbidden. |
| `BR5-031` | note / empirical | accepted | Add innocuous negative controls in future work. | Current controls estimate neither specificity nor reliability. |
| `BR5-032` | major / citation | accepted | Publish a per-key verification table bound to primary records. | Raw registry presence alone is insufficient. |
| `BR5-033` | major / citation | accepted | Add SLSA, Sigstore, Gatekeeper, Temporal, and CWL; register remaining gaps. | Positive precedents do not establish uniqueness. |
| `BR5-034` | minor / citation | accepted | Replace the DSPy DBLP locator with its OpenReview record. | Aggregators remain discovery aids only. |
| `BR5-035` | minor / citation | partial | Publish this finding-by-finding table. | Blind review still receives no private claims ledger. |
| `BR5-036` | note / citation | preserved-note | Preserve pinned official locators and access dates. | Offline build must not require the network. |
| `BR5-037` | major / reproducibility | accepted | Declare Swift, driver, Xcode, SDK, and exact test filters. | A second-machine rerun is absent. |
| `BR5-038` | major / reproducibility | partial | Make manuscript and supplement authoritative for published claims. | The internal ledger remains audit metadata. |
| `BR5-039` | major / reproducibility | partial | Split invariant, stage, completeness, and baseline statuses. | Cross-platform byte portability remains untested. |
| `BR5-040` | minor / reproducibility | accepted | Publish full plan, executable, receipt, bundle, and current-test digests. | Truncated figures must resolve to these values. |
| `BR5-041` | minor / reproducibility | partial | Keep licensing and third-party review author-owned and fail closed. | Codex cannot supply legal clearance. |
| `BR5-042` | minor / reproducibility | accepted | State one author-operator and require ethics/consent before future human timing. | No multi-participant clearance is inferred. |
| `BR5-043` | minor / reproducibility | accepted | Regrade private evidence as internally high-assurance but author-produced. | Independent authorized replication remains absent. |
| `BR5-044` | note / reproducibility | preserved-note | Preserve path-neutral, read-only reproduction and add refusal tests. | Documentation alone does not prove zero-write behavior. |

## v0.9.9-r6 blind-review disposition (uncertified review)

The v0.9.9-r6 certification epoch was adjudicated `noncompliant` on seven
producer-conduct codes and is void as a certification
(`provenance/OPERON-V099R6-RAW-EPOCH-VOID-2026-08-14.md`). Session B — the
blind, network-free reviewer — satisfied its distinguishing constraints in the
derived trace audit (zero represented network events, matching output
receipt), and its review content is dispositioned here as **uncertified
external review**, on the same advisory footing as the v0.9.6/v0.9.7 returns.
Nothing in this section claims certification, and no finding is marked
resolved absent a fresh trace-audited review.

The review examined exactly the sealed v0.9.9-internal PDF
(`d371922d…`), this supplement at its reviewed digest (`8edd1803…`), and the
text projection as a navigation aid. Seven findings: 2 major, 4 minor, 1 note.
The two arithmetic findings were re-verified mechanically against this
supplement before disposition; both reproduced exactly.

| ID | Severity / lens | Disposition | Action |
|---|---|---|---|
| `BR9-001` | major / formal | accepted | The observation profile `omega` is unconstrained, unpublished, and absent from `Gamma_E`, so non-falsification under `TraceSound`/`AuthoritySound` carries no declared strength. Fix scheduled for the next candidate: publish the concrete `omega` (horizon, projection, harness) alongside each equivalence result, add it to `Gamma_E`, and pair it with a positive detection control so an undiscriminating profile is distinguishable from a genuine equivalence. |
| `BR9-002` | major / citation | accepted, corrected in place | The identity-basis paragraph asserted 39 inherited / 6 exceptions; the table's own basis column gives 29 inherited / 13 current / 3 repaired with 16 non-inherited rows. Re-verified mechanically; the paragraph is now derived from the table and the correction is recorded where it stands. The class repeats a v0.9.8-era lesson: hand-maintained counts over generated tables must be generated. |
| `BR9-003` | minor / reproducibility | accepted, corrected in place | The v0.9.5 disposition prose said 27 accepted; the table holds 26 accepted, 13 partial, 4 preserved-note, and 1 superseded (`BR5-005`). Re-verified mechanically; prose corrected and the superseded status is now declared in the tally. |
| `BR9-004` | minor / terminology | accepted | `pi` denotes both the lifecycle policy vector and the observation-profile event projection. Symbol rename scheduled for the next candidate. |
| `BR9-005` | minor / empirical | accepted as declared limitation | `Gamma_E` is published for the historical population only. The boundary is already stated; the next candidate restates it at the `Gamma_E` definition site and records whether a current-pin `Gamma_E` will be published or declined by design. |
| `BR9-006` | minor / systems | accepted | The sole-admitted-runner claim rests on a lexical constructor census, which cannot establish reachability. The census disclaimer is strengthened in the next candidate; a reachability-grade check is registered as future work, not claimed. |
| `BR9-007` | note / reproducibility | accepted | Two machine-readable flags are quoted from artifacts outside the reviewed surface. The next candidate either includes those artifacts in the reviewed surface or attributes the flags to their artifact digests explicitly. |

## v0.9.6 and v0.9.7 advisory-review boundary

The non-certifying v0.9.6 return records 21 findings: six major, 12 minor, and
three notes. The repository-owned audit lists every finding and repair target
in `provenance/OPERON-V096-RETURN-AUDIT-2026-07-31.md`, with the matching
machine record at `results/operon-v096-return-audit.json`. The raw tree failed
the frozen full gate and remains outside release inputs.

The v0.9.7 raw files pass their self-reported structural validator and contain
21 findings (six major, 12 minor, three notes), but the private session trace is
process-noncompliant for the four independently recorded reasons above. The
same return also contains a false prose claim that Crossref omits the CWL
Community author and a retained RFC 2748 record whose first author does not
match the declared primary source. The repository-owned audit is
`provenance/OPERON-V097-RETURN-AUDIT-2026-07-31.md`, with its machine record at
`results/operon-v097-return-audit.json`. The v0.9.8 preflight stop is separately
recorded in
`provenance/OPERON-V098-PREFLIGHT-STOP-2026-08-01.md`; it produced no literature
registry or blind-review finding and has no certifying effect. This v0.9.9
revision may answer the
advisory findings, but it does not mark them resolved: a fresh exact-input,
trace-audited review must independently assess the repaired PDF and supplement.

## Privacy and observer-effect controls

Public artifacts exclude credentials, raw session exports, transcripts,
private absolute paths, and sealed-bundle contents. They contain relative
evidence names, content digests, aggregate measurements, and committed-source
anchors.

Line-confirmation hashes over short candidate strings are guessable and
irreversible after publication. Timestamp-bearing run IDs and the reported
planner time, intervention chronology, and execution telemetry describe one
identifiable author-operator and may support work-pattern inference. They are
not privacy controls. This v0.9.9 artifact remains internal. The current
v1.0 builder therefore requires the author-operator to record explicit,
artifact-bound consent to retain those activity fields.

The current builder implements and tests the explicit-consent branch. A
sanitized alternative remains permissible, but it requires a separate
invariant-preserving projection and validator before release; removal of
timestamp fields alone is not treated as evidence that the published
measurements remain coherent.

The JSON record is an unsigned author attestation whose exact scope and
artifact hashes are mechanically checked. It is a provenance and scope-binding
control, not cryptographically authenticated proof of who authored it or that
valid consent was given. Likewise, the licence-text field records the author's
attestation that the hashed file is the official text; the builder is not a
legal-opinion engine. Bare hashes of short source lines are excluded rather
than presented as anonymity controls.

The historical judgments reported here were made by the single
author-operator. A future matched study that records another person's
authoring or inspection time must obtain and document an applicable ethics
determination plus informed-consent procedure before measurement begins. No
multi-participant ethics clearance is claimed by this internal artifact.

The release gate also cannot certify the intellectual completeness of a
literature search or the semantic correctness of a literature-matrix row.
Those are addressable human scholarly judgments. The gate binds exact prompt,
registry, matrix, log, and disposition bytes and checks their declared
relationships; it does not convert artifact presence into exhaustive coverage.

The wrapper never invokes Mentu CLI or MCP surfaces. It reads measured files
directly, reads committed source through Git object/archive operations, and
writes only to the explicit output directory.
