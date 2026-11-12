# Predictive Cyber Incident Commander

> **Status: research phase complete, prototype not yet built.** This repository contains the concept, the research programme and its synthesis. Raw experiment working files (about 6 GB) are kept locally and are not included.

## The idea

Security teams receive thousands of alerts a day and can investigate only a fraction of them. A real attack often appears as a series of individually weak signals spread across different systems: an unusual login, then a suspicious PowerShell command, then a credential-access event, then a large data transfer.

The **Predictive Cyber Incident Commander** is a proposed defensive decision-support system that works through five stages:

```
Observe → Detect → Reconstruct → Predict → Decide
```

It aims to answer four progressively harder questions: *Is something suspicious happening? What is the attacker doing? What are they likely to do next? What should we do now?* It recommends proportionate defensive actions, but it never carries them out. A human always approves.

The full concept is in [`docs/project-concept.md`](docs/project-concept.md).

## Research programme

Before committing to an architecture, I designed and ran a structured research programme of **12 workstreams**. The research was carried out by AI research agents, each assigned one workstream and working under a shared review gate. Each workstream combined a review of published evidence with a reproducible, offline TensorFlow/Keras experiment wherever an experiment could genuinely test the claim. Negative results were kept and reported.

| # | Workstream | # | Workstream |
|---|---|---|---|
| T01 | Real-world attack progression | T07 | Attack graphs |
| T02 | MITRE ATT&CK-based sequence modelling | T08 | Autonomous response |
| T03 | Security event telemetry schemas | T09 | Defensive action selection |
| T04 | Public temporal datasets | T10 | Containment cost modelling |
| T05 | SIEM and XDR correlation | T11 | Reinforcement learning for cyber defence |
| T06 | Next-stage and next-target prediction | T12 | Contribution landscape |

The operating manual and safety boundary are in [`research/RESEARCH_PROGRAM.md`](research/RESEARCH_PROGRAM.md), and the brief for each workstream is in [`research/tasks/`](research/tasks).

## Key findings

| Experiment | Result | Decision |
|---|---|---|
| Data splitting (T04) | Random splits scored much higher than chronological ones, which shows leakage | Always use chronological, group-disjoint evaluation |
| Next-stage prediction (T06) | A simple **Markov baseline (macro-F1 0.561)** beat a GRU (0.198) | Keep the simple baseline and don't promote the neural model |
| Action selection (T09) | A transparent formula had zero regret, while the Keras version had 0.037 | The formula stays the authority, and the model can only advise |
| Offline RL (T11) | Regret of 0.145 (base costs) and 0.110 (changed costs) missed the no-go thresholds | **No reinforcement learning** in the first version |
| Quality-shift benchmark (T12) | A quality-aware Keras adviser cut raw guard overrides from 0.086 to **0.000**, with a final unsafe rate of 0 in both conditions | Adopt it as the project's core technical contribution |

The T11 results were reproduced byte-for-byte from a fresh, immutable run, verified by a SHA-256 hash.

## Resulting architecture

```
telemetry contract → conservative correlation → evidence-quality snapshot
  → transparent reference scorer (+ optional Keras adviser)
  → external deterministic guard → recommend / abstain → audit record
```

- **The models recommend or abstain, and never act.** A deterministic guard that sits outside every model checks provenance, freshness, entity anchors, contradictions, the rollback plan and named-human approval before any recommendation is shown.
- **Six fixed action strings**, ranging from `monitor` to `recommend_network_containment_review`. The last one is always rejected by the guard in the initial profile.
- **Proposed contribution:** *An Auditable Quality-Shift Benchmark for Guarded Cyber-Incident Recommendations in Synthetic Telemetry*. This is a measurement protocol, not a copy of a commercial SIEM, XDR or SOAR product.

See [`research/shared/synthesis/`](research/shared/synthesis) for the architecture decision record, the dataset decision, the evidence matrix, the research gap register and the contribution statement, and see [`docs/synthesis-report.pdf`](docs/synthesis-report.pdf) for the compiled report.

## Safety boundary

This is strictly defensive research using simulated or synthetic data only. There is no scanning, no exploit development, no malware and no connection to live systems. Every experiment ranks *simulated* actions and never calls a firewall, endpoint, cloud or identity API.

## Next steps

1. Build the fictional telemetry and case generator described in the dataset decision.
2. Implement the guarded recommendation pipeline and the quality-shift benchmark (`EXP-T12-01`) as an interactive application.
3. Audit a public dataset (Windows-APT v3) before making any claim about real data.

## Tech stack (research)

Python · TensorFlow · Keras · MITRE ATT&CK · reproducible experiment tracking (seeds, SHA-256 run hashes)
