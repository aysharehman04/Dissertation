# Biological Ageing Pace as a Predictor of Alzheimer's Conversion in MCI

A statistical and machine learning analysis of whether **DunedinPACNI** (a structural MRI-derived biomarker of biological ageing pace) and **cognitive reserve** (education) predict three-year conversion from mild cognitive impairment (MCI) to Alzheimer's disease, using data from the Alzheimer's Disease Neuroimaging Initiative (ADNI).

**Author:** Aysha Rehman · University of East Anglia, School of Computing Sciences (2026)

> **Note on code and data:** ADNI data is governed by a Data Use Agreement that restricts redistribution, so the underlying dataset and analysis code are not included in this repository. This README documents the project's methodology and findings; the full write-up is available in [`dissertation.pdf`](./dissertation.pdf).

---

## Overview

Early, accurate risk stratification in MCI has become a clinical priority following the approval of anti-amyloid immunotherapies for early Alzheimer's disease. This project investigates two candidate predictors of conversion:

- **DunedinPACNI** — a neuroimaging-derived index of multi-system biological ageing pace
- **Cognitive reserve** — operationalised as years of formal education

using a cohort of **614 ADNI MCI participants** (199 converters, 32.4%), combining nested logistic regression with a benchmarked machine learning pipeline.

## Key Findings

| Result | Value |
|---|---|
| DunedinPACNI as independent predictor of conversion | OR = 1.25, 95% CI 1.03–1.51, p = .022 |
| APOE ε4 (dominant predictor across all models) | OR = 3.13, 95% CI 2.18–4.54, p < .001 |
| Education as independent predictor / moderator | Not significant (p = .274 / p = .441) |
| Primary logistic regression AUC | 0.668–0.673 |
| Best ML classifier (7-feature set, nested 5-fold CV) | AUC = 0.87 (SVM / Logistic Regression) |
| DunedinPACNI's incremental value once cognition is known | Negligible (ΔAUC = −0.001) |

**Headline interpretation:** DunedinPACNI is a statistically significant, non-invasive predictor of MCI-to-AD conversion, independent of APOE ε4 status. However, SHAP and ablation analysis show its apparent contribution in a full ML model is driven almost entirely by baseline cognitive assessment — once cognition is known, PACNI adds essentially nothing. This suggests PACNI's clinical value is likely greatest in **pre-MCI populations**, before cognitive decline is already detectable.

## Methods Summary

- **Data:** ADNI (ADNI-1, GO, 2, 3), N = 614 baseline MCI participants after inclusion criteria (not redistributed here — see note above)
- **Statistical models:** 3 nested logistic regressions, adjusting for age, sex, APOE ε4 carrier status
- **ML models:** 5 classifiers (Logistic Regression, Random Forest, SVM, KNN, XGBoost) under true nested 5-fold cross-validation, with class-weight balancing for imbalance
- **Languages/tools:** R for statistical modelling · Python (scikit-learn, XGBoost, SHAP) for machine learning
- **Validation:** DeLong's method for AUC confidence intervals, Hosmer–Lemeshow test for calibration, VIF for multicollinearity, SHAP for feature-level interpretability

## Data Access

Data used in this project were obtained from the Alzheimer's Disease Neuroimaging Initiative (ADNI) database ([adni.loni.usc.edu](https://adni.loni.usc.edu)), subject to ADNI's Data Use Agreement. Researchers can apply for access directly through ADNI. DunedinPACNI scores were computed using the open-source implementation published by Whitman et al. (2025): [github.com/etw11/DunedinPACNI](https://github.com/etw11/DunedinPACNI).

> Whitman, E. T., et al. (2025). DunedinPACNI estimates the longitudinal pace of aging from a single brain image to track health and disease. *Nature Aging*, 5(8), 1619–1636.

## License

Academic project — for portfolio and academic reference only. ADNI data and any derived analysis code are not distributed in this repository in accordance with the ADNI Data Use Agreement.
