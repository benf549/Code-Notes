# Problem Set 7 Written Answers

## Modeling The Living Cell - Spring 2021

### *Benjamin Fry - bfry2*

*04/25/21*

### Part 1 - Describe The Model

###### a) How Many Species and List

There are 9 species in this system

1. gene_A
2. mRNA_A
3. A
4. gene_A_bound
5. gene_R
6. mRNA_R
7. gene_R_bound
8. R
9. C

###### b) How Many Reactions To Consider

There are 16 reactions to consider here because the forward (a) and reverse reaction (b) for reactions 2 and 5 need to be handled separately. 

###### c) Which Reactions Involve Degradation of A Species

Reactions 11, 12, 13, and 14 are degradation reactions. 

###### d) Which Reactions are Bi-Molecular Association Reactions

Reaction 2a (forward reaction of reaction 2), reaction 5a (forward reaction of reaction 5), and reaction 9 are all bi-molecular association reactions. The fastest rate will depend on the concentrations of the reactants because the rate equation for this type of reaction is as follows:
$$
rate = k[A][B]
$$
however, the rate constant for reaction 9 is significantly higher at $1204\mu M^{-1}hr^{-1}$ compared to the $602\mu M^{-1}hr^{-1}$ so all else equal (all reactant concentrations the same), reaction 9 will have the fastest overall rate.

###### e) How Many States for `geneA` and How Transitions

Gene A exists in two states, an unbound (`geneA`) and an A-bound (`geneA_bound`) state. 

We start with a single copy of `geneA` which is used (non-destructively) to produce an `mRNA_A` . The `mRNA_A` is then used (non-destructively) to produce `A`. The `A` that is produced can then associate with the copy of `geneA` forming a single copy of `geneA_bound` which produces `mRNA_A` at a higher rate than `geneA`. The `geneA_bound` complex can then dissociate reforming `geneA` and `A`.

###### f) Which Gene is More Frequently Transcribed into mRNA

Both of these transcription reactions are first order and the rates of reaction will be defined as follows:
$$
rate = k[X]
$$
where $X$ is the concentration of the gene. The rate constant for the production of `mRNA_A` from `geneA` is $50hr^{-1}$ (reaction 1) while the production of `mRNA_R` from `geneR` (reaction 4) is $0.01hr^{-1}$. Because there can be at most one of each gene, `geneA` is more frequently transcribed into mRNA. 

###### g) Which mRNA is More Frequently Translated to Protein

Both of these translation reactions are first order and the rates of reaction will be defined as follows:
$$
rate = k[X]
$$
where $X$ is the concentration of mRNA. So the actual rate will vary based on the number of mRNA copies but the rate constant for reaction 7 (`mRNA_A` translation) is much higher at $50hr^{-1}$ than that of reaction 8 (`mRNA_R` translation) at $5hr^{-1}$. Thus, `mRNA_A` is more frequently translated into protein than `mRNA_R`.

###### h) Which Species Degrades Most Frequently

The degradation reactions are also a first order reactions and thus the rate is also controlled by concentration of the species. However, the rate constant for the degradation reaction of `mRNA_A` at $10hr^{-1}$ is higher than the others and using the first order rate equation above gives that this reaction will occur most frequently when all else is equal (the other concentrations of reactants are equal).



### Part 2 - Simulate the Model

###### a) What Peaks First Does This Make Sense?

Below is the plot of the 5 runs superimposed on eachother:

![fig1](C:\Users\benfy\Desktop\Modeling\PS7\fig1.jpg)

A always peaks first which makes sense because we are starting with only a single copy of `geneA` and `geneR` with `geneA` being much more likely to be transcribed to `mRNA_A` and `mRNA_A` is much more likely to be translated to `A` which is seen when comparing the rate constants for each of these reactions. As `A` is produced eventually `gene_R_bound` will be formed when the produced `A` reacts with the `geneR` copy which produces `mRNA_R` and thus `R` at a much higher rate. So, the increase in `R` will only really occur after sufficient quantities of `A` have been formed. So, the observed pattern makes sense given this info and what we discussed above. We also note that in all 5 runs, the peaks occur and then due to random differences due to the nature of the stochastic simulation the peaks spread out and generally become less and less correlated with one another.

###### b) Average Height of the Peaks for A and R

The below plot is of the first Gillespie simulation I ran and that was plotted in the above figure but pulled for isolation and measurement of peak heights and wave frequencies.

![fig2](C:\Users\benfy\Desktop\Modeling\PS7\fig2.jpg)

I measured the average peak height to be **1498.5 particles** for A and **1957.75 particles** for R

###### c) Average Wavelength (in  s)

I measured the average wavelength for the A particles to be 25.82 hours or 1549.391 seconds while the average wavelength for the R particles was 25.58 hours or 1534.911 seconds.

###### d) Decrease Degradation Rate

The figure below is the result of the same simulation but with the degradation rate of `R`  reduced from $0.2$ to $0.05hr^{-1}$:

![fig2](C:\Users\benfy\Desktop\Modeling\PS7\fig3.jpg)

As expected, `R` hangs around longer resulting in an increased wavelength for the `A` cycles. Unlike what we are told to expect from the deterministic solution to the system, there is still a clear cyclic pattern in these data. The time between spikes of `A` is just increased from those observed in `figure 2` above as `R` sticking around for longer makes it more difficult for high concentrations of  `A` to occur as any available `A` is most likely to form `C` in the presence of high concentrations of `R`. Only once R has degraded to sufficiently low levels can `A` form a peak which through the reaction coupling produces `R` perpetuating the cycle.



### Problem 3 - Chemical Kinetics and Rate Equations

###### a)

$$
\frac {d[B]} {dt} = -k_1[A][B] -k_4[B]^2 +2k_5[D]
$$

###### b)

$$
\frac {d[C]} {dt} =  -k_3 + k_1[A][B]
$$

###### c)

$$
\frac {d[D]} {dt} =  -k_6[C][D] + k_5[B]^2
$$

