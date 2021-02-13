# Problem Set 1 Written Answers

## Modeling The Living Cell - Spring 2021

### *Benjamin Fry - bfry2*

 

### Problem 1:

Completed in MATLAB script.



### Problem 2:

#### 2a.

The frequency of the residues in the 300 residue sequence is captured in the histogram in figure 1. We would expect the frequency of each residue in the histogram to be at about $0.05 = 1/20$  since each amino acid is equally likely to appear. What we actually see is some noise around this value as by nature of random number sampling, some counts will be slightly above and some will be slightly below the expected frequency. 

#### 2b.

Plotted in Figure 2 using stairs plot and residue labels. 

#### 2c.

The frequency of the residues generated is shown similarly to part a in the histogram in figure 3. The actual frequency of the residues that occur in the sequence is similar to that in the known frequencies from Expasy, however, as expected there is noise that keeps the random sampling from equaling the expected frequencies exactly. When we increase the number of residues to see more of the limiting case by replacing the 300 random numbers with 30,000 random numbers, we can easily see that the frequencies approach the frequencies in the CDF being sampled from. Even still, the 300 residue sequence does a good job of capturing the expected number of residues with the given frequencies. For example, we see that residues like Leucine and Alanine are relatively common while Cysteine and Tryptophan are less common. 

#### 2d.

In reality, residues definitely do not occur completely randomly. Most proteins start with a methionine residue, their secondary structure segments have residues that facilitate stability, and when they interact with membranes, they have regions of hydrophobicity and hydrophilicity that correspond to transmembrane and solvent accessed regions respectively. We would expect biological residues to have similar features to those that neighbor them in the 3-dimensional structure of the protein as we know that proteins have hydrophobic cores and hydrophilic exteriors. 

### Problem 3:

