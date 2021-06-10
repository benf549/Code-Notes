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



#### Week 4 - Tuesday

Switch from an atomic level to a population. We are now talking about chemical kinetics and rate equations. Instead of thinking about structure and how that impacts interactions, we're going to think about rates of interactions. 

##### How Do We Explain Time Dependence of Interacting Species Populations

We are going to develop rate equations from chemical kinetics. We worry now about time dependence rather than spatial interactions. We need to understand problems that are classically solvable with pen and paper or if you need a computer to do it. We want to have toy models available that we can validate our models with.

Given concentrations of the species at $t_0$ what are they at $t_{later}$. This can be predicted directly in simple cases. 

Michaelis-Menten

$E + S \leftrightharpoons ES \to E + P$ 

Reversible binding followed by chemical reaction. When you have a high substrate concentration, the steady-state approximation gives the rate of reaction. 

##### Classes of Reactions Between Populations

1. Zeroth Order

   * $\empty \stackrel{k_0} \to A$

     * $ \frac {dA} {dt} = k_0 $
       $$
       \int dA = \int k_0 dt \\
       A(t) = k_0 t + c
       $$

     * We then use an initial condition to solve for $c$ 

     * $k_0$ has units of concentration per time.

2. First Order (Unimolecular Reaction)

   * $A \stackrel{k_1}\to B$

     * $\frac {dA(t)} {dt} = -k_1 A(t)$

       * Every time an A is consumed, a B is produced. Only reactants contribute to change in time
       * Here, the unknown is A(t), the parameter is $k_1$ and t is the independent variable. Solve by separation of variables

       $$
       \int \frac{dA(t)}{A(t)} = \int -k_1 dt \\
       ln(A(t)) = -k_1 t + c \\
       A(t) = A_0 e^{-k_1t}
       $$

       * This is is a really good example of exponential decay. The Half-Time is how long it takes for the population to decay to half of starting concentration $A(t_{1/2}) = \frac {A_0} 2$ and solving we get $t_{1/2} = ln(2)/k_1$
         * The half time is entirely dependent on the rate constant. 
       * $k_1$ has units of $\frac 1 {time}$

3. Second Order (Bimolecular Reactions)

   * When two things bind to eachother. 

   * $A + B \stackrel{k_2} \to C$

     * This is a search problem, even though A and B are homogeneously mixed in solution. The concentrations of A and B dictate how quickly they can combine and form C. This is LeChatelier's principle. Changing the concentrations change the speed of reaction. This is not the case for a first order reaction. 

     * $\frac {dA(t)}{dt} = -k_2 A(t)B(t)$

     * $\frac {dB(t)}{dt} = -k_2 A(t)B(t)$

     * $\frac {dC(t)}{dt} = k_2 A(t)B(t)$

       * The unknowns here are the concentrations of A and B. We have one parameter which is the rate constant. This relationship is non-linear. We have a product of unknowns.
         * We can write A as a function of B which gives a quadratic equation. Why is the rate of change of A dependent on the product of A and B? 
       * $k_2$ has units of volume/time or 1/(concentration * time)
         * In 2 Dimensions, $k_2$ would have units of area/time and concentration would be measured in area/time

     * $A + A \to C$

       * $\frac {dA}{dt}= -2k_2 A^2$
         $$
         \int \frac {dA} {A^2} = \int-2k_2 dt \\
         \frac{-1}{A} = -2k_2t+C \\
         A(t) = \frac {A_0} {2k_2 A_0 t + 1}
         $$
         where $C = -1/A_0$

   * The bimolecular process is initially faster, then concentration drops and other orders become faster

     * Half-time: $t_{1/2} = \frac{1}{2k_2A_0}$
       * dependent on the initial concentration AND the rate constant for the reaction. 

4. Higher order reactions we assume do not happen as they are so statistically unlikely. 

5. Reversible Reactions

   * $A + B \underset{k_r}{ \stackrel{k_f}{\leftrightharpoons}} C$
     * $\frac {d[A]}{dt} = -k_f [A] [B] + k_r [AB]$
       * $A_0 + AB_0 = A(t) + AB(t)$
       * $B_0 + AB_0 = B(t) + AB(t)$
     * We want to find the steady state. The steady state is defined when $0 = -k_f [A]_{eq}[B]_{eq} + k_r [AB]_{eq}$
       * Solving gives the relationship $K_{eq} = \frac{[A]_{eq}[B]_{eq}} {[AB]_{eq}} = \frac{k_f}{k_r}$ which is independent of time and only dependent on equilibrium concentrations. 

