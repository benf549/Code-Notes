# Reading Notes - Modeling The Living Cell

## Physical Biology of The Cell - Chapter 2 - Physical Scales

###### Intro

Cells are incredibly diverse. We use E. coli as the standard ruler for biological models. Once we know about E. coli, we can begin making estimates about the composition of all cells.

###### 2.1 - E. coli

Nothing smaller than a cell is believed to be alive. Cells take in external energy from the environment to create new cells.  The cell is the simplest unit of replication.

E. coli serves as a good standard to get an idea for the basic needs of a cell and is used for historical reasons. 



*E. coli as a standard ruler*

Like all other cells, E. coli have a DNA based genome, transcription, and translation mechanisms with ribosomes that create proteins for gene expression.

We use the unit the micron to denote 1$\mu m$ 

Cells can have different appearances when grown in rich mediums as opposed to poorer ones. To account for this, the reference growth condition throughout the book is the 'minimal medium' used by microbiologists. This is opposed to the 'rich media' one might grow cells within in the lab

**The size of E. coli**

The **surface area** of an E. coli cell: 
$$
A_{E. coli} = 6\mu m^2
$$
The **volume** of an E. coli cell is about 1 femtoliter:
$$
V_{E. coli} \approx 1\mu m^3
$$


*A Molecular Census* - Approximating the number of different types of molecules in an E. coli cell. 

The cellular interior is highly crowded. The average spacing between protein molecules in the cell is less than 10nm.

###### Example: E. coli Calculations

From above, volume of the cells is about 1 femtoliter, assuming the density of the cell is around that of water (1 g/mL) the mass of the cell is then around 1 picogram.

A cell is approximately 30% dry mass and 70% water. Half of the 30% is protein. As a result, the total protein mass of the cell is 0.15 picogram.

The number of carbon atoms can be guessed by assuming that half the dry mass of the cell is carbon. This gives approximately 10^10^ carbon atoms per cell.

An average protein has 300 amino acids with each amino acid being about 100 Daltons (g/mol). Thus the mean protein has a mass of 30,000 Da. 

Dividing Da by Avogadro's number gives the mass of the protein in grams. Thus, the typical protein has a mass of 5 x 10^-24^ grams. Thus the total number of proteins per cell is the total mass of proteins in the cell divided by the mass of a single protein. Total number is 3 x 10^6^ 

Approximately 1/3 of proteins are implicated in the membrane. Making this approximation, 2 x 10^6^ proteins are cytoplasmic with the remainder 10^6^ membrane proteins. 

We can estimate the number of ribosomes in a cell as being about 20% of all protein mass.  The mass of an individual ribosome is roughly 2.5MDa and a ribosome complex is approximately 1/3 protein and 2/3 RNA by mass. 

Multiplying the total mass of protein by .20 times the fraction of the ribosome that is protein lets us calculate the total number of ribosomes to be 20,000.

A ribosome is approximately 20 nm in diameter and the total volume taken up by them approximated as a sphere is roughly 10^8^ nm^3^ or around 10% of the cell volume. 

Using the surface area given above, we can estimate the number of lipids in the double bilayer of the E. Coli cell as 
$$
N_{lipid} \approx \frac{4 * 0.5 *A_{e. coli}}{A_{lipid}} \approx 2\times 10^7
$$
where the 4 is for the fact that there are 4 surface areas of lipid for each face of the two bilayers and 0.5 for the fact that half of the area is taken up by other things such as membrane proteins. The area of the lipid is estimated as 0.5nm^2^

To estimate the number of water molecules in the cell, we know 70% of the cell volume is water and thus the total water mass is 0.7 pg. We can then find the total number of water molecules in side the cell as about $2 \times 10 ^{23}$ 

To estimate the number of positively charged ions is 100 mM and thus, the estimated number of ions in the cell is about $6 \times 10^7$. An interesting observation from this calculation is that one molecule per E. coli cell is approximately 2nM. 

###### Cell-To-Cell Variability

When cells divide, how much variation is there between the two resulting daughter cells in their quantities of RNA and Protein.

We can view the probability of a molecule going into either cell as a Bernoulli random variable. The combination of all the molecules is then a binomial distribution with probability $p$ where $p$ is the probability of a given molecule going into daughter cell 2. When N is very large, the distribution approximates a Gaussian and when $p$ is much less than 1, a Poisson.

We assume each molecule has a 50% probability of going into either daughter cell. We can use the standard deviation of the binomial distribution to express a good range of values for which the amount of the molecule in either daughter cell would be expect to be.

The standard deviation over the mean (a measure of spread) is equal to 1 over the square root of N. Thus when N is small, the spread is large while when N is large, the spread is small.

###### Cells

Yeast is often used as a model for the eukaryotic cell while E. coli is a better model prokaryote.



## PBOC - Chapter 3 - Time Scales

We can use the cell cycle of E. Coli as a standard stopwatch to compare other measurements to. 

Biological processes can be on the scale of one nanosecond to 10^9^ years. 

The E. Coli doubling time is around 20 minutes or $1.2 \times 10^3 $ seconds. 

Biological processes behave differently. Procedural time is the amount of time it takes for a given procedure to occur. Relative time is the time a process takes from start to finish if it has to wait for another procedure to finish before it can start. Manipulated time is when cells and organisms speed up or slow down key processes like replication and metabolism. 

The cell cycle is the cycle by which one cell divides and becomes two cells. 

Macromolecule synthesis occurs on the scale of 10s of seconds. Enzyme turnover rates are on the scale of 0.5 cycles per second to 600,000 cycles per second. 

#### E. Coli as a Standard Clock

Define cell cycle length as time from birth of a cell from division from parent to that of its offspring. E. coli doubles in length when dividing and maintains a constant cross-sectional area. It is important to use the minimal medium for replication or else the time scale varies dramatically for cell processes. 

The book gives a few examples of models for the growth rate of E. Coli and its use of energy and water. 

#### Procedural Time

Complex processes are built up from many small steps, each of which takes a finite amount of time. Many biological processes are intrinsically repetitive like the replication of DNA or synthesis of proteins. 

##### The Machinery of the Central Dogma

In bacteria, there are about 2 DNA polymerases that read roughly 5Mbps of the genome each starting form the ORI and reading in opposite directions. 

DNA replication occurs at around 2000 bp/s of DNA per replication complex. 

Transcription occurs at approximately 40 nucleotides/s and a typical transcript takes around 25 seconds to produce. 

Protein Synthesis occurs at around $3 \times 10^5 $ amino acids / second for the whole cell and the rate per ribosome is around 15 amino acids/second. Thus the mean time for a single protein synthesis (average around 300 residues) is about 20 seconds.

##### Clocks and Oscillators

Animals and cells have cyclic behaviors that keep them functioning such as the beating of a heart or molecular clocks that regulate circadian rhythm. 

Cyclin is a protein that accumulates and activates a kinase that can phosphorylate a protein that destroys cyclin. This cyclic behavior helps cells keep time and there are a number of similar molecules that all do this at the same time and across many different cells. 

A diurnal clock is independent of temperature change. These clocks help organisms to do the same task at a specific time everyday. External cues like sunlight are not needed to keep time, but when they are available, they can be used to reset the internal clock though not efficiently as we know from jetlag. 



#### Relative Time

Processes are linked in logical sequence. Relative time accounts for the mechanisms that ensure that related processes can be performed in series like putting your socks on before your shoes (event A must be completed before event B can begin).

##### Checkpoints and The Cell Cycle

The eukaryotic cell cycle has checkpoints that ensure that the cycle cannot proceed if certain processes have not been completed. 

The progress of the cell cycle can be monitored by measuring gene expression patterns. To do this, study the networks of interconnected genes that have their expression coupled. 

We can use GFP as a reporter protein by fusing it to proteins implicated in the process of interest. 

Development is another example of a process that is heavily regulated and sequential. 

Signaling cascades help create relative time processes. 

#### Manipulated Time

Enzymes help bring the timescale on which certain chemical processes occur down from millions of years to fractions of a second. They do this by reducing the energy barrier between reactants and products' transition state. 
$$
v \propto e^{-G_{barrier}/k_b T}
$$
In other words, the reaction rate is proportional to the energy barrier separating the states. v is the transition rate in cycles per second, G barrier is the size of the energy barrier between states and $k_b T$ is the thermal energy scale. This is the numerator of a partition function probability scheme

To beat the diffusion speed limit, cell store molecules in compartments and perform reactions in them to increase the rate of substrate collision. 

Diffusion is the random motion of microscopic particles in solution. Sometimes, this is called Brownian motion. The effects of Brownian motion are important for things on the scale of about a micron or smaller. Deterministic forces on these scales have the same contribution to a particle's behavior as  thermal energy does. 

The thermal energy scale is on the order of $k_b T$ where $k_b = 1.38 \times 10^{-23} J/K$ and with $T \approx 300K$ $k_b T$ is approximately $4.1 pN nm$

Diffusion times depend on the length scale. 
$$
t_{diffusion} = \chi ^2 /D
$$
Where $D$ is the diffusion constant and $\chi$ is the distance travelled. The time scale for a diffusing particle to travel a distance $\chi$ scales as the square of that distance. 
$$
D \approx k_b T / 6\pi \eta R
$$
where $\eta$ is the fluid viscosity and R is the radius of the object. We will see this equation later. Using this equation at room temperature, we get that the D for a protein with a 5 nm diameter has a D of approximately 100 $\mu m^2 /s$

Thus, the time for the protein to diffuse across an E. Coli ( $\chi  = 1\mu m$) is  (1^2^ / 100) s or approximately 0.01 second. To diffuse across a giant squid axon which is on the order of 10 cm long, the same equation gives that it would take 10^8^ seconds which is way too long to be useful for a cell. To get around this, the cell utilizes active transport rather than relying on passive diffusion. 

