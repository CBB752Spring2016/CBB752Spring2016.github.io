---
layout: page
title: Network Analysis
group: navigation
weight: 3
---


#### English Card, Brought by Aparna

##### Background

###### Co-expressed gene networks

Gene co-expression analysis is a valuable tool for understanding biological interactions. Co-expressed genes may be involved in the same pathways or have related functions. This also offers insight into the interactions of their protein products. 
One useful way of thinking about and visualizing co-expression is through gene co-expression networks. These are undirected graphs where each node represents a gene and each edge connecting two nodes represents the co-expression of the two genes represented by those nodes. An especially valuable characteristic of gene co-expression networks is that they can be analyzed by traditional computational methods for graphs. Specifically, one of the most biologically relevant analyses is the identification of clusters of co-expressed genes, which can be calculated with minimum cut and other similar network algorithms. 
Within the context of the broader applications of these networks, this project tasked us with developing just the basics: creating a tool to calculate co-expressed gene networks from GCT files of gene expressions.

###### WGCNA

Some pre-existing softwares have similar functions, but they are generally part of larger packages. One such package is WGCNA, a widely used R package that uses weighted correlation network analysis to identify clusters of genes from expression data.[1][2] The package’s functions are not limited to identifying co-expressed genes — rather, that is just one of many tools it offers. Some other functionalities include constructing a network based on the co-expression information, characterizing and visualizing the resulting network, identifying modules (based on minimizing the weights of cuts in the graph), and linking gene clusters to each other and to biologically-relevant data.
For our purposes, the most relevant part of the WGCNA package is its network construction function. Each gene is treated as a node, and edges are constructed between nodes with correlated gene expression patterns. The WGCNA method calculates Pearson correlation coefficients for each pair of genes’ expression profile — the absolute value of this metric is called sij, the co-expression similarity, and falls within the range [0,1]. 
The next step is to construct an adjacency matrix, which will be directly translated into the gene network. Each entry aij of the adjacency matrix represents the degree of co-expression between genes i and j. aij can be calculated based on sij and a pre-determined threshold τ, representing the minimum degree of similarity required for the expression of the two genes to be considered correlated. If sij is greater than τ, aij equals 1; otherwise, aij equals 0. This method is called the unweighted method, because the resulting edges in the network do not have variable weights. The weighted method gives the edges weights corresponding to their actual co-expression similarities, and does not exclude gene pairs on the basis of a threshold. In this method, aij = sij^β, where β is a constant greater than or equal to 1. And so, with either method, the adjacency matrix contains all the co-expression data for the gene network.

##### Our Software

We present new software designed to complete the isolated task of constructing a co-expressed gene network from gene expression data. There are Python and R versions of the program, but both use the same algorithm to convert GCT file inputs into a network characterization.

###### Input

The program requires gene expression data as an input, and also accepts a significance threshold and output file name as optional inputs. If a significance threshold is not provided, 0.05 is used as a default. If an output file name is not provided, “output.csv” is used as a default.
Gene expression data must be provided in Gene Cluster Text (GCT) file format. This tab-delimited format can be easily parsed, and offers just the required information: gene name, gene description, expression in each sample. It is important that the correct input file format is used for accurate parsing. For example, RES file format — an alterative for gene expression data — would not be parsed correctly because it also contains extra columns for labeling each gene as absent or present in each sample.
For consistency, data files should be pre-processed. This is not within the specifications for our software but can be easily accomplished with outside tools. The sample input provided (all_aml_train.preprocessed.gct) has been pre-processed with the GenePattern PreProcessDataset module.[3] The parameters are as follows:
* Apply floor, ceiling and variation filter: yes
* Value for floor threshold: 20
* Value for ceiling threshold: 20000
* Minimum fold change for variation filter: 3
* Minimum delta for variation filter: 100
* Number of outliers per row to ignore when calculating row min and max for variation filterrow normalization: 0
* Perform row normalization: no

###### Co-expression calculations

