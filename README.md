# HFproteomics

This document describes the computational analysis of the **Chan M, Motakis E, Tan SH et al. Prioritizing Post-Myocardial Infarction Heart Failure Candidates Using Plasma Proteomics and Single-Cell Transcriptomics. Submitted to Circulation, 2020 (under review)**. The detailed pipeline is found at [edit here]

Before staring the analysis, the user is requested to clone the repository to his machine as:

```bash
git clone https://github.com/ArisStefanosSn/HFproteomics
```
This will store the folder `HFproteomics` in the working directory of the user. This folder contains all necessary files to run the pipeline. Specifically, subfolder `ProteomicsData` has all data related to the plasma proteomics analysis:

1. source.R: It contains the R libraries and functions used for this analysis. The user is requested to dowload and install the necessary R packages in his machine before performing the analysis. These packages are `Hmisc`, `limma`, `metaRNASeq`, `Rtsne`, `ggplot2`, `lawstat`, `gtools`, `superheat`, `stringr`, `WGCNA`, `gplots`, `plotly`, `scales`, `data.table`, `scater`, `scran`, `randomForest`, `splines` and `ggfortify`. Each package can be downloaded from  Bioconductor as

```bash
if (!requireNamespace("BiocManager", quietly = TRUE))
    install.packages("BiocManager")

BiocManager::install("limma")
```

Somalogic_Design_CDCS.txt: It contains the experimental / clinical information of each patient of the CDCS cohort. The variables have been used for data adjustment / normalisation and in the main analysis of protein prioritisation.

Somalogic_Expression_CDCS.txt: It contains the raw protein expression data of all proteins and all CDCS cohort patients.

Somalogic_Annotation_CDCS.txt: It contains the protein annotation in the CDCS cohort, i.e. the Somalogic IDs, the protein full names, a short version of the protein full names, the UniProt IDs, the Entrez IDs, the protein symbols and a QC variable with values PASS (passed quality control) or FLAG (did not pass quality control).

Somalogic_Design_IMMACULATE.txt: It contains the experimental / clinical information of each patient of the IMMACULATE cohort. The variables have been used for data adjustment / normalisation and in the main analysis of protein prioritisation.

Somalogic_Expression_IMMACULATE.txt: It contains the raw protein expression data of all proteins and all IMMACULATE cohort patients.

Somalogic_Annotation_IMMACULATE.txt: It contains the protein annotation in the IMMACULATE cohort, i.e. the Somalogic IDs, the protein full names, a short version of the protein full names, the UniProt IDs, the Entrez IDs, the protein symbols and a QC variable with values PASS (passed quality control) or FLAG (did not pass quality control). The QC variable is the nly ne that differs in the CDCS and IMMACULATE annotation files.

RF.txt: It contains the pre-computed prediction errors of our supervised Random Forests model (Section 3.5). The user is free to re-compute the values as shown in Section 3.5 with the function rfGroupSeparation() and generate a new set of results. The results will differ only slightly due to the subsampling procedure.

DiNA.txt: It contains the pre-computed differential connectivity estimates of our DiNA model of Section 4.1. The user is free to re-compute the values as shown in Section 4.1 with the functions wgcnaStatsFromPermutation() and summariseDiNA() and generate a new set of results. The results will differ only slightly due to the subsampling procedure.