Bacteria can actually replicate faster than one cell cycle would take if copying the genome began at the beginning of the cell cycle and ended before the end. They do this by beginning the replication process for the daughter cells of their daughter cells. They may have multiple copies of their DNA ready to go in highly favorable growth conditions. 



## PBOC - Chapter 5 - Mechanical and Chemical Equilibrium in the Cell

#### Energy and the Life of Cells

In biological systems, there are at least four kinds of relative energy: chemical energy, mechanical energy, electromagnetic energy, and thermal energy. Living organisms can convert these types of energy into the other types. However, organisms generally cannot use thermal energy to do work because thermodynamics prevents it from being useful. 

We make the assumption for all most all of our models that our system is operating at or near equilibrium such that any small excursion of the system will likely result in it returning to its original state. This assumption isn't too bad because different processes occur at different time scales, so if we can isolate some part of a process at a very short time scale, the environment won't have changed much one small time step into the future from where the current state is. Thus, we can approximate the state as being at equilibrium. 

To model the cell, we will use relationships derived from classical and statistical thermodynamics. 

###### Deterministic and Thermal Forces

Within cells, deterministic and thermal forces are on equal footing with regard to particles bumbling around inside. All molecules inside the cell are jiggling in a non-insignificant way. When we considering the transformations a biological system can undergo, we can picture the range of possibilities as an energy landscape. The landscape can be altered by inputs of energy that cause different energy minima to be favored. Ex: a voltage applied to a voltage gated ion channel membrane causes the channels to open rather than close. 

Brownian motion is highly influential to the behavior of particles around $1 \mu m$ in size. This behavior results from the fact that molecules in these environments are constantly bumping into eachother and other molecules all of which jiggle with thermal energy.

The ratio $E_{det}/k_b T$  allows us to measure the contribution of thermal effects to the overall energy of a system. $E_{det}$ represents the scale of deterministic energies in the problem of interest. $k_b T$ sets the natural energy unit for a single molecule inside a cell. 
$$
k_b T = 4.1 \ pN \ nm = 0.6kcal/mol = 2.5kJ/mol = 25meV
$$
 ![image-20210212010826639](C:\Users\benfy\OneDrive - Johns Hopkins\Documents\Markdown Notes\.images\image-20210212010826639.png)

The figure above shows the relative importance of different types of energy at different length scales. 

The most important takeaway from this, is that on the nanometer scale, the thermal energy scale becomes quite close to the energies of other deterministic forces. 

The energy within an E. Coli cell is mainly stored in the form of energy currency molecules like ATP, NADH, and NADPH. The high energy phosphate being cleaved from an ATP liberates around $20 k_b T$. Easily transferrable electrons on NADH and NADPH are alternative energy sources. A H^+^ gradient is maintained in cells using energy and processes in the cell can be coupled to the destruction of the gradient as a third source of cellular energy. 

> The author estimates that making all of the proteins in an E. Coli cell from glucose costs somewhere on the order of $4.54 \times 10^9$ ATP worth of energy.
>
> Table 5.2 summarizes the costs of every major macromolecule class.



#### Biological Systems as Energy Minimizers

The equilibrium state for a biological system lies that the minimum energy for some function. 

Living systems are by definition out of equilibrium so we have to make the approximation of the system being at equilibrium over small time scales as previously discussed. We view the cell as at mechanical equilibrium as the force of its cytoskeleton pushing out on its membrane is nearly instantaneous and thus acts over a very small timescale. Similarly, for chemical equilibrium, we can make the steady state approximation for reaction equilibria. 

Similar to what we introduced for biological systems as a whole, proteins are energy minimizers themselves. Their folded state exists at the absolute minimum of free energy. 

We can think of entire parts of cells such as their membranes as being at equilibrium at any moment. When modeling free-energy minimization problems, we first need to select a class of 'competitors' and then determine the free energy associated with each competitor. For the shape of a red blood cell, we just have to ensure that the total area enclosed by the shape and the total surface area are the same between shapes, then we can determine the energy associated with maintaining each shape. 

##### Mechanical Equilibrium from a Minimization Perspective

Can be thought of in terms of Newton's Laws. From Newton, we know that translational equilibrium $\sum _i \vec F_i = 0$ or in other words, the sum of all forces acting on the object is zero.  The forces are vectors. PBOC uses **bold** to indicate that a variable is a vector. 

The vector formalism is useful but sometimes it is better to view our equilibrium system as the minimum of some potential energy function. For the example of the spring, we could write the system as two balanced forces, the force of the spring pulling on a weight and the force of a weight pulling on a spring. This same system could be represented as the combination of potential energies: $U(x) = \frac{1}{2} k(x - x_0)^2 - mg(x - x_0)$ where the first term represents the potential energy stored in the spring and the second term represents the gravitational potential energy of the hanging weight (see figure 5.11 in the text)

