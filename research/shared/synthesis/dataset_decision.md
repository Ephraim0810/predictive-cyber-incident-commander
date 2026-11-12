# Dataset decision

## Decision

Use a **schema-faithful fictional telemetry and case generator** for the initial benchmark. Treat the Windows-APT v3 public route as conditional and metadata-only until its raw acquisition audit passes. Do not manufacture response-effect labels from public incident telemetry.

| Candidate/route | Temporal suitability | Licence/availability state | Label suitability | Decision |
|---|---|---|---|---|
| OTRF/Windows-APT proxy evidence | Timestamped host-event/scenario context; T04 shows random split leakage risk | Raw material removed; acquisition/terms/checksum audit still required | No per-event ATT&CK truth or response-effect label established | Conditional public route for future telemetry-only evaluation; not the initial action-label source. |
| LANL unified data | Useful time and host/network relationships | Public source, but predictive-label route must be defended | No accepted response-effect label route | Not selected. |
| UNSW-NB15 | Predominantly network-flow benchmark | Academically usable | Does not meet multi-source incident/response objective | Not selected. |
| CSE-CIC-IDS2018 | Potential traffic/log time fields | Licence and time-field audit required | Not accepted for response labels | Not selected. |
| Schema-faithful fictional cases | Explicit chronological whole-case splits and controllable quality shift | Locally generated; no raw third-party data | Labels/utilities are clearly fictional and limited to protocol testing | **Selected for EXP-T12-01 only.** |

## Mandatory gates for any public extension

1. Record licence/terms, source URL, acquisition date, file checksum and row schema.
2. Preserve occurrence and observation timestamps, immutable provenance and whole-case/group boundaries.
3. Demonstrate that labels predate each prediction decision and do not encode post-incident knowledge.
4. Keep action outcomes, approval, harm, rollback and cost labels unavailable unless independently adjudicated in a governed cyber range.
5. Report chronological and group-disjoint splits; do not merge them with random-split figures.

This decision follows CLM-T04-001–005, CLM-T06-003, CLM-T12-003 and `EXP-T04-01`.

