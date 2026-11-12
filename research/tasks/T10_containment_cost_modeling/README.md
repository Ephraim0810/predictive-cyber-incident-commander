# T10 — Quantifying the business cost of containment

**Assigned agent:** Agent-T10  
**Wave:** 3  
**Depends on:** T01 phases and T05 incident candidates  
**Defensive boundary:** Use hypothetical organisation assumptions; do not use private business data without explicit written permission.

## Decision this task informs

Create a transparent, parameterised utility model that weighs expected incident harm against the disruption caused by a defensive recommendation.

## Research questions

1. Which financial, operational, safety, legal, reputation, and recovery dimensions are used in incident-impact models?
2. How do asset criticality, user roles, time, action reversibility, and uncertainty change containment cost?
3. Which quantities can be responsibly estimated in a student-scale simulated project, and which must remain scenario parameters?
4. How should sensitivity analysis prevent false precision?

## Required research work

- Review incident-cost guidance, cyber-risk methodologies, business-continuity/impact-analysis guidance, and decision-under-uncertainty research. Separate empirical values from illustrative assumptions.
- Write `cost_model_spec.md` defining a normalised 0–100 utility scale or transparent symbolic model, variables, units, ranges, sources, and non-monetary constraints.
- Build `assumption_register.csv` with owner, rationale, evidence, low/base/high range, and expiry/review status.
- Create at least 12 fictional business scenarios: critical service, low-criticality endpoint, privileged identity, false positive, high uncertainty, and action reversibility variants.

## Required TensorFlow/Keras experiment

Run a sensitivity experiment with the T09-safe action space. A `tf.keras` regression model may approximate a simulated cost surface, but it must be compared with the transparent formula/rule baseline. Vary criticality, predicted harm, confidence, action duration, and reversibility; report rank reversals, uncertainty intervals, and where approximation is less trustworthy than the formula. Do not infer monetary loss from arbitrary labels.

## Deliverables

- `sources.csv`, `claim_ledger.csv`, `literature_review.md`, `cost_model_spec.md`, `assumption_register.csv`, `scenario_costs.csv`, sensitivity figures.
- `experiments/EXP-T10-01/` or a documented reason no neural approximation is useful.
- `handoff_packet.md` for T09/T11/T12: model interface, scenario parameters, dominant sensitivities, unsupported quantities.

## Acceptance checks

- Assumptions and evidence are visibly distinct.
- The model supports ranges/sensitivity rather than a single authoritative-looking dollar value.
- Every cost recommendation stays within a fictitious/simulated setting.
