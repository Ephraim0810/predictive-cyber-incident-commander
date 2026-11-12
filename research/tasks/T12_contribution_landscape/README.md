# T12 — Select a meaningful technical contribution

**Assigned agent:** Agent-T12  
**Wave:** 5  
**Depends on:** Accepted packets from T01–T11  
**Defensive boundary:** Propose research/simulation contributions only; do not claim parity with or replacement of production security products.

## Decision this task informs

Choose one narrow, falsifiable technical contribution that is not merely a reimplementation of commercial SIEM/XDR/SOAR functionality and has an evaluable TensorFlow/Keras-based research method.

## Research questions

1. Which relevant commercial capabilities and published methods already address detection, correlation, prediction, graphing, and response recommendation?
2. What gaps remain after considering data availability, simulation fidelity, safety, evaluation, and student-scale compute?
3. Which candidate contribution can be falsified against clear baselines and contribute evidence even if the model loses?
4. Which attractive ideas must be rejected because they duplicate existing functionality, need unavailable labels, or invite unsafe claims?

## Required research work

- Read every accepted task packet and audit its claims against original sources. Do not copy a conclusion without checking its conditions.
- Conduct a focused, current landscape search across peer-reviewed work, official product technical documentation, standards, and open tools. Build `capability_landscape.csv` with capability, provider/paper, inputs, outputs, automation boundary, evaluation evidence, limitations, and source IDs.
- Propose at least three candidate contributions in `contribution_options.md`. For each: problem statement, novelty relative to named prior work/products, data route, TensorFlow/Keras method, baseline, metrics, risks, and kill criteria.
- Choose one in `contribution_decision_record.md`; include a one-sentence falsifiable hypothesis and an explicit rejected-alternatives section.

## Required TensorFlow/Keras experiment

Run a small feasibility experiment only for the selected contribution, using the accepted dataset/interface and the baseline mandated by T06/T09/T11. It must test the contribution’s core claim, include a simple ablation, and be labelled preliminary. If upstream evidence shows no defensible contribution can be tested, do not invent one: document the gap and propose a scoped research extension.

## Deliverables

- `sources.csv`, `claim_ledger.csv`, `capability_landscape.csv`, `contribution_options.md`, `contribution_decision_record.md`.
- `experiments/EXP-T12-01/` if feasible, or an evidence-based no-experiment decision.
- Final `handoff_packet.md` to the synthesis lead, including the recommended project title, one technical contribution, evaluation protocol, safety boundary, and architecture requirements.

## Acceptance checks

- The selected contribution is differentiated against at least three named prior systems/papers using sources, not intuition.
- The hypothesis is falsifiable and has a baseline, metric, and negative-result interpretation.
- The recommendation preserves the human-approved, simulation-only response boundary.
