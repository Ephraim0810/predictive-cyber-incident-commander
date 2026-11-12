# T09 — How defensive actions should be chosen

**Assigned agent:** Agent-T09  
**Wave:** 4  
**Depends on:** T06 prediction, T08 automation boundary, T10 cost model; use T05/T07 interfaces  
**Defensive boundary:** Select among simulated/recommended defensive actions only; no action adapter may affect real systems.

## Decision this task informs

Specify an explainable, constrained policy that converts uncertain incident evidence and predictions into safe action recommendations.

## Research questions

1. What decision frameworks are used for containment under uncertainty: playbooks, risk matrices, multi-criteria decision analysis, Bayesian decision theory, constrained optimisation, or human approval?
2. Which inputs should be separated: evidence confidence, predicted impact, asset criticality, action reversibility, operational disruption, and uncertainty?
3. How should policy reject, defer, or request more evidence rather than overreact?
4. What metrics show a policy is safer than a severity-only rule?

## Required research work

- Review standards/guidance and academic work on incident triage, response playbooks, risk/utility, and human factors.
- Define `action_space_contract.md` with a deliberately small simulated action set: `monitor`, `request_more_evidence`, `recommend_step_up_auth`, `recommend_session_review`, `recommend_host_isolation_review`, `recommend_network_containment_review`. Define prerequisites, reversibility, escalation, and prohibited outputs.
- Create `decision_policy_spec.md` with inputs, guards, scoring/utility formula, abstention rule, explanation schema, human approval requirement, and audit record.
- Make `scenario_suite.csv` with at least 20 synthetic cases spanning uncertainty, criticality, false positives, conflicting signals, and safety constraints.

## Required TensorFlow/Keras experiment

Compare a transparent rules/utility baseline with a `tf.keras` multi-output model that predicts simulated action utility/risk from incident-state features. The Keras model can assist ranking but must be constrained by deterministic safety guards. Evaluate regret versus known simulated utility, unsafe recommendation rate, abstention quality, action stability under small input perturbations, and explanation completeness. Include an ablation without cost/reversibility features.

## Deliverables

- `sources.csv`, `claim_ledger.csv`, `literature_review.md`, `action_space_contract.md`, `decision_policy_spec.md`, `scenario_suite.csv`, testable safety guards.
- `experiments/EXP-T09-01/` with baseline comparison, perturbation tests, and audit records.
- `handoff_packet.md` for T11/T12: recommended policy interface, guardrails, performance/limitations.

## Acceptance checks

- Every action is a recommendation or sandbox simulation and has prerequisites and a rollback/approval statement.
- A high prediction score alone can never override deterministic safety constraints.
- Results report unsafe recommendations, not only average reward/accuracy.
