# Acute Myeloid Leukemia Heatmap Analysis

This repository contains an R Notebook for analyzing acute myeloid leukemia (AML) RNA-sequencing data through clustering heatmaps.
OTHER TRY ISIS
## Overview

This analysis uses RNA-sequencing data from 19 AML model mice to create annotated heatmaps that visualize gene expression patterns and sample clustering. The dataset includes different types of AML mutations (IDH2, TET2, and wild-type) under various treatment conditions.

## Data Source

- **Dataset**: [SRP070849](https://www.refine.bio/experiments/SRP070849) from refine.bio
- **Publication**: [Shih et al., 2017](https://pubmed.ncbi.nlm.nih.gov/28193779/)
- **Samples**: 19 acute myeloid leukemia model mice
- **Processing**: Pre-processed and quantile normalized by [refine.bio](https://www.refine.bio/)

## Analysis Features

### Sample Types
- **IDH2 mutant AML**: Treated with vehicle or AG-221 (first small molecule in-vivo inhibitor of IDH2)
- **TET2 mutant AML**: Treated with vehicle or 5-Azacytidine (Decitabine, hypomethylating agent)
- **Wild-type (WT)**: Control samples

### Key Analyses
1. **Gene filtering**: Selects genes in the upper quartile by variance
2. **Hierarchical clustering**: Both samples and genes
3. **Annotated heatmap**: Color-coded by mutation type and treatment
4. **Expression visualization**: Row-scaled gene expression patterns

## File Structure

```
├── data/
│   └── SRP070849/
│       ├── SRP070849.tsv              # Gene expression matrix
│       └── metadata_SRP070849.tsv      # Sample metadata
├── plots/                              # Generated plots
├── results/
│   └── top_90_var_genes.tsv           # Filtered high-variance genes
└── analysis_notebook.Rmd              # Main analysis file
```

## Requirements

### R Packages
- `pheatmap` - For clustering and heatmap generation
- `magrittr` - For pipe operations (`%>%`)
- `readr` - For reading TSV files
- `dplyr` - For data manipulation
- `tibble` - For data frame operations

### Installation
```r
# Install required packages if not already installed
if (!("pheatmap" %in% installed.packages())) {
  install.packages("pheatmap", update = FALSE)
}

# Load libraries
library(pheatmap)
library(magrittr)
library(readr)
library(dplyr)
library(tibble)
```

## Usage

1. **Download the data** from [refine.bio](https://www.refine.bio/experiments/SRP070849)
2. **Place data files** in the `data/SRP070849/` directory:
   - `SRP070849.tsv` (gene expression matrix)
   - `metadata_SRP070849.tsv` (sample metadata)
3. **Run the analysis** by executing the R Notebook
4. **View results** in the generated plots and results directories

## Key Analysis Steps

### 1. Data Import and Setup
- Reads gene expression matrix and metadata
- Sets gene IDs as row names
- Ensures sample order consistency between datasets

### 2. Gene Selection
- Calculates variance for each gene
- Filters genes in the upper quartile (75th percentile) by variance
- Saves filtered gene list to results directory

### 3. Metadata Preparation
- Extracts mutation type from sample titles (IDH2, TET2, WT)
- Prepares annotation data frame for heatmap
- Maps treatment conditions to samples

### 4. Heatmap Generation
- Creates hierarchical clustering of both genes and samples
- Applies row-wise scaling (z-score normalization)
- Uses custom color palette (blue-black-yellow gradient)
- Annotates samples by mutation type and treatment

## Output Files

- `results/top_90_var_genes.tsv` - High-variance genes used in analysis
- Annotated heatmap visualization showing:
  - Gene expression patterns across samples
  - Sample clustering by mutation type and treatment
  - Color-coded annotations for easy interpretation

## Customization Options

### Gene Selection Criteria
The current analysis uses variance-based gene selection, but you can modify the filtering criteria:
- Fold change analysis
- Statistical significance (t-statistics)
- Gene ontology membership
- Pathway-specific genes

### Visualization Parameters
- Color schemes can be adjusted in the `colorRampPalette()` function
- Clustering methods can be modified through `pheatmap()` parameters
- Annotation colors and labels can be customized

## References

- **Original Analysis**: [refine.bio-examples notebook](https://alexslemonade.github.io/refinebio-examples/03-rnaseq/clustering_rnaseq_01_heatmap.html)
- **Publication**: Shih et al., 2017. "The role of IDH2 mutations in acute myeloid leukemia"
- **Data Source**: Childhood Cancer Data Lab (CCDL) for ALSF
- **Adaptation**: Candace Savonen, October 2021

## License

This analysis is adapted from the refine.bio-examples repository and follows their licensing terms.

---

For questions or issues with this analysis, please refer to the original refine.bio-examples documentation or submit an issue to this repository.