We see that when $x_0 = x$, the potential energy of the system is zero. We can find this system's energy minimum by setting its derivative equal to zero and solving for x. 
$$
x_{eq} = x_0 + \frac{mg}{k}
$$
This result makes sense as a heavier object results in a larger displacement from $x_0$ while a larger spring constant means a stiffer spring which makes the displacement from $x_0$ smaller. 

The spring-tension system comes up a lot in biological systems modeling. 

The minimization of potential energy comes up a lot because one we can characterize a potential system or group of competitors, the competitor with the lowest potential (or free) energy is the most probable one that exists biologically.

#### Math Review

When this book uses `[]` after a function name, they mean this to call attention to the fact that the function is taking in another function rather than a series of parameters. This form of a function is called a **functional** which takes in a function which itself takes in parameters. 

In the example E[u(x)] represents an energy function that is itself a function of a displacement function. Every different configuration of displacements for the system could produce a different energy function. We would then pick the one that minimizes the energy function as the most physically likely.

The energy function can be thought of a sort of cost function where the cost is the energy of a given configuration. A cost function that takes in a function itself is a functional as we saw above.

Finding the maxima and minima of a function simply requires taking the derivative of the function and setting it equal to zero. To identify a maximum, the second derivative of the original function will be less than zero, and a minimum will have a second derivative greater than zero. 

Most of our functions however, will be multivariate so we will want to take partial derivative with respect to our variables of interest. When we have multiple variables to take derivatives of and set to zero, we are left with a system of equations and we want to set each equal to zero. The determinant of the matrix of coefficients (if the equations are linear) will tell whether there is a solution to the system of equations such that each equation is equal to zero for the same input variables that the derivatives were taken with respect to. 

#### Configurational Energy

Potential energy is the language of Mechanical Problems. The minimizer of potential energy for a mechanical equilibrium 

Energy equations that take the form of quadratic functions dependent on displacement from equilibrium are particularly important to physics. We can create these types of energy functions using Taylor Series approximations for a function. This way, we don't need to understand the entire energy landscape, we just need to understand the landscape around equilibrium and then we can make approximations for small displacements from equilibrium. 

![image-20210212154241850](C:\Users\benfy\OneDrive - Johns Hopkins\Documents\Markdown Notes\.images\image-20210212154241850.png)

This function actually simplifies as at equilibrium, we know that the first derivative of this energy function will equal zero. So simplifying, our energy equation becomes:
$$
U(x_{eq} + \Delta x ) \approx U(x_{eq}) + \frac{1}{2} \frac{d^2 U}{dx^2}\bigg\rvert_{eq}\Delta x^2
$$

###### Review of Taylor Expansion

The Taylor expansion is simply building up a simple polynomial formula $f(x) = a_0 + a_1x + a_2 x^2 ...$  

For the purposes of the book, we can get away with using only a second degree polynomial, so we only have to figure out the three $a$ parameters. To figure out these parameters, we can set the function equal to 0 to solve for the first parameter. The second parameter can be found by taking the first derivative of the function and setting that equal to zero, and so on. Thus, we can approximate our function at zero, with:
$$
f(x) \approx f(0) + f'(0)x + \frac{1}{2}f''(0) x^2
$$
To approximate our function as a quadratic, all we need to know is the value of the function and its first two derivatives at the point we're interested in. 



###### Hooke's Law

Elasticity of a rod is described as $\epsilon = \Delta L / L$. When a rod is strained, the different points in the material have different displacements. The $\Delta L$ is the rod's displacement from its unstretched length $L$. Stretching is physically moving the bonds between atoms. 

We can view a solid material as a bunch of small springs connected in series. The relationship between force and stretch in a spring is given by $F = -k\Delta a$ where k is the spring constant and $\Delta a$ is the extension of the spring. This can be extended macroscopically with $\frac{F}{A} = E \frac{\Delta L}{L}$ Where the L ratio is the elasticity from above, the E is a property of the material (Young Modulus) reflecting the stiffness of the rod, and A is the cross-sectional area of the beam. Stress is quantified as the Force per unit Area. Since we view the springs as being connected in parallel, the springs share the load of the force applied. The number of springs is calculated as $A/a_0^2$ where $a_0^2$ is the area taken up by an individual spring. By rearranging, we find that each spring will be extended by $\Delta a = (F/k) (A/a_0^2)$ since the object as a single spring would be extended by $(F/k)$ we can divide this by the total number of springs. The total extension of the spring can be found as $\Delta L = (L/a_0)\Delta a$ where $(L/a_0)$ is the number of springs in the length of the beam that each stretches by $\Delta a$. We can plug what we found back into the relationship above and solve for the E (young modulus) is equal to $k/a_0$ 

We can also use energy to study Hooke's law. We can find the energy with $E_{strain} = \frac{1}{2} k(\Delta a)^2$ or more generally, use $E_{strain} = \frac{EA}{2} \int_0 ^L (\frac{\Delta L}{L})^2 dx$ where A is the cross-sectional area. This integral is essentially adding up all of the microscopic springs' energies in the beam. This energy equation can be rewritten as a functional that calculates the strain energy as a function of the position along the axis of the beam: $E_{strain} = \frac{EA}{2} \int_0 ^L (\frac{du(x)}{dx})^2 dx$