The first step of constructing the co-expressed gene network is to identify genes with correlated expression patterns. First, a Bonferroni correction is used to adjust the threshold p-value (either provided or default) to accommodate multiple hypotheses. Then, the correlation between expression patterns is calculated for every pair of genes. The Pearson correlation coefficient is used as the measure of correlation, and a p-value is calculated for each gene pair based on the t-statistic (assuming the Pearson correlation coefficient follows the Student’s t-distribution). Gene pairs are considered to be co-expressed if their p-value is less than or equal to the Bonferroni-corrected threshold p-value.
The output file contains each co-expressed gene pair, along with its Pearson correlation coefficient, t-statistic, and p-value. One difference between the Python and R programs is that the p-values in the Python program’s output are Bonferroni-corrected, while the p-values in the R program’s output are uncorrected. These two types of information are valuable in different settings, depending on the experimenter’s next steps. Overall, this comprehensive output not only identifies co-expressed genes, but also retains the statistical measures in order to evaluate the degree of co-expression and compare gene pairs’ relative co-expression.

###### Network construction

The output resulting from the previous step provides all the information required for characterizing the co-expressed gene network. Each gene is represented by a node in the network, and each gene pair with correlated expression patterns (based on the significance of the p-value from their Pearson correlation coefficient) is represented as an edge between those two genes. In a weighted graph, the Pearson correlation coefficient can be used to weight the edges proportionally to the degree of co-expression. In an unweighted graph, edges can all have equal weights.
The actual visualization of the graph is not part of the software’s functionality. However, outside tools can again be used to quickly construct clean graphs. One such tool is Cytoscape, a network visualization tool designed to handle biological interaction data.[4] Cytoscape accepts the output file of our software and constructs a network visualization that clearly displays the clusters of co-expressed genes. A sample image is provided, based on the output of running the software on the all_aml_train.preprocessed.gct input file (Figure 1).

###### Comparison to WGCNA

Although this software was not developed based on WGCNA, the two methods share many similarities. Both softwares use similar methods of calculating correlation coefficients and using adjustable thresholds to determine the degree of correlation. However, there are a few core differences between the approaches.
First, the use of the threshold is one that differs between our software and WGCNA — although there is even some discrepancy among different applications of WGCNA. The WGCNA package contains a function called signumAdjacencyFunction that is used for unweighted graphs. To construct unweighted graphs, a threshold is used to delineate the difference between significant correlation (an edge) and insignificant correlation (no edge). However, as its name suggests, the core WGCNA algorithm is based on weighted graphs. In these cases, there is an edge between every pair of gene nodes. The weight of the edge is proportional to the strength of gene expression pattern correlation. Our software falls in between the weighted and unweighted methods. While we do use a threshold to eliminate gene pairs without statistically significant correlation in gene expression patterns, we retain information about the degree of correlation, allowing a weighted graph to be constructed. An additional benefit of our software is that the user has fine control over the threshold; if they prefer that all possible edges are included in the network (like WGCNA’s weighted method), they can set the threshold to 1 so that no gene pairs are excluded.
Even when the unweighted WGCNA method is used, there are some differences in the way the threshold is calculated. Our software extends the calculation of the correlation coefficient one step further to actually carry out a Student’s t-test and calculate the p-value. This determines the statistical significance of the correlation coefficient, and as an added benefit, the output file contains the correlation coefficient, t-statistic, and p-value, permitting further inspection of these values. WGCNA, on the other hand, does not assess statistical significance, and instead tries to build a scale-free network. The threshold is applied directly to sij (absolute value of correlation coefficient), but the user does not have to provide the threshold; instead, there are two functions pickSoftThreshold and pickHardThreshold that test various potential thresholds to determine which best fits a scale-free network topology. Studies have found that threshold selection based on network structure offers more biologically relevant results than selection methods based on probabilities, so this is an advantage of the WGCNA method.[5]
Another difference is the scope of the two softwares. As a package, WGCNA is able to carry out a wider range of functions, many of which help visualize the network, identify clusters, analyze connections, and draw biological conclusions. Even though our software does not have this expanded functionality, it has been designed to be modular (accepting widely-used GCT files and producing output files that are easily used by other softwares), so it is likely that ancillary functions could be developed to form more thorough gene co-expression analysis pipelines.

#### [Python Card](https://github.com/EdKong/CBB752_Final_Project_3.1), Brought by ELK

#### [R Card](https://github.com/dspak/CBB752_Final_Project_3.1), Brought by Dan

#### References

