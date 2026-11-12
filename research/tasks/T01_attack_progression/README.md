# T01 — How cyberattacks progress through enterprise systems

**Assigned agent:** Agent-T01  
**Wave:** 1  
**Handoff ID:** HOF-T01-v1  
**Defensive boundary:** Study public incident reports and safe simulations only. Do not reproduce intrusion steps or create operational attack tooling.

## Decision this task informs

Define a realistic but abstract incident-state model: what phases occur, what signals mark phase transitions, which paths are common versus exceptional, and which stages can be predicted early enough to matter.

## Research questions

1. What high-level paths recur across enterprise ransomware, credential abuse, cloud-account compromise, and insider-like misuse?
2. Which stages are observable in endpoint, identity, network, cloud, email, and application telemetry?
3. Where do real incidents branch, loop, or end without impact?
4. Which common diagrams are pedagogical simplifications rather than evidence about actual order or timing?

## Required research work

- Conduct a deep web literature review: original incident reports, CISA/NIST guidance, MITRE resources, vendor post-incident analyses, and peer-reviewed studies. Start broad, then trace citations backward to primary evidence.
- Build a `phase_taxonomy.md` that separates **tactic**, **technique**, **event**, **asset**, **objective**, and **business impact**.
- Extract at least 12 safely described incident narratives into `incident_sequence_table.csv`; use phase-level labels, observed data sources, uncertainty, and public citation—not operational commands or payload detail.
- Compare at least three competing models of attack progression (linear kill-chain, ATT&CK tactic sequence, and graph/state-transition view). Explicitly record where each fails.

## Required TensorFlow/Keras experiment

Create a small **synthetic, non-operational incident-stream generator** with phase labels. Train a `tf.keras` GRU or LSTM next-phase classifier on sequences of benign abstract event types (for example `identity_alert`, `endpoint_alert`, `network_alert`) and compare it with a majority/Markov baseline. Run an ablation removing event timing and another removing asset context. This experiment tests whether sequence context can recover phase transitions; it does not demonstrate real-world prediction.

Use chronological episode splits, seeds 7/19/42, macro-F1, calibration, and event-prefix accuracy curves. Explain every synthetic-generating assumption and do not present synthetic results as evidence of attacker behaviour.

## Deliverables

- `sources.csv`, `claim_ledger.csv`, `literature_review.md`, `phase_taxonomy.md`, `incident_sequence_table.csv`.
- `experiments/EXP-T01-01/` meeting all master experiment standards.
- `handoff_packet.md`: five findings, limitations, recommended state vocabulary, and data fields needed by T02/T06/T07/T09.

## Acceptance checks

- At least 15 registered sources; at least 12 incident sequences have traceable primary citations.
- The taxonomy states unknown/ambiguous transitions rather than forcing a label.
- The experiment is reproducible and clearly labelled synthetic.
