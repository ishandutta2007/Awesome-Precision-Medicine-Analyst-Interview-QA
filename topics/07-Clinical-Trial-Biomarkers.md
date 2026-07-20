# Topic 07: Clinical Trial Biomarkers

## Overview
Companion diagnostics, biomarker-driven trial design, endpoint selection, and the regulatory path from biomarker discovery to clinical use.

---

### Q1: Distinguish prognostic, predictive, and pharmacodynamic biomarkers with clinical trial examples.

**A:**
- **Prognostic biomarker:** Predicts disease outcome regardless of treatment (e.g., high tumor stage predicts worse survival independent of therapy). Used for risk stratification, not treatment selection.
- **Predictive biomarker:** Predicts differential response to a specific treatment (e.g., HER2 amplification predicts response to trastuzumab; EGFR mutation predicts response to EGFR-TKIs). This is the core biomarker type for precision medicine — it directly informs treatment selection.
- **Pharmacodynamic (PD) biomarker:** Measures a biological response to treatment, confirming target engagement (e.g., reduction in phosphorylated target protein after kinase inhibitor dosing). Used in early-phase trials for dose selection, not necessarily for patient selection.

**Trial design implication:** A biomarker can be prognostic without being predictive (e.g., predicts poor outcome in both arms equally) — a common analytic error is assuming a biomarker associated with outcome in a single-arm or observational study is predictive without a randomized biomarker-by-treatment interaction test.

### Q2: Compare biomarker-stratified, enrichment, and adaptive/umbrella trial designs.

**A:**
**All-comers with stratified analysis:** Enroll all patients regardless of biomarker status; analyze biomarker-positive and negative subgroups separately (pre-specified). Preserves generalizability but requires larger sample size to power subgroup analyses.

**Enrichment design:** Only enroll biomarker-positive patients (e.g., only EGFR-mutant NSCLC). Maximizes statistical power for the target population and treatment effect size, but provides no data on biomarker-negative patients and risks missing efficacy in unexpectedly responsive subgroups.

**Umbrella trial:** Single trial infrastructure testing multiple targeted therapies, each matched to a specific biomarker-defined subgroup within one overall disease (e.g., Lung-MAP). Efficient shared infrastructure/control arm, enables rapid biomarker-driven treatment matching.

**Basket trial:** Tests one targeted therapy across multiple disease types sharing a common biomarker (e.g., NTRK fusion across tumor types for larotrectinib). Efficient for testing biomarker-driven hypotheses across histologies but requires careful handling of tumor-type heterogeneity in response.

**Adaptive design:** Pre-planned interim analyses allow dropping ineffective arms, adjusting randomization ratios (response-adaptive randomization), or enriching for responsive subgroups mid-trial — requires careful statistical planning (alpha spending) to maintain type I error control.

### Q3: What is a companion diagnostic, and what regulatory considerations apply to co-development with a therapeutic?

**A:** A companion diagnostic (CDx) is a test required to safely and effectively use a corresponding therapeutic — typically identifying patients likely to benefit (or at risk of serious adverse events) as part of the drug's approved label.

**Co-development considerations:**
1. **Parallel regulatory pathway:** FDA typically requires CDx approval (PMA pathway) to coincide with the therapeutic's approval — the drug label references the specific validated test
2. **Analytical validation:** CDx must demonstrate accuracy, precision, reproducibility across labs/operators before clinical use
3. **Clinical validation:** Must be validated using the same patient population/samples as the pivotal therapeutic trial — using the assay version that will be commercially available, not a research-use-only prototype
4. **Bridging studies:** If the assay changes between trial and commercial launch (e.g., different platform), a bridging study demonstrating concordance is required
5. **Label specificity:** FDA approval may name a specific test ("labeled" CDx) or allow any validated test meeting performance criteria ("complementary" diagnostic, indicated but not mandated)
6. **Post-market considerations:** Ongoing surveillance for assay performance drift, particularly important as reference ranges/cutoffs may need real-world recalibration

**Analyst's role:** Precision medicine analysts often support cutoff/threshold determination (ROC-based optimization balancing sensitivity/specificity against clinical consequences of misclassification) and concordance analysis between CDx and research assays.

### Q4–Q15: (Representative additional topics)
- Minimal residual disease (MRD) as a surrogate endpoint in oncology trials
- Surrogate endpoint validation criteria (Prentice criteria)
- Biomarker cutoff/threshold determination methodology
- Master protocol trial designs and operational complexity
- Real-time biomarker-driven adaptive randomization
- Regulatory pathways: PMA vs. 510(k) vs. De Novo for diagnostics
- Concordance/bridging study design between assay platforms
- Trial biomarker sample handling/pre-analytical variable control
- Retrospective-prospective biomarker validation studies
- Health authority biomarker qualification programs (FDA, EMA)
- Statistical considerations for biomarker-by-treatment interaction testing
- Biomarker assay analytical validation (LoD, LoQ, precision, linearity)

---

## Summary
Biomarker-driven trial design bridges molecular biology and statistical rigor to enable targeted therapeutic development. Understanding trial design trade-offs and companion diagnostic regulatory pathways is essential for translating discovery biomarkers into clinical practice.