1. Langfelder, P. & Horvath, S. WGCNA: an R package for weighted correlation network analysis. BMC Bioinformatics 9(559), (2008)
2. Zhang, B. & Horvath, S. A General Framework for Weighted Gene Co-expression Network Analysis. Stat Appl Genet Mol Biol 4, Article 17 (2005)
3. Kuehn, H., Liberzon, A., Reich, M. & Mesirov, J.P. Using GenePattern for Gene Expression Analysis. Current Protocols in Bioinformatics 22, 7.12.1–7.12.39 (2008)
4. Shannon, P. et al. Cytoscape: a software environment for integrated models of biomolecular interaction networks. Genome Research 13(11), 2498-504 (2003)
5. Borate, B.R., Chesler, E.J., Langston, M.A., Saxton, A.M. & Voy, B.H. Comparison of threshold selection methods for microarray gene co-expression matrices. BMC Res Notes 2, 240 (2009)

#### Figures

Figure 1: Visualization of co-expression network. Cytoscape was run on output file (output_coexpression.csv) yielded by running pre-processed input file (all_aml_train.preprocessed.gct) through Python version of software.

![Figure 1]({{site.url}}/assets/images/output_coexpressed.png "Figure 1")

---

# Calculating Centrality for Proteins from MITAB2.5 PPI Files

#### English Card, Brought by Edmond Dantes

# Network Centrality

The analysis of the dynamic nature of gene networks holds remarkable potential in uncovering previously unknown biological phenomena. Protein to protein interactions or (PPIs) are of particular interest in the study of gene expression and proteomics (2).  PPIs are crucial to both the functional and structural roles of all biological processes (2). One can think of a PPI network as a collection of nodes interconnected by edges in various fashions (2). In PPIs, nodes represent proteins while edges represent the interaction between two connected proteins (2). Three steps are generally involved in the building of a PPI network, including: identification of genes of interest, using the input to search for interaction data on a PPI database, and the actual network analysis (2). A topological analysis of the resulting network can then help identify nodes that act as hubs and may be developed into biomarkers or therapeutic targets (2). Subsequently, one can break down the network into smaller units(modules) in order to identify areas with more activity (2).  Information derived from PPIs allows for the calculation of both degree centrality and betweenness centrality of co-expressed gene networks (2).   

# Degree and Betweenness Centrality

Degree centrality as well as betweenness centrality are core definitions of a network’s topology. Defining the centrality of a node/s allows one to identify the most highly connected nodes in a network (1). One can then infer the relative importance of a node based on how many nodes it is connected to (1). Nodes with a high degree of centrality will disproportionally affect the functioning of a network if they are altered which may lead to disease (1). In order to calculate degree centrality we divided the degree of a vertex by (n-1). Here the degree of a vertex referred to the number of edges connected to a vertex and n to the total number of vertices. 

Betweenness centrality allows one to evaluate how many pairs of nodes would have to cross a particular node of interest in order to reach one another while minimizing the number of movements (1). We chose the Brandes algorithm to calculate betweenness centrality due to its faster execution (3).

![alt text](https://upload.wikimedia.org/math/4/c/c/4cc6eaa2dce9d504feeed5bd88b96d73.png "Betweenness centrality") (3)
 
CB is the general formula to determine betweenness centrality for a particular vertex or ν (3). Where σst(ν) represents the number of shortest paths connecting s and t passing through ν (1). While σst represents the total number of shortest paths (1). 

# MITAB 2.5 File Format

The MITAB 2.5 format describes binary PPI data where each row corresponds to a pair of interactors (4). The columns are separated by tabulations (4). Unique identifiers for interactors A and B are represented in columns 1 and 2 (4). Alternative identifiers for protein A and B can be found in columns 3 and 4 (4). And aliases for interactors A and B can be found in columns 5 and 6 (4). The seventh column corresponds to the interaction detection method (4).  The eighth and ninth columns correspond to the first author and the identifier for the publication (4). The tenth and eleventh columns correspond to the NCBI taxonomy identifiers for interactors A and B (4). Column twelve corresponds to the interaction type (4). Column thirteen corresponds to the databases used as sources (4). Finally, columns fourteen and fifteen correspond to the interaction identifier and the confidence score (4). 

# R and Python Cards for Centrality Calculations from a MITAB 2.5 File

#### [Python Card](https://github.com/EdKong/CBB752_3.2_centrality), Brought by ELK

#### [R Card](https://github.com/jqz752/cbb752_3.2_R), Brought by Julian

# References:

1) Mascolo, C. (2015). University of Cambridge: Computer Laboratory. Social and Technological Network Analysis. Lecture 3: Centrality Measures. https://www.cl.cam.ac.uk/teaching/1415/L109/l109-lecture3.pdf

