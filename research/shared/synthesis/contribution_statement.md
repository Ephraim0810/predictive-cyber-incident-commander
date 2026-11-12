# Contribution statement

## Recommended title

**An Auditable Quality-Shift Benchmark for Guarded Cyber-Incident Recommendations in Synthetic Telemetry**

## One technical contribution

The contribution is a reproducible, local benchmark that couples a schema-faithful evidence-quality snapshot to a transparent, externally guarded recommendation reference. It measures how a TensorFlow/Keras *adviser* changes raw recommendations under a declared chronological evidence-quality shift, while preserving a separate audit of the deterministic guard's final output.

## Falsifiable hypothesis

On held-out chronological fictional case groups with increased quality failures, the quality-aware Keras adviser will reduce raw guard overrides by at least 0.05 relative to its no-quality ablation, without a nonzero final unsafe rate.

## Baseline, result and negative-result interpretation

- Baseline: T09 transparent formula plus the same external guard.
- Experiment: `EXP-T12-01`, seeds 7/19/42, chronological whole-case 70/15/15 split, quality-aware model versus no-quality ablation.
- Preliminary result: 0.000 ± 0.000 raw overrides for quality-aware versus 0.086 ± 0.077 for no-quality; final unsafe rate was 0 in both conditions because the guard remains binding.
- Falsification: reject the adviser if override reduction is below 0.05 or any final unsafe rate occurs. A pass does not promote the adviser above the formula or establish operational value; low coverage and fictional labels remain material limitations.

## Differentiation

The work does not recreate product-specific correlation, approval or automation features documented by Microsoft Defender XDR, Elastic or Splunk. It also does not claim a new graph detector or cyber-RL controller: T07 is shift-brittle, T06's neural predictor loses to a simple baseline, and T11 is a formal no-go. The narrow novelty is the raw-versus-guarded quality-shift audit with explicit data/label limits. See CLM-T12-001–005 and CLM-T12-008.

