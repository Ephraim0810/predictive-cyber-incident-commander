# Predictive Cyber Incident Commander — Multi-Agent Research Program

## Purpose

This package coordinates the research phase for a proposed **defensive, simulated** system that observes security telemetry, detects an emerging incident, reconstructs its likely attack path, predicts the next stage or target, and recommends a proportionate containment action. It is a research program, not permission to scan, exploit, disrupt, or automate actions against real systems.

The program answers the twelve questions below before the implementation architecture is locked. Every task combines an internet-based evidence review with a reproducible, TensorFlow/Keras experiment where one can genuinely test its research claim. A task may conclude that a proposed model is unsuitable; negative results are valuable and must be preserved.

## Safety, ethics, and operating boundary

- Work only with public datasets, documented simulations, or locally generated **benign/synthetic** telemetry.
- Do not collect credentials, scan public targets, develop payloads, execute malware, bypass access controls, or connect automated response code to a live environment.
- Frame techniques using defensive detection, simulation, offline evaluation, and human-approved response recommendations.
- Handle public datasets according to their licence, terms, privacy notices, and any de-identification conditions. Record these in the source registry.
- A response experiment may rank simulated actions only. It must never call a firewall, endpoint, cloud, identity, or production API.

## Start here

1. Assign one agent to each task README in the table below. Give the agent this `README.md` and its assigned task file.
2. Each agent creates only files inside its own `work/Txx_<slug>/` folder, following the shared naming rules.
3. The agent researches the open web deeply, records evidence before making claims, runs its defined offline experiment (or records why an experiment is not appropriate), and produces the required deliverables.
4. At the end of each wave, run the review gate in **Synthesis protocol**. Do not treat a task as complete merely because it has prose.
5. The synthesis lead merges accepted findings into `shared/synthesis/` and produces the architecture decision record before any product build begins.

## Package structure

```text
Predictive_Cyber_Incident_Commander_Research_Program/
├── README.md                                 # this master operating manual
├── tasks/
│   ├── T01_attack_progression/README.md
│   ├── T02_mitre_attack_modeling/README.md
│   ├── T03_security_event_telemetry/README.md
│   ├── T04_public_temporal_datasets/README.md
│   ├── T05_siem_xdr_correlation/README.md
│   ├── T06_next_stage_target_prediction/README.md
│   ├── T07_attack_graphs/README.md
│   ├── T08_autonomous_response/README.md
│   ├── T09_defensive_action_selection/README.md
│   ├── T10_containment_cost_modeling/README.md
│   ├── T11_rl_cyber_defence/README.md
│   └── T12_contribution_landscape/README.md
└── shared/
    ├── governance/IMPLEMENTATION_PLAN.md
    ├── templates/SOURCE_REGISTRY_TEMPLATE.csv
    ├── templates/EXPERIMENT_CARD_TEMPLATE.md
    ├── templates/CLAIM_LEDGER_TEMPLATE.csv
    └── synthesis/README.md
```

`work/` is created by agents during execution and is intentionally not pre-populated. Do not put unreviewed task work into `shared/synthesis/`.

## Assignment, sequence, and dependencies

| Wave | Agent ID | Task file | Focus | Depends on | Handoff to |
|---|---|---|---|---|---|
| 1 | Agent-T01 | `tasks/T01_attack_progression/README.md` | Real attack progression | — | T02, T06, T07, T09 |
| 1 | Agent-T02 | `tasks/T02_mitre_attack_modeling/README.md` | ATT&CK-based sequence model | T01 findings when ready | T03, T04, T06, T07 |
| 1 | Agent-T03 | `tasks/T03_security_event_telemetry/README.md` | Event schemas and observability | — | T04, T05, T06 |
| 2 | Agent-T04 | `tasks/T04_public_temporal_datasets/README.md` | Dataset suitability audit | T02, T03 | T06, T11, T12 |
| 2 | Agent-T05 | `tasks/T05_siem_xdr_correlation/README.md` | Correlation baselines | T03 | T06, T08, T09 |
| 2 | Agent-T07 | `tasks/T07_attack_graphs/README.md` | Attack graph representations | T01, T02 | T06, T09, T12 |
| 3 | Agent-T06 | `tasks/T06_next_stage_target_prediction/README.md` | Predictive models | T01–T05, T07 | T09, T12 |
| 3 | Agent-T08 | `tasks/T08_autonomous_response/README.md` | Existing response systems | T05 | T09–T12 |
| 3 | Agent-T10 | `tasks/T10_containment_cost_modeling/README.md` | Business impact and utility | T01, T05 | T09, T11, T12 |
| 4 | Agent-T09 | `tasks/T09_defensive_action_selection/README.md` | Safe action-policy design | T06, T08, T10 | T11, T12 |
| 4 | Agent-T11 | `tasks/T11_rl_cyber_defence/README.md` | Offline RL feasibility | T04, T09, T10 | T12 |
| 5 | Agent-T12 | `tasks/T12_contribution_landscape/README.md` | Novel-contribution decision | T01–T11 | synthesis lead |

### Parallelization plan

