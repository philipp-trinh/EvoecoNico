# EvoecoNico – Nicotiana Differential Expression Analysis

RNA-seq differential expression and functional enrichment analysis of *Nicotiana truncata* and *N. excelsior* roots under drought versus control conditions.

This repository contains the analysis code developed for the **WS23/24 Plant Ecological Genomics course** at the **Botany Institute, University of Vienna**.

---

## Overview

The project implements a complete RNA-seq analysis workflow in **R**, starting from STAR/featureCounts output and ending with statistically filtered differentially expressed genes and GO term enrichment results.

The analysis is organized as an **R Markdown notebook** and a set of reusable helper functions that handle data preprocessing, differential expression, quality control, and functional interpretation.

---

## Analysis Workflow

### Data input and preprocessing
- Import of STAR/featureCounts gene count tables.
- Programmatic cleanup of sample and column names.
- Definition of experimental design via compact metadata strings.
- Automatic generation of consistent sample identifiers (e.g. `ECR61`, `TDR90`).
- Construction of sample metadata tables for downstream modeling.
- Automated subsetting by:
  - Species (*N. excelsior*, *N. truncata*)
  - Treatment (drought vs control)
  - Outlier-filtered datasets based on PCA inspection.

### Differential expression analysis
- Differential expression testing using **DESeq2** (`drought vs control`).
- Log2 fold-change shrinkage with **apeglm**.
- Optional CPM-based gene filtering using **edgeR** utilities.
- Statistical diagnostics and quality control:
  - MA plots and dispersion plots
  - Independent filtering inspection
  - Cook’s distance–based outlier detection
- Export of structured DEG tables with effect sizes, p-values, FDR, and regulation direction.

### CPM filtering and threshold exploration
- Custom edgeR-based helper functions to evaluate:
  - Mean CPM thresholds
  - Number of retained genes
  - Number of significant genes at different filter levels
- Generation of plots relating CPM thresholds to DEG counts.

### Functional enrichment (GO analysis)
- GO enrichment analysis for BP, MF, and CC using **topGO**.
- Consolidation of GO results across ontologies.
- Attachment of DEG lists to enriched GO terms.
- Calculation of GO-level z-scores based on gene log2 fold changes.
- Automated generation of:
  - GO barplots (z-score colored)
  - GO network graphs (topGO).

---

## Implemented Scripts and Functions

The repository includes custom R code for:

- Metadata parsing and sample ID generation.
- Species- and condition-specific dataset construction.
- CPM filtering and DEG threshold evaluation (edgeR).
- DESeq2 result structuring and export.
- Gene ID ↔ index mapping utilities.
- GO enrichment wrappers and result aggregation.
- GO barplot and network plot generation.

These scripts are integrated into a single reproducible workflow but can be reused independently.

---

## Technologies

- **Language:** R (R Markdown)
- **Differential expression:** DESeq2, edgeR, apeglm
- **Data handling:** tidyverse, dplyr, tibble, readxl, xlsx
- **Visualization:** ggplot2, ggpubr, plotly, pheatmap, ggrepel
- **Functional enrichment:** topGO, GOplot, gprofiler2