Rate equations are in chapter 15 in the text. They are ubiquitous in kinetics.       

"Show Up On Exam"

Linear is linear in the unknown variable

Nonlinear is nonlinear in the unknown

> $y = x^3 + x^2 + 1$ is linear in the unknown. If we were solving for the roots of the function as in $0 = x^3 + x^2 + 1$, now X is the unknown and the solution is nonlinear. 
>
> When you have a linear system, it is easy to solve analytically
>
> To determine linear vs linear
>
> * Dependent variable appears non-linearly.
>   * $dx/dt$ and $d^nx/dt^n$ are always linear operators. All derivatives of the n-th order are linear. 
>   * $d^2x/dt^2 = wx = f(t)$ where $f(t) = sin(t)$. The derivative is linear because $f(t)$ is completely independent of x. If x was squared in the second relationship or a log, then it would not be linear.

Nonlinear equations are particularly interesting even though they aren't always solvable.

A differential equation that is nonlinear is sensitive to its initial conditions. When we do MD, our force is highly nonlinear. Different simulations will diverge over different initial conditions. 

Nonlinear equations have "multi-stability" or "bifurcation". Even with a fixed set of initial conditions, different parameters can give wildly different stable states. This never happens with linear equations. 



#### Week 4 - Thursday

Numerical Methods for Rate Equations

These will be a focus of homework 3. When you can't solve the equations analytically, we can use numerical methods on computers to describe the system.

there are two main ways:

1. Deterministic - standard numerical methods for ordinary differential equations. You have one initial condition which results in one future.
2. Stochastically - dependent on random variables. Use a master equation formalism. Predict a probability distribution of future concentrations and take the average of the distribution. Stochastic requires that the particles are integer values and thus, there is a possibility for the solution from these processes to diverge from the deterministic functions. To avoid the problems, we use large samples as errors really only arise on small sample sizes. 



##### Stochastic Methods

ODEs can be first order, such that you have a single first derivative: $\frac {dy(t)} {dt} = f(y(t), t)$

Second order ODEs are functions of second derivatives $\frac {d^2y}{dt^2} = f(\frac{dy(t)}{dt}, y(t), t)$. 

Any higher order equation can be solved as a system of first order equations. 

For rate equations, these are initial value problems. Sometimes for bounded systems, there are also spatial concerns. 

Now we will look at first order problems:

Almost all of these solutions will be based on the Taylor expansion. 
$$
\frac {dy(t)}{dt} = f(y(t), t)
$$
How do we choose these solutions? There are two considerations we want to make: Truncation error from not expanding the Taylor series out far enough and Stability (stiffness) which describes how rapidly the function changes. When the function changes very quickly, it is harder to approximate with small steps like in a Taylor series expansion. 

As $h$ the size of the step in time goes down, the error in the approximation goes down. For any Numerical Method, we have a tradeoff between the speed of the algorithm and the time complexity.

The simplest approximation is based on a first order Taylor expansion which we call Euler's method:

A second order Taylor expansion for a generic function. 
$$
f(t + \Delta t)  = f(t) + \frac {df(t)}{dt}(\Delta t) + \frac {\Delta t^2}{2!}\frac {d^2f}{dt^2}
$$
Euler's method truncates the function at the first derivative parameter. For this to work, we must have $\Delta t < 1 $ for the higher order terms to be insignificant:
$$
f(t + \Delta t)  = f(t) + \frac {df(t)}{dt}(\Delta t)
$$
We are approximating the value of a function a time step away from our current position. 

> we know that the first order rate is desribed by $\frac {df}{dt} = -kf$ which is solved with exponential decay. Knowing this, we can check our numerical method's accuracy.

The error from Euler's method is described by $O(\Delta t^2)$. Euler's method is the worst possible method.

We can improve the approximation by employing a centered approximation as was described in the textbook reading for last class. MATLAB uses the Runge-Kutta method which truncates at higher order $\Delta t$ 's

See handwritten notes to for difference between implicit and explicit methods. 



