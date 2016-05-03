---
group: navigation
layout: page
title: Sequence Analysis
---

# Sub-Project 1: calculate FPKM from given SAM and GTF files

## English Card, Brought by Edmond Dantes

RNA-Seq is a relative measurement instead of an absolute one (1). Therefore, it is crucial to normalize samples in order for them to be comparable across experiments (1). Since features differ in length it is necessary to adjust for different lengths as this will affect the number of reads that are produced for different features (1). TPM gives us the number of transcripts of a certain type relative to the proportion of all the other transcripts present in the sample (2). The transcript fraction or (tau) is independent of the mean expressed transcript length (2). While the mean expressed transcript length is likely to vary from sample to sample (3). 

For this reason, TPM offers a net advantage over FPKM because the TPM values are more comparable across species and between samples even if the transcript lengths differ whereas FPKM will offer different results (3). In order to calculate TPM we start by calculating the counts per base (1). We can observe that this rate is dependent on the number of fragments sequenced (1). In order to control for this we can divide this rate by the sum of all the rates recorded (1). This calculation will provide us with the proportion of transcripts in our sample (1). The proportion of transcripts in our sample can then be multiplied by a million to facilitate interpretation (2). 

![alt text][tpm]

[tpm]: https://s0.wp.com/latex.php?latex=%5Ctext%7BTPM%7D_i+%3D+%5Cdfrac%7BX_i%7D%7B%5Cwidetilde%7Bl%7D_i%7D+%5Ccdot+%5Cleft%28+%5Cdfrac%7B1%7D%7B%5Csum_j+%5Cdfrac%7BX_j%7D%7B%5Cwidetilde%7Bl%7D_j%7D%7D+%5Cright%29+%5Ccdot+10%5E6&bg=ffffff&fg=000000&s=0 "Formula for TPM"

Xi and Xj represent the counts for both the feature of interest, and the overall sample (1).
Li and Lj represent the effective lengths for both the feature of interest, and the overall sample (1).

Below we propose two tools that allow the calculation of TPM from given SAM and GTF files in both Python and R.

### References

1) Pimentel, H. (2015). What the FPKM? A review of RNA-Seq expression units. Retrieved from https://haroldpimentel.wordpress.com/2014/05/08/what-the-fpkm-a-review-rna-seq-expression-units/

2) Li, B., Ruotti, V., Stewart, R. M., Thomson, J. A., & Dewey, C. N. (2009). RNA-Seq gene expression estimation with read mapping uncertainty. Bioinformatics, 26(4), 493–500. http://doi.org/10.1093/bioinformatics/btp692

3) Li, B., & Dewey, C. N. (2011). RSEM: accurate transcript quantification from RNA-Seq data with or without a reference genome. BMC Bioinformatics, 12, 323. http://doi.org/10.1186/1471-2105-12-323

## R Card, Brought by Julian

Source code and readme file available [here](https://github.com/jqz752/cbb752_2.2_R).

## Python Card, Brought by Kevin
Source code and readme file[here](https://github.com/kevkid/cbb752_2.2_py)

# Sub-Project 2: calculate differentially expressed genes from GCT file of gene expressions

## Python Card, Brought by Heather


## R Card, Brought by Calvin


## English Card, Brought by Edmond Dantes



# Sub-Project 3: find k-mer motif enrichment from a given nucleotide sequence

## Python Card, Brought by ELK


## R Card, Brought by Julian


## English Card, Brought by Nathan
