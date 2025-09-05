Step-by-Step Logic of the Pipeline

Step 1. Data Preparation: Load the dataset (plasma proteomics + patient metadata); Ensure severity_at_sample is categorical (Mild, Moderate, Severe, Critical); Create a numeric code (severity_code) for modeling.

Step 2. GAM (Generalized Additive Model): For each protein, fit a GAM using severity as predictor; GAM captures non-linear relationships between severity and protein abundance; Store the fitted GAM and predictions for later analysis/plotting.

Step 3. Mixed-Effects Model: Use the GAM predictions as input to a mixed-effects model; Random effect: patient ID (accounts for repeated measures).

Purpose: see if GAM-based trends are significant while accounting for within-patient variation.

Step 4. Extract Key Statistics: For each protein: GAM p-value (is the severity–protein curve significant?). Pseudo R² (explained variance of GAM)Mixed-model coefficient for GAM predictions. Mixed-model p-value (statistical significance after random effects).

Step 5. Partial Dependence Analysis: Compute the effect of severity at each level (Mild, Moderate, Severe, Critical). Tells us direction and magnitude of protein changes across disease severity.

Step 6. Store Outputs: Keep fitted GAM models (for later curve plotting). Save summary results (statistics + partial dependence values) in a dataframe.

Step 7. Export Results: Write all results into a CSV file. This file becomes a ready-to-use summary for interpretation or visualization.

Prepare data → Fit GAM per protein → Add patient random effects (Mixed model) → Extract stats → Compute severity-level effects → Save models + results → Export summary.

----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

Response variable (continuous, e.g., CRP levels, viral load) or categorical (e.g., disease severity)

Time (days since symptom onset or hospitalization)

Patient ID (random effect)

Covariates (age, sex, comorbidities, treatment status)

Methodology:

Model Choice:

Generalized Additive Model (GAM): Extends generalized linear models to allow flexible non-linear relationships between predictors and outcome using smooth functions.

For longitudinal data, GAMs can incorporate random effects or correlation structures to account for repeated measures within individuals.

Results: 

These proteins have the strongest association with severity:

LCN2: 0.735 
SERPINA1: 0.705 
IGLC3: 0.694 
APOB: 0.694 
IGKC: 0.678 
APOC2: 0.663 
CFH: 0.647 
SERPINC1: 0.641 
C9: 0.640 
ORM1: 0.637

Statistical Overview (Summary Stats Across All Proteins)

GAM_P_Value: Mean ~6.00e-09 (all extremely low). 
Pseudo_R_Squared: Mean 0.424, Std 0.150, Min 0.065, Max 0.735. 
Group_Var: Mean 0.110, Std 0.077, Min 0.056, Max 0.399. 
Gam_Pred_Coef: Mean ~1.008, Std ~0.003 (close to 1, as expected). 
Gam_Pred_P_Value: Mean very low (e.g., ~1e-100 or smaller). 
Effect_Critical: Mean 0.407, Std 0.181 (tends positive). 
Effect_Mild: Mean -0.407, Std 0.140 (tends negative). 
Effect_Moderate: Mean -0.153, Std 0.120. 
Effect_Severe: Mean 0.155, Std 0.185.