###### Structures as Minimizers of Free Energy

Qualitatively, we can think of free energy as the difference between energy and the temperature times entropy for the process. The previous statements about energy in general being minimized are true, but only focusing on mechanical energy does not work for systems at small scales which could be dominated by thermal effects. Therefore, we need to use Free Energy.

**Entropy**: A measure of the microscopic degeneracy of a macroscopic state. 

$S = k_b ln(W)$ where $k_b$ is Boltzmann's Constant and W is the number of microstates in the system/macrostate of interest. This is known as Boltzmann's Equation.

When minimizing free energy, we want low internal energy, high temperature, and high entropy which is equivalent to a large number of microstates. 

 Often we can write $W =  $ ${N} \choose m$ where N is the number of possible positions and m is the total number of things to distribute amongst those positions. Entropy is maximized when the number of things to distribute is half the total number of available positions.  

We can use Stirling's Approximation for the factorial to simplify the calculation of the factorial which is written in its simplest form as 
$$
ln(N!) \approx N ln(N) -N
$$
The Hydrophobic effect is driven by entropy as the presence of a hydrophobic molecule in solution deprives water molecules of some of their configurational entropy. Water molecules have six orientations possible for hydrogen bonding when a nonpolar molecule is substituted for one of these partners, the water molecule has to adopt one of only three configurations that still allow it to hydrogen bond maximally as the nonpolar molecule cannot contribute. Using the Boltzmann Entropy equation, we find that
$$
\Delta S = k_b ln(3) - k_b ln(6)
$$
Which represents the energy loss per water molecule that is adjacent to the nonpolar molecule. The total entropic cost of a single water molecule is equal to the number of water molecules that border the nonpolar molecule times $\Delta S$. Further calculations (page 224) show that the total entropic effect is proportional to the area that the nonpolar molecule takes up. This is because the number of water molecules disturbed is proportional to the area of the molecule. 



#### Gibbs Free Energy

We need to use free energy when studying small systems at non-zero temperature. For a closed system in equilibrium, the entropy of the system is maximized which is the second law of thermodynamics.

The example of entropy maximization is presented on page 226. In this derivation, two identical systems when combined have entropies that add. Energy and particle number are conserved before and after the systems unite. When the exchange of energy is allowed, the change in entropy can be written as the differential:

![image-20210212201629271](C:\Users\benfy\OneDrive - Johns Hopkins\Documents\Markdown Notes\.images\image-20210212201629271.png)



Where the subscripts indicate the system they represent. We can further simplify this equation because we know that $dE_1 = -dE_2$ as energy is conserved. Finally we find the thermodynamic explanation of temperature as the change in total internal energy over the change in entropy.
$$
\partial E / \partial S = T
$$
We also know that total volume of the two systems is conserved so when the system has a sliding partition, the the volume adjusts to maximize entropy as well. This gives us the relationship that pressure over temperature is the change in entropy over the change in volume.

When particles are allowed to flow, the number of particles is constant which gives us that 

![image-20210212202112981](C:\Users\benfy\OneDrive - Johns Hopkins\Documents\Markdown Notes\.images\image-20210212202112981.png)

Because N is constant, $dN_1 = -dN_2$ as in the other examples, and these can be used to further condense the above equation. 

We define the chemical potential of the system $\mu$ to be:
$$
\mu /T = -\part S / \part N
$$
at constant energy and volume. Entropy maximization implies equality of chemical potentials on both sizes of the partition. 

Overall, the definition of equilibrium is dependent on the system set up but consistently, entropy maximization is what minimizes the energy of the system. 

![image-20210212202823130](C:\Users\benfy\OneDrive - Johns Hopkins\Documents\Markdown Notes\.images\image-20210212202823130.png)

This equation derived from the above equations states that for any process, mass will flow such that the change in entropy is greater than zero. Therefore, for any process entropy always increases even when the process does not occur at equilibrium. The relationship between the parentheses is the 'driving force' of the mass transfer process. Flux can be modeled with this driving force relationship.

We view the process of free energy minimization as a competition between minimizing the energy of the system and maximizing the entropy of the system.

Maximizing the entropy of the system plus the reservoir with which it is in contact is equivalent to minimizing just the free energy of the system itself. 

The Gibbs Free Energy can be derived from rearranging the first law of thermodynamics and can be written as $dG = d(E_{syst} + pV_{syst} - TS_{syst}) \le 0$ and the non differential form is written $G = E - TS + pV$ 

A negative $\Delta G$ implies that the process will proceed, a $\Delta G$ equal to 0 implies the process is at equilibrium. A $\Delta G$ of greater than zero implies that the reverse process occurs. 



## Chandler Introduction to Modern Statistical Mechanics - Chapter 1 - Fundamentals 

We use statistical thermodynamics because macroscopic systems are composed of many particles which would individually be impossible to keep track of all at once. Ignorance of certain properties of the systems is required. 

