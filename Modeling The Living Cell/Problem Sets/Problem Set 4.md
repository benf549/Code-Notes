# Problem Set 4 Written Answers

## Modeling The Living Cell - Spring 2021

### *Benjamin Fry - bfry2*

*03/25/21*



### 1 - Reduced Units

#### Calculate Temperature in Kelvin

Given $T^* = 1$ and $\epsilon / K_b = 300 K$ then:
$$
T = T^* \times \frac \epsilon {K_b} = 1\times 300 K = 300K
$$

####  The Density in g/cm^3

Given $\rho^* = 0.7$, $M = 40 g/mol$, $\sigma = 3.3 \times 10^{-10}\ m$
$$
m = 40 g/mol \times 1mol/6.022\times 10^{23}particle = 6.64\times10^{-23} g/particle
$$

$$
V = \sigma^3 = (3.3\times10^{-10} m)^3 \times\frac {100^3 cm^3} {1m^3} = 3.5937\times10^{-23}cm^3
$$

$$
\rho = \rho^* \times \frac m V = 0.7\times \frac {6.64\times10^{-23} g/particle} {3.5937\times10^{-23}cm^3} = 1.29 g/cm^3
$$

so, $\rho = 1.29g/cm^3$

#### The Time Step in s

Given $\Delta t^* = 0.005, \sigma=3.3\times 10^{-10}, M = 40g/mol, \epsilon = 300K*k_b$, $T = 300K, K_b = 1.38065\times 10^{-23}m^2kg/s^2K$
$$
\epsilon = T\times K_b = 300K \times (1.38065\times 10^{-23}m^2kg/s^2K) = \\
4.142\times10^{-21} J
$$

$$
m = 40 g/mol \times 1mol/6.022\times 10^{23}particle = 6.64\times10^{-23} g/particle\\
= 6.64\times10^{-26}kg
$$

$$
\Delta t = \Delta t^* \times\sigma\sqrt{m/\epsilon} 
= 0.005 \times (3.3\times10^{-10}) \times \sqrt{\frac{6.64\times10^{-26}kg}{4.142\times10^{-21}kgm^2/s^2}} \\ = 6.06\times10^{-15}s
$$

so $\Delta t =6.06\times 10^{-15}s$

### 2 - Molecular Dynamics

####  a. Plot Shown in Figure 1

This plot shows the total energy, potential energy, and kinetic energy as a function of time. As desired, the total energy is a flat line indicating that it remains constant throughout the simulation. 

#### b. Time Step Too Large

When the time step is too large, the system gains energy and therefore total energy is not conserved and any measurements of potential/kinetic energy or temperature will not be accurate. This is shown in figures 7 and 8 which were generated with a time step of 0.1

#### c. Calculate Average Potential Energies at T = 1, 0.5, and 0.1

These measurements are logged to the console in my MATLAB script. However, one run measured the potential energy as:

| Molecular Dynamics      | T=1      | T=0.5    | T=0.1    |
| ----------------------- | -------- | -------- | -------- |
| **$\langle PE\rangle$** | -21.2295 | -27.3015 | -34.6552 |

The corresponding values I measured from one run from PS2 MCMC sampling were:

| Markov Chain Monte Carlo | kT=1     | kT=0.5   | kT=0.1   |
| ------------------------ | -------- | -------- | -------- |
| **$\langle PE\rangle$**  | -28.2534 | -30.4693 | -31.6269 |

so, overall the two measurements were fairly close but since both rely on stochastic processes the actual numbers vary between runs. Both techniques observed the same trend of decreasing average potential with decreasing temperature.

Energy plots similar to figure 1 can be found in figures 3, and 5 for T = 0.5 and T = 0.1 respectively

#### d. Average T of each simulation

The distribution of T for each simulation is shown in figures 2, 4, and 6

Average T measured for one run of each are shown in the table below

| Molecular Dynamics     | $T_{init}=1$ | $T_{init}=0.5$ | $T_{init}=0.1$ |
| ---------------------- | ------------ | -------------- | -------------- |
| **$\langle T\rangle$** | 0.5634       | 0.2022         | 0.0595         |

The average temperatures are consistently lower than the temperature used to initialize the system, however this is okay because overall energy is conserved which is all that matters in an NVE system. 

### 3 - Brownian Dynamics

#### a. Plot 50,000 step trajectory for kT=10

This plot is shown in Figure 9 with the start and end positions labelled for the random walk and it is superimposed on the contour plot of the potential.

#### b. Repeat for kT=5,1, and 0.5

The respective plots are found in Figure 10, Figure 11, and Figure 12.

As the temperature lowers, it appears the random walk strays less far from its initial position. This makes sense as the particle has less energy to transition between states. 

#### c. 1000 kT=1 trajectories, how many within 0.2

This is logged to the console. The most recent run I ran observed 25 of the 1000 come within 0.2 of the other energy basin's minimum at (1, 0). This is a stochastic process and the exact number does vary between runs. 