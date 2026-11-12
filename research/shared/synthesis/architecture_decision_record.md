# Architecture decision record — guarded research benchmark

## Chosen pipeline

`T03 telemetry contract → T05 conservative correlation → evidence-quality snapshot → transparent T09 reference + optional T12 Keras adviser → external deterministic guard → recommend/abstain audit record`

The interface carries dual timestamps, source provenance, nonblank scoped anchors, quality/missingness indicators, correlation evidence IDs and explicit unknowns. A graph view may be added only as a time-bounded evidence graph, with observed and predicted nodes separated.

## Baselines and metrics

- Authority baseline: T09 transparent guarded formula.
- Adviser: TensorFlow/Keras quality-aware scorer, tested only against a no-quality ablation on fictional cases.
- Required metrics: raw guard-override rate, final unsafe rate, agreement with authored reference, non-abstaining coverage, mean/sample SD for seeds 7/19/42, and chronology/group-split integrity.
- Rejected model choices: T06 neural next-stage predictor (baseline loss), T11 offline RL (no-go thresholds failed), a full exploitability graph (missing required factual inputs), and a commercial SIEM/XDR/SOAR recreation (not differentiated).

## Safety and human boundary

All model outputs are recommendations or abstentions. No output may call a live service, change a configuration, isolate a host, contain a network, or approve an identity/data action. The guard is external to learned scores/rewards and checks provenance, anchor, freshness, contradictions, duplicate-only context, rollback statement and named-human approval. The fixed action strings are `monitor`, `request_more_evidence`, `recommend_step_up_auth`, `recommend_session_review`, `recommend_host_isolation_review`, and `recommend_network_containment_review`; the last is always guard-rejected for the initial profile.

## Evidence basis

CLM-T03-001–005; CLM-T05-001–005; CLM-T07-003–005; CLM-T08-003–005; CLM-T09-002–005; CLM-T10-003–005; CLM-T11-005; CLM-T12-002, CLM-T12-005 and CLM-T12-008.

