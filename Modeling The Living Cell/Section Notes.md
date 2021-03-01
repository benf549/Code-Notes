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



#### Monte Carlo Pseudocode

1. Choose a random particle

   1. Use uniform distribution and ensure that each can be selected. 

2. Assign a displacement

   1. Adjust independently by displacement, should be on interval $(-\delta/2, \delta/2)$ 

3. Enforce PBC

   1. $\Delta x = \Delta r - L*round(\Delta r/L)$

4. Calculate LJPE

   1. $v = 4\epsilon[(\frac \sigma {r_{ij}})^{12} - (\frac \sigma {r_{ij}})^{6}]$

5. Calculate probability of acceptance

   1. $P(x) \Pi(x \to x') = p(x') \Pi(x' \to x)$
      1. $\Pi(x\to x') = g(x\to x')acc(x\to x')$ 
         1. where g is the probability of moving from the uniform distribution and acc is the prob of acceptance based on the Boltzmann distribution. 
   2. The probability of being in this state and transitioning to the next state is the same as the probability of being in the next state and transitioning to this state.

6. Update or reject move.

7. repeat for number of particles

   

### Chemical Kinetics and the Gillespie Algorithm

#### Rate Equations

* 0th order rate equations
  * $\empty \to A$
    * rate constant $k$ 
    * $r = k$
    * $\frac{d[A]}{dt} = -k$
* 1st order rate equations
  * $A \to B$
    * rate constant k
    * $r = k[A]$
    * $\frac {d[B]}{dt} = k[A]$
* 2nd order rate equation
  * $A + B \to C$
    * rate constant k
    * $r = k[A][B]$
* For a reversible reaction
  * $A \leftrightharpoons B$
    * forward rate $k_f$
    * reverse rate $k_r$
    * $\frac {d[A]}{dt} = -k_f{[A]} + k_r [B]$

#### Linear vs Nonlinear Differential Equations

I don't think she gave a very good explanation but I missed it if she did.

#### Euler's Method

Comes from the first order Taylor series:
$$
y(t + h) = y(t) + h \frac {dy}{dt} + ... + \frac {h^n}{n!} \frac {d^ny}{dt^n}
$$
 the first order for which gives:
$$
y(t+h) = y(t) + h \frac {dy}{dt}
$$
Often, we can assume we start at $t_0 = 0$ and are given a $y_0$ 

The algorithm:

1. define some number of attempts
2. loop for j in some number of attempts:
   * $m = f(t_0 y_0)$
   * $y_1 = y_0 + h*m$
   * $t_1 = t_0 + h$
   * $t_0 = t_1, y_0 = y_1$
3. End and plot.

#### Gillespie Algorithm

Step 1: Define stochastic rate constants based on the equation rate constants. We use $c_\mu$ where $\mu$ is the reaction being described. The general ides is that we need to account for the fact that we don't keep track of concentrations or spatial considerations. We assume all particles are spread evenly throughout the box. Since we have the volume of the box, we build this into the rate constant. We also assume we are at high enough concentrations that one particle removed is approximately equal to the original concentration. 

Unimolecular Reaction has no concentration dependence so it is independent of the size of the box. Stochastic rate constant just equal to rate constant

Bimolecular Reaction depends on A and B colliding and going to C so we define a rate constant: $C_\mu = \frac {k\mu}{V}$ while, if you have a bimolecular self reaction such as $A + A \to B$ $C_\mu = \frac {k_\mu}{V}$

Step 2: Define the propensities: $a_\mu = h_\mu C_\mu$ where $h_\mu$ is the number of ways the reaction can react into other forms. 

Unimolecular Reactions: $h_\mu = n_a$ so the number of ways is just the number of particles of A

Bimolecular Reactions: $h_\mu = n_a n_b$ and for a self reaction we use $h_\mu = \frac {n_a (n_a -1)} 2$

Step 3: Calculate the amount of time between collision events. We don't have a time step until something happens.
$$
\tau = \frac {-1} {a_{tot}} ln(URN)
$$
where the total propensity is the sum of each reaction propensity. Propensity is recalculated on each iteration through the reaction loop.

Step 4: Choose a reaction 
$$
\sum _{i = 1}^{\mu - 1} a_i \lt (URN * a_{tot}) \le \sum_{i = 1}^\mu a_i
$$
create a CDF of reaction propensities and choose a random number and pick the first reaction that the random number is less than as in CDF example earlier. 

Step 5: update the system and repeat many times

we can use matrices to update the system. Have a reaction matrix $R_m$

> suppose we have four reactions
>
> $E + S \to ES$
>
> $ES \to E + S$
>
> $ES \to E + P$
>
>  $P \to \empty$ 
>
> we then need to account for each reaction and species in the matrix. in this case, we will have a 4x4 matrix.
>
> | Reaction/Substrate | E    | S    | ES   | **P** |
> | ------------------ | ---- | ---- | ---- | ----- |
> | **1**              | -1   | -1   | 1    | 0     |
> | **2**              | 1    | 1    | -1   | 0     |
> | **3**              | 1    | 0    | -1   | 1     |
> | **4**              | 0    | 0    | 0    | -1    |
>
> The matrix can be initialized with the other constants as it is defined by the reactions available to the matrix. To update, we just index the row for the reaction and add the value in the row to each of our copy number variables. 

