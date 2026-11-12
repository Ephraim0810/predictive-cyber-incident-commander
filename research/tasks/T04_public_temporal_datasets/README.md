# T04 — Public datasets with usable temporal relationships

**Assigned agent:** Agent-T04  
**Wave:** 2  
**Depends on:** T02 attack-label contract; T03 canonical event schema  
**Defensive boundary:** Download/use only datasets permitted by their terms. Do not redistribute restricted raw data in this program.

## Decision this task informs

Select a legal, reproducible data route for offline sequence prediction and response-policy experiments—or formally establish that a synthetic/hybrid route is necessary.

## Research questions

1. Which public cyber datasets preserve session, host, user, alert, and timestamp relationships needed for next-step prediction?
2. What are their licences, access restrictions, collection environments, known artefacts, labels, and temporal leakage risks?
3. How well can each candidate map to the T03 schema and T02 label contract?
4. Which datasets are suited to detection only, sequencing, attack graphs, or response simulation?

## Required research work

- Research at least 10 candidate datasets across network, host, cloud, enterprise simulation, and cyber-range categories. Prioritise original dataset papers and official repositories.
- Produce `dataset_catalog.csv` with URL/DOI, licence, collection date, scale, event sources, timestamp resolution, labels, topology/asset relations, availability check date, and restrictions.
- Create `dataset_scorecard.md` using weighted criteria: temporal integrity, provenance, schema coverage, ATT&CK alignment, licence, reproducibility, class balance, and suitability for each downstream task.
- Verify the top three candidates by obtaining a documented sample or metadata and computing file checksum, schema fields, time range, null rates, class counts, and split risks. Do not claim download success without evidence.

## Required TensorFlow/Keras experiment

For the most suitable accessible candidate, run a small `tf.keras` sequence baseline on a clearly stated task (next event family, next tactic proxy, or anomaly proxy). Compare a timestamp-respecting split to a random split to demonstrate leakage/optimism risk. If no candidate permits this responsibly, build a schema-faithful synthetic benchmark and document why that route was selected.

## Deliverables

- `sources.csv`, `claim_ledger.csv`, `dataset_catalog.csv`, `dataset_scorecard.md`, `dataset_access_log.md`.
- `data_audits/<dataset>/` with non-sensitive metadata, checksums, and profiling output; no unlicensed raw redistribution.
- `experiments/EXP-T04-01/`; `dataset_recommendation.md`; `handoff_packet.md` for T06/T11/T12.

## Acceptance checks

- The selected route has an explicit licence/terms conclusion and a reproducible acquisition or generation procedure.
- The scorecard distinguishes raw data availability from mere paper availability.
- Random and temporal results are never combined as if comparable.
