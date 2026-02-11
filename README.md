# Agentic-AI-Predict-First-CMC
Auditable, journal-benchmarked proof-of-concept for predict-first formulation and CMC using multi-endpoint ML with uncertainty, Pareto triage, active learning, and agentic orchestration.

# Agentic AI for Predict-First Formulation and CMC 

An end-to-end, auditable proof-of-concept that simulates journal-anchored formulation/CMC datasets, trains multi-endpoint predictive models with uncertainty, performs multi-objective Pareto triage, runs active-learning experiment selection, and logs a tool-using agent workflow while producing publication-ready figures and tables.

This repository is designed as a transferable template for Pharmaceutical Sciences digital transformation workflows, replacing the simulated dataset with real experimental formulation, drug delivery, and CMC data while preserving the same orchestration, diagnostics, and governance structure.

## Contents

1. Overview  
2. Repository structure  
3. Quickstart  
4. Outputs and where to find them  
5. Methods summary  
6. How “agentic AI” is implemented here  
7. Reproducibility and auditability  
8. Limitations  
9. License and citation  

## 1. Overview

Formulation and CMC programs often require balancing multiple endpoints at once, for example dissolution performance, particle size and dispersity, encapsulation efficiency, viscosity constraints, and stability. This proof-of-concept demonstrates a predict-first workflow that:

- Simulates a formulation dataset using numeric anchors benchmarked from PubMed-indexed studies (recorded explicitly in a benchmarking table).
- Trains a multi-output model to predict key endpoints from composition and process variables.
- Computes a practical uncertainty proxy from ensemble dispersion and checks whether uncertainty behaves sensibly.
- Applies developability constraints and identifies Pareto-optimal candidates across competing objectives.
- Runs active learning to prioritize the next most informative and valuable experiments.
- Wraps the workflow in a tool-using “agent” that logs actions for traceability and adds guardrails for human review.

## 2. Repository structure

Typical output layout created by the pipeline:

```text
az_psda_agentic_ai_poc_outputs/
  audit_run.json
  trace_agent.jsonl
  supplementary_manifest.json
  supplementary_package.zip
  report_methods_results.md
  report_figure_legends.md
  report_table_captions.md
  modelcard.md
  datasheet.md
  agent_policy.md
  top5_cmc_reasoning_notes.txt
  figures/
    fig_multipanel_main_results.png
    fig_pareto_dissolution_vs_stability.png
    fig_active_learning_R2_*.png
    fig_pred_vs_obs_*.png
    fig_uncertainty_vs_error_*.png
    fig_uncertainty_coverage_*.png
    fig_feature_importance_*.png
    fig_response_*.png
    ...
  tables/
    table_pubmed_benchmarks.csv
    simulated_formulation_dataset.csv
    table_model_metrics.csv
    table_uncertainty_summary.csv
    table_uncertainty_coverage.csv
    table_permutation_importance.csv
    table_pareto_top50_candidates.csv
    table_top20_recommendations.csv
    table_active_learning_history.csv
    table_model_compare_summary.csv
    table_ablation_embedding.csv
    *.tex
```
## 3. Quickstart

Environment
	•	Python 3.10–3.12 recommended
	•	Core dependencies:
	•	numpy, pandas, matplotlib
	•	scikit-learn

Install:
```
pip install numpy pandas matplotlib scikit-learn
```
Run
Run the notebook or the script that contains the full pipeline code. The pipeline writes outputs into:
```
az_psda_agentic_ai_poc_outputs/
```
## 4. Outputs and where to find them

Key tables
	•	tables/table_pubmed_benchmarks.csv
PubMed-indexed numeric anchors used to set plausible ranges for simulation.
	•	tables/simulated_formulation_dataset.csv
Simulated formulation “experiments” with inputs and endpoints.
	•	tables/table_model_metrics.csv
Model performance (R2, MAE) per endpoint.
	•	tables/table_uncertainty_summary.csv and tables/table_uncertainty_coverage.csv
Uncertainty proxy summary and empirical coverage checks.
	•	tables/table_pareto_top50_candidates.csv
Pareto-optimal candidates under developability constraints.
	•	tables/table_top20_recommendations.csv
Utility-ranked shortlist with a rationale string that includes predicted values and uncertainty.

Key figures
	•	figures/fig_multipanel_main_results.png
Main results panel showing prediction accuracy, Pareto region, active learning trajectory, and sensitivity.
	•	figures/fig_pareto_dissolution_vs_stability.png
Trade-off visualization with Pareto-optimal candidates highlighted.
	•	figures/fig_active_learning_R2_*.png
Predictive performance over active learning rounds.

Audit and traceability
	•	audit_run.json
Configuration, constraints, artifact pointers.
	•	trace_agent.jsonl
Tool-level trace of agent calls and outputs.
	•	agent_policy.md
Guardrails and human-in-the-loop rules used by the agent.

## 5. Methods summary

### Dataset simulation

Each row represents a formulation experiment with:
	•	Composition fractions that sum to 1.0 (e.g., lipid, polymer, surfactant, aqueous).
	•	Process settings (e.g., mixing speed, sonication time, temperature, pH).
	•	Drug proxy physicochemical properties (e.g., MW, logP, pKa).

### Endpoints include:
	•	Particle size (nm), PDI, zeta potential (mV)
	•	Encapsulation efficiency (%)
	•	Viscosity (mPa·s)
	•	Dissolution at 30 min (%)
	•	Stability days

Simulation uses mechanistically plausible couplings, for example surfactant and mixing reduce size and PDI, polymer increases viscosity and may increase stability but can reduce dissolution, lipophilicity increases encapsulation but can slow dissolution.

### Modeling

A multi-output Random Forest predicts all endpoints simultaneously from the input features. Performance is evaluated on a held-out test split using R2 and MAE.

### Uncertainty

Tree-ensemble dispersion provides a practical uncertainty proxy. The pipeline evaluates whether uncertainty increases with error and computes empirical coverage of intervals of the form μ ± zσ.

### Multi-objective triage

After filtering candidates by developability constraints, Pareto-optimal solutions are extracted for maximizing dissolution, encapsulation efficiency, and stability while minimizing particle size.

### Active learning

An uncertainty-aware acquisition function selects batches of experiments to label next, improving model performance efficiently.

## 6. How “agentic AI” is implemented here

Agentic AI is implemented as a tool-using workflow engine.

Tools include:
	•	predict_endpoints: runs the model and returns mean predictions and uncertainty proxy.
	•	pareto_filter: applies constraints and extracts Pareto-optimal candidates.
	•	summarize_candidates: returns a concise top-k table for review.

A planner executes a fixed sequence:
predict → constrain → pareto → summarize

Every tool call is logged to trace_agent.jsonl for auditability.

## 7. Reproducibility and auditability
	•	All simulations are seeded.
	•	All outputs are written to a single output directory.
	•	A manifest (supplementary_manifest.json) lists every table and figure.
	•	A ZIP (supplementary_package.zip) bundles the full supplement.
	•	Reports include:
	•	report_methods_results.md
	•	report_figure_legends.md
	•	report_table_captions.md

## 8. Limitations
	•	The dataset is simulated, it demonstrates workflow mechanics and auditability, not real predictive validity.
	•	Uncertainty estimates are pragmatic proxies, calibration must be validated on real datasets.
	•	Real deployment requires structured metadata capture, controlled endpoint definitions, and integration with laboratory systems.

## 9. License and citation
License MIT

## Citation
Petalcorin, M. I. R. (2026). Agentic AI for Predict-First Formulation and CMC (Journal-Benchmarked Proof-of-Concept). GitHub repository