### First Law of Thermodynamics and Equilibrium

The first law concerns internal energy which we abbreviate $E$. 

Internal energy is an extensive property which means it is additive. When two equivalent systems are joined, the internal energy of the combined system is the sum of the internal energy of the systems individually.

Energy is conserved. If the internal energy of a system changes, energy must have flown into or out of the system. Mechanical work can change the internal energy into the system. Heat flow can also change the energy of the system.
$$
dE = dQ +dW
$$
We can define heat as change in internal energy that is not attributable to work. Work is generally force applied over a distance. Pressure-Volume work is a common form of mechanical work. 
$$
dW = -p_{ext}dV
$$
This book uses bold letters to represent vectors. The vector sum of all forms of work applied to the system gives the form:
$$
dW = \vec Fd\vec X
$$
Adiabatic walls of a system prevent heat flow into or out of it. An adiabatic process in which the total internal energy changes must have work done by or on the system. 

There is no quantifiable $Q$ or $W$ that can be obtained from integrating $dq$ or $dw$. Therefore, the $dW$ and $dQ$ are said to be inexact differentials. The book strikes the d in the differentials to indicate this. 

Isolated systems tend to evolve toward a final state. That final state is equilibrium. Equilibrium can be described by a few variables that change depending on the system. One of which is always the internal energy. Nonequilibrium states are characterized by significantly more variables by comparison. 

While no real systems are actually in true equilibrium, many are in metastable equilibrium that allows us to apply equilibrium thermodynamics. If the system appears to be independent of time, history, and there are no flows of energy or matter, then the system can be treated as one which is at equilibrium. 

Thermodynamics can tell us how systems transition between equilibrium states when one or more constants for the initial system are disturbed. 

### Second Law of Thermodynamics

The second law of thermodynamics can help us predict how a system will evolve upon perturbation from equilibrium. 

Define the **Entropy** of a state to be an extensive quantity that takes in the Energy of the system and the parameters that define the system ($\vec X$) : $S(E, X)$. This entropy function is monotonically increasing. If state B is adiabatically accessible from state A, then $S_B \ge S_A$. We say the transition between these states is reversible if the transition from state B to state A is adiabatically accessible as well. This implies that the reverse transition changes entropy with the same relationship: $S_A \ge S_B$. For this to be possible, the entropies of both states must be equal so the overall $\Delta S$ for a reversible process is $= 0$
$$
\Delta S_{adiabatic} \ge 0
$$
for any natural irreversible adiabatic process. The equality holds only for reversible changes. 

In term reversible is used when a process can be exactly undone by an infinitesimal change to the control variables that determine the state of equilibrium system. Metastable equilibria can have reversible processes if processes are carried out slowly enough that each state of the system is allowed to equilibrate. In other words, a reversible process is a transition between equilibrium states. 

Entropy is a state function. It can be written as the differential:
$$
dS = (\frac{\part S}{\part E})_x dE + (\frac{\part S}{\part X})_E dX 
$$
Some algebraic manipulation with the total internal energy differential gives that: 
$$
(\frac{\part S}{\part X})_E  = -(\frac{\part S}{\part E})_x \vec{F}
$$
Since S must monotonically increase with E, we know that the change in S wrt E is always greater than zero. We can use this to define the temperature of the system to be:
$$
T \equiv (\frac{\part E}{\part S})_X \ge 0
$$
temperature is an intensive quantity meaning it is independent of the size of the system.

The internal energy of a system can be written as a function of entropy and work:
$$
dE = TdS + \vec{F}d\vec{X}
$$

### Variational Statement of Second Law

This statement of the second law is most closely tied to fluctuation energetics. 

An internal constraint is a variable that is coupled to an extensive variable but does not alter the total value of the extensive variables: for example a moving piston sealing a gas moves with the internal energy of the gas but movement is coupled to change in internal energy.

The equilibrium state is the state at which $S(E, \vec{X})$ is at a global maximum. This fact gives us the related statement that $E(S, \vec{X})$ is at a global minimum at equilibrium. 

For all perturbations from equilibrium, the change in internal energy is greater than zero and the change in entropy is less than zero.



### Thermal Equilibrium and Temperature

When two systems at equilibrium with different temperatures are brought together, at equilibrium heat flows until the two systems reach thermal equilibrium such that the temperature of both systems are equal.

Energy flow always occurs from a hot body to a cold body. Heat is that energy flow that moves energy due to a temperature gradient. 

#### Heat Capacity

Heat capacity $C$ is defined as:
$$
C = \frac{dQ}{dT} = T\frac{dS}{dT}
$$
We can further distinguish between heat capacity at constant force and at constant parameters:
$$
C_f = T(\frac{\part S}{\part T})_f \\
C_x = T(\frac{\part S}{\part T})_x
$$
and since S is extensive, heat capacity is extensive. 

### Legendre Transforms

Legendre Transforms allow us to express functions dependent on one variable as a new function that is a function of another variable. This helps use derive useful thermodynamic relationships from the equations that we have developed thus far.

