# T07 — Attack graphs and time-aware attack-path representations

**Assigned agent:** Agent-T07  
**Wave:** 2  
**Depends on:** T01 incident states; T02 label contract  
**Defensive boundary:** Model simulated/public organisational assets and relations only. Do not use the work to enumerate or target a real network.

## Decision this task informs

Choose whether—and how—a time-aware graph should represent assets, identities, alerts, ATT&CK labels, and evidence links in the prototype.

## Research questions

1. What distinguishes attack graphs, attack paths, provenance graphs, knowledge graphs, and temporal event graphs?
2. What assumptions do graph methods make about asset inventory, vulnerabilities, credentials, reachability, and attack preconditions?
3. How can a graph express uncertainty and alternative paths without presenting speculation as fact?
4. What graph representation is feasible from T03 telemetry and useful to T06/T09?

## Required research work

- Review foundational attack-graph work, contemporary temporal/provenance/graph-learning work, and at least two practical defensive implementations.
- Produce `graph_representation_comparison.md` covering nodes, edges, direction, time, evidence/provenance, uncertainty, update mechanism, scalability, and assumptions.
- Define `graph_interface_contract.md`: node/edge schemas, IDs, timestamps, confidence, source-event links, and graph update rules compatible with T03/T05.
- Create a small **fictional** organisation graph plus two abstract incident paths in `synthetic_org_graph.json`; visualisation must label predicted edges separately from observed evidence.

## Required TensorFlow/Keras experiment

Do not require a specialised graph-learning package. Derive fixed-size, explainable graph-context features (for example incident-to-asset relation counts, degree buckets, asset criticality tier, evidence recency) and compare a `tf.keras` dense/sequence model with and without those features for T01/T04-safe prediction labels. Report whether graph context helps, its cost, and when it harms generalisation.

## Deliverables

- `sources.csv`, `claim_ledger.csv`, `literature_review.md`, `graph_representation_comparison.md`, `graph_interface_contract.md`, `synthetic_org_graph.json`.
- `experiments/EXP-T07-01/` and a clearly labelled observed-versus-predicted graph figure.
- `handoff_packet.md` for T06/T09/T12: recommended graph scope, required inventory assumptions, evidence/provenance policy.

## Acceptance checks

- No graph node/edge implies a real target or exploitability without direct supporting evidence.
- The chosen design can update from the T03/T05 interfaces without hidden data fields.
- The task records why a full GNN is accepted or rejected for the first prototype.
