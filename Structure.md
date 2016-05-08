---
layout: page
title: Structure Analysis
group: navigation
weight: 4
---

## Table of Contents
***[Distance Between Alpha Carbons](#Calculating-distance-between-alpha-carbons-in-a-pdb-file)***  
***[Lennard-Jones Potential](#Calculating-the-Lennard-Jones-Potential-from-a-Query-Point-and-a-PDB File)***  

---
### Calculating Distance Between Alpha Carbons in a PDB File

> You should assign a proper title
> Please carefully read through and follow the formatting guideline found in [Project 1.2](http://cbb752spring2016.github.io/QCStep)

- Documentation: [Grace](https://github.com/graceliu2016)
- [Python](https://github.com/peter-mm-williams/CBB752_Final_Project_4.1.git): [Peter](https://github.com/peter-mm-williams)
- [R](https://github.com/peter-mm-williams/CBB752_Final_Project_4.1.git): [Calvin](https://github.com/calvinrhodes)

#### Python Card, Brought by Peter
See repository at: https://github.com/peter-mm-williams/CBB752_Final_Project_4.1.git

> Good use of example, instructions on input parameters. I would make a minor edit on formatting. Give a project unified name and use it in your readme section.

#### R Card, Brought by Cavin
See repository at: https://github.com/peter-mm-williams/CBB752_Final_Project_4.1.git

> Good use of example, instructions on input parameters. Ideally, it would be preferred to have a seperate repository for R (for cleaner look), but this is minor and debatable. I would also work on formatting of readme a little more.

I would make a minor edit on formatting. Give a project unified name and use it in your readme section.

##### Acquisition of the spatial data in PDB files

In proteins, structure and function are tightly linked, such that biochemical understanding of the protein is often contingent on understanding the relationship between atoms in space. The spatial and atomic information stored in a PDB file is derived from crystallization and diffraction of the purified protein, followed by phase reconstruction and model refinement. Although there are other methods for obtaining spatial information about proteins, including NMR, SAXS and, more recently, electron cryo-microscopy, protein crystal diffraction remains the gold standard for atomic resolution of structure. Thus, the majority of PDB files deposited in the RCSB database were obtained by this method.

> I would describe more about structure of PDB file. Please also give some example of PDB databases besides RCSB.

##### Calculating the distance between alpha carbons
	
Here, we generate a tool which can identify the distance between any two alpha carbons in a protein. We ask the user to input the PDB file of interest and the indices of the alpha carbons. These indices correspond to the residue number of the alpha carbon's associated amino acid in the primary sequence of the protein. After extracting the x,y,z coordinates for two given alpha carbons from the PDB file, we use the following formula to calculate the distance between them:

![Image of distance formula](https://i.imgsafe.org/98da76c.png)

This output, given in angstroms, is useful in several ways. First, it provides general information about where two carbons are, relative to each other in space. More importantly, this distance can be used to determine whether certain forces and interactions between the atoms are relevant. For example, we can use the calculated distance in coarse-grained models where we only consider interactions between amino acid residues within a certain radius of each other. These models, termed elastic network models, treat proteins like a network of alpha carbons in which each alpha carbon is connected by virtual springs to every other alpha carbon within a distance cutoff [1]. Because of their simplicity, elastic network models and other distance-cutoff models can be used to model protein flexibility in molecular dynamics simulation without requiring excessive computational power.

##### References

[1] Yang, L-W. & Chng, C-P. Coarse-Grained Models Reveal Functional Dynamics - I. Elastic Network Models – Theories, Comparisons and Perspectives. Bioinform Biol Insights, 2, 25-45 (2008). 

> Good. I would mostly work on formatting a little more.

---

### Calculating the Lennard-Jones Potential from a Query Point and a PDB File

- Documentation: [Nathan](https://github.com/NathanNN)
- [Python](https://github.com/wellshl/Final-Project-4.2): [Heather](https://github.com/wellshl)
- [R](https://github.com/graceliu2016/Final-Project-4.2): [Grace](https://github.com/graceliu2016)


### Calculating Dihedral Angles

- Documentation: [Grace](https://github.com/graceliu2016)
- [Python](https://github.com/kevkid/CBB_Bioinformatics_FinalProject_4.3.git): [Peter](https://github.com/peter-mm-williams)
- [R]: [Kevin](https://github.com/kevkid)

#### R Card, Brought by Kevin


##### Protein Backbone Dihedral Angles
The phi and psi protein backbone dihedral angles define the two degrees of freedom of the backbone and sterically determine much of the protein’s local folding structure. Because dihedral angles characterize the angle of rotation between two planes, they are defined by four spatial points. The phi angle measures the angle around the N-Cα bond in the consecutive sequence C’-N-Cα-C. The first C’ in this definition comes from the prior amino acid residue. The psi angle measures the angle around the Cα-C bond in the sequence N-Cα-C-N’, where the last N’ comes from the next amino acid residue. The final possible dihedral angle is omega (Cα’-C’-N-Cα), the peptide bond, which is fixed at (0, 180°) because the partial double bond character of the peptide bond does not allow rotation around the C’-N bond. 

![Dihedral angles schematic](https://i.imgsafe.org/1527d6a.png)

Phi and psi dihedral angles are restricted to certain values, because many angles will produce steric clashes between the backbone and the side chains in the polypeptide sequence. Sterically allowable phi/psi combinations were calculated in the 1963 by G.N. Ramachandran and colleagues using first a hard sphere model and then a reduced radius model. Their findings are presented below in the Ramachandran plot, a phi/psi map which plots regions of allowed dihedral angles. Larger atom sizes produce narrower Ramachandran limits (dark blue regions), while smaller atoms have some more flexibility (light blue regions). In addition, we also note that certain secondary structures have characteristic phi/psi angles. For example, right-handed alpha helices are found in the region around Φ=+45°, Ψ=-45°, while beta sheets are found in the top left-hand corner of the plot. Recent advances in data mining and protein simulation have verified the allowable phi/psi angles predicted by the Ramachandran plot. Studies by Zhou et al. have found that sterics alone can account for the range of phi/psi angles observed in Protein Data Bank structures [1]. Likewise, simulations of coarse-grained hard-sphere models which incorporate only steric interactions have been sufficient recapitulate the biologically observed range of dihedral angles in both backbones and side chains [2]. Thus, when modeling protein folding, backbone dihedral angles are incredibly important constraints on the structure and behavior of the protein. In addition, we can assess the quality of a proposed protein structure by ensuring that its backbone dihedral angles all fall within allowable phi/psi ranges. 

![Ramachandran plot](https://i.imgsafe.org/af879a9.png)

##### Calculating Dihedral Angles

Given the spatial coordinates (x,y,z) of the four points which define two planes, we can calculate the angle between them (theta) in two ways. First, we can find the normal vectors for each plane, n1 and n2, such that each vector is perpendicular to the plane. For two planes with the following Cartesian definition, the normal vectors are n1 = (a1, b1, c1) and n2 = (a2, b2, c2):

![planes definition](http://i.imgsafe.org/b513c1e.png)

In vector notation, we can find the normal vectors by taking the cross-product of two non-collinear vectors on that plane. The cosine of the dihedral angle theta is defined as the dot product of the normal vectors n1 and n2. For a Cartesian definition, this is extremely simple to calculate: 

![cosines definition](http://i.imgsafe.org/408dc73.png)

Likewise, in vector notation, the dihedral angle (indicated as phi) defined by points i,j,k,l, the dot product of the normalized vectors can be used to calculate cosine and sine using the same vector definition as shown above:

![vector cosines sines definition](http://i.imgsafe.org/e84f542.png)

In vector notation, because the arccosine and arccsine functions are limited in range from 0 to π and -π/2 to π/2 radians respectively, implementing this definition to calculate the dihedral angle produces problems of signage. The atan2 function maintains signage information from the cosine and sine angles and and outputs a dihedral angle value in the range (-180°, 180°]. To calculate the dihedral angle phi with this function, we input the x coordinate as cos(phi) and the y coordinate as sin(phi). 

![Atan2 definition](https://upload.wikimedia.org/math/c/8/1/c81848e82ad6e45e9e14f81cb38895a2.png)

##### References

[1] Zhou, AQ, O'Hern, CS, Regan, L (2011). Revisiting the Ramachandran plot from a new angle. Protein Sci., 20, 7:1166-71
[2] Zhou, AQ, O'Hern CS, and Regan, L (2014). Predicting the side-chain dihedral angle distributions of non-polar, aromatic, and polar amino acids using hard-sphere models. Proteins: Structure, Function, and Bioinformatics, 82, 2574.
