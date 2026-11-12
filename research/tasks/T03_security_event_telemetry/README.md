# T03 — What security-event data looks like and what it can prove

**Assigned agent:** Agent-T03  
**Wave:** 1  
**Defensive boundary:** Use schemas, sample logs, and authorised/public data only. Redact sensitive identifiers in examples.

## Decision this task informs

Specify a minimal, cross-source event contract for the simulated organisation and identify what cannot be inferred from telemetry alone.

## Research questions

1. What useful fields appear in endpoint, identity, DNS/network, cloud audit, email, and application logs?
2. How do common standards and platforms represent time, actor, asset, process, parent process, network flow, authentication result, and alert provenance?
3. Which normalisation choices preserve event order and asset relationships?
4. What data-quality failures—clock drift, missing fields, duplicate alerts, sampling, NAT, identity merges—damage correlation or prediction?

## Required research work

- Review official schema documentation (for example OCSF, ECS, OpenTelemetry security events, Windows/Linux/cloud audit documentation where relevant) and empirical telemetry papers.
- Design `canonical_event_schema.json` with required, optional, derived, and prohibited fields. Include definitions, types, examples, nullable policy, timezone rule, and privacy notes.
- Create `telemetry_coverage_matrix.csv`: phase/label from T01/T02 × data source × observable fields × confidence × likely false-positive/false-negative mechanism.
- Construct at least six safe, fictitious, schema-valid sample events in `sample_events.jsonl`, then validate them with a small schema test.

## Required TensorFlow/Keras experiment

Create a synthetic-stream robustness experiment. Encode canonical events into fixed feature vectors; train a small `tf.keras` autoencoder or classifier for a defensively defined anomaly/phase proxy. Systematically drop one source type, perturb timestamps, and duplicate events. Report how performance and calibration change. This tests schema resilience, not intrusion detection effectiveness.

## Deliverables

- `sources.csv`, `claim_ledger.csv`, `literature_review.md`, `canonical_event_schema.json`, `schema_dictionary.md`, `telemetry_coverage_matrix.csv`, `sample_events.jsonl` and validation output.
- `experiments/EXP-T03-01/` with perturbation settings and results.
- `handoff_packet.md` for T04/T05/T06: stable schema version, minimum event fields, and known blind spots.

## Acceptance checks

- Schema validates the samples and preserves UTC timestamp plus source provenance.
- Sensitive content is not included in sample data.
- Observability limitations are explicit instead of silently filled with labels.
