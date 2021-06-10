# Problem Set 5 Written Answers

## Modeling The Living Cell - Spring 2021

### *Benjamin Fry - bfry2*

*04/06/21*

### Problem 1

Is completed in MATLAB script. Average values are logged to the console. When `rng(100)`, observed an average potential energy for the final 1000 time steps of `3.141829` and an average kinetic energy of `16.307426`

The trajectory of the PE and KE with respect to time is plotted in Figure 1

### Problem 2

![image-20210406215102898](C:\Users\benfy\OneDrive - Johns Hopkins\Documents\Markdown Notes\.images\image-20210406215102898.png)

### Problem 3

###### 3a:

The Reynold's Number is the ratio of inertial to viscous forces. It is the density of the fluid $\rho$ in $kg/m^3$ times the velocity of the object inside the fluid or mean velocity of fluid flowing itself $v$ in $m/s$, times a characteristic length scale related to the object being studied $L$ in $m$ which compose the inertial terms of the Reynold's number. The viscosity is the denominator of the Reynold's number represented by $\eta$ measured in $kg/(m* s)$ and it makes up the viscous terms. Overall:
$$
Re = \frac{\rho v L}{\eta}
$$
The Reynold's Number itself is unitless. The Reynold's number is useful because it can give us information about how a fluid flows. Specifically high Reynold's numbers indicate the fluid has a propensity for turbulent flow while low Reynold's number fluids have a propensity for laminar flow. 

###### 3b.

Laminar flow is observed when the Reynold's Number is approximately less than 10 according to lecture, however, the exact cutoff may vary with the other parameters of the system.

###### 3c.

Because laminar flow indicates a low Reynold's Number, the viscous terms dominate and inertial terms vanish. This allows us to disregard the inertial terms of Navier-Stokes and allows us to use Stokes' equation to get analytical solutions for our fluid mechanics.

###### 3d.

The nonlinear term in the Navier Stokes equation represents the acceleration as a result of change in orientation of the velocity vector. In other words, this term is the spatial derivative of the velocity describing the complicated eddies and whorls observed in turbulent flow.

###### 3e.

The velocity at the walls of the tube must be zero.

###### 3f.

The final equation we solve to get the solution from 3e was:
$$
0 = -\frac{\nabla P}{\rho} + \frac{\eta}{\rho}\nabla^2v_z(r)
$$
which simplifies to:
$$
\frac{p(L) - p(0)}{L} = \eta \frac 1 r \frac{\part}{\part r}[r\frac {\part v_z(r)} {\part r}]
$$
The two boundary conditions we need are the No-Slip boundary condition which says the velocity at the wall must be zero. Furthermore, we have the condition that the velocity of the fluid at the center of the tube must not be zero and must also be finite.

### Problem 4

See attached grid paper sheets.

### Problem 5 (extra credit)

###### 5a.

When the solution is propagated to 10 time units, the solution does not reach an equilibrium because the two wells are not equal in height. Propagation out to 100 time units does reach equilibrium. The 10 second propagation is plotted in figure 7 and the 100 second propagation is plotted in figure 8 for comparison. Running for longer times than 100 time units does not create any noticeable difference in the solution which makes sense as the two wells should have equal probability of containing the particle given enough time passes.

###### 5b.

The final solutions to the 10 and 100 second propagation of the PDE are plotted as mentioned in part b. The plots are indicated as part b in the MATLAB script.

###### 5c.

Plotted in figure 9. Observe that this looks the same as the 100 time unit solution supporting my answer for 5a.

###### 5d.

When kT=5, the peaks of the PDE surface broaden and the equilibrium is reached much faster as resetting the maximum time to 10 time units. My plots for this trial are in figures 10 (showing the final frame of the movie) and figure 11 (showing the equilibrium solution of this set of parameters). This is because, a higher temperature gives the particle more energy to explore outside the well minima and makes it more likely to transition between wells in the same amount of time. 

###### 5e.

Based on the plots I generated in figures 12 and 13, setting the potential equal to zero everywhere means that given enough time, the particle is equally likely to be found anywhere in the x,y plane since there is no force applied to it that confines it to what were energy wells where there previously was a potential.