Take for example the reversible work differential ($\mu$ is the chemical potential of a species in the system and n is the number of moles of that species. It is an intensive property that controls mass/particle equilibrium).
$$
\vec f d\vec x = -pdV + \sum _{i = 1} ^r \mu_idn_i \\
dE  = TdS -pdV + \sum _{i = 1} ^r \mu_idn_i
$$
 Therefore, we have our energy function $E(S, V, n_i)$ dependent of entropy, volume, and mole numbers for each chemical species. 

A Legendre transform allows us to convert this function of S, V, and n to a function of T, V, and n.

![image-20210212231333062](C:\Users\benfy\OneDrive - Johns Hopkins\Documents\Markdown Notes\.images\image-20210212231333062.png)

this general form takes the function of x and converts it to a function of u.



#### Application to Thermodynamics

To apply this concept, let's transform $E(S, V, n)$ to a function $A(T, V, n)$ :
$$
A = E - TS
$$
where we call $A$ the **Helmholtz free energy** which operates in systems of constant entropy, pressure, and chemical potential?
$$
dA = -SdT -pdV + \sum _{i = 1} ^r \mu_idn_i
$$
The Legendre transform allows us to convert any conjugate pair. 



Further, we can convert $E(S, V, n)$ to $G(T, p, n)$ through a similar transform.
$$
G = E - TS + pV = H - TS
$$
and 
$$
H = E + pV
$$
the differentials of which are:
$$
dG = -SdT -Vdp + \sum _{i = 1} ^r \mu_idn_i \\
dH = -TdS + Vdp + \sum _{i = 1} ^r \mu_idn_i
$$
By substituting in the variational statements we derived earlier, we can see the following relationships:

![image-20210212232548397](C:\Users\benfy\OneDrive - Johns Hopkins\Documents\Markdown Notes\.images\image-20210212232548397.png)

### Maxwell Relationships

Using the exact differential relationships from the differentials above, we get a table of equivalent relationships. This is due to the fact that for an exact differential, the second partial derivative of a parameter with respect to the other differential is equal to the other parameter's second derivative.

$(\part S/\part V)_{T,n} = (\part p/\part T)_{V,n}$

$(\part S/\part p)_{T,n} = (\part V/\part T)_{p,n}$

$(\part C_v/\part V)_{T,n} = T(\part^2 p/\part T^2)_{V,n}$

$(\part p/\part T)_{V,n} = -(\part p/\part V)_{T,n}(\part V/\part T)_{p,n}$

Relate Heat Capacity to isothermal compressibility and thermal expansion:
$$
C_p - C_v = -T(\part p/\part V)_{T,n} [(\part V/\part T)_{p,n}]^2
$$

### Extensive Functions and Gibbs-Duhem Equation

$$
0 = SdT - Vdp + \sum_{i=1}^r n_i d\mu_i
$$

We can represent the $\mu$ as the Gibbs free energy per mole for a single component system so:
$$
G = \sum_i\mu_i n_i
$$
We can also show that pressure is proportional to the sum of the mole-fraction of species in the system



## PBOC - Chapter 6 - Statistical Mechanics

When dealing with very large numbers of molecules, we use a probabilistic interpretation of their behavior to describe their behavior on average. 

When developing statistical mechanics, it is common to use lattice models to set up a number of distinct states for molecules to occupy with a number of molecules distributed amongst the spaces in the lattice. 

We know from before, the total number of microstates is given by $\Omega \choose L$ where $\Omega$ is the number of lattice points and L is the number of ligands (ligand binding example).

The probability of encountering a given microstate is given by its energy.

We can express the probability of a given microstate with energy $E_i$ as a function of its partition function Z:
$$
p(E_i) = \frac{1}{Z} e^{-E_i/k_bT}
$$

$$
Z = \sum_{i=1}^N e^{-E_i/k_b T}
$$

This partition function is the partition function for the Boltzmann distribution which will be derived later. Since we require that the sum of all microstate energy probabilities is equal to 1, Z must just be the sum of all energy probabilities to normalize the probability of a single microstate energy.

Once we have a probability distribution that represents the different microstates, we can calculate important characteristics of the system such as the average energy $\langle E \rangle = \sum _{i=1} ^ N E_i p(E_i)$  This equation states that the ensemble average energy is just the sum of the energies weighted by their probabilities. 

We use angle brackets $\langle ... \rangle$ to represent an ensemble average value. 

 A useful trick for wrangling partition functions is to know that (given $\beta = 1/k_b T)$:
$$
\frac{\part}{\part \beta}Z = -E_i e^{-E_i/k_b T}
$$
With this relationship, we can write the average energy as:
$$
\langle E \rangle = -\frac{1}{Z} \frac{\part}{\part \beta} Z = -\frac{\part}{\part \beta} ln(Z)
$$
When modeling ligand-receptor binding, use a lattice model and view the states as either receptor bound or ligand bound. The energy only changes if the ligand is bound to the receptor. So, each unbound state is equal energy and each bound state is equal energy. 

