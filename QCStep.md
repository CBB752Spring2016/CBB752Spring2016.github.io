---
layout: page
title: QC Step
group: navigation
weight: 1
---

## Table of Contents
**[Quality Statistics](#quality-statistics)**  
**[Sequence Read Trimming](#sequence-read-trimming)**  

---

## Quality Statistics

- Documentation: [Aparna](https://github.com/apnathan)
- [Python](https://github.com/peter-mm-williams/CBB752_Final_Project_1.2.git): [Peter](https://github.com/peter-mm-williams)
- [R](https://github.com/dspak/CBB752_Final_Project_1.2): [Dan](https://github.com/dspak)

##### Background

###### Phred quality scores

DNA sequencing offers incredibly information-rich output. In addition to the reads, another crucial piece of information is the quality of the reads. Given the massive size of next-gen sequencing data, it is necessary for users to be able to receive quality scores in a format that permits rapid, automated discrimination between high and low quality reads.
Phred quality scores were developed to address this issue. First described in a 1998 paper, they were originally designed for ABI sequencers and have gone through multiple incarnations as sequencing technology has advanced.[1] Initially, Phred scores were calculated for Sanger sequencing data by comparing “ideal peaks” (predicted with Fourier methods) to the actual peaks in the chromatogram, generated from fluorescence analysis of a gel with the ddNTP-extended fragments. From this comparison, error probabilities (P) are calculated based on the spacing, resolution, and relative sizes of called and uncalled peaks. Lower P values indicate higher quality reads.
The actual Phred quality score (Q) is calculated for each base as Q = -10log(P). By this equation, if a base has Q = 20, then its P = 10e-2, so there’s a 1% chance the base is an error, or 99% probability that the base is correct. (This is a typical 1% significance threshold that we will revisit as an upper bound for low quality reads.) Higher quality reads have lower P values that translate to higher Q values.
With the advent of next-gen sequencing, the method of calculating Phred scores has not changed significantly. Rather than using peak comparison with chromatograms, instead quality score tables are generated based on parameters measured from a dataset with known accuracy. P values are still measured based on the difference between the theoretical and experimental values, and Q values are calculated using the same logarithmic relationship.
Studies have shown that Phred scores are a reliable measure of base accuracy, even when there is variable quality between bases within the same read, and they often predict an error rate higher than the actual rate.[2]

###### FASTQ files

FASTQ is a file format that provides detailed read quality information.[3] It was designed to be compatible with Phred scores, which can each be stored base-by-base as single characters in a FASTQ file. The ASCII character (A) for a given Phred score (Q) is A = Q + 33. Thus, a sequence of bases can be represented as a string of ASCII characters. Most sequencing platforms are compatible with this type of quality scoring, with the exception of Solexa, which uses a modified logarithmic relationship between Q and P. However, Solexa quality scores are ultimately indistinguishable from Phred quality scores.[3]
FASTQ files are structured with four lines for each read. Each line contains a specific type of information.
1. Title line: @Title and description (description is optional)
2. Sequence line: sequence of bases in read
3. Repeated title line (optional): +Title and description
4. Quality line: ASCII character string representing quality of each base
The title lines begin with @ (if the first title line) or + (for all following title lines) in order to identify them. With the information encoded in FASTQ format, the user is able to differentiate between high and low quality sequences, and the structured format allows this to be done in an automated fashion.

###### FastQC

FastQC is one of a multitude of softwares that are designed to parse FASTQ files for their quality scores and return relevant statistics and charts.[4] FastQC takes a variety of common file formats as input, including FASTQ, SAM, and BAM. The program is composed of a series of modules, each of which carries out a different quality control measurement. Since FASTQ is available as either an interactive or non-interactive (higher throughput) version, the output statistics and charts for each module are either presented in an interactive browser or in a static HTML file.
There are 12 analysis modules included in FastQC: Basic Statistics, Per Base Sequence Quality, Per Sequence Quality Scores, Per Base Sequence Content, Per Sequence GC Content, Per Base N Content, Sequence Length Distribution, Duplicate Sequences, Overrepresented Sequences, Adapter Content, Kmer Content, and Per Tile Sequence Quality. Each module has quality thresholds for which the program issues a warning or a failure. Based on which modules are low quality, you can infer what issues may have occurred in your library preparation or sequencing method. For example, high adapter content may indicate that adapters must be trimmed more stringently. Lower quality scores for specific tiles is a sign of a bubble or obstruction in part of the flowcell, while low overall quality results from an overloaded flowcell.

##### Our Software

We have designed quality control software that performs a limited but effective series of quality control tests in order to offer feedback on the reliability of sequencing data and point the user toward potential sources of bias. There are Python and R versions of the program, which both analyze sequencing data in FASTQ format.

###### Input

The program takes in a FASTQ file as its input. This file contains sequence reads and their corresponding Phred quality scores (represented as ASCII character strings). The input file is parsed in four-line blocks, and the last line of each block is interpreted as the quality score line. All the quality score lines are stored in an array where each row represents a read, and the number of columns equals the length of the longest read. This array is then used as the basis for calculating further quality control statistics.

###### Modules

We designed the program to carry out a subset of the quality control measurements used in FastQC. Specifically, our program’s modules are:

1.) Sequence Length Distribution:
As the program processes the FASTQ entry for each read, it also calculates the read length. These values are then expressed as a histogram. Different patterns of read lengths are expected for different forms of sequencing technology, so this graph should be interpreted with some nuance. For Illumina sequencing, for example, reads should all be of equal length. If the distribution or magnitudes of sequence lengths stray from the expectation, this could indicate a problem with the sequencing or base calling processes.

2.) Per Base Sequence Quality: 
The program calculates statistics to describe the distribution of Phred quality scores at each position in the read. Mean-based and median-based metrics are both used to better describe both the center and spread of the scores. For each read position, there is one boxplot centered at the mean with the box extending one standard deviation in either direction, and there is another boxplot centered at the median with the box extending from the 25th to 75th percentiles. It is expected that quality scores will decrease toward the end of the read, as the risk of base mismatch increases, but this graph allows the user to determine when this decline begins and how quickly it occurs. Based on the thresholds established in FastQC, the user should be wary if a position’s 25th percentile has a quality score below 10 or if its median is less than 25. The user should consider the data to be low quality if any position’s 25th percentile has a quality score below 5 or if its median is less than 20.[4]

3.) Per Sequence Mean Quality Distribution
This final module calculates the distribution of mean Phred quality scores for reads (average of Phred scores for all bases in read). The program generates a histogram of mean scores. Higher scores are preferred, and FastQC considers a most frequent score of less than 27 (0.2% error rate) to be a threshold for caution and less than 20 (1% error rate) as a threshold for rejection.[4] If there is a second cluster of mean Phred scores with high frequencies, this may indicate that these reads were somehow sequenced differently (with higher or lower quality, depending on their relative Phred scores in comparison to the modal Phred score.)

Our program also informally provides some of the information from the Basic Statistics module: specifically, filename and number of sequences. These were two important pieces of information that were worth including even if they weren’t part of a formal module. Some of the other information from the Basic Statistics module (the items related to sequence length) can be determined from our Sequence Length Distribution module.
These modules were chosen from the 12 offered by FastQC because these three provide the most basic measures of quality that are relevant to all datasets. Specifically, these metrics are informative even if the data is high-quality. Many of the modules in FastQC have specific quality thresholds, and if the module’s score dips below that value, the user is informed that their reads are lacking in quality in at least one way. However, if the reads are good, these metrics are not particularly helpful because they can offer no other information to guide future analyses.
The three statistics that we selected are able to discern between high and low quality reads, as detailed above in the description of each of their functions. FastQC defines thresholds for each of them. However, they can still be valuable tools even if there are no significant biases in the data. Even if the sequence length distribution for reads follows the expected trend (e.g., all the same length, following a normal distribution, etc.), it is useful to know what length the reads actually are, or what their median is. Per base sequence quality provides crucial information about the spread of quality scores and allows users to visualize how quality scores drop off toward the ends of reads. And per sequence mean quality distribution may reveal a cluster of reads with low quality scores that merit further inspection.

###### Output

The program provides a primary output in the form of a text file containing the input filename and the number of reads it contains. Then, it contains the filename for each module’s output graph. Each module produces one graph, saved as an image file — a histogram for modules 1 and 3, and a boxplot graph for module 2. These graphs visually present important quality control statistics. If the graphs show that the data is high quality, then the information in the graphs can just be used to inform future analyses of the sequencing data by understanding minor biases and notable trends. If the graphs reveal significant loss of quality due to biases in the sequencing method or human error, further analysis is required to pinpoint the source of the error. The other FastQC modules may come in handy for this task, as they are each more closely linked to one particular error-prone aspect of the sequencing process.

#### [Sample Python Code](https://github.com/peter-mm-williams/CBB752_Final_Project_1.2.git)

#### [Sample R Code](https://github.com/dspak/CBB752_Final_Project_1.2)

#### References

1. Ewing, B., Hillier, L., Wendl, M.C., & Green, P. Base-Calling of Automated Sequencer Traces Using Phred. Genome Res 8(3), 175-94 (1998).
2. Richterich, P. Estimation of Errors in “Raw” DNA Sequences: A Validation Study. Genome Res 8(3), 251-259 (1998).
3. Cock, P.J.A., Fields, C.J., Goto, N., Heuer, M.L., & Rice, P.M. The Sanger FASTQ file format for sequences with quality scores, and the Solexa/Illumina FASTQ variants. Nucleic Acids Res 38(6), 1767-71 (2010).
4. Andrews, S. FastQC. Babraham Bioinformatics, (2016). http://www.bioinformatics.babraham.ac.uk/projects/fastqc/

---

~~### Sub-Project 2: trim reads based on quality score from FastQ file~~

> This is a temporary title. Remove "Sub-Project X" and assign a proper title.

## Sequence Read Trimming

#### Contributed By

- Documentation: [Nathan](https://github.com/NathanNN)
- [Python](https://github.com/wellshl/CBB752_Final_Project_1.3): [Heather](https://github.com/wellshl)
- [R](https://github.com/dspak/CBB752_Final_Project_1.3): [Dan](https://github.com/dspak)

~~#### Python Card, Brought by Heather~~

~~See project repository: https://github.com/dspak/CBB752_Final_Project_1.3.git~~

> It should ALWAYS start by documentation first, followed by python and R examples, then referece at the end.

~~#### English Card, Brought by Nathan~~

#### What is a FASTQ file? 

FastQ file is a text file with the FASTQ format, designed to contain a nucleotide sequence and its associate quality score in the ASCII character-encoding scheme. This format is used as output data for high-throughput sequencing from companies like Illumina [1]. 


#### What is quality score?

In the ASCII encoding scheme, a set of characters are put into order to denote quality, for example“!” is the lowest quality score and “~” is the highest. Quality is determined by the PHRED software, in which the quality score Q = -10*log(10)*P [2]. The score correlates with the probability of getting the incorrect base call, for example a quality score of 10 means the probability of base call will be incorrect 1 in 10, while a score of 60 means the probability 1 in 1000000 will be incorrect.The basis of this base-calling algorithm our tool will utilize consists of predicting peak locations, identifying observed peaks, matching predicted peaks to observed peaks, and find missed peaks. Illumina FASTQ format starts with “@” followed by the record identifier and sequence length, after that is a nucleotide sequence. The next line starts with the “+” followed by the optional title, then after that is the quality line for the above nucleotide sequence. There are several different quality score metrics, including Illumina Q+64 and Sanger Q+33. To get Q+64, one need to add Illumina 1.3+”Q+64” using ASCII characters 64-to-126 to score 0-to-62 on the P scale. For Q+33, one need to add the Probability values of Phred scores 0-to-93 with ASCII codes characters 33-to-126.    

> There are different quality score metrics used for different sequencing platform. This type of information is actually quite useful. Maybe you can use this section to explain more. For example, there are Illumina Q+64 and Sanger Q+33, for more information, http://www.somewhereville.com/?p=1508#more-1508


> What's the use of peak calling in this read trimming tool? This is not a base-calling algorithm and this part needs to be updated with relavent information.

#### What is our implementation for trimming sequences based on quality scores?

The rationale for such a tool is that high-throughput sequencing have high quality portions from the 5’ end which slowly degrades as sequencing proceed to the 3’ end. Before we can use this data for biological research, it is imperative to cut out poorly defined nucleotides. Our tool will take in a FASTQ file and a score file as input and then output the nucleotide sequence trimmed based on the quality score. The tool will also have options for a threshold quality score as well as a minimum read length. Our algorithm will utilize the sliding window technique, where we propose to calculate the average of quality scores within a window of 4 nucleotides then compare it to an arbitrary threshold quality score we wanted. If the average is larger or equal to the threshold, the nucleotides will be kept in the final sequence. If the average is below the threshold, we will remove all 4 nucleotides as well as the rest of that nucleotide sequence.

> Is 4 a fixed window size?

#### What is the biological relevance for this tool?

This tool will be a quick asset in organizing biological data for further assembly or research. The test file we are using for our tool includes the genome read of a fungus. The reason for testing this genome is because it has relevance in assembly. These sequences are half of a paired-end read, as such quality is low in the middle region where assembly of two sequences happens [3]. By using this tool we can filter out paired-end sequences with low quality at their 3’ ends and therefore prevent assembly. Only sequences with adequate quality will proceed to assembly of the genome. Some existing tools that remove low quality reads are Trimmomatic and Fastx. Trimmomatic is a trimming tool on the USAELLAB.org website [4]. It can take in a file and remove low quality bases using a 4-base wide sliding window, dropping bases below quality score 15 and also ignore sequences that are less than 36 bases long. Fastx toolkit is available at the Hannon lab from Cold Spring Harbor Laboratory. The available tools allow users to convert FASTQ to FASTA files, find the reverse-complement of sequences, and filter sequences based on quality.        

> Maybe a survey of existing tools and existing methods for removing low quality reads is missing.

#### [Sample Python Code](https://github.com/wellshl/CBB752_Final_Project_1.3)

> I see that both R and Pyhton code are in the same repository. It would be preferred to have a seperate repository for Python and R.
> Please work on formatting of readme a little more. Also, it would be nice to have a sample output of Python code for example shown.

~~#### R Card, Brought by Dan~~

#### [Sample R Code](https://github.com/dspak/CBB752_Final_Project_1.3.git)

#### References

> Reference should be numbered

[1] Cock, P. et al. 2010. The Sanger FASTQ file format for sequences with quality scores, and the Solexa/Illumina FASTQ variants. Nucleic Acids Res. 38(6): 1767–1771.

[2] Edwing, B. et al. 1998. Base-calling of automated sequencer traces using phred. Genomic Res. 8(3): 175-185.

[3] Shaw, J. et al. 2015. Biosynthesis and genomic analysis of medium-chain hydrocarbon production by the endophytic fungal isolate Nigrograna mackinonnii E5202H. Appl Microbiol Biotechnol. 99(8): 3715-3728. 

[4] Bolger, A. et al. 2014. Trimmomatic: A flexible trimmer for Illumina Sequence Data. Bioinformatics. Btu170. 
