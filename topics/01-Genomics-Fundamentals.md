# Topic 01: Genomics Fundamentals

## Overview
Sequencing technologies, reference genomes, variant calling, and the foundational data structures underlying precision medicine analysis.

---

### Q1: Compare short-read (Illumina) vs. long-read (PacBio/Nanopore) sequencing. When would you choose each for a precision medicine pipeline?

**A:** 
**Short-read (Illumina):**
- Read length: 100–300 bp; accuracy: 99.9%+ (Q30)
- Strengths: Low cost (~$300–600/genome), high throughput, mature variant-calling pipelines (GATK)
- Weaknesses: Struggles with repetitive regions, structural variants, phasing

**Long-read (PacBio HiFi / Oxford Nanopore):**
- Read length: 10–100+ kb; PacBio HiFi accuracy ~99.9%, Nanopore ~95–99%
- Strengths: Resolves structural variants, repeat expansions (e.g., triplet repeats), haplotype phasing, fusion transcripts
- Weaknesses: Higher cost per sample, lower throughput, more complex bioinformatics

**Clinical decision:**
- Germline SNV/indel screening (e.g., hereditary cancer panels): short-read suffices, cost-effective
- Structural variant disorders (e.g., facioscapulohumeral dystrophy, fragile X): long-read preferred
- Cancer fusion detection, complex rearrangements: long-read or hybrid approach
- Population-scale screening programs: short-read for cost reasons, with long-read reflex testing for ambiguous cases

### Q2: What is a reference genome, and what are the implications of reference bias in precision medicine?

**A:** A reference genome (e.g., GRCh38/hg38) is a composite representative sequence used to align patient reads. It is not a "normal" genome — it's a mosaic assembled from multiple individuals, predominantly of European ancestry in earlier builds.

**Reference bias implications:**
- Variants in regions absent from or divergent from the reference (structural variation, novel insertions) are systematically missed — disproportionately affecting underrepresented ancestries
- Alignment algorithms favor reads matching the reference; true variants near reference gaps get lower mapping quality, are filtered out
- Pangenome references (e.g., Human Pangenome Reference Consortium) reduce bias by representing population diversity as a graph rather than linear sequence

**Precision medicine impact:** Underrepresentation of non-European populations in reference panels and reference genomes contributes to lower diagnostic yield and higher VUS rates for those populations — a major health equity concern.

### Q3: Explain the GATK best-practices variant calling workflow at a high level.

**A:**
```
Raw reads (FASTQ)
  → Alignment (BWA-MEM) → BAM
  → Mark duplicates (Picard)
  → Base quality score recalibration (BQSR)
  → Variant calling (HaplotypeCaller) → GVCF
  → Joint genotyping (GenotypeGVCFs) → VCF
  → Variant filtering (VQSR or hard filters)
  → Annotation (VEP, ANNOVAR, SnpEff)
```
Key rationale: GVCF-based joint calling allows cohort-level genotyping without re-calling from scratch when new samples are added, and improves genotype accuracy at low-coverage sites by borrowing statistical strength across samples.

### Q4–Q18: (Representative additional topics)
- Whole-genome vs. whole-exome vs. targeted panel trade-offs (cost, coverage, diagnostic yield)
- Coverage depth requirements for germline vs. somatic calling (30x vs. 500-1000x)
- Phred quality scores and their statistical meaning
- CNV/SV detection algorithms (read-depth, split-read, paired-end evidence)
- Trio-based sequencing for de novo variant discovery
- Mitochondrial genome sequencing considerations (heteroplasmy)
- Sequencing batch effects and how to control for them
- FASTQ/BAM/VCF/GVCF file format details and when each is used
- Genome build liftover challenges (hg19 to hg38)
- Repeat expansion detection methods (ExpansionHunter)
- Somatic vs. germline variant calling differences (tumor-normal pairing)
- Single-cell sequencing basics relevant to precision oncology
- Sequencing QC metrics (Ti/Tv ratio, contamination estimates, coverage uniformity)
- Cost/turnaround-time trade-offs in clinical sequencing workflows
- Population stratification and ancestry inference methods

---

## Summary
Mastery of sequencing technology trade-offs, reference genome limitations, and standard variant-calling pipelines is foundational for all downstream precision medicine analysis.
