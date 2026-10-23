# AI Literacy and Metacognitive Awareness as Predictors of Critical Thinking Engagement in the Age of AI Usage Among Indian University Students

A cross-sectional study (N = 339 Indian university students) testing whether AI
literacy and metacognitive awareness are statistically associated with critical
thinking engagement, independently of how much students use generative AI and
how much they offload cognitive work onto it.

## Summary

Generative AI adoption in higher education has raised concern that offloading
cognitive work onto AI tools erodes students' critical thinking. Most existing
work treats AI literacy as a protective factor and focuses on AI usage itself;
this study instead tests AI Literacy (AIL) and Metacognitive Awareness (MMR)
as **direct, simultaneous predictors** of Critical Thinking Engagement (CTE),
alongside AI Usage (AIU) and Cognitive Offloading (CO), in a one-step latent
structural equation model — supplemented by bootstrap resampling, a
structural-slope invariance test (does the AIL/MMR → CTE relationship change
with usage intensity?), a Gaussian-mixture person-centered profile analysis,
a Random Forest/SHAP robustness check, and a common-method-bias diagnostic.

**Headline result:** AI Literacy (β = .446, p < .001) and Metacognitive
Awareness (β = .398, p < .001) are significant, positive, comparably-sized
predictors of CTE (R² = .591). AI Usage is not a significant predictor
(β = .086, p = .287). Cognitive Offloading shows a negative but non-significant
trend under the primary estimator (β = −.141, p = .074), which becomes
significant under an ordinal-appropriate robustness check (p = .039) — so this
one path is reported as estimator-sensitive rather than settled. No
statistically detectable moderation of the AIL/MMR → CTE relationships by AI
usage intensity was found (p = .705). A person-centered profile analysis and a
machine-learning (Random Forest/SHAP) check, run on the same data, converge on
the same pattern.

The full numeric results are in [`results/key_results.json`](results/key_results.json).

## Repository structure

```
notebooks/   7 analysis notebooks, in pipeline order (00 → 06)
results/     exported, de-identified model artifacts (no respondent-level data)
  key_results.json            measurement model, structural model, all robustness checks
  profile_model.json          fitted Gaussian-mixture profile model + verified classifier formula
  item_construct_mapping.json full item codebook: wording, construct, scale, reverse-scoring
  figures/                    the two study figures (vector PDF + PNG)
data/        README only — see "Data availability" below
```

## Analysis pipeline

| Notebook | What it does |
|---|---|
| `00_pilot_study_reliability.ipynb` | Pilot study (N=55 analytic, from 60 recruited): reliability (α, ω) and item diagnostics |
| `01_data_cleaning.ipynb` | Raw survey export → exclusion cascade (duplicates, consent, attention checks, straightlining) → reverse-scored analytic dataset (N=339) |
| `02_measurement_model.ipynb` | Full 25-item, 5-factor CFA; reliability (α, CR, AVE); discriminant validity (HTMT) |
| `03_structural_model.ipynb` | One-step latent SEM predicting CTE from AIU/CO/AIL/MMR; VIF; bootstrap CIs; exploratory AIL×MMR interaction |
| `04_invariance.ipynb` | Additive covariate block (usage/level/field) + structural-slope invariance test (is the AIL/MMR → CTE slope stable across usage levels?) |
| `05_person_centered_profiles.ipynb` | Gaussian-mixture clustering on AIU/CO/AIL/MMR (k=2–4), profile validation via Tukey HSD and k=3-vs-k=4 cross-tabulation |
| `06_ml_robustness.ipynb` | Cross-validated linear regression vs. tuned Random Forest; SHAP feature importance |

Each notebook's markdown cells explain *why* each step is done, not just what
the code does — read them in order.

## Data availability

The individual-level dataset is **not included** in this repository, consistent
with the participant consent terms and the ethics approval granted for this
study (see `data/README.md` for the full explanation and the column schema
needed to run the notebooks against your own compatible export). The
`results/` folder contains the fitted, aggregate model outputs instead —
nothing in it is traceable to an individual respondent.

## Using the exported model artifacts

`results/profile_model.json` includes the fitted k=3 Gaussian-mixture profile
model (mixing weights, per-profile means/variances in standardized space, the
standardization constants, and a step-by-step classification formula). The
formula was checked against scikit-learn's own `.predict()` on all 339
respondents with zero mismatches, so it can be reimplemented directly in
another language or application without needing access to the raw data.

## Reproducing the analysis

```
pip install -r requirements.txt
```

Run the notebooks in order (00 → 06). Notebook 00 and 01 each need their own
raw survey export (see `data/README.md`); every later notebook consumes the
CSV/JSON that the previous one writes out.

## Author

Aysel Thomas, MSc Data Science, CHRIST (Deemed to be University), Bengaluru.

## License

Code and exported results: MIT (see `LICENSE`). No participant data is
included or licensed here.
