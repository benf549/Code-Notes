# TA Section Notes

*Modeling the Living Cell*

### Section 2 - Model Development and Problem Set 1

###### PS1

Label axes but otherwise default settings for plots are okay.

###### Problem 9

Estimate the volume and surface area from an image. Not going to be precise they're looking for explained assumptions. Just clearly explain and document thought process and how answer was found. 

###### Model Development

Fundamental forces and their timescales.

The strong nuclear force, electromagnetic force, weak nuclear force, and gravitational force are the four fundamental forces. Relative strengths: gravity : 1, strong: 10^38, EM: 10^26, weak: 10^23. The length scales are basically gravity - EM - (weak - strong?)

Very small models are dictated by Quantum Mechanics. Very large things get planetary/Newtonian and relativistic mechanics. We deal with things in between so no mathematical models fully apply perfectly unlike either extreme. 

Protein Models: 3d atomic model, bead model, AA sequence, chemical kinetics models

Cell Models: whole cell (interactions with other cells at larger scale), Ordinary Differential Equations (odes can model cellular function), spatial model (cells interact on a grid in space), vertex model

###### Numerical Estimation

*Length*

A single cell prokaryote is 1-3$\mu m$ in length. 

> example: estimate the number of proteins in one cell
>
> 1. A cell is approximately 70% water and 30% dry by mass
> 2. The density of the cell is approximately that of water.
> 3. If you estimate the volume of the cell, you can convert to mass with density
> 4. An amino acid is about 100g/mol on average and the average protein is 300 AAs
> 5. If you can estimate the moles from the AA molar mass, use Avogadro's number to get proteins/cell

*Timescales*

Range from 10^-18^ to 10^18^s. 10^5^ is approximately one day. The life span of a human is around 10^7^. 

Protein folding is 10^-6^s to 1s. Sidechain rearrangement occurs around 10^-9^s. Around 10^-15^seconds is the speed of covalent bond vibration. 

> example: calculate the rate of protein production in the cell
>
> cell division takes 3 * 10^3^s about, we know there are about 10^3^ proteins per second and 300 AA / protein
>
> If there are about 20,000 ribosomes per cell, there are about 15 AA / per second / ribosome