##### Stochastic Simulation

Also known as the Gillespie Algorithm which is described in the textbook in chapter 19, but the original paper is actually pretty good and readable. 

Gillespie is an exact algorithm. The other methods we talked about had error that went with the $h$ or size of the time step. 

This is an exact method that solves coupled chemical reactions and it can handle, 0th, 1st, and 2nd order reactions. 

It is very specific to solving the problem of chemical reactions. It even works with 3rd order reactions despite them being unlikely to occur. 

The algorithm captures fluctuations in the particle number. It is event driven so there is no fixed $\Delta t$. Because there is no discretization of time, there is no error associated with this. Solves for integer copy numbers. 

Assume species are well mixed in volume: $V$, the number of initial species is $N$ there are $m$ reaction channels that allow these species to interconvert and interact such as the forward and reverse reactions and any side reactions. 

The well mixed requirement breaks down at phase boundaries

Suppose we have $x_1, x_2, x_3 \underset{t}\to x_1(t), x_2(t)$

we define the Master Equation:
$$
\frac {dP}{dt}(x_1, x_2, x_3, t) =  \sum_{\nu = 1}^m = P(\vec x-\nu,t)a(\vec x-\nu) - P(\vec x, t)a(\vec x)
$$
the rate of change of being in the state is the rate of being in the state or the rate of leaving the state. Probability is jumping into state minus jumping out.

For a simple model:

Suppose we have two reactions: $x_3 \to x_3 + x_1$ (at $k_1$)and $x_1 \to x_2$ (at $k_2$)

the transition probabilities are: $a_1 = x_3 k_1$ and $a_2 = x_1 k_2$

prediction: $1 - (a_1 + a_2)$

for this scheme, we have to keep track of the copy numbers for x_1 and x_2.
$$
P(x_1, x_2, t+dt) = P(x_1, x_2, t) \times (1 - (a_1 + a_2)) + \Delta ta_2 P(x_1+1, x_2-1, t) + \Delta t a_1 P(?)
$$
**I didn't catch that whole thing. **


$$
P(\tau, \mu)d\tau
$$
where tau is the time interval and $\mu$ is the reaction types. mu is on the interval 0 to m and tau is on zero to infinity.

Average transition probability for a 0th order reaction is $C_\mu = v*k_\mu$

where C is the probability. 

For a first order reaction: $C_\mu = k_\mu$

second order reactions are $C_\mu = \frac {k_\mu}{v}$

We then need the reaction propensity which depends on copy numbers.

For a 0th order reaction $h_\mu =1$ 1st order is $h_\mu = x_1$ and 2nd order is $h_\mu = x_1x_2$
$$
a_\mu dt = h_\mu C\mu dt
$$

$$
P(\tau, \mu) = P_0 (\tau) P(\mu, \Delta \tau) = P_0(\tau)a_\mu d\tau = P_0(\tau) = e^{-\sum_\mu ^m a_\mu \tau}
$$

 This was an obviously complicated derivation but implementing the algorithm itself is not that bad. 
$$
P(\tau, \mu) = P_1(\tau)P_2(\mu) \\
P_1(\tau) = a_0e^{-a_0\tau} \\
P_2(\mu) = \frac {a_\mu}{a_0} \\
a_0 = \sum_{\mu=1}^m a_\mu \\
\tau = \frac 1 {a_0}ln(\frac 1 {URN})
$$
To sample we have 
$$
\sum_{\nu = 1} ^{\mu -1} a_{\mu} / a_0		\lt URN2
$$
The pseudocode:

```pseudocode
1. Initialize species concentrations x1, x2 @ t=0
2. Calculate C_\mu for all reactions (happens once at beginning)
3. Calculate h_\mu for all reactions which changes on every iteration. h is the propensity of the reaction that changes based on the number of species in solution.
4. Calculate a_0 = sum(all reactions) = sum(c_\mu * h_\mu)
5. Sample \tau from 1/a_0 ln(URN1)
6. Sample \mu with \mu(URN2)
7. Update species involved in reaction \mu. If x_1 goes to x_2, then you lose one x_1 and gain one x_2.
Repeat from 3 over all cycles. 
```

the sum over all the $\mu$s is essentially a CDF we are sampling from like in the first homework. 

