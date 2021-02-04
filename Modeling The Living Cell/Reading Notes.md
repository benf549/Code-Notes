# Reading Notes - Modeling The Living Cell

### Physical Biology of The Cell - Chapter 2

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



