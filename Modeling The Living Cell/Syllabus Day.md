# Syllabus Day

## Intro to Models and Algorithms in Biological Systems

###### Why Models

We know a lot of info about cells but modeling allows us to test whether we understand how that info pertains to the structure/function of the cells. Just having info doesn't necessarily mean we understand how/why a cell operates/malfunctions

Quantitative computer simulations can be predictive if done correctly. 

All cells have similar components/molecules: Proteins, Lipids, Nucleic Acids, Carbohydrates. Millions of these molecules are in the cells and are moved around by random thermal motion and the electromagnetic force (charge interactions) as well as active transport for directionality.

Many structures in the cell assemble spontaneously like the lipid bilayer.

If we could describe the dynamics of these molecules and their interactions, we could simulate the whole cell. Equations from physics and chemistry are used.

Basic Science: discovers the individual interactions between thousands of diverse components.

Applications: Computational models produce highly detailed output that can replace in vivo experiments. Highly applicable to drug design.

> Example Pathway: Clathrin Mediated Endocytosis
>
> Vesicle formation and import to move particles across the cell membrane. Important at the neuronal synapse and thus dissociation is implicated in some neurodegenerative diseases.
>
> They model the spatial and temporal dynamics that can be used to form predictive models.

Differential Equations are essential for describing physical phenomena.

###### Goals For This Course

- Learn to model biological systems from molecular to cellular.
- Learn to make approximations and essential physics to not include unnecessary details.
- Learn a variety of algorithms and how to implement them.
- Make connections to experiments. 

Uses *Phillips - Physical Biology of the Cell*. The book helps move from the conceptual model to quantitative models. Models in the book are simplified to be solved analytically (as opposed to numerically - with the computer).

The textbook simplifies the models for learning, so we will deviate from the textbook to develop more advanced models.

Additional text will be provided.

* Understanding Molecular Simulation - Frenkel and Schmitt

###### Failures of these models

- Wrong physical model - scale is important.
- Too little detail
  - Ex: get structure right but cant do time dependence.
- Incorrect assumptions
  - Bacteria are too large to experience purely Brownian motion
- Does not describe data
  - Even though model seems right the data disagrees
    - Perhaps there is something unknown to be discovered!

###### Grading

* Problem Sets - 50%
  * Can work with others but cannot plagiarize. Discussing code is okay but have to write ourselves.
  * Lab sessions are essential for homeworks.
* One Midterm Exam - 25%
  * March. 
* Final (group) Project - 25%
  * Started in the last 3-4 weeks of the class. She will suggest protein folding model. 
  * Or design your own project - Use a real protein, do a disease spread model. 