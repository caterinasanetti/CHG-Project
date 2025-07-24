# CHG-Project
A complete workflow to characterize the genomic landscape of a cancer patient from matched tumor-normal data. This was a final project for the Computational Human Genomics course at the University of Trento.

**Authors:** Maccarone Giulia, Rizzolo Maria Luce, Salsano Anna, Sanetti Caterina

## 1. Project Overview

This project focuses on the genomic analysis of a single cancer patient for precision medicine. The objective is to characterize the landscape of somatic genomic alterations (acquired in the tumor) through the computational analysis of matched tumor and normal DNA samples. The analysis aims to identify the aberrations driving tumorigenesis, define their influence on the disease, and assess their potential clinical relevance.

## 2. Key Findings

The analysis revealed a highly unstable tumor genome, characterized by critical somatic events:

*   **Driver Mutation in TP53:** A high-impact somatic splice-acceptor mutation was identified in the `TP53` tumor suppressor gene. Being absent in the normal sample and present at a high variant allele frequency (VAF ~69%) in the tumor, it was classified as an early, clonal event, fundamental to tumor development.
*   **Germline Risk Background:** The analysis highlighted a germline nonsense mutation in the `BRCA1` gene, associated with hereditary breast and ovarian cancer syndrome. This genetic predisposition context is crucial for interpreting the somatic events.
*   **Somatic Copy Number Alterations (SCNAs):** Extensive large-scale deletions were detected, leading to the loss of key tumor suppressor genes, including `BRCA1`, `PML`, `TP53BP1`, and `ERBB2`.
*   **Mutational Signatures:** The mutational signature analysis revealed a strong presence of the "clock-like" signatures **SBS1** and **SBS5** (associated with aging) and, critically, the **SBS54** signature, a well-established hallmark of Homologous Recombination Deficiency (HRD), consistent with the pathogenic `BRCA1` mutation.
*   **Purity and Ploidy:** The tumor sample was found to be of high purity (estimated between 64% and 71%), with a ploidy of approximately 2.27.

## 3. Computational Workflow Summary

The analysis pipeline was designed to ensure the highest data quality and robust variant identification.
1.  **Data Pre-processing:** The initial BAM files were processed to correct alignment artifacts (local realignment around indels with GATK) and systematic sequencing errors (Base Quality Score Recalibration - BQSR). PCR duplicates were removed with Picard.
2.  **Germline Variant Calling:** Germline variants were identified in parallel with `bcftools` and `GATK UnifiedGenotyper` to assess concordance.
3.  **SCNA Analysis:** Somatic copy number alterations were identified by comparing read depths between the tumor and normal samples using `samtools mpileup` and `VarScan2`, followed by segmentation (CBS) and annotation.
4.  **Somatic Variant Calling:** Somatic mutations (SNVs and indels) were called using VarScan2's somatic mode.
5.  **Annotation and Filtering:** All variants were functionally annotated with `SnpEff` and filtered with `SnpSift` to identify high-impact and clinically relevant events (using databases like ClinVar).
6.  **Advanced Analysis:** Tumor purity and ploidy were estimated with `CLONET.R`, and mutational signatures were analyzed with `COSMIC SigProfiler`.

## 4. Software and Tools Used

*   **Alignment & Pre-processing:** GATK (v3.x), Picard, Samtools
*   **Variant Calling:** bcftools, GATK UnifiedGenotyper, VarScan2
*   **SCNA Analysis:** VarScan2, Bedtools, R (`CBS.R` script)
*   **Annotation & Filtering:** SnpEff, SnpSift
*   **Downstream Analysis:** R (`CLONET.R` and `TPES` scripts), COSMIC SigProfiler
*   **Visualization:** Integrative Genomics Viewer (IGV)
*   **Databases:** HapMap, ClinVar, cBioPortal

