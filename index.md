---
layout: page
title: CBB752Spring2016 Final Project
---

About the Course
----------------

-   **Title:** Bioinformatics: Practical Application of Data Mining & Simulation

-   **Instructor:** [Gerstein, Mark](<http://www.gersteinlab.org>)

-   **Introduction:** Bioinformatics encompasses the analysis of gene sequences,
    macromolecular structures, and functional genomics data on a large scale. It
    represents a major practical application for modern techniques in data
    mining and simulation. Specific topics to be covered include sequence
    alignment, large-scale processing, next-generation sequencing data,
    comparative genomics, phylogenetics, biological database design, geometric
    analysis of protein structure, molecular-dynamics simulation, biological
    networks, normalization of microarray data, mining of functional genomics
    data sets, and machine-learning approaches to data integration.

-   Check out our [awsome course website](<http://cbb752b16.gersteinlab.org>).

-   Check out [this awsome post of related bioinformatics
    topics](<%7B%%20post_url%202016-4-10-Categories-of-knowledge-for-bioinformatics-education%20%%7D>).

About the Final Project
-----------------------

-   **Why:** Instead of generating papers or codes that nobody would ever read
    (expect for the TAs), we want to encourage the innovative generation of
    products that could potentially benefit the bioinformatics community.

-   **When:** Released at April 14th, and will be due at 11:59pm May 5th.

-   **How:** Each student will coorporate with classmates to work on three (or
    four for extra credits) different projects. The generated codes and
    documents will be published on this website to be resources for later
    students and researches.

-   **What:** Project topics are as following. Students can choose three to four
    favorite projects to work on.

### For all sub-projects, your group will have to provide

1.  R card: sample input, source code in R, sample output, and documentation on
    how to execute your code

2.  Python card: sample input, source code in Python, sample output, and
    documentation on how to execute your code

3.  English card: methodology and background introduction

### Available Topics (Note that this is a draft and if you see an issue come to us and we would edit it accordingly)

#### 1. QC steps

1.1 Propose a tool that removes barcode or sequence identifier from FastQ file.(Discard)

1.2 Propose a tool that generates “quality control statistics” from FastQ file. (P:Peter, E:Aparna, R:Dan)

1.3 Propose a tool that trims reads based on quality score from FastQ file. (E:Nathan, P:Heather, R:Dan)

#### 2. Sequence Analysis

2.1 Propose a tool that generates pileup format from SAM file.(Discard)

2.2 Propose a tool that calculates FPKM (or TPM, and justify your choice) from
given SAM and GTF files. (R:Julian, P:Kevin, E:Edmond Dantes)

2.3 Propose a tool that calculates intersection between two BED files. (Discard)

2.4 Propose a tool that calls SNVs from pileup file, and generate the output in
VCF format. (Discard)

2.5 Propose a tool that calculates differentially expressed genes from GCT file
of gene expressions.(E:Edmond Dantes, P:Heather, R:Calvin)

2.6 Propose a tool that finds k-mer motif enrichment from a given nucleotide
sequence.(E:Edmond Dantes, R:Julian, P:ELK)

#### 3. Network Analysis

3.1 Propose a tool that calculates co-expressed gene network from GCT file of
gene expressions.(R:Dan, P:ELK, E:Aparna)

3.2 Propose a tool that calculate their degree centrality and betweenness
centrality from PPI file. PPI data can be downloaded from DIP, BIND, MIPS, MINT,
and InAct databases.(E:Edmond Dantes, R:Julian, P:ELK)

3.3 Propose a tool that calculates enrichment level of gene expression data
given pre-defined gene sets
([http://software.broadinstitute.org/gsea/msigdb](<https://urldefense.proofpoint.com/v2/url?u=http-3A__software.broadinstitute.org_gsea_msigdb&d=AwMFaQ&c=-dg2m7zWuuDZ0MUcV7Sdqw&r=PnTFVO2L44pkkv9ojQ0IMDygcpAI3ijI-U1aZXdN85Y&m=0qYw2y8MqbEaBguyXvxmBwvTb67SzblG5ILDT9kuscI&s=ah6gw5_TiY43zaFez-Xxusu-JRdMKObrVsokKQOUCyw&e=>)).(P:Kevin, R:Calvin, E:Aparna)

#### 4. Structure Analysis

4.1 Propose a tool that calculate distance between two alpha carbons from a PDB
file. (The program should output a distance between two atoms in angstroms) (P:Peter, R:Cavin, E:Gawain)

4.2 Propose a tool that calculate the Lennard-Jones potential based on the input
of a PDB file consisting of just alpha carbons and a query point’s xyz
coordinates. (R:Gawain, E:Nathan, P:Heather)

4.3 Propose a tool that calculate the dihedral angle based on the input of four
points’ xyz coordinates in PDB format.(R:Kevin, E:Gawain, P:Peter)





## Grouping Assignment


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
    <th class="tg-yw4l">1.2</th>
    <th class="tg-yw4l">1.3</th>
    <th class="tg-yw4l">2.1</th>
    <th class="tg-yw4l">2.2</th>
    <th class="tg-yw4l">2.3</th>
    <th class="tg-yw4l">2.4</th>
    <th class="tg-yw4l">2.5</th>
    <th class="tg-yw4l">2.6</th>
    <th class="tg-yw4l">3.1</th>
    <th class="tg-yw4l">3.2</th>
    <th class="tg-yw4l">3.3</th>
    <th class="tg-yw4l">4.1</th>
    <th class="tg-yw4l">4.2</th>
    <th class="tg-yw4l">4.3</th>
  </tr>
  <tr>
    <td class="tg-yw4l">Julian</td>
    <td class="tg-yw4l">R</td>
    <td class="tg-yw4l"></td>
    <td class="tg-yw4l"></td>
    <td class="tg-yw4l"></td>
    <td class="tg-yw4l"></td>
    <td class="tg-yw4l">R</td>
    <td class="tg-yw4l"></td>
    <td class="tg-yw4l"></td>
    <td class="tg-yw4l"></td>
    <td class="tg-yw4l">R</td>
    <td class="tg-yw4l"></td>
    <td class="tg-yw4l">R</td>
    <td class="tg-yw4l"></td>
    <td class="tg-yw4l"></td>
    <td class="tg-yw4l"></td>
    <td class="tg-yw4l"></td>
  </tr>
  <tr>
    <td class="tg-yw4l">Kevin</td>
    <td class="tg-yw4l">P/R</td>
    <td class="tg-yw4l"></td>
    <td class="tg-yw4l"></td>
    <td class="tg-yw4l"></td>
    <td class="tg-yw4l"></td>
    <td class="tg-yw4l">P</td>
    <td class="tg-yw4l"></td>
    <td class="tg-yw4l"></td>
    <td class="tg-yw4l"></td>
    <td class="tg-yw4l"></td>
    <td class="tg-yw4l"></td>
    <td class="tg-yw4l"></td>
    <td class="tg-yw4l">P</td>
    <td class="tg-yw4l"></td>
    <td class="tg-yw4l"></td>
    <td class="tg-yw4l">R</td>
  </tr>
  <tr>
    <td class="tg-yw4l">Edmond Dantes</td>
    <td class="tg-yw4l">E</td>
    <td class="tg-yw4l"></td>
    <td class="tg-yw4l"></td>
    <td class="tg-yw4l"></td>
    <td class="tg-yw4l"></td>
    <td class="tg-yw4l">E</td>
    <td class="tg-yw4l"></td>
    <td class="tg-yw4l"></td>
    <td class="tg-yw4l">E</td>
    <td class="tg-yw4l"></td>
    <td class="tg-yw4l"></td>
    <td class="tg-yw4l">E</td>
    <td class="tg-yw4l"></td>
    <td class="tg-yw4l"></td>
    <td class="tg-yw4l"></td>
    <td class="tg-yw4l"></td>
  </tr>
  <tr>
    <td class="tg-yw4l">ELK</td>
    <td class="tg-yw4l">P/E</td>
    <td class="tg-yw4l"></td>
    <td class="tg-yw4l"></td>
    <td class="tg-yw4l"></td>
    <td class="tg-yw4l"></td>
    <td class="tg-yw4l"></td>
    <td class="tg-yw4l"></td>
    <td class="tg-yw4l"></td>
    <td class="tg-yw4l"></td>
    <td class="tg-yw4l">P</td>
    <td class="tg-yw4l">P</td>
    <td class="tg-yw4l">P</td>
    <td class="tg-yw4l"></td>
    <td class="tg-yw4l"></td>
    <td class="tg-yw4l"></td>
    <td class="tg-yw4l"></td>
  </tr>
  <tr>
    <td class="tg-yw4l">Aparna</td>
    <td class="tg-yw4l">E</td>
    <td class="tg-yw4l"></td>
    <td class="tg-yw4l">E</td>
    <td class="tg-yw4l"></td>
    <td class="tg-yw4l"></td>
    <td class="tg-yw4l"></td>
    <td class="tg-yw4l"></td>
    <td class="tg-yw4l"></td>
    <td class="tg-yw4l"></td>
    <td class="tg-yw4l"></td>
    <td class="tg-yw4l">E</td>
    <td class="tg-yw4l"></td>
    <td class="tg-yw4l">E</td>
    <td class="tg-yw4l"></td>
    <td class="tg-yw4l"></td>
    <td class="tg-yw4l"></td>
  </tr>
  <tr>
    <td class="tg-yw4l">Dan</td>
    <td class="tg-yw4l">R</td>
    <td class="tg-yw4l"></td>
    <td class="tg-yw4l">R</td>
    <td class="tg-yw4l">R</td>
    <td class="tg-yw4l"></td>
    <td class="tg-yw4l"></td>
    <td class="tg-yw4l"></td>
    <td class="tg-yw4l"></td>
    <td class="tg-yw4l"></td>
    <td class="tg-yw4l"></td>
    <td class="tg-yw4l">R</td>
    <td class="tg-yw4l"></td>
    <td class="tg-yw4l"></td>
    <td class="tg-yw4l"></td>
    <td class="tg-yw4l"></td>
    <td class="tg-yw4l"></td>
  </tr>
  <tr>
    <td class="tg-yw4l">Nathan</td>
    <td class="tg-yw4l">E</td>
    <td class="tg-yw4l"></td>
    <td class="tg-yw4l"></td>
    <td class="tg-yw4l">E</td>
    <td class="tg-yw4l"></td>
    <td class="tg-yw4l"></td>
    <td class="tg-yw4l"></td>
    <td class="tg-yw4l"></td>
    <td class="tg-yw4l"></td>
    <td class="tg-yw4l">E</td>
    <td class="tg-yw4l"></td>
    <td class="tg-yw4l"></td>
    <td class="tg-yw4l"></td>
    <td class="tg-yw4l"></td>
    <td class="tg-yw4l">E</td>
    <td class="tg-yw4l"></td>
  </tr>
  <tr>
    <td class="tg-yw4l">Heather</td>
    <td class="tg-yw4l">P/E</td>
    <td class="tg-yw4l"></td>
    <td class="tg-yw4l"></td>
    <td class="tg-yw4l">P</td>
    <td class="tg-yw4l"></td>
    <td class="tg-yw4l"></td>
    <td class="tg-yw4l"></td>
    <td class="tg-yw4l"></td>
    <td class="tg-yw4l">P</td>
    <td class="tg-yw4l"></td>
    <td class="tg-yw4l"></td>
    <td class="tg-yw4l"></td>
    <td class="tg-yw4l"></td>
    <td class="tg-yw4l"></td>
    <td class="tg-yw4l">P</td>
    <td class="tg-yw4l"></td>
  </tr>
  <tr>
    <td class="tg-yw4l">Peter</td>
    <td class="tg-yw4l">P/E</td>
    <td class="tg-yw4l"></td>
    <td class="tg-yw4l">P</td>
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
    <td class="tg-yw4l">P</td>
    <td class="tg-yw4l"></td>
    <td class="tg-yw4l">P</td>
  </tr>
  <tr>
    <td class="tg-yw4l">Calvin</td>
    <td class="tg-yw4l">R/E</td>
    <td class="tg-yw4l"></td>
    <td class="tg-yw4l"></td>
    <td class="tg-yw4l"></td>
    <td class="tg-yw4l"></td>
    <td class="tg-yw4l"></td>
    <td class="tg-yw4l"></td>
    <td class="tg-yw4l"></td>
    <td class="tg-yw4l">R</td>
    <td class="tg-yw4l"></td>
    <td class="tg-yw4l"></td>
    <td class="tg-yw4l"></td>
    <td class="tg-yw4l">R</td>
    <td class="tg-yw4l">R</td>
    <td class="tg-yw4l"></td>
    <td class="tg-yw4l"></td>
  </tr>
  <tr>
    <td class="tg-yw4l">Gawain</td>
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
    <td class="tg-yw4l">E</td>
    <td class="tg-yw4l">R</td>
    <td class="tg-yw4l">E</td>
  </tr>
</table>





Feel free to contact the TAs if you have any concerns about the assignment! 
Otherwise start garthering your group members and having your first discussion!!!

