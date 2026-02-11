# Model Card, Multi-output formulation endpoint predictor

## Model details

- **Model type:** Multi-output Random Forest (tree ensemble).

- **Inputs:** Composition fractions, process parameters, and drug physicochemical proxy features.

- **Outputs:** Particle size, PDI, zeta potential, encapsulation efficiency, viscosity, dissolution at 30 min, stability days.

- **Uncertainty proxy:** Tree-ensemble dispersion (σ) per endpoint.

- **Intended setting:** Predict-first triage and prioritization for formulation/CMC workflows.


## Intended use

This proof-of-concept supports, (i) in silico screening of candidate formulations, (ii) multi-objective triage under constraints, (iii) uncertainty-aware next-best-experiment selection, and (iv) generation of auditable recommendations.


## Performance

See `tables/table_model_metrics.csv` for R2 and MAE by endpoint, and `tables/table_model_compare_summary.csv` for bootstrap comparisons.


## Limitations

- Data are simulated using PubMed-benchmarked numeric anchors, not experimental datasets.

- Uncertainty is a heuristic proxy, calibration must be validated on real assay data.

- Feature space is simplified, real CMC requires richer descriptors and structured metadata.


## Ethical and safety considerations

- This workflow is for research and decision support, not autonomous release decisions.

- Human-in-the-loop review is required for experimental execution and quality gating.


## Reproducibility

- Seeded simulation and saved artifacts, see `audit_run.json` and `supplementary_manifest.json`.
