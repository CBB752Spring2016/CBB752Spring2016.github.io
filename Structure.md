---
layout: page
title: Structure Analysis
group: navigation
weight: 4
---



### Sub-Project 1: calculate distance between two alpha carbons from a PDB file

#### Python Card, Brought by Peter
See repository at: https://github.com/peter-mm-williams/CBB752_Final_Project_4.1.git

#### R Card, Brought by Cavin
See repository at: https://github.com/peter-mm-williams/CBB752_Final_Project_4.1.git

#### English Card, Brought by Gawain

 In proteins, structure and function are tightly linked, such that biochemical understanding of the protein is often contingent on understanding the relationship between atoms in space. The spatial and atomic information stored in a PDB file is derived from crystallization and diffraction of the purified protein, followed by phase reconstruction and model refinement. Although there are other methods for obtaining spatial information about proteins, including NMR, SAXS and, more recently, electron cryo-microscopy, protein crystal diffraction remains the gold standard for atomic resolution of structure. Thus, the majority of PDB files deposited in the RCSB database were obtained by this method.
	
 Here, we generate a tool which can identify the distance between any two alpha carbons in a protein. We ask the user to input the PDB file of interest and the indices of the alpha carbons. These indices correspond to the residue number of the alpha carbon's associated amino acid in the primary sequence of the protein. After extracting the x,y,z coordinates for two given alpha carbons from the PDB file, we use the following formula to calculate the distance between them:

![Image of distance formula](https://i.imgsafe.org/98da76c.png)

This output, given in angstroms, is useful in several ways. First, it provides general information about where two carbons are, relative to each other in space. More importantly, this distance can be used to determine whether certain forces and interactions between the atoms are relevant. For example, we can use the calculated distance in coarse-grained models where we only consider interactions between amino acid residues within a certain radius of each other. These models, termed elastic network models, treat proteins like a network of alpha carbons in which each alpha carbon is connected by virtual springs to every other alpha carbon within a distance cutoff [1]. Because of their simplicity, elastic network models and other distance-cutoff models can be used to model protein flexibility in molecular dynamics simulation without requiring excessive computational power.

[1] Yang, L-W. & Chng, C-P. Coarse-Grained Models Reveal Functional Dynamics - I. Elastic Network Models – Theories, Comparisons and Perspectives. Bioinform Biol Insights, 2, 25-45 (2008). 


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

# Protein Backbone Dihedral Angles
The phi and psi protein backbone dihedral angles define the two degrees of freedom of the backbone and sterically determine much of the protein’s local folding structure. Because dihedral angles characterize the angle of rotation between two planes, they are defined by four spatial points. The phi angle measures the angle around the N-Cα bond in the consecutive sequence C’-N-Cα-C. The first C’ in this definition comes from the prior amino acid residue. The psi angle measures the angle around the Cα-C bond in the sequence N-Cα-C-N’, where the last N’ comes from the next amino acid residue. The final possible dihedral angle is omega (Cα’-C’-N-Cα), the peptide bond, which is fixed at (0, 180°) because the partial double bond character of the peptide bond does not allow rotation around the C’-N bond. 

![Dihedral angles schematic](https://i.imgsafe.org/1527d6a.png)

Phi and psi dihedral angles are restricted to certain values, because many angles will produce steric clashes between the backbone and the side chains in the polypeptide sequence. Sterically allowable phi/psi combinations were calculated in the 1963 by G.N. Ramachandran and colleagues using first a hard sphere model and then a reduced radius model. Their findings are presented below in the Ramachandran plot, a phi/psi map which plots regions of allowed dihedral angles. Larger atom sizes produce narrower Ramachandran limits (dark blue regions), while smaller atoms have some more flexibility (light blue regions). In addition, we also note that certain secondary structures have characteristic phi/psi angles. For example, right-handed alpha helices are found in the region around Φ=+45°, Ψ=-45°, while beta sheets are found in the top left-hand corner of the plot. Recent advances in data mining and protein simulation have verified the allowable phi/psi angles predicted by the Ramachandran plot. Studies by Zhou et al. have found that sterics alone can account for the range of phi/psi angles observed in Protein Data Bank structures [1]. Likewise, simulations of coarse-grained hard-sphere models which incorporate only steric interactions have been sufficient recapitulate the biologically observed range of dihedral angles in both backbones and side chains [2]. 

![Ramachandran plot](https://i.imgsafe.org/af879a9.png)

# Calculating Dihedral Angles

TBC

# References

[1] Zhou, AQ, O'Hern, CS, Regan, L (2011). Revisiting the Ramachandran plot from a new angle. Protein Sci., 20, 7:1166-71
[2] Zhou, AQ, O'Hern CS, and Regan, L (2014). Predicting the side-chain dihedral angle distributions of non-polar, aromatic, and polar amino acids using hard-sphere models. Proteins: Structure, Function, and Bioinformatics, 82, 2574.
