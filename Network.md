---
layout: page
title: Network Analysis
group: navigation
weight: 3
---


~~### Sub-Project 1: calculate co-expressed gene network from GCT file of gene expressions~~

> Please carefully read through and follow the formatting guideline found in [Project 1.2](http://cbb752spring2016.github.io/QCStep)

#### [Python Card](https://github.com/EdKong/CBB752_Final_Project_3.1), Brought by ELK

> This is mostly a comment about formatting. I saw usage note within the code. It is preferred to put readme.md at your repository and put a short description about the program, on how to run, what parameters to take, sample input and output. In this way, you can put a link to git repo instead. Otherwise, great work.

#### [R Card](https://github.com/dspak/CBB752_Final_Project_3.1), Brought by Dan

> This is mostly a comment about formatting. I saw usage note within the code. It is preferred to put readme.md at your repository and put a short description about the program, on how to run, what parameters to take, sample input and output. In this way, you can put a link to git repo instead. Otherwise, great work.

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

> Very good background and comparison with exisitng software package! Good use of references as well. I would just work more on overall formatting of the project.

~~##### References~~

#### References

1. Langfelder, P. & Horvath, S. WGCNA: an R package for weighted correlation network analysis. BMC Bioinformatics 9(559), (2008)
2. Zhang, B. & Horvath, S. A General Framework for Weighted Gene Co-expression Network Analysis. Stat Appl Genet Mol Biol 4, Article 17 (2005)
3. Kuehn, H., Liberzon, A., Reich, M. & Mesirov, J.P. Using GenePattern for Gene Expression Analysis. Current Protocols in Bioinformatics 22, 7.12.1–7.12.39 (2008)
4. Shannon, P. et al. Cytoscape: a software environment for integrated models of biomolecular interaction networks. Genome Research 13(11), 2498-504 (2003)
5. Borate, B.R., Chesler, E.J., Langston, M.A., Saxton, A.M. & Voy, B.H. Comparison of threshold selection methods for microarray gene co-expression matrices. BMC Res Notes 2, 240 (2009)

~~##### Figures~~

#### Figures

Figure 1: Visualization of co-expression network. Cytoscape was run on output file (output_coexpression.csv) yielded by running pre-processed input file (all_aml_train.preprocessed.gct) through Python version of software.

![Figure 1](https://github.com/dspak/CBB752_Final_Project_3.1/blob/master/output_coexpressed.jpeg "Figure 1")

> figure is not showing from [final project website](http://cbb752spring2016.github.io/Network) can you check?

---

# Calculating Centrality for Proteins from MITAB2.5 PPI Files

#### [Python Card](https://github.com/EdKong/CBB752_3.2_centrality), Brought by ELK

#### [R Card](https://github.com/jqz752/cbb752_3.2_R), Brought by Julian

#### English Card, Brought by Edmond Dantes

The analysis of the dynamic nature of gene networks holds remarkable potential in uncovering previously unknown biological phenomena. Protein to protein interactions or (PPIs) are of particular interest in the study of gene expression and proteomics(2).  PPIs are crucial to both the functional and structural roles of all biological processes(2). One can think of a PPI network as a collection of nodes interconnected by edges in various fashions(2). In PPIs, nodes represent proteins while edges represent the interaction between two connected proteins(2). Three steps are generally involved in the building of a PPI network, including: identification of genes of interest, using the input to search for interaction data on a PPI database, and the actual network analysis(2). A topological analysis of the resulting network can then help identify nodes that act as hubs and may be developed into biomarkers or therapeutic targets(2). Subsequently, one can break down the network into smaller units(modules) in order to identify areas with more activity(2).  Information derived from PPIs allows for the calculation of both degree centrality and betweenness centrality of co-expressed gene networks(2).   

Degree centrality as well as betweenness centrality are core definitions of a network’s topology. Defining the centrality of a node/s allows one to identify the most highly connected nodes in a network(1). One can then infer the relative importance of a node based on how many nodes it is connected to(1). Nodes with a high degree of centrality will disproportionally affect the functioning of a network if they are altered which may lead to disease(1). In order to calculate degree centrality we divided the degree of a vertex by (n-1). Here the degree of a vertex referred to the number of edges connected to a vertex and n to the total number of vertices. 

Betweenness centrality allows one to evaluate how many pairs of nodes would have to cross a particular node of interest in order to reach one another while minimizing the number of movements(1). We chose the Brandes algorithm to calculate betweenness centrality due to its faster execution(3).
 (3)
 
CB is the general formula to determine betweenness centrality for a particular vertex or ν(3). Where σst(ν) represents the number of shortest paths connecting s and t passing through ν(1). While σst represents the total number of shortest paths(1). 


References:
1) Mascolo, C. (2015). University of Cambridge: Computer Laboratory. Social and Technological Network Analysis. Lecture 3: Centrality Measures. https://www.cl.cam.ac.uk/teaching/1415/L109/l109-lecture3.pdf
2) Xia, J., Benner, M. J., & Hancock, R. E. W. (2014). NetworkAnalyst - Integrative approaches for protein-protein interaction network analysis and visual exploration. Nucleic Acids Research, 42(W1), 167–174. http://doi.org/10.1093/nar/gku443
3) Brandes, U. (2001). A faster algorithm for betweenness centrality*. The Journal of Mathematical Sociology, 25(2), 163–177. http://doi.org/10.1080/0022250X.2001.9990249


---

### Sub-Project 3: calculate enrichment level of gene expression data given pre-defined gene sets

#### Python Card, Brought by Kevin

#### R Card, Brought by Calvin

#### English Card, Brought by Aparna
