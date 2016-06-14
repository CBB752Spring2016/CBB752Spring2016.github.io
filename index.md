---
layout: page
title: CBB752 Spring 2016 Final Project
---

About the Course
----------------

-   **Title:** Bioinformatics: Practical Application of Data Mining & Simulation

-   **Instructor:** [Gerstein, Mark](<http://www.gersteinlab.org>)

-   **TAs**: [Huang, Xiu](http://xiu-huang.com) & [Lee, Donghoon](http://hoondy.com)

-   **Introduction:** Bioinformatics encompasses the analysis of gene sequences,
    macromolecular structures, and functional genomics data on a large scale. It
    represents a major practical application for modern techniques in data
    mining and simulation. Specific topics to be covered include sequence
    alignment, large-scale processing, next-generation sequencing data,
    comparative genomics, phylogenetics, biological database design, geometric
    analysis of protein structure, molecular-dynamics simulation, biological
    networks, normalization of microarray data, mining of functional genomics
    data sets, and machine-learning approaches to data integration.

-   Check out our awesome [course website](<http://cbb752b16.gersteinlab.org>).

-   Check out our [post on bioinformatics](<{% post_url 2016-4-10-Categories-of-knowledge-for-bioinformatics-education %}>).

About the Final Project
-----------------------

- **Why?**

   Instead of generating papers or codes that nobody would ever read (expect for the TAs), we want to encourage the innovative generation of products that could potentially benefit the bioinformatics community.

- **When?**

    Released: April 14th

    Due: May 9th 11:59PM

- **How?**

    Each student will coorporate with classmates to work on three (or four for extra credits) different projects. The generated codes and documents will be published on this website to be resources for later students and researches.

- **What?**

    Project topics are as following. Students can choose three to four favorite projects to work on.

### For each sub-project, a group of three people will work on:

1.  **R card**: sample input, source code in R, sample output, and documentation on
    how to execute your code

2.  **Python card**: sample input, source code in Python, sample output, and
    documentation on how to execute your code

3.  **English card**: methodology and background introductory documentation

### Topics and Grouping Assignment

#### 1. [QC steps]({{site.url}}/QCStep)

1.1 ~~Propose a tool that removes barcode or sequence identifier from FastQ file~~.(**Discard**)

1.2 Propose a tool that generates “quality control statistics” from FastQ file. (**[E:Aparna]({{site.url}}/QCStep#quality-statistics), [P:Peter](https://github.com/CBB752Spring2016/CBB752_Final_Project_1.2.git), [R:Dan](https://github.com/CBB752Spring2016/CBB752_Final_Project_1.2)**)

1.3 Propose a tool that trims reads based on quality score from FastQ file. (**[E:Nathan]({{site.url}}/QCStep#sequence-read-trimming), [P:Heather](https://github.com/CBB752Spring2016/CBB752_Final_Project_1.3), [R:Dan](https://github.com/CBB752Spring2016/CBB752_Final_Project_1.3)**)

#### 2. [Sequence Analysis]({{site.url}}/Sequence)

2.1 ~~Propose a tool that generates pileup format from SAM file~~.(**Discard**)

2.2 Propose a tool that calculates FPKM (or TPM, and justify your choice) from
given SAM and GTF files. (**[E:Edmond Dantes]({{site.url}}/Sequence#quantifying-rnaseq), [P:Kevin](https://github.com/CBB752Spring2016/cbb752_2.2_py), [R:Julian](https://github.com/CBB752Spring2016/cbb752_2.2_R)**)

2.3 ~~Propose a tool that calculates intersection between two BED files~~. (**Discard**)

2.4 ~~Propose a tool that calls SNVs from pileup file, and generate the output in
VCF format~~. (**Discard**)

2.5 Propose a tool that calculates differentially expressed genes from GCT file
of gene expressions.(**[E:Edmond Dantes]({{site.url}}/Sequence#differential-gene-expression), [P:Heather](https://github.com/CBB752Spring2016/mbb752_2.5_R), [R:Calvin](https://github.com/CBB752Spring2016/mbb752_2.5_R)**)

2.6 Propose a tool that finds k-mer motif enrichment from a given nucleotide
sequence.(**[E:Nathan]({{site.url}}/Sequence#k-mer-enrichment), [P:ELK](https://github.com/CBB752Spring2016/2.6_kmer_enrichment), [R:Julian](https://github.com/CBB752Spring2016/cbb752_2.6_R)**)

#### 3. [Network Analysis]({{site.url}}/Network)

3.1 Propose a tool that calculates co-expressed gene network from GCT file of
gene expressions.(**[E:Aparna]({{site.url}}/Network#coexpression-network), [P:ELK](https://github.com/CBB752Spring2016/CBB752_Final_Project_3.1), [R:Dan](https://github.com/CBB752Spring2016/CBB752_Final_Project_3.1)**)

3.2 Propose a tool that calculate their degree centrality and betweenness
centrality from PPI file. PPI data can be downloaded from DIP, BIND, MIPS, MINT,
and InAct databases.(**[E:Edmond Dantes]({{site.url}}/Network#network-centrality), [P:ELK](https://github.com/CBB752Spring2016/CBB752_3.2_centrality), [R:Julian](https://github.com/CBB752Spring2016/cbb752_3.2_R)**)

3.3 Propose a tool that calculates enrichment level of gene expression data
given pre-defined gene sets
([http://software.broadinstitute.org/gsea/msigdb](<https://urldefense.proofpoint.com/v2/url?u=http-3A__software.broadinstitute.org_gsea_msigdb&d=AwMFaQ&c=-dg2m7zWuuDZ0MUcV7Sdqw&r=PnTFVO2L44pkkv9ojQ0IMDygcpAI3ijI-U1aZXdN85Y&m=0qYw2y8MqbEaBguyXvxmBwvTb67SzblG5ILDT9kuscI&s=ah6gw5_TiY43zaFez-Xxusu-JRdMKObrVsokKQOUCyw&e=>)).(**[E:Aparna]({{site.url}}/Network#gene-set-enrichment-analysis), [P:Kevin](https://github.com/CBB752Spring2016/cbb752_3.3_py), [R:Calvin](https://github.com/CBB752Spring2016/mbb752_3.3_R)**)

#### 4. [Structure Analysis]({{site.url}}/Structure)

4.1 Propose a tool that calculate distance between two alpha carbons from a PDB
file. (The program should output a distance between two atoms in angstroms) (**[E:Gawain]({{site.url}}/Structure#calculating-distance-between-alpha-carbons-in-a-pdb-file), [P:Peter](https://github.com/CBB752Spring2016/Python_Distance_Calculation.git), [R:Cavin](https://github.com/CBB752Spring2016/mbb752_4.1_R)**)

4.2 Propose a tool that calculate the Lennard-Jones potential based on the input
of a PDB file consisting of just alpha carbons and a query point’s xyz
coordinates. (**[E:Nathan]({{site.url}}/Structure#calculating-the-lennard-jones-potential-from-a-query-point-and-a-pdb-file), [P:Heather](https://github.com/CBB752Spring2016/Final-Project-4.2), [R:Gawain](https://github.com/CBB752Spring2016/Final-Project-4.2)**)

4.3 Propose a tool that calculate the dihedral angle based on the input of four
points’ xyz coordinates in PDB format.(**[E:Gawain]({{site.url}}/Structure#calculating-dihedral-angles-from-pdb-file), [P:Peter](https://github.com/CBB752Spring2016/Dihedral_Angle_Calc.git), [R:Kevin](https://github.com/CBB752Spring2016/CBB_Bioinformatics_FinalProject_4.3.git)**)

## Grouping Assignment Table

<style type="text/css">
.tg  {border-collapse:collapse;border-spacing:0;}
.tg td{font-family:Arial, sans-serif;font-size:14px;padding:10px 5px;border-style:solid;border-width:1px;overflow:hidden;word-break:normal;}
.tg th{font-family:Arial, sans-serif;font-size:14px;font-weight:normal;padding:10px 5px;border-style:solid;border-width:1px;overflow:hidden;word-break:normal;}
.tg .tg-yw4l{vertical-align:top}
</style>
<table class="tg">
  <tr>
    <th class="tg-yw4l">Name</th>
    <th class="tg-yw4l">Primary</th>
    <th class="tg-yw4l">1.1</th>
    <th class="tg-yw4l"><a href="http://cbb752spring2016.github.io/QCStep#quality-statistics">1.2</a></th>
    <th class="tg-yw4l"><a href="http://cbb752spring2016.github.io/QCStep#sequence-read-trimming">1.3</a></th>
    <th class="tg-yw4l">2.1</th>
    <th class="tg-yw4l"><a href="http://cbb752spring2016.github.io/Sequence#quantifying-rnaseq">2.2</a></th>
    <th class="tg-yw4l">2.3</th>
    <th class="tg-yw4l">2.4</th>
    <th class="tg-yw4l"><a href="http://cbb752spring2016.github.io/Sequence#differential-gene-expression">2.5</a></th>
    <th class="tg-yw4l"><a href="http://cbb752spring2016.github.io/Sequence#k-mer-enrichment">2.6</a></th>
    <th class="tg-yw4l"><a href="http://cbb752spring2016.github.io/Network#coexpression-network">3.1</a></th>
    <th class="tg-yw4l"><a href="http://cbb752spring2016.github.io/Network#network-centrality">3.2</a></th>
    <th class="tg-yw4l"><a href="http://cbb752spring2016.github.io/Network#gene-set-enrichment-analysis">3.3</a></th>
    <th class="tg-yw4l"><a href="http://cbb752spring2016.github.io/Structure#calculating-distance-between-alpha-carbons-in-a-pdb-file">4.1</a></th>
    <th class="tg-yw4l"><a href="http://cbb752spring2016.github.io/Structure#calculating-the-lennard-jones-potential-from-a-query-point-and-a-pdb-file">4.2</a></th>
    <th class="tg-yw4l"><a href="http://cbb752spring2016.github.io/Structure#calculating-dihedral-angles-from-pdb-file">4.3</a></th>
  </tr>
  <tr>
    <td class="tg-yw4l"><a href="https://github.com/jqz752">Julian</a></td>
    <td class="tg-yw4l">R</td>
    <td class="tg-yw4l"></td>
    <td class="tg-yw4l"></td>
    <td class="tg-yw4l"></td>
    <td class="tg-yw4l"></td>
    <td class="tg-yw4l"><a href="https://github.com/CBB752Spring2016/cbb752_2.2_R">R</a></td>
    <td class="tg-yw4l"></td>
    <td class="tg-yw4l"></td>
    <td class="tg-yw4l"></td>
    <td class="tg-yw4l"><a href="https://github.com/CBB752Spring2016/cbb752_2.6_R">R</a></td>
    <td class="tg-yw4l"></td>
    <td class="tg-yw4l"><a href="https://github.com/CBB752Spring2016/cbb752_3.2_R">R</a></td>
    <td class="tg-yw4l"></td>
    <td class="tg-yw4l"></td>
    <td class="tg-yw4l"></td>
    <td class="tg-yw4l"></td>
  </tr>
  <tr>
    <td class="tg-yw4l"><a href="https://github.com/kevkid">Kevin</a></td>
    <td class="tg-yw4l">P/R</td>
    <td class="tg-yw4l"></td>
    <td class="tg-yw4l"></td>
    <td class="tg-yw4l"></td>
    <td class="tg-yw4l"></td>
    <td class="tg-yw4l"><a href="https://github.com/CBB752Spring2016/cbb752_2.2_py">P</a></td>
    <td class="tg-yw4l"></td>
    <td class="tg-yw4l"></td>
    <td class="tg-yw4l"></td>
    <td class="tg-yw4l"></td>
    <td class="tg-yw4l"></td>
    <td class="tg-yw4l"></td>
    <td class="tg-yw4l"><a href="https://github.com/CBB752Spring2016/cbb752_3.3_py">P</a></td>
    <td class="tg-yw4l"></td>
    <td class="tg-yw4l"></td>
    <td class="tg-yw4l"><a href="https://github.com/CBB752Spring2016/CBB_Bioinformatics_FinalProject_4.3.git">R</a></td>
  </tr>
  <tr>
    <td class="tg-yw4l"><a href="https://github.com/MichaelMengual">Edmond Dantes</a></td>
    <td class="tg-yw4l">E</td>
    <td class="tg-yw4l"></td>
    <td class="tg-yw4l"></td>
    <td class="tg-yw4l"></td>
    <td class="tg-yw4l"></td>
    <td class="tg-yw4l"><a href="http://cbb752spring2016.github.io/Sequence#quantifying-rnaseq">E</a></td>
    <td class="tg-yw4l"></td>
    <td class="tg-yw4l"></td>
    <td class="tg-yw4l"><a href="http://cbb752spring2016.github.io/Sequence#differential-gene-expression">E</a></td>
    <td class="tg-yw4l"></td>
    <td class="tg-yw4l"></td>
    <td class="tg-yw4l"><a href="http://cbb752spring2016.github.io/Network#network-centrality">E</a></td>
    <td class="tg-yw4l"></td>
    <td class="tg-yw4l"></td>
    <td class="tg-yw4l"></td>
    <td class="tg-yw4l"></td>
  </tr>
  <tr>
    <td class="tg-yw4l"><a href="https://github.com/EdKong">ELK</a></td>
    <td class="tg-yw4l">P/E</td>
    <td class="tg-yw4l"></td>
    <td class="tg-yw4l"></td>
    <td class="tg-yw4l"></td>
    <td class="tg-yw4l"></td>
    <td class="tg-yw4l"></td>
    <td class="tg-yw4l"></td>
    <td class="tg-yw4l"></td>
    <td class="tg-yw4l"></td>
    <td class="tg-yw4l"><a href="https://github.com/CBB752Spring2016/2.6_kmer_enrichment">P</a></td>
    <td class="tg-yw4l"><a href="https://github.com/CBB752Spring2016/CBB752_Final_Project_3.1">P</a></td>
    <td class="tg-yw4l"><a href="https://github.com/CBB752Spring2016/CBB752_3.2_centrality">P</a></td>
    <td class="tg-yw4l"></td>
    <td class="tg-yw4l"></td>
    <td class="tg-yw4l"></td>
    <td class="tg-yw4l"></td>
  </tr>
  <tr>
    <td class="tg-yw4l"><a href="https://github.com/apnathan">Aparna</a></td>
    <td class="tg-yw4l">E</td>
    <td class="tg-yw4l"></td>
    <td class="tg-yw4l"><a href="http://cbb752spring2016.github.io/QCStep#quality-statistics">E</a></td>
    <td class="tg-yw4l"></td>
    <td class="tg-yw4l"></td>
    <td class="tg-yw4l"></td>
    <td class="tg-yw4l"></td>
    <td class="tg-yw4l"></td>
    <td class="tg-yw4l"></td>
    <td class="tg-yw4l"></td>
    <td class="tg-yw4l"><a href="http://cbb752spring2016.github.io/Network#coexpression-network">E</a></td>
    <td class="tg-yw4l"></td>
    <td class="tg-yw4l"><a href="http://cbb752spring2016.github.io/Network#gene-set-enrichment-analysis">E</a></td>
    <td class="tg-yw4l"></td>
    <td class="tg-yw4l"></td>
    <td class="tg-yw4l"></td>
  </tr>
  <tr>
    <td class="tg-yw4l"><a href="https://github.com/dspak">Dan</a></td>
    <td class="tg-yw4l">R</td>
    <td class="tg-yw4l"></td>
    <td class="tg-yw4l"><a href="https://github.com/CBB752Spring2016/CBB752_Final_Project_1.2">R</a></td>
    <td class="tg-yw4l"><a href="https://github.com/CBB752Spring2016/CBB752_Final_Project_1.3">R</a></td>
    <td class="tg-yw4l"></td>
    <td class="tg-yw4l"></td>
    <td class="tg-yw4l"></td>
    <td class="tg-yw4l"></td>
    <td class="tg-yw4l"></td>
    <td class="tg-yw4l"></td>
    <td class="tg-yw4l"><a href="https://github.com/CBB752Spring2016/CBB752_Final_Project_3.1">R</a></td>
    <td class="tg-yw4l"></td>
    <td class="tg-yw4l"></td>
    <td class="tg-yw4l"></td>
    <td class="tg-yw4l"></td>
    <td class="tg-yw4l"></td>
  </tr>
  <tr>
    <td class="tg-yw4l"><a href="https://github.com/NathanNN">Nathan</a></td>
    <td class="tg-yw4l">E</td>
    <td class="tg-yw4l"></td>
    <td class="tg-yw4l"></td>
    <td class="tg-yw4l"><a href="http://cbb752spring2016.github.io/QCStep#sequence-read-trimming">E</a></td>
    <td class="tg-yw4l"></td>
    <td class="tg-yw4l"></td>
    <td class="tg-yw4l"></td>
    <td class="tg-yw4l"></td>
    <td class="tg-yw4l"></td>
    <td class="tg-yw4l"><a href="http://cbb752spring2016.github.io/Sequence#k-mer-enrichment">E</a></td>
    <td class="tg-yw4l"></td>
    <td class="tg-yw4l"></td>
    <td class="tg-yw4l"></td>
    <td class="tg-yw4l"></td>
    <td class="tg-yw4l"><a href="http://cbb752spring2016.github.io/Structure#calculating-the-lennard-jones-potential-from-a-query-point-and-a-pdb-file">E</a></td>
    <td class="tg-yw4l"></td>
  </tr>
  <tr>
    <td class="tg-yw4l"><a href="https://github.com/wellshl">Heather</a></td>
    <td class="tg-yw4l">P/E</td>
    <td class="tg-yw4l"></td>
    <td class="tg-yw4l"></td>
    <td class="tg-yw4l"><a href="https://github.com/CBB752Spring2016/CBB752_Final_Project_1.3">P</a></td>
    <td class="tg-yw4l"></td>
    <td class="tg-yw4l"></td>
    <td class="tg-yw4l"></td>
    <td class="tg-yw4l"></td>
    <td class="tg-yw4l"><a href="https://github.com/CBB752Spring2016/mbb752_2.5_R">P</a></td>
    <td class="tg-yw4l"></td>
    <td class="tg-yw4l"></td>
    <td class="tg-yw4l"></td>
    <td class="tg-yw4l"></td>
    <td class="tg-yw4l"></td>
    <td class="tg-yw4l"><a href="https://github.com/CBB752Spring2016/Final-Project-4.2">P</a></td>
    <td class="tg-yw4l"></td>
  </tr>
  <tr>
    <td class="tg-yw4l"><a href="https://github.com/peter-mm-williams">Peter</a></td>
    <td class="tg-yw4l">P/E</td>
    <td class="tg-yw4l"></td>
    <td class="tg-yw4l"><a href="https://github.com/CBB752Spring2016/CBB752_Final_Project_1.2.git">P</a></td>
    <td class="tg-yw4l"></td>
    <td class="tg-yw4l"></td>
    <td class="tg-yw4l"></td>
    <td class="tg-yw4l"></td>
    <td class="tg-yw4l"></td>
    <td class="tg-yw4l"></td>
    <td class="tg-yw4l"></td>
    <td class="tg-yw4l"></td>
    <td class="tg-yw4l"></td>
    <td class="tg-yw4l"></td>
    <td class="tg-yw4l"><a href="https://github.com/CBB752Spring2016/Python_Distance_Calculation.git">P</a></td>
    <td class="tg-yw4l"></td>
    <td class="tg-yw4l"><a href="https://github.com/CBB752Spring2016/Dihedral_Angle_Calc.git">P</a></td>
  </tr>
  <tr>
    <td class="tg-yw4l"><a href="https://github.com/calvinrhodes">Calvin</a></td>
    <td class="tg-yw4l">R/E</td>
    <td class="tg-yw4l"></td>
    <td class="tg-yw4l"></td>
    <td class="tg-yw4l"></td>
    <td class="tg-yw4l"></td>
    <td class="tg-yw4l"></td>
    <td class="tg-yw4l"></td>
    <td class="tg-yw4l"></td>
    <td class="tg-yw4l"><a href="https://github.com/CBB752Spring2016/mbb752_2.5_R">R</a></td>
    <td class="tg-yw4l"></td>
    <td class="tg-yw4l"></td>
    <td class="tg-yw4l"></td>
    <td class="tg-yw4l"><a href="https://github.com/CBB752Spring2016/mbb752_3.3_R">R</a></td>
    <td class="tg-yw4l"><a href="https://github.com/CBB752Spring2016/mbb752_4.1_R">R</a></td>
    <td class="tg-yw4l"></td>
    <td class="tg-yw4l"></td>
  </tr>
  <tr>
    <td class="tg-yw4l"><a href="https://github.com/graceliu2016">Gawain</a></td>
    <td class="tg-yw4l">R/E</td>
    <td class="tg-yw4l"></td>
    <td class="tg-yw4l"></td>
    <td class="tg-yw4l"></td>
    <td class="tg-yw4l"></td>
    <td class="tg-yw4l"></td>
    <td class="tg-yw4l"></td>
    <td class="tg-yw4l"></td>
    <td class="tg-yw4l"></td>
    <td class="tg-yw4l"></td>
    <td class="tg-yw4l"></td>
    <td class="tg-yw4l"></td>
    <td class="tg-yw4l"></td>
    <td class="tg-yw4l"><a href="http://cbb752spring2016.github.io/Structure#calculating-distance-between-alpha-carbons-in-a-pdb-file">E</a></td>
    <td class="tg-yw4l"><a href="https://github.com/CBB752Spring2016/Final-Project-4.2">R</a></td>
    <td class="tg-yw4l"><a href="http://cbb752spring2016.github.io/Structure#calculating-dihedral-angles-from-pdb-file">E</a></td>
  </tr>
</table>