2) Xia, J., Benner, M. J., & Hancock, R. E. W. (2014). NetworkAnalyst - Integrative approaches for protein-protein interaction network analysis and visual exploration. Nucleic Acids Research, 42(W1), 167–174. http://doi.org/10.1093/nar/gku443

3) Brandes, U. (2001). A faster algorithm for betweenness centrality*. The Journal of Mathematical Sociology, 25(2), 163–177. http://doi.org/10.1080/0022250X.2001.9990249

4) Google Code Archive. Psimi – PsimiTabFormat.wiki. https://code.google.com/archive/p/psimi/wikis/PsimiTabFormat.wiki

---

### Gene Set Expression Enrichment Calculator

#### English Card, Brought by Aparna

##### Background

###### Gene sets

While many traditional methods have been developed for bioinformaticians to quantify the enrichment of a gene, recent studies have been moving away from this single gene approach and toward gene set analysis. 
In conventional single-gene approaches — or individual gene analysis (IGA) — the differential expression of certain genes is measured between two phenotypes. A threshold is used to determine which genes have significant enrichment, and then, these genes are compared against ontologies and pathways to determine their functions. However, this method is flawed because it relies on an arbitrary threshold and often misses somewhat significant enrichment across multiple related genes in favor of significant enrichment in one gene.[1] There also might not be any biological theme to support a more meaningful analysis.[2]
Gene sets are groups of related genes identified based on prior biological knowledge of pathways and ontologies.[1] A gene set may include all the genes in a pathway, or all the genes on a chromosome. This offers a richer picture of enrichment and differential expression, because even if there isn’t one very significantly enriched gene, there may be less significant enrichment across a gene set.[3] 

##### Gene set enrichment analysis

One method in particular has been developed for identifying differential expression of gene sets. Gene set enrichment analysis (GSEA) involves determining whether the differential expression of elements of a gene set is random or enriched in a specific way.[2] There are many ways to implement GSEA, but we will focus on Subramanian et al.’s procedure. The genes in the samples are ordered in a list based on their degree of differential expression (positively enriched genes at the top, negatively enriched genes at the bottom), and then we analyze the distribution of elements of the gene set throughout this list. The degree of overrepresentation is quantified by an enrichment score (ES), which is then tested for statistical significance. We also identify a subset of the gene set called the “leading-edge subset.” The ES is calculated by cumulatively adding and subtracting when a gene in the list is or isn’t in the gene set, respectively. The amount added or subtracted is based on how significant the differential expression is. 
From this method, we can also construct a subset of the gene set called the “leading-edge subset.” As the ES is calculated, there will be a maximum |ES| at some point; after that point, the ES will trend more toward 0. The leading-edge subset is the genes that are encountered before this maximum |ES| is achieved, and they are the main enriched genes.

##### Our Software

We have used the GSEA approach to develop a program that identifies enriched genes from a gene set in gene expression data. There are Python and R versions of the program.

###### Input

This program requires three inputs;
1.) GCT file with expression data: often the result of a microarray experiment, and contains the expression level of each gene in each sample.
Ex:
```
#1.2																																						
7129	38																																						
Name	Description	ALL_19769_B-cell	ALL_23953_B-cell	ALL_28373_B-cell ...  
AFFX-BioB-5_at	AFFX-BioB-5_at (endogenous control)	-214	-135	-106 ...  
AFFX-BioB-M_at	AFFX-BioB-M_at (endogenous control)	-153	-114	-125 ...  
AFFX-BioB-3_at	AFFX-BioB-3_at (endogenous control)	-58	265	-76 ...  
AFFX-BioC-5_at	AFFX-BioC-5_at (endogenous control)	88	12	168 ...  
...  
...  
...  
```
2.) CLS file with class label data: provides the names of the phenotypes being compared, and matches samples to their correct class.
Ex:
```
38 2 1
# ALL AML
0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 1 1 1 1 1 1 1 1 1 1 1
```
3.)	Gene set: category name followed by list of names of genes in set
Ex:
```
HALLMARK_ADIPOGENESIS
> Genes up-regulated during adipocyte differentiation (adipogenesis).
ABCA1
ABCB8
ACAA2
ACADL
ACADM
ACADS
ACLY
ACO2
ACOX1
ADCY6
ADIG
ADIPOQ
...
```

