# Metamorphic Oversight — A Simulation Study of Board-Level Risk-Oversight Consistency

> Replication code for the manuscript *"Stress-Testing the Boardroom: Metamorphic
> Perturbation of AI Risk and the Consistency of Board-Level Oversight,"* currently
> under **double-blind review** at an anonymized journal. Author and affiliation
> information is withheld for review.

## Overview

This repository contains a fully reproducible **simulation study** that validates a
measurement approach for **board-level risk-oversight consistency**. Boards are
modeled as decision systems that classify AI-related boundary-case risks. Because no
external oracle defines the "correct" risk classification, oversight quality is
assessed through **metamorphic relations** — logical constraints that judgments must
satisfy across controlled transformations of a scenario (e.g., adding a protective
control must not *raise* the assessed risk).

Synthetic boards and directors judge boundary-case vignettes arranged in metamorphic
pairs under a **two-stage design** (independent judgment → coordination intervention
→ revised judgment). The study demonstrates three things:

1. **Construct validity.** A **convergence index** (Stage 1 → Stage 2) separates
   *healthy pluralism* (dispersion that resolves) from *oversight failure*
   (dispersion that persists), whereas **Stage-1 dispersion alone cannot** — the two
   classes overlap on dispersion but separate sharply on convergence.
2. **Determinant recovery.** Board characteristics predict the consistency metrics in
   the pre-specified directions: AI literacy lowers metamorphic violations; diversity
   raises Stage-1 dispersion *and* raises convergence; escalation authority,
   independence, and CEO tenure raise convergence.
3. **Classification & power.** Combining dispersion with convergence identifies
   oversight failure more accurately than dispersion alone (ROC/AUC), and a Level-2
   power analysis quantifies how many boards are needed to detect board-level effects.

The entire pipeline is deterministic under a single fixed random seed.

## Repository structure

```
.
├── data/                                 # synthetic datasets (written by notebook 00)
├── notebooks/
│   ├── 00_data_generation.ipynb          # simulation data-generating process
│   ├── 01_construct_validity.ipynb       # convergence vs. dispersion separation
│   ├── 02_determinant_recovery.ipynb     # OLS recovery of directional hypotheses
│   ├── 03_classification_power.ipynb     # ROC/AUC and Level-2 power analysis
│   ├── 04_robustness.ipynb               # multi-seed (300) stability of all findings
│   └── 05_metamorphic_relations.ipynb    # data-driven view of the four relation families
├── results/
│   ├── figures/                          # greyscale figures (.png @ 600 dpi and .pdf)
│   └── tables/                           # result tables (.csv)
├── requirements.txt
└── README.md
```

Each notebook is a single, self-contained code cell with an English header comment.

## Requirements

- Python 3.11+ (developed on 3.13)
- Install dependencies:

```
pip install -r requirements.txt
```

## Reproducing the results

Run the notebooks **in order** from the `notebooks/` directory:

```
cd notebooks
jupyter nbconvert --to notebook --execute --inplace 00_data_generation.ipynb
jupyter nbconvert --to notebook --execute --inplace 01_construct_validity.ipynb
jupyter nbconvert --to notebook --execute --inplace 02_determinant_recovery.ipynb
jupyter nbconvert --to notebook --execute --inplace 03_classification_power.ipynb
jupyter nbconvert --to notebook --execute --inplace 04_robustness.ipynb
jupyter nbconvert --to notebook --execute --inplace 05_metamorphic_relations.ipynb
```

Notebook `00` writes the datasets to `data/`; notebooks `01`–`03` read them and write
figures and tables to `results/`. Notebook `04` regenerates the data-generating process
across 300 seeds (it does not read `data/`) and is self-contained. You may also open and
run the notebooks in Jupyter.

## Outputs

| Notebook | Figures | Tables |
|---|---|---|
| 01 | `fig01_dispersion_vs_convergence`, `fig02_separation_panels` | `table01_metrics_by_class`, `table02_separation_B_vs_C` |
| 02 | `fig03_coef_convergence` | `table03_determinants` |
| 03 | `fig04_roc`, `fig05_level2_power` | `table04_auc`, `table05_power` |
| 04 | `fig06_robustness_cohend`, `fig07_robustness_auc` | `table06_robustness_summary` |
| 05 | `fig08_metamorphic_relations` | `table07_violation_by_relation` |

Figures are greyscale, exported at 600 dpi (`.png`) and as vector `.pdf`, without
embedded captions (captions belong in the manuscript).

## Data statement

All data are **fully synthetic**, produced by the simulation. No human-subject,
personal, or proprietary data is used. This is a measurement-validation simulation,
not an empirical survey.

## Anonymity

This repository is prepared for **double-blind review** and contains no author,
institution, or funding information. If you fork or re-host it, use an anonymized git
identity and strip any commit history that could reveal authorship before sharing the
link with reviewers.

## License

To be specified by the authors (e.g., MIT) upon de-anonymization.
