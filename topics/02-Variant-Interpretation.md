# Topic 02: Variant Interpretation

## Overview
ACMG/AMP classification, pathogenicity assessment, VUS management, and clinical reporting of genetic variants.

---

### Q1: Walk through the ACMG/AMP 2015 classification framework categories.

**A:** Evidence is grouped into categories combined via a point/rule-based system:

**Pathogenic evidence:**
- PVS1 (very strong): Null variant (nonsense, frameshift, canonical splice) in a gene where loss-of-function is a known disease mechanism
- PS1–PS4 (strong): Same amino acid change as established pathogenic variant; de novo occurrence; functional studies; prevalence in affected vs. controls
- PM1–PM6 (moderate): Mutational hotspot, absent from controls, in trans with pathogenic variant, protein length change, de novo (unconfirmed), phenotype specificity
- PP1–PP5 (supporting): Cosegregation, in-silico prediction, phenotype match, family history

**Benign evidence:**
- BA1 (stand-alone): Allele frequency >5% in population databases
- BS1–BS4 (strong): Frequency too high for disorder, lack of segregation, healthy adult homozygote, in-vitro functional studies showing no damage
- BP1–BP7 (supporting): Missense in gene where truncating variants cause disease, in-silico benign, synonymous with no splice impact

**Final classification:** Combine evidence codes into Pathogenic / Likely Pathogenic / VUS / Likely Benign / Benign using the defined combining rules.

### Q2: How do you handle a Variant of Uncertain Significance (VUS) in a clinical report, and what steps can reclassify it?

**A:** VUS should **not** be used to guide clinical management alone. Report language should explicitly state insufficient evidence exists and clinical correlation is advised.

**Reclassification pathway:**
1. **Segregation analysis** — test additional family members (affected/unaffected) to strengthen or weaken evidence
2. **Functional studies** — minigene splicing assays, protein function assays
3. **RNA sequencing** — assess splicing impact directly for intronic/splice-region variants
4. **Population database updates** — periodic re-review as gnomAD grows (variant may be reclassified as benign if frequency data accumulates)
5. **Literature/ClinVar monitoring** — automated periodic re-analysis pipelines flag variants with new submissions
6. **Case-level data sharing** — contribute to ClinVar/Matchmaker Exchange to enable case aggregation

Labs should have a defined reanalysis policy (e.g., annual or biennial) since ~10-15% of VUS get reclassified within 2 years, predominantly to benign.

### Q3: What is the difference between clinical validity and clinical utility of a genetic test?

**A:**
- **Analytical validity:** Does the test accurately/reproducibly detect the variant? (sensitivity, specificity, precision)
- **Clinical validity:** Does the variant reliably predict the clinical phenotype/outcome? (penetrance, odds ratio, evidence strength)
- **Clinical utility:** Does using this test result actually improve patient outcomes? (does it change management, and does that change help?)

A variant can have strong clinical validity (well-established pathogenic) but limited clinical utility if no actionable intervention exists. Precision medicine analysts must evaluate all three dimensions before recommending test adoption into practice — this maps onto the ACCE framework (Analytic validity, Clinical validity, Clinical utility, Ethical/legal/social implications).

### Q4–Q17: (Representative additional topics)
- Penetrance and expressivity in variant risk communication
- Secondary/incidental findings (ACMG SF v3.2 gene list) reporting obligations
- Splice-site variant prediction tools (SpliceAI, MaxEntScan) and interpretation caveats
- Copy number variant classification (ACMG/ClinGen CNV guidelines)
- Mosaicism detection and its interpretive challenges
- Compound heterozygosity and phasing considerations
- Polygenic risk scores vs. monogenic variant interpretation
- ClinVar star ratings and conflicting interpretation resolution
- Pathogenicity in genes with variable expressivity/incomplete penetrance
- Pharmacogenomic variant star-allele nomenclature basics
- Cascade testing and family variant confirmation workflows
- Ethnic-specific founder variants and their interpretation nuances
- Report structure: what belongs in a clinical genomic report
- Discordant results between orthogonal confirmation methods (Sanger vs. NGS)

---

## Summary
Variant interpretation combines statistical evidence, functional biology, and clinical judgment. Analysts must communicate uncertainty responsibly and maintain reanalysis pipelines as evidence evolves.
