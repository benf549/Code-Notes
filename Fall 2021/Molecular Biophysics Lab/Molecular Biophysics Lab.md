# Molecular Biophysics Lab Lecture Notes

*Benjamin Fry* - Fall 2021

### Introduction

MBL is a continuation of the work of the previous labs. Continuing a project that started from COVID MBL. Data hasn't been collected yet so this is a research project. We try to connect theory to experiment so spend as much time as possible in as out of the lab. We read a lot of papers to try to understand the projects. We will write a research manuscript in pieces throughout the semester. 

###### Forces responsible for protein folding

The hydrophobic effect is the major driving force of protein folding. Hydrogen bonding creates secondary structure motifs. Van der Waals (charge-induced dipole, dipole-dipole, and induced dipole-induced dipole) and electrostatics.

###### Can we predict a fold from a sequence

From CASP we can predict protein structure from sequence using AlphaFold and Rosetta. Directed Evolution via (Frances Arnold) applies selective stress to bacteria which may eventually result in the fold you're looking for. From first principles, we don't know how to do it. 

###### The project for the semester

Repeat proteins simplify the questions. RNAse A is a typical globular protein used for unfolding studies. We can study repeat proteins which have very few long-range contacts (Notch ankyrin repeat protein). Now they have constructed a consensus repeat protein in which every copy of the protein subunits is exactly the same. Wild type Notch ankyrin has $\Delta G = -3.2 kcal$ while a consensus protein of the repeat protein has a much higher stability at $\Delta G = -23.5 kcal$ 

Finding the consensus is taking a whole bunch of sequences, aligning them and taking the most probable residue at that position. This worked well for repeat proteins, now they are applying this same idea to globular proteins. The consensus protein looks exactly like the crystal structures of the wild type. The globular consensus protein is even more stable the more homologs are used to generate the consensus.

SNase is generally a model system for biophysical studies. It has been engineered over many years to be more stable than the wild type. Doug bet Bertrand that the consensus sequence would be more stable. The consensus protein is 2/2.5 kcals less stable than the wild type. Juliette Lecomte also tried this with truncated hemoglobins which behaved strangely as well. It is odd that there are some proteins where the consensus technique does work and some where it doesn't. 

###### The Oligomer Binding Domain

a 5 strang $\beta$ Barrel arranged in greek key motif. The loop connecting beta 3 and beta 4 is often an alpha helix. This variable loop and beta residues are tuned for binding a particular ligand. SNase is a variation of the OB fold. If you cut off the C-terminus and leave the OB fold, you get something that folds only if you make some directed mutations which stabilize the core. If you take the consensus protein from above of SNase, you cut off the C-terminus leaving only the OB fold, you get a more stable version of SNase (cSNOB mutant). They then took the wild type and grafted the consensus C-terminus onto the wild type OB fold, the stability increases. The reverse did not express. The consensus OB seems to be folded but does not want to express or fold with the WT C-terminus. 

We will be working on variants of this combination of the consensus with wild type design to try to understand what is going on. 

We will take a look at temperature and stability, pH effects (consensus proteins tend to be enriched in ionizable groups), and far-UV CD for folding quantification. 

###### Next Week's Assignments

There is a paper on blackboard, read that to understand the process behind making the consensus nucleases. Since this is a writing course, we will be making figures as part of our writing. We will make two figures, one in PyMol showing the structure, throughout the semester's writing assignments we should use PyMol to see if we can predict the interactions to explain our results. We will also make a figure summarizing the data, to do this, we will need to fit the data with python, and predict the $\Delta G$

We can use python, Mathematica, R etc... for curve fitting. 

### Consensus Sequence Generation

We will be working with SNase. wt-SNase shown in one color, cSN is the consensus sequence. The chimera with wt-OB fold and consensus helices is what we want to work with. The opposite chimera did not express. We can show the chimera colored based on which protein each component came from originally. 

We can rank the energy for each of the 20 aa's at each position and create a partition function. We create an ensemble of proteins and expect that most will mutate to the most stable residue. This proves the thermodynamics behind why consensus should work. Nature doesn't care about making the most stable residue, though the cell might rather prioritize activity so this assumption falters here.  We have an approximate version of this in nature by aligning all known sequences and taking the most probable residue at this position.  

In practice, we obtain a large set of homologous proteins, then curate the sequences to filter out low quality data, and then generate an MSA, and finally determine the consensus sequence. This is pretty easy.

There are different decisions you can make to arrive at different consensus sequences.

To obtain our sequences, there are a couple different ways we could go about it. Curated data sets exist on certain websites for very common proteins. Rarer/more complicated proteins won't have this. You rely on the assumptions the people who created this used when they created this. Alternatively we can perform a homology search for the sequence of interest (BLAST).

This relies on creating pairwise alignments. Score (mis)matches using Point Accept Mutation matrix (PAM) or Block Substitution Matrix (BLOSUM). These scoring matrices quantitatively compare the similarity of organisms based on mutation rates. You also have to identify indels so we penalize gaps formation and extension. Pay a lot to open a gap, but extending a gap is relatively cheap. Usually an * indicates an exact match while a : indicates a conservative substitution or . as not similar. but whoever encoded these alignment tools may not have made the same decisions for what counts as a conservative substitution as what you would choose. 

