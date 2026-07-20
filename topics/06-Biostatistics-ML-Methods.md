# Topic 06: Biostatistics & ML Methods

## Overview
Survival analysis, feature selection, model validation, and statistical rigor for precision medicine applications.

---

### Q1: When would you use Cox proportional hazards vs. a machine learning survival model (e.g., random survival forest) for treatment outcome prediction?

**A:**
**Cox proportional hazards:**
- Pro: Interpretable hazard ratios per covariate; well-established inferential framework (confidence intervals, p-values); works well with moderate sample sizes and limited covariates
- Con: Assumes proportional hazards (constant hazard ratio over time) — must be checked (Schoenfeld residuals) and violated often in real biomarker data; assumes linear relationship between covariates and log-hazard unless explicitly modeled otherwise
- Best for: Regulatory-facing analyses, biomarker validation studies where interpretability and statistical rigor are paramount

**Random survival forest / gradient boosted survival models:**
- Pro: Captures nonlinear relationships and interactions automatically; no proportional hazards assumption; often better predictive performance with many covariates (e.g., multi-omic feature sets)
- Con: Less interpretable (though SHAP values help); requires larger sample sizes to avoid overfitting; less standardized for regulatory submission

**Practical decision:** Use Cox for primary/confirmatory analysis (especially regulatory-facing biomarker qualification), and ML survival methods for exploratory discovery and hypothesis generation, ideally validating any ML-discovered signal in a subsequent Cox-based confirmatory analysis.

### Q2: Explain the multiple testing problem in genomic association studies and the main correction approaches.

**A:** Testing hundreds of thousands to millions of variants (GWAS) or tens of thousands of genes (differential expression) for association inflates false positive rate dramatically under naive p<0.05 thresholding.

**Correction methods:**
- **Bonferroni correction:** α_adjusted = α / n_tests — very conservative, controls family-wise error rate (FWER); standard GWAS threshold is p < 5×10⁻⁸ (derived from ~1M independent tests in the genome)
- **Benjamini-Hochberg (FDR):** Controls the expected proportion of false positives among rejected hypotheses — less conservative, standard for RNA-seq differential expression (q-value < 0.05)
- **Permutation-based methods:** Empirically derive the null distribution by shuffling phenotype labels — accounts for correlation structure (LD) that Bonferroni ignores, computationally expensive but most accurate for correlated tests

**Practical guidance:** Use genome-wide significance (5×10⁻⁸) for GWAS discovery; use FDR for exploratory omics (transcriptomics/proteomics) where follow-up validation is planned; always report both the correction method and the effective number of independent tests when LD structure reduces true multiple-testing burden.

### Q3: How do you validate a precision medicine predictive model to avoid overfitting and ensure generalizability?

**A:**
**Internal validation:**
1. **Train/validation/test split** or **k-fold cross-validation** — nested CV when hyperparameter tuning is involved to avoid optimistic bias
2. **Stratified sampling** to maintain outcome/subgroup balance across folds, especially important for rare outcomes
3. **Bootstrap validation** (e.g., .632+ bootstrap) for small clinical cohorts where held-out test sets aren't feasible

**External validation:**
4. **Temporal validation** — test on more recently collected data than training set
5. **Geographic/institutional validation** — test on data from different sites/populations to assess transportability
6. **Population subgroup analysis** — explicitly evaluate performance across ancestry, sex, age groups to detect differential performance (equity concern)

**Reporting standards:**
7. Follow **TRIPOD** (Transparent Reporting of a multivariable prediction model) guidelines for reporting
8. Report calibration (not just discrimination/AUC) — a model can have good AUC but poor calibration, leading to miscalibrated risk estimates that mislead clinical decisions
9. Report confidence intervals on all performance metrics, not point estimates alone

**Key pitfall:** Data leakage — ensure no information from test set (including preprocessing statistics like normalization parameters) leaks into training; for multi-omic data, ensure batch effect correction is fit only on training data.

### Q4–Q17: (Representative additional topics)
- Feature selection under high dimensionality (LASSO, elastic net, stability selection, Boruta)
- Class imbalance handling in rare disease/rare outcome prediction
- Propensity score methods for confounding control in observational precision medicine studies
- Bayesian methods for small-sample clinical genomics (hierarchical models, shrinkage)
- Time-varying covariates in longitudinal treatment response modeling
- Competing risks analysis (e.g., death from disease vs. other causes)
- Meta-analysis methods for combining biomarker effect sizes across studies
- Power calculation for precision medicine biomarker studies
- Calibration vs. discrimination trade-offs in risk prediction models
- Explainability methods (SHAP, LIME) for clinical ML model interpretation
- Handling informative censoring in survival analysis
- Polygenic risk score construction and validation methodology
- Cross-ancestry portability of statistical genetics models
- Sample size/power considerations for rare variant association studies

---

## Summary
Rigorous biostatistics and validation practices distinguish clinically trustworthy precision medicine models from overfit research curiosities. Analysts must balance statistical power, interpretability, and generalizability across diverse patient populations.
