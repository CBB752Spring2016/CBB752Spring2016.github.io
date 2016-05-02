---
group: navigation
layout: page
title: QC Step
---


### Sub-Project 1: generates “quality control statistics” from FastQ file

#### Python Card, Brought by Peter


#### R Card, Brought by Dan


#### English Card, Brought by Aparna




### Sub-Project 2: trim reads based on quality score from FastQ file


#### Python Card, Brought by Heather

See project repository: https://github.com/dspak/CBB752_Final_Project_1.3.git

#### R Card, Brought by Dan


#### English Card, Brought by Nathan

#### What is a FASTQ file? 

FastQ file is a text file with the FASTQ format, designed to contain a nucleotide sequence and its associate quality score in the ASCII character-encoding scheme. This format is used as output data for high-throughput sequencing from companies like Illumina (Cock, et al. 2010). 


#### What is quality score?

In the ASCII encoding scheme, a set of characters are put into order to denote quality, for example“!” is the lowest quality score and “~” is the highest. Quality is determined by the PHRED software, in which the quality score Q = -10*log(10)*P (Edwing, et al. 1998). The score correlates with the probability of getting the incorrect base call, for example a quality score of 10 means the probability of base call will be incorrect 1 in 10, while a score of 60 means the probability 1 in 1000000 will be incorrect.


#### How does the algorithm works?

The basis of this base-calling algorithm consists of predicting peak locations, identifying observed peaks, matching predicted peaks to observed peaks, and find missed peaks. Illumina FASTQ format starts with “@” followed by the record identifier and sequence length, after that is a nucleotide sequence. The next line starts with the “+” followed by the optional title, then after that is the quality line for the above nucleotide sequence. 


#### What is our implementation for trimming sequences based on quality scores?

The rationale for such a tool is that high-throughput sequencing have high quality portions from the 5’ end which slowly degrades as sequencing proceed to the 3’ end. Before we can use this data for biological research, it is imperative to cut out poorly defined nucleotides. Our tool will take in a FASTQ file and a score file as input and then output the nucleotide sequence trimmed based on the quality score. The tool will also have options for a threshold quality score as well as a minimum read length. Our algorithm will utilize the sliding window technique, where we propose to calculate the average of quality scores within a window of 4 nucleotides then compare it to an arbitrary threshold quality score we wanted. If the average is larger or equal to the threshold, the nucleotides will be kept in the final sequence. If the average is below the threshold, we will remove all 4 nucleotides as well as the rest of that nucleotide sequence.


#### What is the biological relevance for this tool?

This tool will be a quick asset in organizing biological data for further assembly or research. The test file we are using for our tool includes the genome read of a fungus. The reason for testing this genome is because it has relevance in assembly. These sequences are half of a paired-end read, as such quality is low in the middle region where assembly of two sequences happens (Shaw, et al., 2015). By using this tool we can filter out paired-end sequences with low quality at their 3’ ends and therefore prevent assembly. Only sequences with adequate quality will proceed to assembly of the genome.  


Reference:

Cock, P. et al. 2010. The Sanger FASTQ file format for sequences with quality scores, and the Solexa/Illumina FASTQ variants. Nucleic Acids Res. 38(6): 1767–1771.

Edwing, B. et al. 1998. Base-calling of automated sequencer traces using phred. Genomic Res. 8(3): 175-185.

Shaw, J. et al. 2015. Biosynthesis and genomic analysis of medium-chain hydrocarbon production by the endophytic fungal isolate Nigrograna mackinonnii E5202H. Appl Microbiol Biotechnol. 99(8): 3715-3728. 


