# Topic 05: Clinical Data Pipelines

## Overview
EHR data extraction, HL7/FHIR interoperability, data harmonization, and building reliable pipelines connecting molecular data to clinical context.

---

### Q1: Explain how HL7 FHIR is used to integrate genomic data with clinical records. What resources are relevant?

**A:** FHIR (Fast Healthcare Interoperability Resources) provides standardized resources for representing genomic data alongside clinical data:

- **Observation (genomics profile):** Represents individual variant findings (gene, HGVS notation, zygosity, clinical significance)
- **DiagnosticReport:** Wraps the overall genomic test report, linking to constituent Observations
- **MolecularSequence:** Represents raw sequence-level data (less commonly used directly; often referenced)
- **Specimen:** Links test results to the biological sample and collection metadata
- **Condition/MedicationRequest:** Connects genomic findings to diagnoses and prescribing decisions for CDS purposes

**Integration pattern:**
```
Lab genomic pipeline (VCF) → Structured report generation 
  → FHIR Genomics Reporting IG-compliant resources 
  → FHIR server / EHR ingestion 
  → CDS Hooks trigger at prescribing (pharmacogenomic alert) 
  → Clinician-facing SMART on FHIR app for detailed variant review
```

**Why this matters:** Without standardized representation, genomic findings become unstructured PDF reports buried in EHR document repositories — unusable for automated CDS, cohort identification, or reanalysis triggers when new evidence emerges.

### Q2: How do you handle data harmonization when combining EHR data across multiple institutions with different coding systems?

**A:**
**Common heterogeneity sources:**
- Diagnosis codes: ICD-9 vs. ICD-10 vs. institution-specific problem lists
- Lab results: LOINC codes inconsistently applied; different units/reference ranges
- Medications: local formulary codes vs. RxNorm vs. NDC
- Free-text clinical notes with no structured equivalent

**Harmonization approach:**
1. **Terminology mapping:** Map all codes to standard ontologies (ICD-10, LOINC, RxNorm, SNOMED CT) using crosswalk tables; validate mappings with clinical informaticist review
2. **Common Data Model (CDM):** Transform to OMOP CDM or similar to enable standardized analytics across sites (used in OHDSI network studies)
3. **Unit harmonization:** Convert all lab values to standard units; validate against expected physiological ranges to catch conversion errors
4. **NLP extraction:** For unstructured notes, use validated NLP pipelines (e.g., cTAKES, custom clinical BERT models) with institution-specific validation before trusting extracted concepts
5. **Data quality auditing:** Compare distributions across sites post-harmonization to detect residual systematic differences (site as a confounder)

**Governance:** Establish a data dictionary and mapping documentation that's versioned and reviewed by both informatics and clinical domain experts — undocumented mapping decisions are a major source of downstream analytic errors.

### Q3–Q16: (Representative additional topics)
- OMOP Common Data Model structure and use in multi-site studies
- De-identification/anonymization techniques for clinical-genomic linked data (Safe Harbor vs. Expert Determination)
- ETL pipeline design for clinical genomics (validation, idempotency, error handling)
- Data lineage and provenance tracking for regulated clinical pipelines
- Structured vs. unstructured EHR data extraction trade-offs
- Real-time vs. batch pipeline architectures for CDS alerts
- Master patient index and record linkage/deduplication challenges
- Longitudinal EHR data modeling for outcomes research
- Data versioning for reanalysis (variant reclassification propagation)
- Handling missing/incomplete clinical documentation in observational cohorts
- Consent management integration with data pipelines (opt-out/opt-in tracking)
- Interoperability testing and validation strategies
- Cloud vs. on-premise considerations for PHI-containing genomic pipelines
- Audit logging requirements for clinical genomic data access

---

## Summary
Clinical data pipelines are the connective tissue between molecular findings and actionable patient care. Reliable harmonization, standards adoption (FHIR/OMOP), and rigorous data governance are essential to avoid silent errors that propagate into clinical decisions.
