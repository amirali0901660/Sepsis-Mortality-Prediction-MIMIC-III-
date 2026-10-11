# Sepsis Mortality Prediction Using MIMIC-III

**Clinical machine learning | SQL | Python | XGBoost | Explainable AI**

A university project developed for the **Data Analytics in Healthcare** course at **Vrije Universiteit Brussel (VUB)**. The project investigates mortality prediction for ICU patients with sepsis using routinely collected clinical information from the [MIMIC-III Clinical Database](https://physionet.org/content/mimiciii/1.4/).

> **Data access notice:** MIMIC-III is credentialed, restricted-access clinical data. This repository does **not** distribute MIMIC-III records, patient-level extracts, individual predictions, access credentials, or other restricted material. Anyone seeking to reproduce the analysis must independently obtain authorization from PhysioNet and comply with the applicable Data Use Agreement.

## Project overview

The project developed and evaluated a clinical machine-learning workflow for predicting mortality among ICU patients with sepsis. The workflow included cohort selection, SQL-based extraction, clinical feature engineering, model comparison, hyperparameter tuning, probability calibration, and model interpretation.

### Reported project results

| Item | Reported result |
| --- | --- |
| Sepsis cohort | 4,676 patients |
| Engineered variables | 35 clinically motivated features |
| Feature window | First 24 hours of the ICU stay |
| Extraction pipeline | 8 SQL queries using BigQuery |
| Models compared | Logistic Regression, Random Forest, XGBoost |
| Best reported test ROC-AUC | **0.794** (95% CI: **0.765–0.822**) |
| Reference SOFA ROC-AUC | **0.713** |
| Probability calibration | Brier score **0.186 → 0.181** after Platt scaling |

*These results are transcribed from the project's CV summary. The complete notebook and experimental methodology have not yet been independently reviewed for this public release. Confirm the metrics, endpoint definition, patient/admission splitting, and evaluation details against the original results before publishing.*

## Methodology

### 1. Cohort construction and data preparation

- Queried MIMIC-III through BigQuery to construct a cohort of patients with sepsis.
- Addressed MIMIC-specific considerations including duplicate admissions, age de-identification, and multiple ICU stays per hospital admission.
- Applied physiological plausibility bounds during clinical feature extraction.

### 2. Clinical feature engineering

- Constructed **35 features** from measurements available during the first 24 hours of ICU stay.
- Included information from vital signs, laboratory results, Glasgow Coma Scale (GCS), FiO2, and components of the Sequential Organ Failure Assessment (SOFA) score.
- Examples of laboratory measurements include lactate, creatinine, and bilirubin.

### 3. Modeling and evaluation

- Compared **Logistic Regression**, **Random Forest**, and **XGBoost**.
- Used randomized hyperparameter search (50 iterations), threshold selection using Youden's J statistic, and Platt probability calibration.
- Evaluated discrimination using ROC-AUC, including a reported 95% confidence interval, and compared results with the SOFA score.
- Examined XGBoost predictions with **SHAP TreeExplainer**; the project identified lactate, blood urea nitrogen (BUN), and SpO2 among the most influential variables.

## Technologies

Python · SQL · BigQuery · pandas · NumPy · scikit-learn · XGBoost · SHAP

## Repository contents

The public release is intended to contain **reviewed and sanitized code only**. The final layout will depend on the files approved for release.

```text
sepsis-mortality-prediction/
├── README.md
├── notebooks/            # Sanitized notebooks, with patient-data outputs removed
├── sql/                  # Reviewed SQL queries, if cleared for publication
├── src/                  # Reusable preprocessing/training code, if available
└── figures/              # Reviewed aggregate, non-identifying figures
```

> Files or directories shown above are a proposed organization, not a claim that each one is already included.

## Reproducibility and data access

MIMIC-III is not bundled with this repository. To reproduce the research:

1. Obtain independent credentialed access to [MIMIC-III on PhysioNet](https://physionet.org/content/mimiciii/1.4/).
2. Complete the required training and accept the applicable Data Use Agreement.
3. Set up a compliant local or approved computing environment and obtain the database through authorized channels.
4. Review the published code, queries, environment requirements, and methodological notes before running the analysis.

**Execution instructions and dependency versions will be added after the notebook and project files have been reviewed.** No public dataset or runnable end-to-end reproduction is promised at this stage.

## Limitations
- Methodological limitation: Median imputation was fitted before the train/validation/test split in the original coursework implementation. This introduces potential data leakage and may make the reported evaluation  results optimistic. The notebook is preserved as originally implemented.
- This is an academic retrospective modeling project, not a validated clinical decision-support system.
- Model performance on one retrospective MIMIC-III cohort does not establish generalizability to other hospitals, populations, or prospective clinical settings.
- The reported metrics should be interpreted according to the original study's outcome definition, cohort criteria, and validation design; full details will be documented after review.
- Prediction performance and SHAP feature attribution should not be interpreted as evidence of causality.

## Dataset citation

Johnson, A. E. W., et al. **MIMIC-III, a freely accessible critical care database.** *Scientific Data* 3, 160035 (2016). https://doi.org/10.1038/sdata.2016.35

Dataset: [MIMIC-III Clinical Database, version 1.4](https://physionet.org/content/mimiciii/1.4/), https://doi.org/10.13026/C2XW26

## Author

**Amirali Youneszadeh**  
MSc Applied Computer Science Engineering, Vrije Universiteit Brussel  
[GitHub](https://github.com/amirali0901660) · [LinkedIn](https://www.linkedin.com/in/amir-ali-younes-zadeh-1a641931a)

