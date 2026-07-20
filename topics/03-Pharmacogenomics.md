# Topic 03: Pharmacogenomics

## Overview
Drug-gene interactions, star-allele nomenclature, dosing guidelines, and clinical decision support for medication selection.

---

### Q1: Explain CYP2D6 star-allele genotyping and why it's clinically important for drug metabolism.

**A:** CYP2D6 metabolizes ~25% of commonly prescribed drugs (codeine, tamoxifen, many antidepressants/antipsychotics). Star alleles (*1, *2, *4, *10, etc.) denote haplotypes with defined functional impact:

- **Normal function:** *1, *2 (combine for "normal metabolizer" if diplotype activity score ~1–2)
- **Decreased function:** *10, *17, *41 (reduced enzyme activity)
- **No function:** *3, *4, *5, *6 (null alleles — nonsense, deletion, splice defects)
- **Increased function:** *1xN, *2xN (gene duplication — ultrarapid metabolizers)

**Activity score system:** Each allele assigned 0 (no function), 0.25–0.5 (decreased), or 1 (normal); diplotype activity score sums both alleles, mapping to phenotype:
- 0: Poor metabolizer (PM)
- 0.25–1.0: Intermediate metabolizer (IM)
- 1.25–2.25: Normal metabolizer (NM)
- >2.25: Ultrarapid metabolizer (UM)

**Clinical example — codeine:** Codeine is a prodrug converted to morphine via CYP2D6. PMs get inadequate analgesia (can't activate the drug); UMs risk life-threatening opioid toxicity (rapid conversion to morphine) — this is why FDA contraindicates codeine in known UM patients, particularly nursing mothers and pediatric post-tonsillectomy patients.

### Q2: What is CPIC, and how do you use CPIC guidelines in a clinical decision support pipeline?

**A:** CPIC (Clinical Pharmacogenetics Implementation Consortium) publishes peer-reviewed, evidence-graded guidelines translating genotype into actionable prescribing recommendations for specific drug-gene pairs (e.g., CYP2C19-clopidogrel, TPMT/NUDT15-thiopurines, HLA-B*57:01-abacavir).

**Pipeline integration:**
1. Genotype patient (targeted panel or extract from WGS/WES using specialized callers like Stargazer/Aldy/PharmCAT)
2. Translate genotype → diplotype → phenotype using CPIC allele-function tables
3. Match phenotype + prescribed/considered drug against CPIC guideline table
4. Generate structured CDS alert (e.g., via CDS Hooks/FHIR) at point of prescribing in the EHR
5. Include guideline evidence level (A/B/C/D) and actionable recommendation text
6. Version-control guideline updates (CPIC guidelines are periodically revised) and propagate to historical results via reanalysis triggers

**Key design consideration:** CDS alert fatigue — only fire actionable, high-evidence-level alerts to avoid clinicians ignoring pharmacogenomic warnings.

### Q3: Describe HLA pharmacogenomic testing and its role in preventing severe adverse drug reactions.

**A:** Certain HLA alleles predispose to severe immune-mediated hypersensitivity reactions:
- **HLA-B*57:01:** Abacavir hypersensitivity — FDA requires testing before prescribing; near 100% negative predictive value avoids reaction
- **HLA-B*15:02:** Carbamazepine-induced Stevens-Johnson syndrome/toxic epidermal necrolysis — strongly associated in patients of Southeast/East Asian ancestry
- **HLA-A*31:01:** Broader carbamazepine hypersensitivity across ancestries

**Testing considerations:** HLA typing requires specialized methods (sequence-specific PCR, NGS-based HLA callers) due to extreme polymorphism and linkage disequilibrium complexity. Because these associations are strongly ancestry-correlated, universal (rather than ancestry-targeted) testing is increasingly recommended to avoid perpetuating disparities and missing at-risk patients outside the "typical" ancestry group.

### Q4–Q16: (Representative additional topics)
- TPMT/NUDT15 testing for thiopurine dosing in oncology/IBD
- Warfarin dosing algorithms combining CYP2C9/VKORC1 genotype with clinical factors
- Phenoconversion: how drug-drug interactions can mimic genetic poor-metabolizer phenotype
- DPYD testing before fluoropyrimidine chemotherapy (5-FU/capecitabine toxicity)
- Preemptive vs. reactive pharmacogenomic testing models
- PharmGKB vs. CPIC vs. DPWG guideline differences
- Pharmacogenomic panel design trade-offs (targeted vs. exome-derived PGx)
- Star-allele calling challenges from short-read NGS (CYP2D6 structural complexity)
- Return of pharmacogenomic results and lifetime utility/reanalysis
- Multi-gene interaction complexity (e.g., combined CYP2D6+CYP2C19 phenoconversion)
- Direct-to-consumer PGx testing limitations and clinical-grade confirmation needs
- Regulatory landscape: FDA table of pharmacogenomic associations

---

## Summary
Pharmacogenomics translates genotype into actionable, drug-specific prescribing guidance. Analysts must understand star-allele complexity, guideline sourcing (CPIC/DPWG/PharmGKB), and CDS integration to prevent adverse events and optimize efficacy.