A global alignment algorithm attempts to align every position in the query to every position in the sequences. Works best when sequences are similar and roughly equal in length. Uses the Needleman-Wunsch algorithm. The other alignment algorithm is a local alignment. This aligns only a portion of the sequence(s). This is useful for more dissimilar sequences with domains/regions of similarity. Uses the Smith-Waterman algorithm. Both algorithms guarantee the best alignment but these are horrendously slow. We need something that approximates these methods to quickly query against millions of sequences.

BLAST is a heuristic that breaks the sequence into words and matches the words against the database. This gives an approximation of a local alignment though it is not guaranteed to give the optimal solution like Smith-Waterman. Profile Hidden Markov Models (HMMER) takes the state of the model you're trying to predict where the future states depend only on the current state. Hidden because observable states are assumed to correlate to unobserved states. The observed state is the protein sequence and the unobserved state is protein structure. It is another alignment tool. HMMER can take into account the physics of the structure and predict similarity based on sequences. 

We will use HMMER to create our consensus sequences. 

Once we create our data set, we need to refine it to remove incomplete/partial hits. We will remove sequences that deviate in length too far (X%) from the median to filter homologs that may have evolved different functions. We don't want features of added groups leaking into our consensus sequence.  We also remove those that are just the OB fold which could have completely different or no function. 

We also want to cluster sequences by identity to filter out sequences that are very similar to eachother. Since bacteria can horizontal gene transfer, we can find identical genes over and over again. This would bias the final dataset towards these genes' features. Our database is also likely biased towards many bacteria vs more difficult species to sequence.

We will just run a script that does the filtering for us. We can create a Multiple Sequence Alignment based on our pairwise alignments. A progressive alignment procedure compares in order of pairwise distances between pairs and use a 'guide tree' to align the collection of pairs. Sorts by best pairwise alignments and goes from most similar to least similar. MSA is allowed to split into smaller MSAs and can be realigned before being recombined. There are a lot of other nuances to make these better. HMMs can also be used to do this as well by relying on position specific probability distributions. HMMs are more dynamic and can refine themselves as the alignments are built.

Once we are ready to create the consensus, we create a table of position x {aa residues U gap }. Also need to determine cutoff for when a gap exists at less than half the positions but there is no consensus. 

Covariation is a problem where the identity of a residue at a particular position would conditionally influence the probability of a position somewhere else in the protein. 

### Structural Analysis of cSNase

Want to further study the consensus protein. Want to look for mismatches/entropy like the Barrick paper. The protein generally gained charged residues while losing polar uncharged residues. Unlike the findings of the Barrick paper, we traded Lysine for Arginine. Arginine has a much higher pKa and resonance to delocalize charge over its terminal group. Lysine functions much more like a point charge. Arginine makes a lot more interactions that Lysine can't. Arginine wants to hydrogen bond and stay charged while lysine is easier to bury and change its pKa. Despite being both basic they are pretty similar. The Glu and Asp have slightly different properties but much less than the basic groups.

The consensus sequences in the paper tended to stay about the same in net charge. We observed a decrease in net charge which is odd. Are the effects split evenly between the OB fold and the C-terminus. Chimera 1 (chm1) had less significant changes from the wild type and has a very similar charge to the wild type. This was the one that worked, so maybe this could be part of the reason why. Chimera 1 was the wild type OB fold with the consensus c-terminal helices. Chimera 2 had the majority of the significant changes which means they were localized to the OB fold domain. This protein was the wild-type c-terminal helices with a consensus OB fold.  

Strange that our consensus was enriched in Arg and Val and that the charge decreased by 6, but it doesn't seem that different from the other consensus proteins discussed in the paper. 

###### Alexandrescu et al. Paper

Nuclease appears to be a two domain unfolder. They wanted to see if the OB fold is an independent unit that evolution diverged and recriuted to do other things. They first tried to generate the OB fold of nuclease and studied it with NMR.

In small molecule NMR, you see splitting by equivalent protons. In protein NMR, we can see the methyls, alpha carbons, amides etc but not individual resolution. The broad, clustered peaks in figure 1b show that there isn't a distinct environment for each type of molecular part. This indicates an unfolded protein which we know it was as the wild type OB domain doesn't really fold. Figure 1c shows the SN-OB protein (with two stabilizing point mutations) had much clearer peaks which indicates a better fold. Figure 1d shows good dispersion indicating a good fold for SN-OB. 

Figure 2 shows the OB fold is conserved evolutionarily. 

They used NMR despite experimental complexity because they wanted to be able to compare tertiary structures. Techniques like CD only tell you about the presence of secondary structure.

NOEs (Nuclear Overhauser Effect) tells you residue level information about the orientation of each residue. Short range NOEs are from residues being next to eachother in primary structure. Long range NOEs are interactions between residues that are near eachother in 3D space and separated in primary structure. There are gaps in the long range NOEs indicating less rigid structure in these regions. Using the NOE  data, they were able to essentially run an MD simulation that recapitulates the short and long range contacts.

