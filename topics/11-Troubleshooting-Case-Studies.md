# Topic 11: Troubleshooting & Case Studies

## Overview
Debugging real-world pipeline failures, QC anomalies, and applied problem-solving scenarios.

---

### Q1: A clinical exome pipeline suddenly shows a 3x increase in the number of variants called per sample compared to last month. Walk through your troubleshooting approach.

**A:**
**Systematic troubleshooting framework:**

1. **Check for pipeline/software version changes:** Was the aligner, variant caller, or reference genome updated? A silent tool version bump is the most common cause of sudden systematic shifts
2. **Check reference/annotation database updates:** Did the annotation source (VEP cache, ClinVar, gnomAD) update? This wouldn't change raw variant *calls* but could affect downstream filtering if filters reference annotation fields
3. **Check sequencing run QC metrics:** Compare Ti/Tv ratio, contamination estimates, coverage depth/uniformity, duplicate rate against historical baseline — a shift in Ti/Tv ratio toward 1.0 (from expected ~2.0-3.0 for WES) strongly suggests increased false-positive calls, often from contamination or quality degradation
4. **Check for reagent/wet-lab batch changes:** New sequencing reagent lot, library prep kit change, or different sequencing center can introduce systematic artifacts
5. **Check filtering logic:** Was a hard filter threshold or VQSR model inadvertently changed/disabled in a pipeline update?
6. **Sample provenance check:** Rule out sample mix-up (wrong sample type, contamination between samples) via identity/relatedness checks
7. **Isolate variable:** Re-run a known-good historical sample through the current pipeline version — if variant count changes, the issue is pipeline-side, not sample-side

**Root cause example:** Most commonly, this pattern traces to either (a) a variant caller version update changing default sensitivity, or (b) a reference/annotation update causing previously-filtered low-confidence calls to pass current filters. Both require a formal validation re-run and sign-off before returning to production given clinical use.

### Q2: Case study — A pharmacogenomic CDS alert fired incorrectly, recommending a dose reduction for a patient who was actually a normal metabolizer. How would you investigate?

**A:**
**Investigation steps:**
1. **Verify raw genotype call:** Pull the raw VCF/genotype data for the relevant gene (e.g., CYP2D6) — confirm the actual sequenced genotype independent of any downstream interpretation logic
2. **Verify star-allele translation:** Check whether the genotype-to-star-allele calling tool (e.g., Stargazer, PharmCAT) correctly translated the raw genotype — CYP2D6 is particularly prone to miscalling due to structural complexity (gene conversion with pseudogene CYP2D7, copy number variation)
3. **Verify diplotype-to-phenotype mapping:** Confirm the correct CPIC activity score table version was used — guideline updates periodically revise allele function assignments
4. **Verify CDS rule logic:** Check the clinical decision support rule engine — was the correct phenotype-to-recommendation mapping applied, or was there a logic error (e.g., off-by-one in activity score thresholds)?
5. **Check for stale data:** Was this an older result generated under a previous guideline version that wasn't reanalyzed after a CPIC update?
6. **Check for phenoconversion:** Was a drug-drug interaction present that should have triggered a *phenotype override* (e.g., patient genetically normal metabolizer but taking a strong CYP2D6 inhibitor, making them phenotypically poor metabolizer) — this may not be a pipeline error but a legitimate phenoconversion flag that needs clearer alert language

**Resolution & prevention:** Document root cause, implement regression test case covering this specific scenario, and if the issue affected other patients, initiate a broader lookback/reanalysis to identify all affected cases — clinical pharmacogenomic CDS errors require formal quality event reporting per lab quality management system procedures.

### Q3–Q15: (Representative additional topics)
- Debugging discordant results between two orthogonal confirmation methods
- Investigating unexpected batch effects in a multi-omic cohort study
- Troubleshooting low on-target coverage in a targeted panel run
- Root-causing a sample identity/swap suspicion via genetic fingerprinting
- Handling an unexpected drop in variant calling sensitivity after pipeline migration
- Investigating a cluster of false-positive pharmacogenomic star-allele calls
- Debugging FHIR resource validation failures in a clinical genomics integration
- Troubleshooting inconsistent polygenic risk score outputs across ancestry groups
- Root-causing a data pipeline failure that silently dropped samples
- Investigating an unexpected VUS reclassification surge after a database update
- Debugging performance degradation in a population-scale variant query system
- Case study: responding to an incidental finding disclosure dilemma

---

## Summary
Real-world precision medicine analysis requires systematic, hypothesis-driven troubleshooting across wet-lab, bioinformatics, and clinical interpretation layers. Strong candidates demonstrate structured debugging methodology, not just domain knowledge.
