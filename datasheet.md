# DataSheet, Simulated formulation/CMC dataset

## Motivation

A synthetic dataset was generated to demonstrate an agentic AI and predict-first workflow for formulation/CMC tasks under realistic numeric ranges benchmarked from journal-indexed studies.


## Composition

- **Rows:** Simulated formulations.

- **Columns:** Composition fractions, process parameters, drug proxy descriptors, and endpoints.

- **File:** `tables/simulated_formulation_dataset.csv`.


## Collection process

Data are simulated using mechanistically plausible relationships and additive noise. Benchmark anchors and PMIDs are recorded in `tables/table_pubmed_benchmarks.csv`.


## Recommended uses

- Benchmarking pipeline mechanics, uncertainty workflows, active learning, and multi-objective triage.


## Not recommended uses

- Direct estimation of real-world formulation performance.

- Regulatory decisions.


## Known biases and constraints

- Structural assumptions reflect one plausible nanoformulation regime and may not generalize.

- Feature distributions are shaped by chosen priors.
