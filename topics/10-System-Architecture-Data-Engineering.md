# Topic 10: System Architecture & Data Engineering

## Overview
Scalable genomic pipelines, cloud infrastructure, and system design for precision medicine data platforms.

---

### Q1: Design a scalable cloud architecture for processing WGS data for a population-scale precision medicine program (100,000+ genomes).

**A:**
**Key requirements:** Cost efficiency at scale, reproducibility, compliance (HIPAA-eligible infrastructure), elastic compute for variable workload.

**Proposed architecture:**
```
Ingestion: Sequencer output → Secure object storage (encrypted, versioned)
                ↓
Orchestration: Workflow manager (WDL/Nextflow via Cromwell or AWS Batch/Google Life Sciences)
                ↓
Processing: Containerized GATK best-practices pipeline (Docker/Singularity)
    - Elastic compute (spot/preemptible instances for cost reduction, ~60-80% savings)
    - Parallelized by chromosome/interval for scatter-gather efficiency
                ↓
Joint genotyping: Periodic batch joint-calling (GVCF merge) as cohort grows
                ↓
Storage: Tiered storage — hot (recent/active) vs. cold/archive (completed, rarely accessed) 
    - CRAM instead of BAM for ~30-40% storage reduction
                ↓
Query layer: Variant database (e.g., BigQuery, Hail-based) for population-scale querying
                ↓
Access layer: API/CDS integration with appropriate access controls and audit logging
```

**Design decisions & rationale:**
- **Spot/preemptible instances:** Genomic pipelines are largely batch/non-time-critical, making them ideal for interruptible, discounted compute
- **CRAM over BAM:** Reference-based compression significantly reduces storage costs at scale — critical when storing 100K+ genomes
- **Workflow standardization (WDL/CWL):** Ensures reproducibility and portability across compute environments, critical for regulatory audit trails
- **Incremental joint-genotyping:** Avoid full cohort re-calling for every new sample; use GVCF-based approaches (GenomicsDB) that scale incrementally

**Compliance considerations:** HIPAA-eligible cloud services (BAA in place), encryption at rest/in transit, VPC isolation, comprehensive audit logging of all data access.

### Q2: How would you design a variant reanalysis pipeline that automatically flags patients for reclassification when a VUS is updated in ClinVar?

**A:**
**System components:**
1. **Variant knowledge base sync:** Scheduled job (daily/weekly) pulling ClinVar updates, diffing against last-known classifications
2. **Patient-variant index:** Reverse-lookup table mapping each unique variant to all patients who carry it (critical infrastructure — must be maintained as new patients are sequenced)
3. **Change detection:** When a variant's classification changes (e.g., VUS → Likely Pathogenic), trigger a review workflow
4. **Clinical significance filter:** Only auto-flag changes crossing actionable thresholds (e.g., VUS→LP/P or P→B) — avoid alert fatigue from minor evidence-level changes that don't change the categorical classification
5. **Genetic counselor/clinician review queue:** Flagged cases routed for human review before any patient contact — automated systems should never directly notify patients without clinical review
6. **Audit trail:** Full logging of classification history, source evidence, and review decisions for regulatory/quality purposes
7. **Patient contact workflow:** Integration with clinical scheduling/outreach systems once review confirms reclassification is clinically significant and actionable

**Key engineering challenges:**
- Scale: Need efficient variant-to-patient indexing (not re-scanning all VCFs on every ClinVar update) — this is typically the primary bottleneck in real implementations
- False-positive management: Not every classification change warrants patient contact (e.g., evidence level within same category)
- Consent/contactability: System must track whether patients consented to be recontacted and have current contact information

### Q3–Q16: (Representative additional topics)
- Data lake vs. data warehouse architecture for multi-omic clinical data
- Workflow orchestration tools comparison (Nextflow, WDL/Cromwell, Snakemake)
- Containerization and reproducibility in bioinformatics pipelines
- Genomic data compression strategies (CRAM, gVCF, BCF)
- Building queryable variant databases at population scale (Hail, BigQuery)
- Microservices vs. monolithic architecture for clinical genomics platforms
- API design for genomic data access (GA4GH standards)
- Disaster recovery and backup strategies for irreplaceable genomic data
- Cost optimization strategies for large-scale genomic compute
- CI/CD practices for validated clinical bioinformatics pipelines
- Monitoring and observability for production genomic pipelines
- Data pipeline testing strategies (unit tests for bioinformatics tools, golden file validation)

---

## Summary
Precision medicine data platforms require careful architectural decisions balancing scale, cost, compliance, and reproducibility. Analysts increasingly need data engineering fluency alongside domain genomics/clinical expertise.
