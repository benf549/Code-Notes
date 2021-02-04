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

$E_{thermal} = K_\beta T$ where $K_\beta$ is Boltzmann's constant measured in Joules/kelvin
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

