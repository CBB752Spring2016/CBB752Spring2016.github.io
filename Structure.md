---
group: navigation
layout: page
title: Structure Analysis
---



### Sub-Project 1: calculate distance between two alpha carbons from a PDB file

#### Python Card, Brought by Peter
See repository at: https://github.com/peter-mm-williams/CBB752_Final_Project_4.1.git

#### R Card, Brought by Cavin
See repository at: https://github.com/peter-mm-williams/CBB752_Final_Project_4.1.git

#### English Card, Brought by Gawain

 In proteins, structure and function are tightly linked, such that biochemical understanding of the protein is often contingent on understanding the relationship between atoms in space. The spatial and atomic information stored in a PDB file is derived from crystallization and diffraction of the purified protein, followed by phase reconstruction and model refinement. Although there are other methods for obtaining spatial information about proteins, including NMR, SAXS and, more recently, electron cryo-microscopy, protein crystal diffraction remains the gold standard for atomic resolution of structure. Thus, the majority of PDB files deposited in the RCSB database were obtained by this method.
	
 Here, we generate a tool which can identify the distance between any two alpha carbons in a protein. After extracting the x,y,z coordinates for two given alpha carbons from the PDB file, we use the following formula to calculate the distance between them:

![Image of distance formula](https://i.imgsafe.org/98da76c.png)

This output, given in angstroms, is useful in several ways. First, it provides general information about where two carbons are, relative to each other in space. More importantly, this distance can be used to determine whether certain forces and interactions between the atoms are relevant. For example, we can use the calculated distance in coarse-grained models where we only consider interactions between amino acid residues within a certain radius of each other. These models, termed elastic network models, often treat proteins like a network of alpha carbons in which each alpha carbon is connected by virtual springs to every other alpha carbon within a distance cutoff. Because of their simplicity, elastic network models and other distance-cutoff models can be used to model protein flexibility in molecular dynamics simulation without requiring excessive computational power.


### Sub-Project 2: calculate the Lennard-Jones potential based on the input of a PDB file consisting of just alpha carbons and a query point’s xyz coordinates

#### Python Card, Brought by Heather



#### R Card, Brought by Gawain
Placeholder repository at: https://github.com/graceliu2016/Final-Project-4.2

#### English Card, Brought by Nathan




### Sub-Project 3: calculate the dihedral angle based on the input of four points’ xyz coordinates in PDB format

#### Python Card, Brought by Peter
See repository at https://github.com/kevkid/CBB_Bioinformatics_FinalProject_4.3.git

#### R Card, Brought by Kevin


#### English Card, Brought by Gawain
