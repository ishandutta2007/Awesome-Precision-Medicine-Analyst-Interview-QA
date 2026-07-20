# Topic 12: Industry Context & Ethics

## Overview
Health equity, incidental findings, market landscape, and the ethical frontiers of precision medicine.

---

### Q1: Discuss the health equity implications of underrepresentation in genomic reference databases and how analysts can mitigate downstream harms.

**A:** Genomic reference databases (gnomAD, ClinVar, GWAS catalogs) are historically dominated by individuals of European ancestry (~80%+ in early gnomAD releases, improving but still imbalanced). This creates compounding downstream harms:

**Mechanisms of harm:**
1. **Higher VUS rates in underrepresented populations:** Population-specific benign variants absent from reference databases get misclassified as rare/potentially pathogenic due to PM2 (absence from controls) criteria — a variant common and benign in an African population but absent from a Euro-centric database appears rare and suspicious
2. **Polygenic risk score (PRS) portability failure:** PRS models trained predominantly on European GWAS data show substantially reduced predictive accuracy when applied to other ancestries (documented accuracy drops of 2-5x), risking systematically worse risk stratification for non-European patients
3. **Missed diagnoses:** Population-specific pathogenic variants underrepresented in training/reference data may be missed entirely by variant callers and interpretation pipelines tuned to well-characterized populations

**Mitigation strategies for analysts:**
- Actively favor and contribute to diversity-focused reference efforts (All of Us, H3Africa, gnomAD's expanding diverse cohorts)
- Report ancestry-stratified performance metrics for any predictive model, not just aggregate performance
- Apply appropriate caution/caveats in clinical reports when population-matched reference data is limited for a patient's ancestry
- Advocate within organizations for diverse cohort recruitment in biomarker discovery studies, not just diverse confirmation cohorts

### Q2: How should a precision medicine analyst approach the ethical tension between broad genomic data sharing (for scientific progress) and individual privacy/autonomy?

**A:** This is a genuine, unresolved tension without a single correct answer — analysts should demonstrate awareness of the trade-offs rather than a dogmatic position.

**Arguments for broad sharing:**
- Rare disease diagnosis often depends on matching cases across institutions/countries (Matchmaker Exchange model) — restrictive data silos directly delay diagnoses
- Statistical power for genomic discovery scales with sample size; balkanized data reduces scientific progress for everyone, including future patients
- Federated/collaborative models increasingly allow analysis without raw data transfer (reducing but not eliminating privacy trade-offs)

**Arguments for restriction/caution:**
- Genomic data is uniquely and permanently identifying — cannot be "reset" like a password if compromised
- Implicates biological relatives who never consented
- Historical harms (e.g., Havasupai Tribe case, where blood samples were used beyond consented scope) demonstrate real risks of broad/future-use consent models, particularly for marginalized communities with justified distrust of research institutions
- Insurance/employment discrimination risks persist despite GINA's gaps (life, disability, long-term care insurance not covered)

**Practical middle-ground approaches:**
- Tiered/controlled access models (rather than fully open or fully closed)
- Dynamic consent platforms allowing ongoing patient control over data use
- Community-engaged research models, particularly for historically exploited populations
- Federated analysis approaches that answer scientific questions without centralizing raw data

### Q3: What is the current market/industry landscape for precision medicine, and what trends should analysts be aware of?

**A:**
**Key industry segments:**
- **Clinical genomic testing labs:** Diagnostic companies (hereditary cancer panels, carrier screening, pharmacogenomics, NIPT)
- **Oncology precision medicine:** Companion diagnostics, comprehensive genomic profiling (tumor sequencing), MRD monitoring — one of the most mature precision medicine markets
- **Pharma/biotech biomarker programs:** Internal translational science teams supporting drug development with patient stratification biomarkers
- **Health system precision medicine programs:** Academic medical centers building internal genomics/CDS infrastructure
- **Direct-to-consumer genomics:** Consumer-facing companies with variable clinical-grade rigor

**Notable trends (as of 2026):**
- Increasing FDA scrutiny/oversight of laboratory-developed tests (LDT rule implementation)
- Growth of liquid biopsy and circulating tumor DNA (ctDNA) for both diagnosis and MRD monitoring
- Expansion of newborn genomic screening pilots raising new consent/incidental-finding questions for a population that cannot consent
- Increasing integration of AI/ML-based variant interpretation tools, alongside corresponding regulatory framework development (FDA's evolving AI/ML SaMD guidance)
- Growing emphasis on health equity in biomarker discovery funding priorities (NIH All of Us, industry diversity commitments)
- Payer coverage remaining a persistent bottleneck — clinical validity/utility evidence bar for reimbursement often lags behind technical capability

### Q4–Q15: (Representative additional topics)
- Incidental/secondary findings disclosure policies and ACMG SF gene list evolution
- Direct-to-consumer genomics: clinical-grade vs. entertainment-grade distinction
- Newborn sequencing programs and unique ethical considerations
- Genetic counseling workforce shortage and its impact on scaling precision medicine
- Reimbursement/payer landscape challenges for novel genomic tests
- Precision medicine in low-resource settings — global health equity considerations
- AI/ML regulatory framework evolution for genomic interpretation tools
- Patient advocacy group roles in precision medicine research prioritization
- Data monetization ethics (research use vs. commercial use of patient genomic data)
- Precision medicine workforce trends and required skill evolution
- Public trust and genomic research participation disparities
- The role of large language models in clinical variant interpretation support

---

## Summary
Precision medicine analysts operate at the intersection of rapidly evolving science, market forces, and profound ethical questions. Strong candidates demonstrate nuanced understanding of trade-offs rather than simplistic positions, and awareness of how technical decisions carry equity and ethical implications.
