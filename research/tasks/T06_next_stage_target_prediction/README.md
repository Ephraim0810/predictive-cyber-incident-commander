# T06 — Next-stage and next-target prediction

**Assigned agent:** Agent-T06  
**Wave:** 3  
**Depends on:** Accepted T01–T05 and T07 packets  
**Defensive boundary:** Predict from offline benign/simulated/public telemetry. Do not create target-selection tools for use against systems.

## Decision this task informs

Choose a prediction target, model family, and evaluation protocol that make a defensible claim about useful early warning.

## Research questions

1. How do studies define next action, next tactic, next alert, next host, or next critical asset?
2. Which inputs are available at decision time, and how do papers prevent hindsight leakage?
3. How do sequence, graph, and hybrid models compare when data are sparse, imbalanced, or partially observed?
4. Which performance level and lead time would be operationally meaningful in a simulated organisation?

## Required research work

- Systematically review at least 15 studies, grouping them by prediction target, data source, model, split method, metrics, and limitations in `prediction_literature_matrix.csv`.
- Define `prediction_target_contract.md`: unit of prediction, observation cutoff, horizon, label availability, abstention policy, top-k interpretation, and human-facing explanation requirement.
- Review reported results sceptically: flag random splits, target leakage, unsupported latency claims, and incomparable metrics.

## Required TensorFlow/Keras experiment

Implement three models on the T04-selected route: a frequency/Markov or logistic baseline, a `tf.keras` GRU/LSTM sequence model, and a Keras model using correlated/graph-derived features from T05/T07. Use fixed chronological splits, seeds 7/19/42, prefix-length evaluation, top-1/top-3 recall, macro-F1, Brier score/ECE, and measured replay latency. Perform at least two ablations: no timing/context, and no correlation/graph features. Report failures by class and abstention threshold.

## Deliverables

- `sources.csv`, `claim_ledger.csv`, `literature_review.md`, `prediction_literature_matrix.csv`, `prediction_target_contract.md`.
- `experiments/EXP-T06-01/` with comparison table, calibration plot, latency log, and error analysis.
- `handoff_packet.md` for T09/T12: selected target/model recommendation, evidence of benefit, uncertainty and limits.

## Acceptance checks

- Train/test split respects information available before the forecast horizon.
- The baseline is reported alongside neural models.
- A claim of usefulness includes both predictive quality and lead-time/latency evidence.
