# Problem Set 3 Written Answers

## Modeling The Living Cell - Spring 2021

### *Benjamin Fry - bfry2*

*02/28/21*

 

### Problem 1:

**a)** in MATLAB script. 

**b)** Plot of Solution vs Time shown in Figure 1. Plot of Error vs Time shown in Figure 2. 

We see that as time increases from the initial conditions, the error appears to increase exponentially.

### Problem 2:

**b)** Equation 1 is a second order reaction because two species (y1 and y2) must collide for it to occur. Equation 2 is a first order reaction because it is only dependent on one species (y1). Equation 3 is also a first order reaction as it also is only dependent on one species (y1). 

**c)** solved in MATLAB main script. 

**d)** Plot of solutions in Figure 3. 

### Problem 3:

**a)** Given an area of $A=5\ mi^2$ and initial conditions for y1 and y2 in count per area:

Copy number of prey: $X_1 = A \times y_1 = 5\ mi^2 \times \frac {55\ copies}{1\ mi^2} = 275\ copies$

Copy number of predator: $X_2 = A \times y_2 = 5\ mi^2 \times \frac {110\ copies}{1\ mi^2} = 550\ copies$



**b)** The Stochastic Rate Constants for the Gillespie algorithm implementation are as follows:

$c_1 = k_2/A = \frac {0.04\ mi^2}{tu} \times \frac 1 {5\ mi^2} = 0.008\ tu^{-1}$

$c_2 = k_1 = 12\ tu^{-1}$

$c_3 = k_4 = 8\ tu^{-1}$ 

where $c_\mu$ is the stochastic rate constant for the $\mu^{th}$ reaction.



**c)** There are 3 different reactions

**d)** There are 2 species to keep track of (y1 and y2)

**e)** The reaction propensities are as follows:

$a_1 = X_1X_2c_1 = 275\times550\times0.008 = 1210$ 

$a_2 = X_1c_2 = 275\times 12 = 3300$

$a_3 = X_2c_3 = 550 \times 8 = 4400$

where $X_i$ is the copy number for which prey is i=1, predator is i=2. The copy numbers and stochastic rate constants as calculated above for the $\mu^{th}$ reaction as above.



**f)** If reaction 1 occurs first, one prey and one predator are consumed and two predators are produced. Overall, one predator is produced and one prey is consumed. So, given that we started with 275 prey and 550 predators, reaction one occurring leaves us with 274 prey and 551 predators. If the birth process occurs first, starting with the same numbers of prey and predators, since one prey is consumed and two are produced, the net process produces one prey, so we would have 276 prey and 550 predators. If this question wants us to consider reaction 2 occurring after reaction 1, we would have 275 prey and 551 predators.

**g)** The Gillespie algorithm is implemented in the MATLAB script. The plot with two different trajectories is in Figure 4.

**h)** This comparison is plotted in Figure 5. The two solutions are very similar in that they both produce a cyclic pattern of population growth and contraction. When the prey population grows, the predator population grows until it reaches some limit, and the prey population begins shrinking and the coupled predator population then also shrinks. This pattern appears in both the stochastic and deterministic solution. Due to the nature of the stochastic solution, there is more variability between solutions and the stochastic solution tends to overshoot and undershoot the deterministic solution around the peaks and troughs of the curves. In between these regions and even at them though, the Gillespie algorithm does a very good job at finding a solution to the ODE. 