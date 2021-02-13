# Modeling The Living Cell

### Class Notes

#### Week 2 - Tuesday

I have decided that this class is a lot of info and it'll be better to have the content typed. 

###### Energy Scales

We will use many concepts from thermodynamics but we wont go too far in-depth because this is not a course on thermodynamics. 

Chandler Chapter 1 for a formal review of Thermodynamics.

Physical Biology of Cell Chapter 5 review of thermodynamics. 



*Types of Energy*

Potential and Kinetic

Types of potential energy - chemical, electrical, gravitational, light (electromagnetic), thermal energy - the only one that cannot be used to do work, nuclear energy, mechanical. 

Thermal energy comes from the random jiggling of molecules and therefore cannot be used to do work.  

When we think about energy we need to understand the scales at which the various types of energy are relevant.

What are the units of energy - Joules, or $\frac{kg m^2}{s^2}$ which can be remembered as W = F*D and F = ma. 

The free energy is the energy available to do work. 



Thermal Energy Scale

$E_{thermal} = K_b T$ where $K_ b$ is Boltzmann's constant measured in Joules/kelvin
$$
K_\beta = \frac{8.3145} {6.022 \times 10 ^{23}} = 1.38 \times 10^{-23} J/K
$$
At room temperature (25$^\circ C$ )
$$
K_\beta T \approx 0.6 kcal/mol \approx 2.5 kJ/mol
$$


 A covalent bond ~ 500 kJ/mol; Thus, we need enzymes to bring the energy barrier down for spontaneous bond cleavage to occur as the thermal energy is too low to do it on its own.

A hydrogen bond ~ 8-15 kJ/mol



*Energy Scale*

Recommended human energy intake is around 2000 kcal there are about 4.184kJ/kcal so we take in around $8 \times 10^6J$

