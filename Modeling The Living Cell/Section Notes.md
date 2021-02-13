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

### Section 3 - Thermodynamics Review

*02/08/2021*

Make sure that homework is in a zip file and that the data files provided for the homeworks are included in the code. 

Last week was thermodynamics review



#### Canonical Ensemble

A way of describing transitions between states in systems that are at equilibrium with a large thermal reservoir. We look at a subsystem of the reservoir that can exchange energy.

Constants: N - Particle Number, V - Volume, T - Temperature

The potential of the canonical ensemble is the Helmholtz Free Energy.
$$
p(i) = \frac{e^{-Ei/k_b T}}{Q}
$$
Where Q is the Canonical Partition Function:
$$
Q = \sum_i^{no. states} e^{-E_i/k_b T}
$$
Where $E_i$ is the energy of a given state. 
$$
P(2) / P(1) = e^{-\Delta E/k_b T}
$$


#### Entropy

We define the entropy as the number of microstates. A microstate is a particular configuration of particles. 
$$
S = k_b ln(\Omega)
$$
Where $k_b$ is Boltzmann's constant or $8.3145/6.022 \times 10^{23}$ 

$\Omega$ is the number of microstates available to the system a given energy level. Two microstates may have different configurations at the same energy and may reversibly transition between the microstates. 

The highest entropy is the multiplicity at the given energy level. 



### Monte Carlo Simulation

A way of exploring the energy landscape of a particle configuration. 

Suppose we have a system of particles in a box, they have a Kinetic Energy $ = \frac{1}{2}mv^2$ and a potential energy $V(\vec{r})$ 
$$
\int \int dp^N dr^N
$$
The box is a Canonical Ensemble so **N, V, T**  are constant. 

We need to integrate over the momenta and radii. 

The Hamiltonian Operator is an operator that takes in the position and momenta of a system. It is a way of calculating the total energy of the system. Here we extend this concept to an N-dimensional system of particles. 
$$
H(p^N, r^N) = p^2/2m + V(\vec{r})
$$
Our integral can be viewed as a partition function. Before, our energies were discrete and now they are continuous by nature of the integration. 
$$
\frac{1}{N!} \frac{1}{\nu^{3N}}\int dp^N e^{-p^2/2mk_b T} \int dr^N e^{-V(\vec{r})/k_bT}
$$

$$
= \frac{1}{N!} (\frac{2mk_bT}{\nu^2})^\frac{3N}{2} \int dr^N e^{-V(\vec{r})/k_bT}
$$



First we generate an initial configuration and see what equilibrium state is reached. Next, we calculate the potential energy of the system, to do this, we use the Leonard Jones potential. This is a sum of attractive and repulsive Van Der Waals forces. 
$$
V(\vec{r}) \propto (\frac{1}{r_{ij}^6} - \frac{1}{r_{ij}^{12}})
$$
Then calculate the Boltzmann Factor $e^{-H/k_b T}$

Last, implement the Monte Carlo Algorithm. Randomly generates a new configuration for the system by a small factor, then decides whether to accept the change based on the difference in energy produced by the change. Determines the likelihood of the system making that transition.  