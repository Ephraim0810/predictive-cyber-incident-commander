# Multi-Agent Research Program Implementation Plan

**Goal:** Produce decision-grade, reproducible evidence for a predictive cyber-incident commander before product architecture is selected.

**Architecture:** Twelve bounded research tasks create independent handoff packets in `work/`; the master README defines their interfaces, waves, and acceptance gates. A synthesis lead consumes only reviewed packets and creates the architecture decision record.

**Tech stack:** Public web research; Python; TensorFlow/Keras for neural experiments; pandas/NumPy for transparent preprocessing; local/synthetic telemetry only.

**Spec:** `../../README.md`

## Execution checklist

- [ ] Create `work/Txx_<slug>/` for each assigned task.
- [ ] Copy the three shared templates into that task folder before research begins.
- [ ] Record sources and evidence claims as they are discovered, rather than backfilling citations.
- [ ] Freeze the dataset split before model tuning and record its checksum/licence.
- [ ] Run baseline, proposed model, and at least one ablation/comparison with the declared seeds.
- [ ] Write the handoff packet; pass the task review gate; then expose it to downstream tasks.
- [ ] Run the wave, evidence, reproduction, architecture, and contribution gates in `README.md`.

## Review checklist

- [ ] The task stayed within the defensive/synthetic boundary.
- [ ] Findings distinguish evidence, inference, and hypothesis.
- [ ] Citations are primary where possible and traceable in the source registry.
- [ ] The experiment has a documented split, seed set, metrics, and limitations.
- [ ] No downstream recommendation is based on an unverified handoff.