When the receptor is unbound, there are L ligands occupying $\Omega$ states. When bound, there are L-1 ligands occupying the $\Omega$ states. 

if $\epsilon_{solution}$ is the energy of a ligand in solution and $\epsilon_b$ is the energy of a ligand when bound to its receptor, we can model the state in which no ligands are bound as:
$$
{\Omega \choose L} e^{-\epsilon_{solution}L\beta}
$$
When the receptor is bound:
$$
e^{-\beta \epsilon_b} \times {\Omega \choose L-1} e^{-\epsilon_{solution}(L-1)\beta}
$$
The partition function is then the sum of these two relationships. When $\Omega$ is significantly larger than L, we can approximate ${\Omega \choose L}$ as $\Omega^L$ (see page 243 for justification)

We can then write the probability of the a bound ligand as:
$$
p_{bound} = \frac{e^{-\beta \epsilon_b} \times {\Omega \choose L-1} e^{-\epsilon_{solution}L\beta}}{({\Omega \choose L} e^{-\epsilon_{solution}L\beta}) + (e^{-\beta \epsilon_b} \times {\Omega \choose L-1} e^{-\epsilon_{solution}(L-1)\beta})}
$$
expanding out the 'choose' notation and multiplying the top and bottom by $L!/\Omega^L e^{\beta L}$ gives another equation for p of the form:
$$
p_{bound} = \frac{(L/\Omega)e^{-\beta\Delta\epsilon}}{1 + (L/\Omega)e^{-\beta\Delta\epsilon}}
$$
when $\Delta \epsilon = \epsilon_b - \epsilon_{sol}$ This takes the form of a rectangular hyperbola which is what we would expect for a plot of the probability of ligand bound. If we let $c = L/\Omega V_{box}$ be the concentration of the ligand and set $c_0 = 1/V_{box}$ as the reference concentration, then:
$$
p_{bound} = \frac{(c/c_0)e^{-\beta \Delta\epsilon}}{1 + (c/c_0)e^{-\beta \Delta\epsilon}}
$$
which takes the exact form of a hill function with n=1. A physically appropriate $V_{box}$ is 1nm^3^ which puts the reference concentration at 0.6M which is close enough to 1M in biochemical standard state.

#### Derivation of the Boltzmann Distribution

I am actually not taking notes on this lol. I'm pretty sure this doesn't mater for this class but its on page 249



#### Ideal Gases

The entropy of an ideal gas represents the freedom to rearrange molecular positions and velocities. 

Since we consider ideal gas molecules independent of one another, a probability that describes a system of one ideal gas molecule will describe a system of many molecules as probabilities multiply.

Imaging some ideal gas molecules confined within a box. The microscopic state of the system is characterized by the spatial coordinates and momenta of each molecule. The position of the molecules in the box is uniform so we can ignore the energy related to being in different locations. The energy of the system is dictated by the momenta of the particles:
$$
E = \rho^2_x/2m
$$
where $\rho_x$ is the x component of the momentum of one molecule and m is its mass. The same probability that dictates the behavior of the x  component equally holds for the y and z component of the momentum. The above equation comes from the fact that $KE = (1/2)mv_x^2$ and $\rho_x = mv_x$ 
$$
P(\rho_x) = \frac{e^{-\beta E}}{\sum^{no.states}e^{-\beta E_i}}
$$
where the sum over the number of states in this case is not a discrete number, rather it is an integral over all small changes in momenta:
$$
\int_{-\infin}^{\infin} e^{-\beta \rho_x^2/2m} d\rho_x = \sqrt{\frac{2m\pi}{\beta}}
$$
Where the solution to the integral comes from manipulating the gaussian integral. This is extremely important to physics and probability. 

Using the constraint $\langle E \rangle = (1/2)k_b T$, we can solve for $\beta = 1/k_b T$ which confirms that the behavior of the ideal gas momenta follows a Boltzmann Distribution. 

> The Gaussian Integral:
>
> $\int_{-\infin}^\infin e^{-ax^2} = \sqrt{\frac{\pi}{a}}$

#### Chemical Potential

The chemical potential of a dilute solution has a logarithmic relationship with its concentration. 
$$
\mu_{solute} = (\frac{\part G_{tot}}{\part N_s})_{T,p}
$$
which in other words, the chemical potential tells us the free energy cost associated with changing the number of molecules of that species in solution. 
$$
G_{tot} = N_{H_2O}\mu^0_{H_2O} + N_s\epsilon_S - TS_{mix}
$$
in other words this equation is saying that the total free energy is the free energy of the water plus the solute free energy minus the mixing entropy of the solute in solution. 
$$
\mu_i = \mu_i0 + k_bT \ ln(\frac{c_i}{c_{i,0}})
$$
the concentrations can be substituted in for parameters of the lattice model as in the earlier example. Here, the subscript zero indicates the value at a reference state which in this case is probably 1M.

#### Osmotic Pressure