The Ramachandran plots generated show that the beta barrel is well determined structurally. The loops and alpha helices are allowed to flop around. 

Figures 3g and 3h show the averaged structure of the proteins. We can see the skew of the alpha helix and tighter core created by the point mutations. 3h shows the 3 layers of the beta barrel, the hydrophobic plug and skewed helix. 

In conclusion, they believe the OB fold is a 'primordial fold' that got integrated into more complex folds. Once the OB domain fold gets integrated to SNase, it loses the ability to fold without its c-terminal helices. The SN-OB mutations stabilize the OB fold in exchange for less global stability. Partially folded proteins are bad and lead to aggregation. This is why cells favor a two state fold (folded or unfolded). The two mutations restore the ability of the OB fold to form independently of the C-terminal helices. The beta barrel in SN-OB is similar to SNase. The loss of folding autonomy for the motif may be necessary to maximize cooperativity and stability. 

###### PyMol Variant Comparison

The N and C termini have high gap likelihood, these are poorly defined so they shouldn't matter too much. Gaps can also be introduced in the c-terminal helices. 

Used http://curie.utmb.edu/getarea.html to calculate SASA for each residue.

### SNase and Protein Unfolding Studies

We take advantage of the fact that Trp exists in a hydrophobic pocket of the protein. We don't have to do CD which would suck because it is much more expensive. Tryptophan fluorescence can be used to quantify unfolding. We will know our protein is in the native state, we will not see fluorescence due to the quenching of the emission by the solvent. 

The $\Delta G$ for most globular proteins ranges from -5 to -10 kcal/mol. The ratio of native to denatured at pH = 7 is around 5000:1

We use denaturation experiments to calculate thermodynamic parameters assuming a linear native and denatured baseline. We can take the point where $f_d$ and $f_n$ are equal ($\Delta G$ = 0). We can measure the fraction denatured from the native baseline:
$$
y_{obs} = \frac{y_d + y_n e^-\Delta G/RT}{1 + e^-\Delta G /RT}
$$
check that though.

Sometimes, when there are sloping baselines, we can take the non-flat baselines into account by fitting them to a line. 
$$
y_d = m_dx+b\\
y_n = m_nx+b
$$
We can now fit the data set as a whole at once, but we used to not be able to fit all at once. We only care about the $\Delta G$ and $m$ value so we can fit the baselines first and then plug the fit parameters into the original equation. 

By plotting $K_{eq}$ in the transition region of the unfolding curve, we get the linear dependence of $K_{eq}$ wrt [denat]. The factor of RT doesn't really matter for the value of m. We can multiply the intercept by RT then to get the value of $\Delta G$. We can then extrapolate $\Delta G$ back to where there is no denaturant to get the value we can actually compare between proteins ($\Delta G_{H2O}$):
$$
y = m[denat] + \Delta G_{h2o}
$$
The m value, does have some thermodynamic meaning. There are also non-linear denaturant binding models but these don't work that well since there is usually a nice linear dependence meaning we can find a meaning for m value. The best thing the m value tends to correlate with is the Solvent Accessible Surface Area. We also get that the heat capacity is linearly correlated with m value. Measure of the surface area that is exposed during unfolding $\Delta ASA$. Could also be a measure of the cooperativity of unfolding.  

Urea and Guanidinium HCl mess with the ability of water to solvate things. The exact mechanism for how they unfold the proteins is unknown, but it doesn't really matter for us.

Guanidinium is a much stronger denaturant. We expect the extrapolated $\Delta G_{H2O}$ for both denaturants should be the same though

###### Shortle & Meeker

Found that the m-values for Class I proteins had smaller m values while Class II proteins had larger m value than wild type. The mutations they had to screen were created by a faulty nuclease. The m-value is related to accessible surface area. We see that single mutants when combined have m-values that are additive.

Their CD @ 222nm data showed that maybe the variant that does not show nice cooperative denaturation, has an intermediate. We know from the previous paper that this might be the OB fold domain of the protein being folded despite the high concentration of denaturant. This protein had the stabilizing mutations we studied in the last paper. 

Since the tryptophan is in the c-terminal alpha helices, we may not be able to tell if we have reached the denatured state or a locally unfolded state where something like the OB-fold is still folded but the tryptophan residue is quenched. They alternatively propose that there is a range of unfolded surface areas for the denatured state of the protein. There are denatured states that become increasingly denatured with more denaturant. This was an issue for the Class I variants which changed in m-value with increased denaturant. 

Since the mutations they found to increase the m (surface area) were all from non-polar to polar we may be able to see the surface area increase by these polar residues having more favorable interactions with the solvent rather than relying on hydrophobic collapse to keep it away from the surface. The mutations that decrease the m (surface area) generally increase the non-polar character of the position which would increase the compactness of the protein at this position. 

Quick aside: Met is generally non-polar but because its sulfur is sorta like an oxygen (below on periodic table), it is less non-polar than a very non-polar residue like Ile. 

Take-Aways: largely linear extrapolation is correct, but point mutations can alter the Cm and m 
