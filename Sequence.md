---
layout: page
title: Sequence Analysis
group: navigation
weight: 2
---

~~# Sub-Project 1: calculate FPKM from given SAM and GTF files~~

> Please carefully read through and follow the formatting guideline found in [Project 1.2](http://cbb752spring2016.github.io/QCStep)

# Quantifying RNA-seq Using RPKM/FPKM/TPM Based on SAM & GTF Files

## English Card, Brought by Edmond Dantes

RNA-Seq is a relative measurement instead of an absolute one (1). Therefore, it is crucial to normalize samples in order for them to be comparable across experiments (1). Since features differ in length it is necessary to adjust for different lengths as this will affect the number of reads that are produced for different features (1). TPM gives us the number of transcripts of a certain type relative to the proportion of all the other transcripts present in the sample (2). The transcript fraction or (tau) is independent of the mean expressed transcript length (2). While the mean expressed transcript length is likely to vary from sample to sample (3). 

For this reason, TPM offers a net advantage over FPKM because the TPM values are more comparable across species and between samples even if the transcript lengths differ whereas FPKM will offer different results (3). In order to calculate TPM we start by calculating the counts per base (1). We can observe that this rate is dependent on the number of fragments sequenced (1). In order to control for this we can divide this rate by the sum of all the rates recorded (1). This calculation will provide us with the proportion of transcripts in our sample (1). The proportion of transcripts in our sample can then be multiplied by a million to facilitate interpretation (2). FPKM uses the same rate calculated for TPM but divides it by the total number of reads sequenced and then multiplies it by a billion (1).

![alt text][tpm]

[tpm]: https://s0.wp.com/latex.php?latex=%5Ctext%7BTPM%7D_i+%3D+%5Cdfrac%7BX_i%7D%7B%5Cwidetilde%7Bl%7D_i%7D+%5Ccdot+%5Cleft%28+%5Cdfrac%7B1%7D%7B%5Csum_j+%5Cdfrac%7BX_j%7D%7B%5Cwidetilde%7Bl%7D_j%7D%7D+%5Cright%29+%5Ccdot+10%5E6&bg=ffffff&fg=000000&s=0 "Formula for TPM"

For TPM: X_i and X_j represent the counts for both the feature of interest, and the overall sample (1).
         L_i and L_j represent the effective lengths for both the feature of interest, and the overall sample (1).

![alt text][fpkm]

[fpkm]: https://s0.wp.com/latex.php?latex=%5Ctext%7BFPKM%7D_i+%3D+%5Cdfrac%7BX_i%7D%7B+%5Cleft%28%5Cdfrac%7B%5Cwidetilde%7Bl%7D_i%7D%7B10%5E3%7D%5Cright%29+%5Cleft%28+%5Cdfrac%7BN%7D%7B10%5E6%7D+%5Cright%29%7D+%3D+%5Cdfrac%7BX_i%7D%7B%5Cwidetilde%7Bl%7D_i+N%7D+%5Ccdot+10%5E9++&bg=ffffff&fg=000000&s=0 "Formula for FPKM"
         
For FPKM: X_i represents the count of the feature of interest (1).
          L_i represents the effective length of the feature of interest (1).
          N represents the total number of reads sequenced (1). 

Below we propose two tools that allow the calculation of TPM from given SAM and GTF files in both Python and R.

SAM stands for "Sequence Alignment/Map". It is a standard, tab-delimited format produced by alignment software. Each alignment line in SAM has 11 mandatory fields for essential alignment information such as mapping position, and variable number of optional fields for flexible or aligner specific information (4). More details on SAM format specification can be found [here](http://samtools.github.io/hts-specs/SAMv1.pdf). Because of their usually large file sizes, SAM files are more commonly stored as BAM files, which are the machine-readable, binary version of SAM files, and can be converted using [Samtools](http://www.htslib.org/). 

GTF stands for "Gene Transfer Format". It is a standard, tab-delimited format commonly used for describing the structure of transcripts (introns, exons, start sites, UTRs, etc.) and how transcripts are related to the genes they encode. Each line in GTF has 9 mandatory fields: the first eight represent locations along the genome, information about how those regions were defined, and what they represent; and the last, "attributes" field contains information about the relationships between genes and their transcripts (4). More details on GTF format specification used in GENCODE can be found [here](http://www.gencodegenes.org/data_format.html).

Given a SAM file, which informs one the location in the genome to which each read is mapped, and a GTF file, which informs one the gene located at a given location in the genome, one could start calculating the read depth at each base position within the range of a given gene. 

### References

1) Pimentel, H. (2015). What the FPKM? A review of RNA-Seq expression units. Retrieved from https://haroldpimentel.wordpress.com/2014/05/08/what-the-fpkm-a-review-rna-seq-expression-units/

2) Li, B., Ruotti, V., Stewart, R. M., Thomson, J. A., & Dewey, C. N. (2009). RNA-Seq gene expression estimation with read mapping uncertainty. Bioinformatics, 26(4), 493–500. http://doi.org/10.1093/bioinformatics/btp692

3) Li, B., & Dewey, C. N. (2011). RSEM: accurate transcript quantification from RNA-Seq data with or without a reference genome. BMC Bioinformatics, 12, 323. http://doi.org/10.1186/1471-2105-12-323

