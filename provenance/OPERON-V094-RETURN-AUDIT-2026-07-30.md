# Operon v0.9.4 return audit — 2026-07-30

## Verdict

The return is **not certifying evidence for `v0.9.4-internal`**. It binds the
correct manuscript and contains substantively useful literature and blind
review outputs, but it does not conform to the frozen raw-return contract or
the repository validator. It must therefore remain immutable advisory
evidence. No raw file may be edited to repair it, and no Codex certification
directory may claim that it passed.

This finding supersedes the coordinator narrative's statement that the return
was compliant. The narrative appears to have validated a more permissive local
schema rather than the frozen repository gate.

## External inputs

The raw session export remains outside Git.

| Input | Bytes | SHA-256 |
| --- | ---: | --- |
| Claude Science session export `2e98979d_2026-07-30T18-37-57.json` | 2,479,575 | `d78b8527e799d1910c51397b53b033a3ba6a26a0b49c66016b85ceaa8a3f97d1` |
| Pasted coordinator narrative | 12,674 | `2532efbb03d24ac6e7ba6033fccdf98eb16c0cf98b6c3caead2688cbcc34298a` |
| Downloaded raw-return tarball | 333,784 | `bf5b13d3fa1b5b61d497a220e753608b71f6cf7b6f69986ff4569011a6cf9fd9` |

The repository-owned raw root is `operon-v094/`. It contains exactly 16
regular files, no symlinks or other file types, and has the validator's
path-neutral tree digest
`e99a53c83493f25eeae1ffc2b19239b3e7d5f2ebbb58de321e5e3eda3d3c82b6`.

## What passed

- All 16 substantive files are byte-identical across the live raw root, the
  flat downloads, and the tarball's substantive members.
- The three returned protocol templates match
  `operon-protocol-v094/` byte-for-byte.
- The staged PDF and supplement match the canonical v0.9.4 artifacts.
- All 14 review-projection fields match the current package. Their canonical
  projection digest is
  `b596713e38e10140b12985c8f3569c01816009c4979a818d7b8199b87acd3182`.
- The attestation binds all ten raw context outputs by exact byte count and
  SHA-256.
- Context identifiers are distinct:
  `4f8b1c2e-7a3d-4e59-9b06-2d1f8a5c4e73` for Context A and
  `b7e29d04-6c81-4a3f-8e52-9f0a3b6d1c48` for Context B.
- Both isolation reports pass the frozen v2 schema and report zero memory,
  recall, prior-session, cross-context, or memory-tool markers.
- The prior-art registry and blind-review result pass their structural
  validators. The registry contains 53 records: 33 retained, 17 background,
  one counterexample, and two exclusions. The blind review contains 23
  findings: nine major, 11 minor, and three notes.
- `preflight_operon_bundle` accepts the attested paper version. This is only a
  version preflight and is not a certification result.

## Contract failures

### 1. Transport archive is not a closed 16-file bundle

Python's tar reader exposes 20 AppleDouble `._*` regular files in addition to
the 16 substantive files. Each AppleDouble file is 163 bytes with SHA-256
`b54a8cb891e00ae552b23b33551a17d5348be2803b2a5f1c922b467fd00f8dc2`
and magic `00051607`. A wholesale extraction therefore violates the closed
layout and would fail `E_RAW_LAYOUT`. BSD `tar -t` hides these entries, so its
listing is insufficient for this check.

The repository-owned raw root is clean because those transport metadata files
were not copied into it. The original tarball is retained by hash as transport
provenance, not as a certifying archive.

### 2. Both file-open logs violate the exact schema

The frozen gate permits exactly four top-level keys:
`schema`, `context_id`, `parent_directory_listed`, and `entries`. Each entry
must contain exactly `path` and `kind`.

Context A adds `local_reads_permitted`,
`withheld_files_named_by_appendix_not_opened`, and
`blocked_external_attempts`; its 22 entries add `purpose` and `opened_at`.
Context B adds `network_access_used`, `external_reads`, `derived_reads`, and
`entry_count`; its five entries add `purpose`, and substantive entries add
digest, byte-count, or page metadata.

The repository validator therefore stops with:

```text
E_FILE_OPEN_LOG_INVALID: file-open log contains an undeclared top-level field
```

Context A also aggregates multiple deliberate external reads under placeholder
paths such as `<doi>`, `<arxiv_id>`, and `<query>`, rather than recording each
open as required by the queue.

### 3. Eighteen identifier attempts violate canonical request equality

The following attempts do not match the canonical resolver URL derived by the
frozen verifier:

```text
a001 a003 a004 a005 a006 a007 a008 a009 a024
a025 a030 a031 a035 a036 a044 a050 a052 a053
```

The first 16 are non-excluded arXiv records using HTTP, versionless `id_list`
requests rather than the verifier-derived HTTPS request containing the exact
versioned identifier. `a052` is a Crossref bibliographic search for an
exclusion, and `a053` is an arXiv title search for an exclusion; neither has a
canonical exact-identifier endpoint under its declared resolver kind.

The direct repository check fails first with:

```text
E_IDENTIFIER_LOG_INVALID: identifier attempt does not use the canonical resolver endpoint: a001
```

## Permitted use

The return may be used as:

- a bounded literature-discovery and positioning input;
- a source of candidate identifiers for independent Codex verification;
- an exact-input blind review of the v0.9.4 PDF and supplement;
- a major-revision agenda.

It may not be used as:

- a compliant Operon certification;
- evidence that the release gate passed;
- novelty, priority, exhaustive-coverage, or correctness certification;
- authorization for a public release.

The nine major findings remain substantive review inputs even though the
return failed its machine contract. A later manuscript revision must
disposition them on their merits. Any next certifying run must return a fresh
closed bundle, use the exact file-open schema, emit canonical identifier
attempts, validate against the repository-owned raw gate before attestation,
and bind the exact revised PDF and supplement.
