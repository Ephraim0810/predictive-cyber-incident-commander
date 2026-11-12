# Evidence matrix — accepted program synthesis

This matrix records the architecture decisions authorised by accepted handoffs only. A source/claim identifier is required for every decision; experiments are conditional on their fictional or audited data route.

| Architecture choice | Evidence and claim IDs | Decision and boundary |
|---|---|---|
| Incident-state representation | CLM-T01-001–005; CLM-T02-003–005 | Use a branching, uncertainty-aware incident-state view. ATT&CK mappings are evidential annotations, not automatic chronological truth. |
| ATT&CK versioning | CLM-T02-001–002 | Pin the ATT&CK release/checksum and retain a migration field; do not silently mix releases. |
| Telemetry contract | CLM-T03-001–005 | Require occurrence and observation timestamps, immutable provenance, scoped entity anchors, evidence IDs and explicit unknown fields. |
| Correlation | CLM-T05-001–005 | Correlate only via declared nonblank scoped anchors and time windows; preserve source events and never treat a vendor confidence score as authority. |
| Public-data route | CLM-T04-001–005; CLM-T06-003 | Use schema-faithful fictional data unless a public candidate passes raw-file, terms, provenance, row-label and group-split audits. |
| Evaluation splitting | CLM-T04-004; CLM-T06-001–005 | Use chronological, group-disjoint evaluation; do not pool random and temporal results or claim a generic context benefit. |
| Graph interface | CLM-T07-001–005 | Use only a time-bounded evidence graph with observed and predicted hypotheses separately styled. Do not construct an exploitability graph without asset/vulnerability/reachability evidence. |
| Prediction baseline | CLM-T06-001–005; EXP-T06-01 | Retain simple baselines, abstention and calibration. T06's neural variants did not justify promotion over the Markov baseline. |
| Response authority | CLM-T08-003–005; CLM-T09-003–005 | The system may recommend or abstain only. Deterministic provenance, freshness, anchor, contradiction, duplicate, rollback and named-human gates stay outside models. |
| Action vocabulary | CLM-T09-001–005; CLM-T11-005 | Use T09's six fixed recommendation strings; network-containment review is always guard-rejected in this profile. No executor or external connector is allowed. |
| Utility/cost model | CLM-T10-001–005 | Keep a transparent fictional 0–100 utility index and ranges. It is not currency; safety/legal/approval constraints are non-compensable gates. |
| Reinforcement learning | CLM-T11-001–005; EXP-T11-01 | No-go for initial implementation: T11 exceeded its regret threshold and missed its stability threshold under changed costs. No online exploration or policy deployment. |
| Selected technical contribution | CLM-T12-001–005; CLM-T12-008; EXP-T12-01 | Build an auditable quality-shift benchmark that reports raw-versus-guarded recommendation behaviour. It is a measurement protocol, not SIEM/XDR/SOAR parity. |

## Cross-task experimental evidence

- `EXP-T04-01`: random splitting materially exceeded chronological performance; the decision is to preserve temporal/group splits.
- `EXP-T06-01`: Markov macro-F1 (0.561 ± 0.039) exceeded raw GRU macro-F1 (0.198 ± 0.050); the neural predictor is not promoted.
- `EXP-T09-01`: the transparent formula had zero known-utility regret; guarded Keras had 0.0367 ± 0.0437 approximation regret and no authority to bypass guards.
- `EXP-T11-01`: shielded fitted-Q regret was 0.145 ± 0.028 (base) and 0.110 ± 0.040 (changed cost), with stability 0.806; all fail the declared no-go criteria. A fresh immutable `run_synthesis_repro` reproduced the saved metrics byte-for-byte (SHA-256 `34DED9366C622571091007086252A9765F349BD4FFE93E5B3A0DAD0920DB6284`).
- `EXP-T12-01`: quality-aware Keras had raw guard overrides 0.000 ± 0.000 versus 0.086 ± 0.077 for the no-quality ablation. Final unsafe rate was zero in both because the external guard, not the model, is binding.
