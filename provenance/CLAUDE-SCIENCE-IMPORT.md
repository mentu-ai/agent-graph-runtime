# Claude Science import record

**Captured:** 2026-07-26  
**Purpose:** preserve what the rate-limited Claude Science session completed
without treating its unfinished work as paper evidence.

## External inputs

| Input | SHA-256 | Size | Repository disposition |
|---|---|---:|---|
| `d3283886_2026-07-26T16-46-53.json` | `ac45dd357e0df394efdf667018f18c301496b2ee1570cf18746a67c4082e467f` | 1,219,993 bytes | Remains outside Git |
| downloaded `SOURCE-MAP.md` | `d33863ec731769bab0cd0118ba9cdd293f1535f189147eec4b3f08917fb33da5` | 13,323 bytes | Reconciled into the repository-owned source map |

## Session result

- Export version: `1.0`
- Conversation: `Repository Provenance and Source Mapping`
- Root frame: `d3283886-e9f2-454b-9cad-8d8216264f9b`
- Project: `proj_c3deea228944`
- Frames: 6
- Root status: failed
- Failure: HTTP 429, `rate_limit`
- Reset reported by the service: 2026-07-28 21:00 CST
- Usage reported by the export: 11,228,003 input tokens; 132,262 output
  tokens; USD 15.0148

The root had saved source mapping and was waiting for two prior-art delegates.
Both delegates then failed under the same usage limit.

## Completed artifacts

1. `SOURCE-MAP.md`
   - artifact id `aedaa406-c713-4802-93cf-bcc43a193b4f`
   - version id `5a4d8901-0306-4435-b67b-aea1e0c4493d`
2. `ground_truth.json`
   - artifact id `d4e356f3-f804-4833-9d18-fe1c1b276cfe`
   - version id `16ad5a50-6dc2-43ab-b3ca-6d76500d513a`
   - not downloaded; the transient artifact is unavailable

Three REVIEWER frames completed and returned passing findings over the
source/provenance/pilot assertions. Their quoted checks remain useful audit
context, but they do not recreate the unavailable `ground_truth.json`.

## Not completed

No literature matrix, verified prior-art registry, formal model, claims ledger,
manuscript, figures, matched-study protocol, integrity sweep, or final handoff
was produced.

The failed delegate frames contain broad search activity. Those records are
query seeds only. No candidate from those partial searches may enter the paper
without fresh source and identifier verification.

## Reconciliation rule

The downloaded map is a dated reconnaissance artifact, not source truth. The
repository-owned `SOURCE-MAP.md` records corrections and current provenance.

