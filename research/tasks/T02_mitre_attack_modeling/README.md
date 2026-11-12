# T02 — MITRE ATT&CK tactics and techniques for realistic sequence modelling

**Assigned agent:** Agent-T02  
**Wave:** 1  
**Depends on:** T01 vocabulary reconciliation at the Wave 1 gate  
**Defensive boundary:** Map defensive telemetry to ATT&CK; do not translate techniques into actionable intrusion instructions.

## Decision this task informs

Choose an ATT&CK-aligned label space that is useful for prediction without treating ATT&CK as a guaranteed chronological attack script.

## Research questions

1. What ATT&CK objects, versions, data sources, and relationships are relevant to enterprise telemetry modelling?
2. How have researchers converted multi-label technique evidence into sequence labels, and what information is lost?
3. Which tactic/technique pairs are overly broad, rare, co-occurring, or difficult to observe?
4. How should uncertainty, multiple concurrent tactics, and platform differences be represented?

## Required research work

- Read official ATT&CK documentation, STIX/TAXII or ATT&CK data representations where relevant, technique detection guidance, and at least six sequence-modelling papers.
- Produce `attack_label_contract.md`: exact proposed fields, version-pinning method, mapping granularity, `unknown`/`other` policy, and examples at safe semantic level.
- Build `mapping_quality_matrix.csv` that maps T01 phase states to ATT&CK labels, candidate telemetry evidence, ambiguity, and expected observability.
- Audit three published ATT&CK-labelled datasets/studies for label provenance, temporal validity, class imbalance, and label leakage.

## Required TensorFlow/Keras experiment

Using only a licensed public/synthetic label sequence, compare two `tf.keras` formulations: (a) next-tactic multiclass prediction and (b) next-technique multi-label sigmoid prediction. Use identical event prefixes and report exact-match, macro-F1, top-k recall, label-frequency baseline, and calibration. Include an ablation that collapses techniques to tactics. The result is a label-design decision, not a general ATT&CK benchmark.

## Deliverables

- `sources.csv`, `claim_ledger.csv`, `literature_review.md`, `attack_label_contract.md`, `mapping_quality_matrix.csv`, `dataset_label_audit.md`.
- `experiments/EXP-T02-01/` with pinned ATT&CK release and data checksum.
- `handoff_packet.md` for T03/T04/T06/T07: chosen label contract, ambiguities, and non-negotiable caveats.

## Acceptance checks

- No claim says ATT&CK prescribes a universal sequence.
- Each map entry distinguishes direct detection evidence from inferred technique.
- The task identifies a versioned label set a later experiment can reproduce.
