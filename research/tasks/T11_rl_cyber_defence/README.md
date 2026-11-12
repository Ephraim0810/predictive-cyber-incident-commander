# T11 — Reinforcement learning in autonomous cyber defence

**Assigned agent:** Agent-T11  
**Wave:** 4  
**Depends on:** T04 data route, T09 action policy, T10 cost model  
**Defensive boundary:** Evaluate offline/simulated agents only. No online learning, exploration, or live response deployment.

## Decision this task informs

Determine whether offline/simulated reinforcement learning offers a meaningful, safe contribution beyond constrained supervised policy ranking for the initial project.

## Research questions

1. What cyber-defence RL environments, state/action abstractions, reward functions, and benchmarks have been published?
2. How do reward hacking, simulator mismatch, sparse reward, non-stationarity, unsafe exploration, and partial observability affect validity?
3. Which algorithms and claims are actually reproducible under modest compute and TensorFlow/Keras constraints?
4. What evidence threshold justifies including RL rather than treating it as future work?

## Required research work

- Systematically review at least 15 RL-defence papers/environment documents. Create `rl_evidence_matrix.csv` with environment, observation, actions, reward, algorithm, baseline, evaluation, reproducibility, safety limits, and reported failure mode.
- Write `rl_feasibility_decision.md` comparing: no RL, contextual-bandit-like offline ranking, and simulated sequential RL. Give an explicit go/no-go recommendation.
- Define `offline_rl_safety_protocol.md`: no live calls, fixed action set from T09, deterministic safety shield, held-out scenario evaluation, seed reporting, and simulator disclosure.

## Required TensorFlow/Keras experiment

Build a small simulated incident-response environment from T09/T10 scenarios. Implement either a Keras DQN for the fixed, safe action set or a supervised fitted-Q-style approximation; no external RL framework is required. Compare it with the T09 rule/utility baseline over held-out scenario trajectories. Measure cumulative simulated utility, unsafe-action attempts blocked by the shield, policy stability across seeds, and generalisation under changed cost parameters. If RL cannot beat or safely match the baseline, state that it is not selected.

## Deliverables

- `sources.csv`, `claim_ledger.csv`, `literature_review.md`, `rl_evidence_matrix.csv`, `rl_feasibility_decision.md`, `offline_rl_safety_protocol.md`.
- `experiments/EXP-T11-01/` with environment spec, reward disclosure, baseline, results, and failure analysis.
- `handoff_packet.md` for T12: go/no-go result, reproducibility status, safety risks, recommended scope.

## Acceptance checks

- No result is described as autonomous real-world defence.
- Reward, transition assumptions, and safety shield are fully disclosed.
- A weaker/negative RL outcome leads to a clear no-go recommendation rather than reward tuning until a desired conclusion appears.