A charged sphere (electrostatics as dictated by coulomb's law) is shown below. 

Bond energy can be viewed as putting an electron in a box. 

Mechanical energy for bending energy of a 20:1 rod increases with length as expected. 

![image-20210202140623673](C:\Users\benfy\OneDrive - Johns Hopkins\Documents\Markdown Notes\.images\image-20210202140623673.png)

The energies of all of these energy sources are on the scale of thermal energy at around the microscopic scale. This graph is in chapter 5 of the textbook I believe.



###### Thermodynamics Review

Exists separately from statistical mechanics. The macroscopic description of equilibrium and small deviations from equilibrium. Statistical mechanics describes the microscopic counterpart of thermodynamics. Deals with energy, timescales, and system stability. 



*First Law of Thermodynamics - Energy is Conserved*

Total internal energy of a closed system is constant. 
$$
U = K + P
$$
Doubling the size of the system doubles the Total Internal Energy. Because of this, we say energy is extensive. Combining two systems at the same temperature results in the same temperature. Thus, we say that energy is an intensive property.

Equilibrium:

The change in energy is the change in heat plus the change in work. $dQ$ is heat transfer and $dW$ is energy transfer. Energy only changes. 
$$
dE = dQ + dW
$$
The change in work is a force applied over a distance.
$$
dW = F\times dX
$$
Adiabatic Process - a process for which there is no heat transfer: $dQ = 0$



*Second Law of Thermodynamics - Entropy of a closed system increases or stays the same for any process*

Entropy can be thought of as a function $S(E, X)$ that takes in Energy and X a number of states? that is monotonically increasing with E.



A Reversible Process:

An adiabatic reversible process has 
$$
dS = 0\\dQ = 0
$$
An adiabatic irreversible process has $\Delta S \gt 0$

We define reversibility as something that occurs slowly enough to be exactly retraced.

We will need to prove our simulations are reversible in the future.

Reversible processes occur within the 'manifold of equilibrium states'. If you do something reversibly, every point in the process can be thought of as being at equilibrium. 

More on Equilibrium:

For an equilibrium system, we need to be able to track its volume, chemical potential , and number of molecules, temperature, and pressure.

Equilibrium is independent of its time and history. Monte Carlo simulation will exploit time independence to simulate equilibrium behavior. 

Molecular systems in the cell are never truly at equilibrium but at very small timescales, can be assumed to be at equilibrium. 



Entropy:

Measure of microscopic degeneracy of a macroscopic state. For a macromolecule, this is the number of configurations. 

At constant E:

This equation only applies if every state has exactly the same entropy
$$
S = K_{\beta}ln(\Omega)
$$
Where $\Omega$ is the number of microstates

At constant T:

This equation applies if the states have different energies. 
$$
S = K_\beta \sum_i^N P_i ln(P_i)
$$
where $P_i = \frac{1}{\Omega}$ 



Protein Entropy:

A longer protein will have more entropy because its residues can have more configurations

A lattice model can show the different states of the entropy. Rotations and translations do not add to the entropy of the molecule. 

![image-20210202144455289](C:\Users\benfy\OneDrive - Johns Hopkins\Documents\Markdown Notes\.images\image-20210202144455289.png)

Here we can say that 
$$
E = \sum ^{\#bonds} E_{bond}
$$
By adding just one extra residue, we add many more states.

![image-20210202144628915](C:\Users\benfy\OneDrive - Johns Hopkins\Documents\Markdown Notes\.images\image-20210202144628915.png)

#### Week 2 - Thursday

Boltzmann Ensembles, Free Energy, 

###### Ensembles

**Microcanonical Ensemble**

An ensemble is an assembly of all the microstates consistent with the constraints describing macroscopic states.

The **N, V, E** (microcanonical) ensemble has constant number of particles N, volume V, and energy E within each microstate.

The ensemble average energy is written $\langle E \rangle = \sum _{i }^{no.\ states} E_i p_i$ 

In the NVE ensemble since the energy is the same between all microstates, the energy in the sum is the same for all of them and average is just that energy.

The microcanonical has constant PE and KE via $E = PE + KE$

$dE = 0, dS = 0$ at equilibrium from second law.

$dE = TdS - pdV + \mu dN$ 

> recall from BPC that this takes the form of an exact differential such as that of $f(x,y,z)$
>
> $df = \frac{df}{dx}dx + \frac{df}{dy}dy + \frac{df}{dz}dz$

$T = \frac{dE}{dS}_{V,N}$

> From the second law of thermodynamics, therefore $T \ge 0$

$P = -\frac{dE}{dV}_{S,N}$

$\mu = \frac{dE}{dN}_{V,S}$

The microcanonical ensemble is closed and isolated. 

The probability of each state is $p_i = \frac{1}{\Omega}$ and since each state is the same energy, each probability is the same. 

At equilibrium, the energy is minimized.



**Canonical Ensemble**

The **N, V, T** (canonical) ensemble has different state probabilities. 

At equilibrium, the free energy is minimized (this is true of any ensemble where energy can fluctuate)

Legendre Transform gives us that $A = E - ST$ and  $dA = dE - SdT - TdS$

Plugging the $dE$ from above in:
$$
dA = -SdT - pdV + \mu dN
$$
If E decreases, does A always decrease? Well, as E goes down S must do down but since S is negative in the above equation, A would go up as the negative contribution decreases in magnitude. Thus, a lowering of the internal energy does not necessarily lower the Helmholtz Free Energy.



**Gibbs Ensemble**

This is the most studied ensemble. **N,P,T** ensemble has fixed number of particles, pressure, and temperature. 

Another Legendre Transform gives:
$$
G = E - ST - pV = H - ST
$$
H (Enthalpy) is the stabilizing contribution in the system while S (entropy) is the destabilizing contribution.



**Canonical/Boltzmann Distribution**

This is a subset of the microcanonical distribution. The other ensembles can be thought of as the same.

 A subsystem of the microcanonical ensemble does not have to have the same energy, it just has to average to the same temperature as the rest of the microcanonical ensemble. View the other distributions as small fluctuations in the bath of a microcanonical ensemble. 

$E_{total} = E_{system} + E_{bath}$ and is constant. 

We assert that the probability of the Boltzmann distribution is:
$$
p_{microstate} \propto e^{\frac{-E}{K_BT}} = e^{-E\beta}
$$

$$
P_j = \frac{e^{-\beta E_j}}{\sum_i^{no.\ states} e^{-\beta E_i}}
$$

The partition function $Q$ is the factor that relates the probability of a microstate to the energy of the states.
$$
Q = \sum_i^{no.\ states} e^{-\beta E_i} = \sum_i^{no.\ energy\ levels}  \Omega(E_i) e^{-\beta E_i}
$$
The professor is using $\nu$ instead of $j$ 

$\Omega (E_i)$ is the multiplicity of energy state $i$

 

**Plot of Energy vs Probability**

![image-20210204141535652](C:\Users\benfy\OneDrive - Johns Hopkins\Documents\Markdown Notes\.images\image-20210204141535652.png)

Lower energy correlates with lower entropy. Extraordinarily low energies are unlikely. Thus, the probability falls after certain low energies. 

$K_b$ is a constant, but as $T$ (temperature) increases, the probability curve shifts up and probabilities of each energy level increase. The system can easily transition between states. Lower temperature, shifts the curve down. 

This shows up on our exam:

The partition function is related to whatever energy is being minimized. 

**NVT:** minimizes $A$. Therefore, $A = -K_b T ln(Q)$. 

**NPT:** minimizes G. Therefore, $G = -K_bTln(\Theta)$

> $$
> \Theta = {\sum_i^{all\ states} e^{-\beta(E_i-pV_i)}}
> $$

$S = -K_b p_i ln(p_i)$



###### Open/Closed State System Example

Suppose a system has two states, an open and closed state. The energy of the system closed is $\epsilon_{closed}$ and open is $\epsilon_{open}$ 

There is exactly 1 closed state and 1 open state
$$
Q = e ^{-\epsilon_{open}/K_bT} + e ^{-\epsilon_{closed}/K_bT}
$$
The probability of the open state is just the open contribution to Q over Q and likewise for the closed probability.

Rearrangement gives that 
$$
P_{open} = \frac{1}{1 + e^{\epsilon_{closed} - \epsilon_{open}/KT}}
$$
This is a sigmoid function that appears as below:

![image-20210204143747135](C:\Users\benfy\OneDrive - Johns Hopkins\Documents\Markdown Notes\.images\image-20210204143747135.png)

When $\Delta E = \epsilon_{closed} - \epsilon_{open}$ (it is more probable that you find yourself in the opened state). The change in $\Delta E$ as a result of a stimulus is a function of the channel being observed. Ex: a large change is caused from a voltage potential 



###### Ideal Gas Example

We want to be able to describe every possible microstate that the particles could occupy.

The classical ideal gas: has molecules that have absolutely no interactions between the molecules. The only thing we have to keep track of is the momentum of the particle. The particle has perfectly elastic collisions with the wall.

V = L^3^ where L is the length of the cube the particles are in

 $E = PE + KE$ 

$PE = V(r^N)$

$KE = KE(p^N) = \frac{1}{2} p_i^2 / m$

Where $p$ is a vector describing the momentum of the particle. The momenta of the paricle in every direction x, y, and z are completely independent of one another. 

$\vec{p} = [p_x, p_y, p_z]$ and $p =  v\times m$ measured in $kg*m /s$

$p_i^2 = p_x^2 + p_y^2 + p_z^2$ This finds the square of the magnitude of the momentum
$$
Q = \sum_j ^ {no.states} e^{-\sum\frac{p_i^2}{2m_i}} = V^N (\sqrt{2\pi m k_b T})^{3N} / N! h^{3N}
$$
That equation for Q might be wrong according to prof.. she didn't have her notes. . .



#### Week 3 - Tuesday

*02/09/2021*



We can use the Monte-Carlo simulation to approximate the value of an integral for this partition function. 
$$
p(\{r^N\}, \{p^N\}) = e^{-[PE + KE]/k_b T} / Q
$$


##### Harmonic Oscillator

Harmonic oscillators show up a lot in molecular modeling. Very good for representing bond vibrations. The oscillator can approximate the behavior of two particles approaching eachother. However, it breaks down when the bond between the particles would break. 

Recall Taylor Expansions: $f(x) = f(x_0) + (x-x_0)f' + \frac{(x - x_0)^2}{2}f''$

At the minimum, the second term drops out as derivative at minimum is zero. 
$$
Q = \int dx_1 \int dx_2 = \int dx_2 \int dx_{1,2} \ e^{-\frac{1}{k_b T} (x_{12} - x_0)^2 /2}
$$

$$
\langle V\rangle = \int dx_{12} V(x_{12}) P(x_{12}) \int dp P(x_{12}) = (\int dx_{12} V(x_{12}) e^{-V(x_{12})/k_b T} ) / Q
$$

Q is hard to find, but, we can use Monte Carlo Simulation to eliminate it from our calculations. 



##### Height Example

If we want to calculate the average height of the population, we could sum over all student heights then divide by total number of students. 

Alternatively, we could take each student and turn the heights into a probability distribution with a histogram which would be approximately normal. The average height would then be
$$
\langle h \rangle = \int_0^\infin dh \ hP(h)
$$

##### Sampling Random Numbers

For any kind of stochastic modeling (probability distribution sampling rather than marching through time which would be deterministic) we need to sample from some kind of appropriate distribution.

Computers normally sample from a pseudorandom uniform numbers or URNs. The algorithm generates random numbers from a random seed. The pseudorandomness is helpful in debugging because we can set the seed and always get the same sequence of random numbers. The maximum number of random numbers that a computer can sample from is 2^64^ (64 bit computer) the maximum number of integers

A probability distribution must integrate to 1 and be everywhere greater than or equal to 0. 

Any random distribution can be calculated from manipulations of the URN. 

Cumulative Distribution Function (CDF): The CDF goes from 0 to 1 which is the integral $\int _0 ^x p(x') dx'$. By using the URN, randomly generated number set equal to a y value of the CDF and working backwards, can calculate the x value that would generate that value. 

When you have a discrete distribution, we want to be able to transform to a cumulative distribution. So once we have a cumulative distribution, we can map randomly generated values to their corresponding values on the CDF. This will be used in the homework to sample uniformly from the amino acids. 



##### What is Monte Carlo Simulation

A broad class of computer algorithms that rely on repeated random sampling. A numerical method of integration (you could do it with dice). Relies on repeated random sampling to get a numerical solution to a problem. Dates back to the 1940s.

Three general classes of problems it is used to solve:

* Numerical Integration
  * An alternative to Riemann sum. When you have a multidimensional problem, it's much more efficient to do a stochastic sampling rather than a one-dimensional problem. 
* Optimization
  * A way to find the global minimum of cost function
* Sampling From A Probability Distribution
  * We will do this on homework. 

What is the version that we will use in our code?

###### Markov Chain Monte Carlo (MCMC)

This is a specific version of Monte Carlo where we sample from our probability distribution by doing a random walk through the space. 

We do a random walk in the variable space and observe the resulting probability. A random walk is just hopping forwards or backwards in whatever space. A way to sample points. 

Random Walk: Next position is defined by current position  $X + \Delta X$. You don't have to recall every position you have been, you just have to know where you are at the moment. 

The walk is biased by the probability itself so larger changes in probability lead to larger steps in the direction of greater probability density. 

You jsut need to sample from something proportional to a probability distribution not even a probability distribution, because you are only looking at a $\Delta f(x)$

Metropolis-Hastings Algorithm: 

Two properties the algorithm must obey. Generates a collection of states (microstates). For our purposes, sample N states from gas molecules.

1. Need a stationary distribution. 
   * For example an equilibrium NVT distribution. A sufficient condition is **detailed balance**. If you can show that your algorithm is detailed balanced, you have shown that you are sampling from a stationary distribution: Transition between states has to be reversible. 
2. Distribution has to be unique
   * Guaranteed by Ergodicity: In an ergodic system, all states can be reached from any other state.



#### Week 3 - Thursday

##### Monte Carlo

Frenkel and Smit Chapter 3 Covers in Detail. 

1. Pick an initial state $x$ (we are given this state in the homework)
2. Generate a move from a distribution 
   * $g(x \rarr x')$ is the distribution. The move doesn't have to follow any physical laws, the accept/reject rule will correct if the move is impossible. 
3. Accept or reject the move $x \rarr x'$
4. Store new state, either $x'$ if move was accepted or $x$ if move was rejected.
   * Think about this as accepting the current state as the best configuration. We might end up staying in a given state for several steps. 
5. Return to step 2.



Lattice Example

When you have a number of configurations, monte carlo samples them based on their probabilities from their partition function. Some states will be higher or lower energy which will affect their probabilities. 

See OneNote Drawing

Pick a bead and allow the bead to explore its possible moves and select the lowest energy configuration to move to. 

It is important that the probability of a move is the same going forwards and backwards. This is the concept of Detailed Balanced.



Acceptance Probabilities

How do they relate to the stationary distribution and to our move generation probability. 

**Detailed Balance**

A key component of Monte Carlo sampling and will absolutely appear on the exam.

The probability of being in state x and traveling to state x' has to be equivalent to the probability of being in state x' and transitioning from state x' to state x.

By state, we could mean transitioning from one lattice position to another. 
$$
p(x)\Pi(x \rarr x') = p(x')\Pi(x' \rarr x)
$$
Where $p(x)$ is probability of being in state x and $\Pi(x\rarr x')$ is transition probability.
$$
\Pi(x\rarr x') = g(x \rarr x') \ acc(x\rarr x')
$$
This says that the 
$$
\frac{acc(x \rarr x')}{acc(x' \rarr x)} = \frac{p(x')g(x' \rarr x)}{p(x)g(x \rarr x')}
$$
We know that the actual probability of any state is given by:
$$
p(x) = \frac{f(x)}{Q}
$$
However, looking at the acceptance ration, the ratio of $p(x) / p(x')$ is the division of $Q$. This means we can do the calculation without actually knowing the partition function. 



If the Right Hand Side of the equation is > 1, then accept $x \rarr x'$ 

else $acc(x \rarr x') = RHS$



Acceptance probability is either greater than 1 or the acceptance probability is less than one. When it is less than one, we accept the move. 


$$
acc(x\rarr x') = min[1, \frac{p(x')g(x' \rarr x)}{p(x) g(x \rarr x')}]
$$


>Ex: $p(x) = e^{-E(x)/k_b T} / Q$
>
>Assert that $g(x \rarr x') = g(x' \rarr x)$
>
>$acc(x \rarr x')  = min[1, exp(-\Delta E/k_b T)]$
>
>Where $\Delta E = E(x') - E(x)$ which can be read $E_{new} - E_{old}$
>
>If $\Delta E = 0$ always accept.
>
>If $\Delta E < 0$, energy has gone down, $E_{new} < E_{old}$ this is favorable so always accept.
>
>If $\Delta E > 0$, energy has gone up, $E_{old} < E_{new}$, this is unlikely but we will accept this transition if $e^{-\Delta E / k_b T} > URN$  [a Uniform Random Number]. 
>
>* As the temperature goes up, we can be more forgiving about large energy changes. 

Calculating an Ensemble Average Energy 
$$
\langle E \rangle = \int E p(x) dE = \sum_i^{no. configs} E_i / N_{config}
$$
  When the same energy is encountered, we still need to add them in the sum.

Trial Moves

Select one bead randomly

Select $\Delta X, \Delta Y, \Delta Z$ separately. Probability should be symmetric so the probability should be selected from $[-1, 1]$ uniform distribution. 

$[-\Delta, +\Delta]$ uniform is okay, random number from the normal distribution is also okay. 

Choosing positive and negatives helps ensure that every move is theoretically reversible and the Detailed Balance is maintained.

$p(-\Delta) = p(+\Delta)$



Empirical Observations about Monte Carlo

1. Efficiency is best when acceptance rate is around 20%

   * A very low or very high acceptance rate won't do a very good job of converging to a clear energy minimum. It is better to reject the majority of moves. 
   * Too small of displacements can lead to very high acceptance rates which isn't good either

2. Move Fewer Beads at Once

3. Size of $\Delta$

   * Too small isn't useful neither is too large. 
   * Want a $\Delta E$ on the order of $k_b T$ 
     * This depends on the gradient of the energy change but we can look at the energy function and calculate how the energy changes.

   

##### Lennard Jones Potential

The energy depends on the distance between particles. 

![image-20210211144053461](C:\Users\benfy\OneDrive - Johns Hopkins\Documents\Markdown Notes\.images\image-20210211144053461.png)

##### Symmetric Boundaries

To find the image distances, break the problem into a component-wise comparison. 

$\Delta X_{ij} = x_i - x_j$

$\Delta X_{ij} = \Delta X_{ij} - Boxlength * round(\Delta x_{ij} / boxlength)$

![image-20210211144933873](C:\Users\benfy\OneDrive - Johns Hopkins\Documents\Markdown Notes\.images\image-20210211144933873.png)