If the expression data is not pre-processed, some pre-processing is required to ensure that only high quality expression data is used and that identifiers from the three files are compatible. Standard pre-processing via GenePattern’s PreprocessDataset module is sufficient.[4] The resulting expression data will be restricted to certain thresholds, normalized, and filtered for proper sampling and high-quality measurements.
Additionally, identifiers need to be the same across all three files. This may require removing prefixes or suffixes added to gene names for experiment-specific purposes.

###### Method

Since Subramanian et al.’s method requires an ordered list, the first step is to sort the list of genes identified in the expression data. The genes are sorted based on the p-values resulting from a t-test. We identify the genes at the intersection of this ordered list and the inputted list of gene set elements. P-values are weighted so that they are relative to the sum of all p-values.
Then, the program walks through the ordered list to build the cumulative ES. For every gene marked as being in the gene set, the weighted p-value is added to a running-sum and stored as the current value of Phit. For every gene not in the gene set, a “miss” value is added to a separate running sum, which is stored as Pmiss. The miss value is calculated as the reciprocal of the difference in the sizes of the ordered list and the gene set, multiplied by the number of genes that have been encountered in the ordered list so far that were not in the gene set. The formal definitions of Phit and Pmiss from Subramanian et al. are included below:

![alt text](http://i.imgur.com/aqYa4SV.png "Algorithm")

where S is a gene set, i is the index in the ordered list, |rj|p is a weighted p-value (p is an arbitrary exponent selected to scale this value), NR is the sum of the weighted p-values for all genes in S, and NH is the number of genes in S.
After the program has iterated through the entire ordered list, it conducts a pairwise comparison of the Phit and Pmiss values at each index to determine the maximum absolute difference between the two values. This difference is returned as the enrichment score.

###### Output

The program outputs the calculated enrichment score. This value is representative of the overall degree of enrichment of genes in this gene set, and a high enrichment score indicates that the given gene set is differentially expressed between the two phenotypes, so the biological process that unites these genes might contribute to the disease phenotype in question.

###### Further steps

Our software offers a condensed version of the GSEA method and provides the enrichment score, which is the minimum amount of useful information required for a user to make judgments about the enrichment of a particular gene set. However, there are still more functionalities that can be easily incorporated into this program. For example, a permutation test can be added to determine the statistical significance of the ES. Depending on the user’s needs, the ES can be modified to accommodate multiple hypotheses. We could also keep track of the leading-edge subset for further investigation in downstream analyses. These functionalities, while not in this version of the program, can easily be added in a modular fashion so that interested users can include them in their individual pipelines.

#### Python Card, Brought by Kevin. Code found [here](https://github.com/kevkid/cbb752_3.3_py).

#### [R Card](https://github.com/calvinrhodes/mbb752_3.3_R), Brought by [Calvin](https://github.com/calvinrhodes)

#### References

1. Nam, D. & Kim, S. Gene-set approach for expression pattern analysis. Brief Bioinform 9(3), 189-97 (2008).
2. Subramanian, A., Tamayo, P., Mootha, V.K., Mukherjee, S., Ebert, B.L, Cillette, M.A., Paulovich, A., Pomeroy, S.L., Golub, T.R, Lander, E.S., & Mesirov, J.P. Gene set enrichment analysis: A knowledge-based approach for interpreting genome-wide expression profiles. Proc Nat Acad Sci 102(43), 15545-50 (2005).
3. Maciejewski, H. Gene set analysis methods: statistical models and methodological differences. Brief Bioinform 15(4), 504-18 (2013).
4. Kuehn, H., Liberzon, A., Reich, M. & Mesirov, J.P. Using GenePattern for Gene Expression Analysis. Current Protocols in Bioinformatics 22, 7.12.1–7.12.39 (2008)