Start T01, T03, and a preliminary T02 in parallel. T02 may use a provisional T01 interface, then must reconcile it at the Wave 1 gate. Start T04, T05, and T07 after their named upstream **handoff packet** exists. T06, T08, and T10 can then proceed in parallel. T09 and T11 follow; T12 starts only when it can cite all accepted task conclusions. This order deliberately prevents an attractive model from being chosen before data, labels, costs, and response constraints are understood.

## How to assign a README to an agent

Copy this exact instruction, replacing the bracketed fields:

> You are **[Agent-Txx]**. Read the master program at `README.md`, then read only `tasks/[task-folder]/README.md`. Complete that task within the defensive/simulation boundary. Use the internet for deep research; log sources and claims with the shared templates; run only the specified offline TensorFlow/Keras experiment or document the evidence-based reason it is inapplicable. Write all work under `work/Txx_[slug]/`. Deliver the required handoff packet and do not alter another agent's folder or any shared synthesis file.

The orchestrator gives an agent upstream `handoff_packet.md` files once approved. A downstream agent must cite a handoff by task ID and version, then independently verify any claim it relies on.

## Universal evidence standard

Each task needs a source registry and claim ledger. A minimum task bibliography is **15 sources**, including:

- at least 6 peer-reviewed papers or reputable conference papers;
- at least 3 primary/authoritative sources (for example: original dataset paper, dataset repository/documentation, MITRE, NIST, CISA, vendor technical documentation, or government guidance);
- at least 2 sources published or updated in the last 24 months, where the subject can drift;
- at least 2 contradictory, limiting, or negative sources if they exist.

Do not inflate the count with search-result pages, AI summaries, unsourced blogs, or duplicate reporting. Use IEEE-style in-text citations in reports and stable URLs/DOIs in `sources.csv`. For every material conclusion, add a claim ID to `claim_ledger.csv`, state whether it is directly supported or an inference, and link it to one or more source IDs and experiment IDs.

## Experiment standard (TensorFlow/Keras only)

Python preprocessing may use standard-library Python, NumPy, pandas, and scikit-learn **only for data splitting and conventional non-neural baselines**. Neural models must use `tensorflow` and `tf.keras`; do not substitute PyTorch, JAX, or an opaque hosted model.

Every experimental task must provide:

- `environment.txt`: OS, Python, TensorFlow/Keras, CUDA/GPU (if any), package versions, and hardware disclosure;
- `README.md`: research question, hypothesis, scope, dataset licence, exact run command, and limitations;
- `src/` with readable scripts or a clean, executable notebook;
- `config.json`: seeds, chronological/random split method, preprocessing, model parameters, threshold choices, and training budget;
- `results/metrics.csv`, `results/figures/`, and `results/run_log.csv`;
- an experiment card based on the shared template;
- at least three seeds (`7`, `19`, `42`) unless deterministic computation makes this irrelevant;
- a leakage check: timestamps, host IDs, labels, and train/test entities must be assessed and documented;
- an ablation or comparison that tests one meaningful design choice;
- confidence intervals or mean and standard deviation where multiple seeds are run.

Use chronological evaluation for time-ordered data whenever possible. Never claim real-time performance without measuring event-to-decision latency on the stated machine and replay rate. Never claim causality from an observational dataset.

## Naming and version rules

- Task folders: `work/T01_attack_progression/` through `work/T12_contribution_landscape/`.
- Files: lowercase snake case; dated decision records use `YYYY-MM-DD_topic.md`.
- Sources: `SRC-T01-001`; claims: `CLM-T01-001`; experiments: `EXP-T01-01`; handoffs: `HOF-T01-v1`.
- Every chart must include title, units, dataset/split, seed aggregation, and source/experiment ID in its caption.
- Never overwrite a prior result: create `run_001`, `run_002`, etc. Add a short reason to `run_log.csv`.

## Synthesis protocol and quality gates

At the end of every task, the agent produces `handoff_packet.md` containing: five validated findings; the top three limitations; dataset/model recommendation; unresolved questions; all file paths; and a one-paragraph decision implication. The reviewer checks source counts, citations, code rerunnability, leakage assessment, and whether the conclusion actually follows from the evidence. Rejected work returns with specific corrections.

The synthesis lead performs these gates:

1. **Wave gate:** reconcile terminology, telemetry schema, ATT&CK mappings, and dataset licences across accepted packets.
2. **Evidence gate:** sample at least five claims per task; ensure cited sources support the actual wording.
3. **Reproduction gate:** independently rerun one representative experiment from T04, T06, T09, and T11 when applicable, or record the exact blocker.
4. **Architecture gate:** choose data interface, prediction target, graph representation, action space, human-approval boundary, evaluation metrics, and baseline systems. Each choice must link to claim IDs.
5. **Contribution gate:** T12 must show the proposed contribution differs from commercial capabilities and prior studies, with a falsifiable evaluation plan.

## Completion definition

The research phase is ready to transition only when all task handoffs are accepted, the synthesis record names an explicit technical contribution, at least one compatible public/simulated dataset route is selected, and the proposed system has a reproducible offline benchmark. Otherwise, record the gap and revise the research plan; do not proceed on confidence alone.
