# Topic 04: Multi-Omic Integration

## Overview
Combining genomics, transcriptomics, proteomics, and metabolomics data for a unified molecular picture of disease.

---

### Q1: What are the main strategies for integrating multi-omic datasets, and what are their trade-offs?

**A:**
**1. Early integration (concatenation-based):** Combine all omic features into one matrix before modeling.
- Pro: Captures cross-omic interactions directly
- Con: Curse of dimensionality (e.g., 20K genes + 500K methylation sites + 10K proteins); different scales/distributions need careful normalization; risk of one omic type dominating

**2. Late integration (ensemble-based):** Train separate models per omic layer, combine predictions.
- Pro: Handles heterogeneous data types naturally; missing modalities per-sample don't break the pipeline
- Con: Misses cross-omic interaction effects that only manifest jointly

**3. Intermediate/joint integration (e.g., MOFA, joint NMF, similarity network fusion):** Learn shared latent factors across omics.
- Pro: Captures shared variance structure, dimensionality reduction with biological interpretability
- Con: Computationally intensive; factor interpretation requires domain expertise

**4. Knowledge-based/pathway-level integration:** Map each omic layer to pathways/gene sets, integrate at pathway level.
- Pro: Biologically interpretable, robust to noise in individual features
- Con: Limited by completeness of pathway databases; loses gene-level resolution

**Practical choice:** For clinical decision support with small-to-moderate sample sizes, pathway-level or late integration is preferred for interpretability and robustness; MOFA-style joint integration is common in discovery research with larger cohorts (TCGA-scale).

### Q2: How would you handle missing modalities when integrating multi-omic data across a real-world patient cohort?

**A:** In practice, patients rarely have complete multi-omic profiles (e.g., tumor tissue for genomics but no matched proteomics).

**Strategies:**
1. **Complete-case analysis:** Only use samples with all modalities — simplest but drastically reduces sample size and introduces selection bias (patients with more testing may be sicker/different)
2. **Modality-specific imputation:** Use cross-omic correlation structure to impute missing layers (e.g., predict expression from methylation using learned relationships) — risky if imputation model is trained on non-representative data
3. **Late-fusion models that tolerate missingness:** Train separate per-omic models; at inference, combine only available modality predictions with re-normalized weights
4. **Multi-task/shared latent variable models (e.g., MOFA+):** Naturally handle missing views during factor learning by only using observed data in the likelihood
5. **Sensitivity analysis:** Always report performance stratified by data completeness to surface bias

**Key principle:** Document and report the missingness mechanism (MCAR/MAR/MNAR assumption) — clinical multi-omic data is rarely missing completely at random (e.g., proteomics often only ordered for advanced/refractory cases).

### Q3–Q16: (Representative additional topics)
- Batch effect correction across omic platforms (ComBat, limma, RUV)
- Single-cell multi-omics (CITE-seq, multiome ATAC+RNA) analysis considerations
- Feature selection strategies for high-dimensional multi-omic data (LASSO, elastic net, stability selection)
- Pathway enrichment analysis methods (GSEA, ORA) and multiple testing correction
- Protein-genome concordance and its use in QC (identity confirmation)
- Spatial transcriptomics integration with histopathology
- Multi-omic biomarker discovery vs. validation pipeline design
- Network-based integration methods (WGCNA, similarity network fusion)
- Handling different sample sizes/depths across omic layers
- Cross-platform normalization challenges (RNA-seq vs. microarray legacy data)
- Tumor heterogeneity considerations in bulk multi-omic tumor profiling
- Germline-somatic variant deconvolution in tumor sequencing
- Longitudinal multi-omic data (treatment response trajectories)
- Multi-omic data harmonization for federated/multi-site studies

---

## Summary
Multi-omic integration requires balancing statistical power, interpretability, and missing data realities. Choice of integration strategy should match sample size, clinical interpretability needs, and downstream decision-support requirements.
