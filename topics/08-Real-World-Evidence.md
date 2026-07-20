# Topic 08: Real-World Evidence (RWE)

## Overview
Claims data, registries, causal inference from observational data, and the use of real-world data (RWD) to support precision medicine decisions.

---

### Q1: What is the difference between real-world data (RWD) and real-world evidence (RWE), and what are common RWD sources?

**A:**
- **RWD:** Raw data relating to patient health status/care collected outside traditional RCTs — EHRs, claims/billing data, patient registries, wearables, patient-reported outcomes
- **RWE:** Clinical evidence about product usage, benefits, or risks *derived from analysis* of RWD — RWE is the conclusion; RWD is the raw material

**Common sources:**
- **Administrative claims:** Comprehensive care capture (all billed encounters) but limited clinical granularity (diagnosis codes, not lab values/genomics); good for long-term outcome/cost tracking
- **EHR data:** Rich clinical detail (labs, notes, vitals) but limited to single-system encounters (patients seeking care elsewhere are invisible) — "informed presence" bias
- **Disease registries:** Curated, often prospective data with structured clinical detail (e.g., tumor registries) but selection bias toward participating centers/patients
- **Patient-generated data:** Wearables, PROs — captures outcomes between clinical encounters but variable data quality/completeness

**Precision medicine use case:** RWE increasingly supports post-market safety surveillance, label expansion, and — under FDA's RWE framework — can supplement or in some cases substitute for traditional trial evidence for specific regulatory purposes.

### Q2: Explain confounding by indication and how you'd address it in an observational precision medicine outcomes study.

**A:** Confounding by indication occurs when the reason a treatment was prescribed is itself associated with the outcome, independent of the treatment's true effect — e.g., a targeted therapy might be preferentially given to healthier patients with better prognosis, making the drug look more effective than it is.

**Mitigation approaches:**
1. **Propensity score methods:** Model probability of treatment assignment given observed covariates; use for matching, stratification, or inverse probability weighting to balance measured confounders between treated/untreated groups
2. **New-user (incident user) design:** Compare patients at treatment initiation rather than including prevalent users, avoiding immortal time bias and depletion-of-susceptibles bias
3. **Active comparator design:** Compare against another active treatment for the same indication rather than untreated patients — reduces confounding by indication since both groups had the same clinical reason to be treated
4. **Instrumental variable analysis:** Use a variable that affects treatment assignment but not outcome directly (e.g., prescriber preference/formulary variation) to approximate randomization — requires strong, often untestable assumptions
5. **Negative control outcomes:** Test the analysis pipeline against an outcome that shouldn't be affected by treatment — residual association suggests uncontrolled confounding

**Critical limitation:** Propensity scores and related methods can only balance *measured* confounders — unmeasured confounding (e.g., frailty, performance status not captured in claims data) remains a fundamental threat to causal inference from observational precision medicine data.

### Q3–Q15: (Representative additional topics)
- Target trial emulation framework for observational causal inference
- Immortal time bias and how to avoid it in cohort study design
- Linking genomic data with claims/EHR data for real-world biomarker studies
- FDA's RWE framework and use cases for regulatory decision-making
- Common data models for multi-site RWE studies (OMOP, Sentinel)
- Missing data mechanisms in RWD and appropriate handling
- Generalizability vs. internal validity trade-offs (RCT vs. RWE)
- Synthetic control arms using historical/real-world data
- Loss to follow-up and informative censoring in registry data
- Validating RWD-derived outcomes against gold-standard chart review
- Ancestry/diversity representation gaps in RWD sources
- Post-marketing safety signal detection from real-world pharmacovigilance data

---

## Summary
RWE extends precision medicine evidence generation beyond controlled trials, but requires rigorous causal inference methodology to address the confounding and bias inherent in observational data.
