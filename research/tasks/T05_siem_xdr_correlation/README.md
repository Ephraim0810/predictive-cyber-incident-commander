# T05 — How SIEM/XDR systems correlate alerts

**Assigned agent:** Agent-T05  
**Wave:** 2  
**Depends on:** T03 canonical schema  
**Defensive boundary:** Study documented correlation and build offline replay logic only; no production integrations or automated controls.

## Decision this task informs

Define the non-neural correlation layer that turns raw events into evidence-bearing incident candidates for later prediction and response ranking.

## Research questions

1. How do contemporary SIEM/XDR products describe entity, temporal, rule, graph, and alert correlation?
2. What is verified product capability versus marketing language?
3. What open research methods produce incident clusters, and how are precision, recall, analyst workload, and latency evaluated?
4. Which correlation features are appropriate inputs to a Keras sequence model?

## Required research work

- Compare at least four documented systems and at least six academic/open approaches. Use official technical documentation and note version/date.
- Write `correlation_pattern_catalog.md` covering temporal windows, shared entities, causal/evidence links, alert suppression, deduplication, confidence aggregation, and provenance.
- Implement a small transparent offline correlator for T03-safe events: rules for same entity, bounded time window, and shared asset/identity. Generate `incident_candidates.jsonl` with source-event IDs and rationale.
- Build an analyst-impact table: false merge, split incident, duplicate, stale evidence, and missing telemetry failure cases.

## Required TensorFlow/Keras experiment

Use labelled synthetic episodes or approved public data to compare (a) raw event-sequence model and (b) the same Keras model augmented with correlation-cluster features. Use a fixed split and measure macro-F1, calibration, number of candidate incidents, and replay latency. Do not claim a vendor-equivalent XDR result.

## Deliverables

- `sources.csv`, `claim_ledger.csv`, `literature_review.md`, `correlation_pattern_catalog.md`, `correlator_spec.md`, and safe correlator code/tests.
- `incident_candidates.jsonl`, `analyst_impact_matrix.csv`, `experiments/EXP-T05-01/`.
- `handoff_packet.md` for T06/T08/T09: candidate incident interface, evidence fields, limitations.

## Acceptance checks

- Every incident candidate records the underlying event IDs and correlation rationale.
- The correlator has test cases for duplicate, temporal-boundary, and entity-collision behaviour.
- Product claims are tied to official documentation rather than product pages alone.
