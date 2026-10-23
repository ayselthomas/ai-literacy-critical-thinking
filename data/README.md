# Data availability

The individual-level survey dataset (raw N = 368; final analytic N = 339) is
**not included in this repository**.

This is a deliberate decision, stated in the study's data and code availability
statement: participants consented under an anonymity and limited-use
agreement, and the study's ethics approval (CHRIST (Deemed to be University)
Research Committee on Ethics, RCEC) does not authorize public deposit of the
individual-level dataset. The dataset is available from the corresponding
author upon reasonable request, consistent with the consent terms.

## What you need to actually run the notebooks

Every notebook in `../notebooks/` expects one of these files, none of which
ship with this repo:

| File | Produced by | Needed by |
|---|---|---|
| `raw_survey_export.csv` (33 columns, same structure as the live questionnaire) | — (your own export) | `01_data_cleaning.ipynb` |
| `AI_Literacy_CT_First_60_Samples.csv` (33-column pilot export) | — (your own export) | `00_pilot_study_reliability.ipynb` |
| `items_numeric_reversed.csv`, `meta.csv` | `01_data_cleaning.ipynb` | `02_measurement_model.ipynb`, `04_invariance.ipynb` |
| `items_final_measurement_model.csv`, `final_items.json` | `02_measurement_model.ipynb` | `03_structural_model.ipynb` |
| `composite_scores.csv` | `03_structural_model.ipynb` | `04_invariance.ipynb`, `05_person_centered_profiles.ipynb`, `06_ml_robustness.ipynb` |

## Column map for a compatible raw export

Columns are 0-indexed. Columns 6–32 use `AGREE_MAP` (Strongly Disagree=1 … Strongly
Agree=5) for Metacognitive Awareness/AI Literacy items, or `FREQ_MAP` (Never=1 …
Almost Always=5) for AI Usage/Cognitive Offloading/Critical Thinking Engagement
items — see `results/item_construct_mapping.json` for the exact wording and
response scale of every item.

- `0`: Timestamp · `1`: information-sheet confirmation · `2`: consent ·
  `3`: level of study · `4`: field of study · `5`: daily AI usage time
- `6–10`: Metacognitive Awareness (item 10 reverse-worded)
- `11`: attention check 1 (valid response: "Disagree")
- `12–16`: AI Usage (item 12 reverse-worded)
- `17–21`: AI Literacy (item 21 reverse-worded)
- `22–26`: Cognitive Offloading (item 26 reverse-worded)
- `27`: attention check 2 (valid response: "Almost Always")
- `28–32`: Critical Thinking Engagement (item 32 reverse-worded)

## Reproducing the key results without the raw data

You don't need the raw dataset to use the study's *outputs* — `../results/`
contains the fully fitted, de-identified model artifacts (aggregate parameters
only, no respondent-level rows): the structural/measurement model results
(`key_results.json`), the fitted person-centered profile model with a verified
classification formula (`profile_model.json`), and the full item codebook
(`item_construct_mapping.json`).
