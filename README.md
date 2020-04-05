# HFproteomics

This document describes the computational analysis of the **Chan M, Motakis E, Tan SH et al. Prioritizing Post-Myocardial Infarction Heart Failure Candidates Using Plasma Proteomics and Single-Cell Transcriptomics. Submitted to Circulation, 2020 (under review)**[1]. 

The detailed pipeline is found at [edit here]

Before starting the analysis, the user is requested to clone the repository to his machine as (from the terminal):

```bash
$ git clone https://github.com/ArisStefanosSn/HFproteomics
```
This will store the folder `HFproteomics` in the working directory of the user. This folder contains all necessary files to run the pipeline. First, the zipped file `ProteomicsData.tar.gz` should be extracted as:

```bash
$ tar -xf ProteomicsData.tar.gz
```

The extracted folder `ProteomicsData` has all **data related to the plasma proteomics analysis**:

1. source.R: It contains the R libraries and functions used for this analysis. The user is requested to dowload and install the necessary R packages in his machine before performing the analysis. These packages are `Hmisc`, `limma`, `metaRNASeq`, `Rtsne`, `ggplot2`, `lawstat`, `gtools`, `superheat`, `stringr`, `WGCNA`, `gplots`, `plotly`, `scales`, `data.table`, `scater`, `scran`, `randomForest`, `splines` and `ggfortify`. Each package can be downloaded from  Bioconductor. For example, to install `limma` (from R studio):

```bash
R> if (!requireNamespace("BiocManager", quietly = TRUE))
+   install.packages("BiocManager")

R> BiocManager::install("limma")
```

2. Somalogic_Design_CDCS.txt: It contains the experimental / clinical information of each patient of the CDCS cohort. The variables have been used for data adjustment / normalisation and in the main analysis of protein prioritisation. The pipeline document contains a brief overview of the clinical variables / patient characteristics of this file.

3. Somalogic_Expression_CDCS.txt: It contains the raw protein expression data of all proteins and all CDCS cohort patients.

4. Somalogic_Annotation_CDCS.txt: It contains the protein annotation in the CDCS cohort, i.e. the Somalogic IDs, the protein full names, a short version of the protein full names, the UniProt IDs, the Entrez IDs, the protein symbols and a QC variable with values PASS (passed quality control) or FLAG (did not pass quality control).

5. Somalogic_Design_IMMACULATE.txt: It contains the experimental / clinical information of each patient of the IMMACULATE cohort. The variables have been used for data adjustment / normalisation and in the main analysis of protein prioritisation. The pipeline document contains a brief overview of the clinical variables / patient characteristics of this file.

6. Somalogic_Expression_IMMACULATE.txt: It contains the raw protein expression data of all proteins and all IMMACULATE cohort patients.

7. Somalogic_Annotation_IMMACULATE.txt: It contains the protein annotation in the IMMACULATE cohort, i.e. the Somalogic IDs, the protein full names, a short version of the protein full names, the UniProt IDs, the Entrez IDs, the protein symbols and a QC variable with values PASS (passed quality control) or FLAG (did not pass quality control). The QC variable is the nly ne that differs in the CDCS and IMMACULATE annotation files.

8. tstar.txt: It contains the 10,000 random t-test statistics and the t-test statistic of the cross-cohort reproducible 36-protein set to validate it via a subsampling based statistical testing (Section 3.4). The user is free to re-compute the values as shown in Section 3.4 with the function `clusterSignificance()` and generate a new set of results. The results will differ only slightly due to the subsampling procedure.

9. RF.txt: It contains the pre-computed prediction errors of our supervised Random Forests model to validate the cross-cohort reproducible 36-protein set (Section 3.5). The user is free to re-compute the values as shown in Section 3.5 with the function `rfGroupSeparation()` and generate a new set of results. The results will differ only slightly due to the subsampling procedure.

10. DiNA.txt: It contains the pre-computed differential connectivity estimates of our DiNA model of Section 4.1. The user is free to re-compute the values as shown in Section 4.1 with the functions `wgcnaStatsFromPermutation()` and `summariseDiNA()` and generate a new set of results. The results will differ only slightly due to the subsampling procedure.

11. CytoscapeInput_HF_edges_blue.txt: It contains the edges of the WGCNA network of the HF patients. It is used to retrieve all the proteins that are directly connected to the significant network proteins of our study.

**The data related to the transcriptomics analysis** of Section 5 are stored in the *.RData* format. Each dataset consists of three components, i.e. a matrix of normalised gene expression profiles for *G* genes and *N* samples (cells or nuclei), a matrix summarising the design of the experiment and the characteristics of the *N* samples and a matrix of pre-computed differential expression estimates forthe *G* genes. Specifically: 

1. nonMyo.RData: It contains the data of the 440 Sham and 390 MI mouse cardiac fibroblasts of our respective single-cell RNA-seq expreriment [2]. The raw data are available upn reasonable request from the authors. The differential expression analysis was done with Seurat comparing the Sham vs MI conditions.

2. snMyo.RData: It contains the data of the 85 Sham and 100 TAC high-quality cardiomycyte nuclei of our single-nuclei RNA-seq experiment [3]. The raw data are available from **NCBI SRA SRP049944**, under the BioProject code PRJNA264588. The differential expression analysis was done with edgeR comparing the Sham vs TAC conditions.

3. tsMyo.RData: It contains the data of the 88 Sham, 69 day-3 TAC, 83 day-7 TAC and 73 4-weeks TAC high-quality cardiomycytes of the single-cell RNA-seq experiment **GSE95140**[4]. The differential expression analysis was done with edgeR comparing all pairwise Sham vs TAC conditions.

4. hMyo.RData: It contains the data of the 71 Healthy and 488 DCM high-quality human cardiomycytes of the single-cell RNA-seq experiment **GSE95140**[4]. The differential expression analysis was done with edgeR comparing the Healthy vs DCM conditions.

## References

[1] Chan M, Motakis E, Tan SH et al. Prioritizing Post-Myocardial Infarction Heart Failure Candidates Using Plasma Proteomics and Single-Cell Transcriptomics. Submitted to Circulation, 2020 (under review).

[2] Ackers-Johnson M, Li PY, Holmes AP, O'Brien SM, Pavlovic D and Foo RS. A Simplified, Langendorff-Free Method for Concomitant Isolation of Viable Cardiac Myocytes and Nonmyocytes From the Adult Mouse Heart. Circ Res. 2016;119:909-20.

[3] See K, Tan WLW, Lim EH, Tiang Z, Lee LT, Li PYQ, Luu TDA, Ackers-Johnson M and Foo RS. Single cardiomyocyte nuclear transcriptomes reveal a lincRNA-regulated de-differentiation and cell cycle stress-response in vivo. Nature communications. 2017;8:225.

[4] Nomura S, Satoh M, Fujita T, Higo T, Sumida T, Ko T, Yamaguchi T, Tobita T, Naito AT, Ito M, Fujita K, Harada M, Toko H, Kobayashi Y, Ito K, Takimoto E, Akazawa H, Morita H, Aburatani H and Komuro I. Cardiomyocyte gene programs encoding morphological and functional signatures in cardiac hypertrophy and failure. Nat Commun. 2018;9:4435.