4) Davis, S. File Formats and RNA-seq. Retrieved from http://watson.nci.nih.gov/~sdavis/tutorials/RNASeqBeginnerTutorial/RNASeqTutorial.html

## [R Card](https://github.com/jqz752/cbb752_2.2_R), Brought by Julian

> This is mostly a comment on formatting, but very good job on detailed usage information. I would just assign this project a unified name and change the title on readme.

## Python Card, Brought by Kevin
Source code and readme file [here](https://github.com/kevkid/cbb752_2.2_py)

> Good job on general description about methodology, however I would put more information about usage information of your python code. Currently, its minimal and simple, but sample input and expected output format and parameter information would be useful here.

---

# Sub-Project 2: calculate differentially expressed genes from GCT file of gene expressions

## Python Card, Brought by Heather


## R Card, Brought by Calvin


## English Card, Brought by Edmond Dantes



# Assessing k-mer Enrichment of FASTA Sequences

## [Python Card](https://github.com/EdKong/2.6_kmer_enrichment), Brought by ELK


## [R Card](https://github.com/jqz752/cbb752_2.6_R), Brought by Julian


## English Card, Brought by Nathan

#### What is a k-mer and its purpose?  

K-mer is a bioinformatics term which corresponds to the substring of length k in a string obtained from DNA sequencing (Pevzner, et al. 2001). Mathematically, the number of possible k-mers in a given string of length l is: l – k + 1. K-mer anlysis is often done along with De Brujin graphs for sequence assembly. The de Bruijn graph is composed of the nodes being (k – 1)-mers and the edges being the k-mers. Basically the graph is made and simplified such that contiguous regions of the genome are identified (Chikhi and Medvedev, 2014). K-mer algorithms are designed to better resolve genomic shotgun assembly. Previous algorithms designed to organize the assembly were inadequate in solving the “repeat problems” in finding the correct path to the graph. The current k-mer algorithm is widely used as a simpler and less error-prone way for large scale genomes assembly.  


#### How to find the k-mer size ideal for sequence assembly? 

The de Brujin graph is constructed from a collection of sequencing reads without knowing the finished sequence. Pevzner et al., 2001 was able to correct the errors in reads and visualize the final sequences before making the graph by using the approximation that the sequence of a genome while unknown we can find the a set of tuples in this genome. In general, picking a smaller k-mer size for analysis will improve data management as edge counts of the de Brujin graph decrease (Zerbino and Birney, 2008). The tradeoff is potential for higher k-mer sequences overlap and more ambuigities when constructing the genome. Higher k-mer size will make working with de Brujin graph longer to process and possibility for non-overlapping. The advantage is constructing the final genome would be easier and lower possibility for repetition. 


#### What algorithm our tool uses to define k-mer enrichment? 

Our tool answers the question “is a k-mer sequence being overrepresented in a given l-length sequence?” The software will take in a FASTA file as input and a user specified k-mer string such as “CATTAG”. The output of this program will be the expected and actual counts of hits to this specific k-mer string, as well as the p-value for this binomial distribution. The program will first count all the bases A, C, G, T in the file, then it will scan the file to find the probability of seeing the specified k-mer. Since a base has the possibility to be one out of four bases, there will be 4^k possible sequences, and the probability for a single match of 2 random sequences is 1/(4^k). Our tool will utilize a scanning window to check for an exact match to the k-mer. The statistics we are using will be the Bernoulli distribution, where the expected counts of hits will be obtained from independent Bernoulli trials. The p-value is p = 1/(4^k), so the binomial distribution has parameters p = 1/(4^k) and n = L-k+1. 

Reference:

Pevzner, P. et al., 2001. An Eulerian path approach to DNA fragment assembly. Proc Natl Acad Sci U S A. 98(17): 9748-9753. 

Chikhi, R. and Medvedev, P., 2014. Informed and automated k-mer size selection for genome assembly. Bioinformatics. 30(1):31-37.

Zerbino, D. and Birney, E., 2008. Velvet: algorithms for de novo short read assembly using de Brujin graphs. Genome Research. 18(5):821-829.
