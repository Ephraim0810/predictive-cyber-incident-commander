# T08 — Existing autonomous cyber-response systems

**Assigned agent:** Agent-T08  
**Wave:** 3  
**Depends on:** T05 correlation interface  
**Defensive boundary:** Evaluate described systems and simulated response only. No real account, endpoint, network, cloud, or email action is permitted.

## Decision this task informs

Set the project’s automation boundary: what is recommendation-only, what could be safely simulated, what requires human approval, and what should be out of scope.

## Research questions

1. Which response capabilities are documented for modern endpoint/XDR/SOAR platforms, and under what confidence/approval conditions?
2. How do research systems frame containment, recovery, analyst-in-the-loop review, rollback, and safety constraints?
3. What evidence exists for response efficacy, false containment harm, explainability, and adoption barriers?
4. Which claimed autonomy is actually rule automation rather than adaptive decision-making?

## Required research work

- Compare at least five systems/approaches across commercial, open-source, standards guidance, and academic prototypes. Use first-party technical sources for product capabilities.
- Create `response_capability_matrix.csv`: trigger, evidence required, action, approval, rollback, blast radius, audit trail, documented limitations, and source.
- Write `automation_boundary_policy.md` defining Level 0 observe, Level 1 recommend, Level 2 human-approved simulated action, and prohibited live execution. Recommend a level for the project with evidence.
- Extract at least six response failure/safety cases from credible sources and translate them into testable safeguards.

## Required TensorFlow/Keras experiment

If data support it, train a small `tf.keras` confidence-calibration or selective-prediction model that chooses **recommend / abstain** from incident evidence features. Compare naive fixed confidence threshold with calibrated/abstaining policy, reporting coverage, error rate among recommendations, and unsafe-recommendation rate on synthetic scenarios. Otherwise, create a deterministic simulated policy test suite and document that neural learning would be unjustified.

## Deliverables

- `sources.csv`, `claim_ledger.csv`, `literature_review.md`, `response_capability_matrix.csv`, `automation_boundary_policy.md`, `safeguard_test_cases.md`.
- `experiments/EXP-T08-01/` or a documented inapplicability decision and deterministic safety test results.
- `handoff_packet.md` for T09–T12: recommended autonomy level, mandatory safeguards, evidence limits.

## Acceptance checks

- All actions remain simulated/recommendation-only.
- Product claims state their documented conditions and version/date.
- The policy includes abstention, audit logging, and human override.
