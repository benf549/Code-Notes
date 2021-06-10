### Rosetta REU Bootcamp

[Zoom Link For Online](https://zoom.us/j/93205175017?pwd=bXlHSGptbjFieXlTU3ljVlZrbE9sUT09)

###### Bootcamp Introduction - 06/07/2021

Rosetta has over 100 labs, millions of lines of code and thousands of individual licenses. Rosetta can be used for protein structure prediction which has the goal of predicting a protein fold from the primary sequence. CASP is a competition for theoretical groups to predict the structure compared to a previously unknown solved fold. The year 2000 was the first time anyone had produced reliable results at CASP. Gray worked on docking at the CAPRI challenge.

The FoldIt game uses Rosetta under the hood. AlphaFold in 2018 uses deep learning to convert distance matrice into 3D structures. Gray's lab uses DeepH3 to do Antibody structure prediction which can do better than Rosetta in that specific case. 

Protein Design milestones: In the late 90s, the Zn finger protein was redesigned without zinc and was still able to fold. A new fold never seen before was created by Kuhlman in 2003. The first De Novo Enzyme was created in 2008. Small Molecule binders were created by Tinberg in 2013. Nanotube Binders were created in 2011. Protein Cages were designed in 2012. 

There are two fundamental problems in the structure prediction and design field. The first is how a protein knows what structure to fold into. Each residue has rotatable bonds and planar groups which give the polymer flexibility. There are more possible conformations for a 300 residue protein to explore than would be possible in the age of the univese. This is Levanthal's Paradox. Say you can solve the sampling challenge, how would we know which one is the correct structure? We can use the minimization of the energy function as per Anfinsen's Dogma. Anfinsen realized this by temperature melting a protein and then cooling it back down and observing that the structure/function was resumed. Rosetta works by this minimization of energy.

Some energies we might need to simulate would be Van Der Waals forces as simulated by the Lennard Jones potential, Coulombic Forces as simulated with coulomb force, Hydrogen Bonding which can determine secondary structures, Sidechain Rotamer energy can be predicted statistically by how often you see different sidechain states. 

Rosetta is a type of search strategy which searches different conformations for low energies. Rosetta uses 'fragments' which are 9 residue sequences and generate possible configurations and searches all the known possible conformations. They can also use gradient descent or monte carlo sampling to move throughout an energy surface to find an energy minimum. 

Rosetta is object oriented. 

![image-20210607104956851](C:\Users\benfy\OneDrive - Johns Hopkins\Documents\Markdown Notes\.images\image-20210607104956851.png)

See the handbook for financial things and Camille is a resource for any administrative stuff. 

###### Introduction To Python

We will be using PyRosetta which is a version of Rosetta (the entire thing) which is entirely accessible from python. This means they wrapped the C++ in a python API so it can be used for rapidly prototyping applications. 

We will use Google CoLab for Jupyter Notebooks

Here are some Python examples:

```python
str1 = "String1" 
str2 = "String2"
print(str1 + str2)
#Prints two digits after decimal
str1 = "float %.2f" % 1.0
print(str1)
str2 = "integer %d" % 2
print(str2)
```

Control Flow:

```python
x = 25
if (x < 15):
    print("Less")
    x += 1
elif (x < 20):
    print("More")
else:
    print("Most")
```

For Loops:

```python
print("loop 1")
for i in range(5):
    print(i)
    
print("\nloop 2")
for i in range(10,2,-2):
    print(i)
```

While Loops:

```python
i = 1
while i < 100:
    if i < 10:
        i += 2
    elif i % 3 == 1:
        i += 4
    else:
        i += 20
    print(i)
```

Continue and Beak

```python
#Loop from zero to nine
for i in range(10):
    if i % 4 == 0:
        continue
    print("Current number: {0}".format(i))
    for j in range(i % 4):
        if j > 1:
            break
        print("Counting remainders: {0}".format(j + 1))
```

Rosetta was historically indexed from residue n=1 to n=end while python is zero indexed which means we need to add 1 to for loop iterations with `range` or set the range from 1 to n+1.

Regular Expressions:

```python
import re 

text = "What are we hiding from this message?"

print(re.sub(r"r", '_', text))
print(re.sub(r" h(\w+)", ' _', text))
print(re.sub(r"(\w+)r(\w+)", '_', text))

print(re.match(r"hiding", text))
print(re.search(r"hiding", text))
```

Python is pass by value for numerical variables but pass by reference for dictionaries. 

More advanced functions:

```python
def mult(*argv):
    #Multiplies all arguments
    ans = 1
    for arg in argv:
        ans *= arg
    return ans

def remainder(x, y):
    return x % y

def double(x):
    return 2 * x
        
def compose(a, b, *argv):
    return a(b(*argv))

print(compose(double, mult, 2, 3, 4))
print(compose(double, double, 2))
print(compose(double, remainder, 5, 3))
```

Using a lambda:

```python
import re

def make_subst(find, repl):
    #Returns a function to replace characters
    return lambda text : re.sub(find, repl, text)

#Create two functions
dna_conv = make_subst("U", "T")
rna_conv = make_subst("T", "U")

print(dna_conv("AAUCGUUA"))
print(rna_conv("AATCGTTA"))
```

Lists:

```python
a = [1, 2, 3]
#Appending a new element
a.append(4)
# [1, 2, 3, 4]
#You can also concatenate two lists with +
b = a + [10, 11]
# [1, 2, 3, 4, 10, 11]
```

List Comprehensions:

```python
a = [1,2,4,5]
#Put only odd numbers in b
b = [x for x in a if x % 2 != 0]
```

we can think of them as similar to set notation

$S = \{x | 0\le x\le 20, x\ mod\ 3 = 0\}$

`[x for x in range(21) if x % 3 == 0]`

We can use them in place of for loops:

```python
S = [(i,j,k) for i in range(2) for j in range(2) for k in range(2)]
```

Dictionaries are like hash maps (associative arrays):

```python
animal_legs = {"snake": 0, "dogs":4, "duck":2}
animal_legs["centipede"] = 100

for k,v in animal_legs.items():
    print("{0}: {1}".format(k, v))
```

to have a dictionary with default values, we can use:

```python
from collections import defaultdict
coutn_aa = defaultdict(int) #Sets all new keys to default of 0

seq = "WKKAAGKLKW"
for aa in seq:
    count_aa[aa] += 1
print(count_aa)
```

A set is very rapid to search for an element because they are likely stored as binary search trees.

Declaring Classes:

```python
class Teacher:
    def __init__(self, name = "Mrs. Boring"):
        self.name = name
        
    def __str__(self):
        return "Hi I'm " + self.name
    
    def grade_homework(self):
        print("Grade inflation for all! A.")

teacher = Teacher()
print(teacher)
teacher = Teacher("Ramya")
print(teacher)
teacher.grade_homework()
```

Inheritance:

```python
class NiceTeacher(Teacher):
    def __init__(self ):
        Teacher.__init__(self, "Mrs. Nice")
        
    def give_candy(self):
        print("Here's some candy!!!")

class MeanTeacher(Teacher):
    def __init__(self ):
        Teacher.__init__(self, "Mrs. Mean")
        self.ask_count = 0
    
    def give_candy(self):
        if self.ask_count > 1:
            print("Here's some candy!!!")
            self.ask_count = 0
        else:
            print("Not this time.")
            self.ask_count += 1

nice_teacher = NiceTeacher()
print(nice_teacher)
nice_teacher.give_candy()

mean_teacher = MeanTeacher()
print(mean_teacher)
mean_teacher.give_candy()
mean_teacher.give_candy()
mean_teacher.give_candy()
mean_teacher.give_candy()
```

Python classes allow us to implement polymorphism, inheritance, and encapsulation. We can import abstract methods to prevent instantiation of a class directly. 

```python
from abc import ABC, abstractmethod
class Teacher(ABC):
    def __init__(self, name = "Mrs. Boring"):
        self.name = name
    def __str__(self):
        return "Teacher: " + self.name
    @abstractmethod
    def give_candy(self):
        pass
    
teacher = Teacher()
```

###### Pose Lecture

A `pose` is a central class in Rosetta and PyRosetta. A `pose` describes a molecular system which means it could be a single chain protein, a protein and its ligand, a heterodimer, RNA aptamer, a big RNP like the ribosome. 

The `pose` contains the coordinates of all atoms in the system, the bonds between them, the environment of the system, and more. It contains a sequence of residues, energy terms (like constants but the actual energy calculations and energies are held in a separate class), conformation of the protein and how conformation changes propagate, and information about the corresponding PDB (protein data bank) file.

Within the `pose` object, there is a `conformation` object which holds the residues. There is also a description of the kinematics of the system. A `residue` is another class which contains the information about the accessible torsion angles, the torsion angles of each residue which are redundant with the coordinates of the atoms stored in the `pose`. The residue also holds its sequence position and thus what other residues it is bound to. If you had the coordinates and the dihedral angles desync from eachother, you probably made an error.

Encapsulation is a SWE technique which means only the classes that contain an object can mutate the variables like dihedral angles. Only `private` functions manipulate the coordinates. The `conformation` class re-computes  dihedrals when coordinates change and vice versa.

`ResidueType` is another class representing the chemical layer which tells you how many atoms are contained in the residue, the inter-residue chemical bonds, which atoms are hydrogen bond donors, the partial charges of atoms in the residues. It is the chemical description of what it means to be an Alanine residue for example. This is so each Alanine in the sequence points to the reference data for the Alanine rather than creating a new copy.

Any place where a residue can be protonated and deprotonated adds a `ResidueType` object that can be pointed to. Modifications like phosphorylation and being at the N and C terminus are also different chemically. This is why we only point to the residues as needed. The class also contains the optimal bond lengths and angles of that residue.

The `Conformation` class defines how coordinate changes propagate through the system and provides access to some pose geometry. `pose.conformation()` is used to access this as any python object. The conformation also gives some bond lengths, angles, and torsions which are easily accessible. 

The `Energies` class is created once a `pose` is scored. Contains a record of the calculated energies broken down by term. Stores information about the last time the Pose was scored and the cache allows for efficient scoring and helps avoid redundant calculations. 

The `PDB_Info` class stores information about the PDB file from which the pose was read if applicable. Sometimes the N or C termini may begin numbering differently than the pose numbering such as not having a rigid structure (which means it was likely omitted) or just numbering from 0.

There are methods for manipulating a pose such as

Setting torsion, bond lengths, and angles:

```python
pose.set_phi(residue_id, new_angle)
```

Setting atom positions:

```python
#Don't use this
residue.set_xyz(atom_index, xyz_vector)
#You would actually want to do this in the conformation layer
```

though this might not update the conformation layer which could desync the angles and coordinates. In C++, the coordinates are `const` but this doesn't translate to python. 

Changing residues:

```python
pose.replace_residue(seq_pos, new_residue)
```

which allows you to do something like protein engineering/design.

Pose can be created from scratch with something like `pose_from_sequence("AAA")` which creates an Alanine trimer. Initializes the pose with its ideal coordinates with extended conformation (all torsions at 180 deg).

Geometry changes are propagated. The geometry is stored in terms of distances and angles rather than xyz coordinates. A `FoldTree` indicates the direction in which a geometry change is propagated. 

We can visualize changes to the pose from PyRosetta with PyMOL.

###### Score Functions - 6/8/21

![image-20210608093456911](C:\Users\benfy\OneDrive - Johns Hopkins\Documents\Markdown Notes\.images\image-20210608093456911.png)

Virginia recommends reading this paper. They've recorded tis lecture as it is an example of the journal club presentations. 

What is a score function for? Basically everything in Rosetta uses a score function. The lowest energy configuration is the most probable so out score function should help identify these.

![image-20210608093758218](C:\Users\benfy\OneDrive - Johns Hopkins\Documents\Markdown Notes\.images\image-20210608093758218.png)

The centroid mode is easier to see and lower resolution. Generally, we can use centroid mode first to find a region of minima. We can then switch to the full-atom energy landscape which is not as smooth a landscape (it is jagged and more noisy). There is a simplified score function in centroid mode
$$
\Delta E = \sum _i w_i E_i (\Theta_i, aa_i)
$$
Total energy is a linear combination of the energy of each amino acid scaled by the weight. $\Theta$ is the geometric degrees of freedom, $aa$ is the amino acid identity, $w_i$ is the weight

Energy terms to consider:

1. Nonbonded atom pairs
2. Hydrogen and disulfide bonds
3. Backbone and sidechain torsions
4. Other features
5. Other environments

Utilizes the Lennard Jones Potential. Calculates the attractive and repulsive forces separately. Allows us to adjust the weight of the attractive and repulsive forces separately. Coulombic attractions are accounted for using the `fa_elec​` function. 

Solvation energy. This is the most energy-intensive part of the protein model. Proteins bury hydrophobic residues and expose their hydrophilic residues. Rosetta represents the solvent as bulk water with the Lazaridis-Karplus (LK) implicit Gaussian exclusion. `fa_sol` represents the bulk water around the protein. The `k_ball_wtd` models water near polar atoms.

Hydrogen Bonding. Has electrostatic and covalent components. The electrostatics are accounted for in coulombic attractions. There is an H-Bond model that evaluates energies by comparing them to bonds in 8000 solved crystal structures. 

Disulfide Bonds. Require a map that explicitly models the bonds so there are more degrees of freedom. Rosetta has an orientation dependent model to calculate covalently bonded cysteine pairs. `Dslf_fa13` accounts for sulfur-sulfur distances, bond angles, and dihedrals.

Ramachandran-based backbone scoring. Measure deviation for each residue from ideal Ramachandran plots. Calculates the Bayesian probability of a conformation given existing backbone conformation

Side Chains Positioning. Is also accounted for on a residue by residue basis.

There are more score functions you can add to the score function such as for handling:

1. Other biomolecules (carbohydrates, DNA/RNA)
2. Modeling in non-aqueous environments
3. Extreme pHs
4. Docking has a different weight patch
5. Symmetric proteins must account for symmetry

The score functions calculate the energies in Rosetta Energy Units which have no real meaning but the numbers from Ref2015 have been calibrated to be approximately `kcal/mol`. Scores are calculated per-residue so a larger protein will have a larger score. It isn't a measure of free energy (cant compare stability directly). Scoring is essential to many protocols so you have to score or you will not succeed. 

Score functions can be used to calculate absolute energies ($\Delta G$) and change in energy ($\Delta \Delta G$) between two states.

###### Macromolecular Modeling with Movers

A mover is a class that can modify a pose. They are classes that derive from a base class called `Mover`. There are hundreds of subclasses of Mover that can do different things to the pose. Most established Rosetta protocols are wrapped as movers. Mover documentation is found on the Wiki. 

Using a mover. initialize it, configure it in some way, once configured we can apply the mover to a pose. 

```python
import pyrosetta
from pyrosetta import rosetta

pyrosetta.init()

pose = rosetta.core.import_pose.pose_from_file(pose, 'input.pdb')
sfxn = rosetta.core.scoring.get_score_function()
fast_design_rounds = 1
fast_design = rosetta.protocols.denovo_design.movers.FastDesign(sfxn, fast_design_rounds)
```

There is also a way to create the mover in **Rosetta scripts style** which is based on the XML language. 

```python
xmlobj = rosetta.protocols.rosetta_scripts.XmlObjects.create_from_string(
'''
<MOVERS>
	<FastDesign name="fastdes" repeats="1"/>
</MOVERS>
''')
fast_design = xmlobj.get_mover('fastdes')
```

the XML objects class is the more stable version of it. So, if you want to write longer-lasting code it's probably better to use the XML version. 

###### Searching Energy Minima by Minimization and Monte Carlo Sampling

Recall Leventhal's Paradox. There are more configurations for a 200 residue protein than atoms in the universe. ex: $3^{100}$. Thus, exhaustive enumeration of the configuration is impossible. 

Anfinsen's dogma tells us that the native protein structure is found at the energy minimum for the structure. There are some exceptions to this including Prions which have a kinetic trap that they get stuck in as well as intrinsically disordered proteins. 

Physics Based Protein Structure Prediction. The global free energy minimum can be found using physics. 

```python
def predict_structure(sequence):
    return argmin(all_conformations, key=free_energy)
```

The Side Chain Design Problem. There are 20 amino acids and we can choose 100 of them. Each torsion angle for a sidechain has 3 possible (staggered) configurations. This adds to the complexity of the sequence. 

```python
def side_chain_design(backbone_structure):
    bestE = 123456; best_seq = None
    for seq in all_sequences:
        if bb_strructure = predict_structure(seq) and E(seq) < bestE:
            best_seq = seq; bestE = E(seq)
     return best_seq
```

Define a confined region in the conformational space (only sample side chains near starting structure). Only sample configurations that are near the minimum?? missed the last part.

Minimization. Rosetta has a deterministic process that finds a nearby local minimum. Minimization cannot travel over energy barriers (it gets stuck in kinetic traps). Just modifying phi and psi means we operate in $2^n$ dimensional space. Therefore we are operating in very high dimensions. We choose a vector in the direction of steepest descent (we move along the gradient) and we take a step along that new direction and repeat until we have found the minimum. There are alternatives to gradient descent including Line Minimization, Conjugate Gradient, Quasi-Newton Methods (employs second derivatives see L-BFGS method). Finding the global minimum of a high-dimensional space is not a trivial problem (np-complete) and there is currently no one-size fits all solution to it.

Move Maps. A class that let you specify what degrees of freedom should be modified during minimization. Move maps use `set_bb()` which allow you to set the backbone conformations. `set_chi()` allows sidechain degrees of freedom to be manipulated. `set_jump()` connects non-chemical-bonded chains (allows us to hold particular parts of the structure together while allowing other parts of the structure to change [for example two beta strands can be held together while a loop between them is allowed to vary.])

![image-20210608164421836](C:\Users\benfy\OneDrive - Johns Hopkins\Documents\Markdown Notes\.images\image-20210608164421836.png)

the energy landscape is rugged and filled with local minima so it is very hard to find the true minimum. 

Monte Carlo Sampling. Works by using random number generation. Moves to lower energies and has a probability of moving to a higher energy state which is scaled according to the Boltzmann weight of the change in energy. A higher change in energy is less likely. A higher temperature makes the same transition more likely even if it tends away from the local minimum.

Simulated Annealing. We begin with a high $kT$ and transition to a lower $kT$ as we begin to narrow in on an energy minimum. 

Detailed Balance. Any state can be reached from any other in a finite number of steps. 

###### *ab initio* Folding and Comparative Modeling

Guessing a fold from the sequence with no prior information about the fold. We know we can't explore all combinations of phi, psi, and chi angles so we have to make assumptions to narrow down our search criteria. We rely on the fact that local sequence biases the protein structure. To address this, we use fragments of known structures. We use 9-mer and 3-mer fragments. We then look at all of these and see how well they fit into the structure. To do this, need to know ideal bond angles from Ramachandran plots to ensure no extreme/unlikely angles are introduced. 

Example of a fragment library:

![image-20210609093845833](C:\Users\benfy\OneDrive - Johns Hopkins\Documents\Markdown Notes\.images\image-20210609093845833.png)

IIH and VIH are similar so we should check if the structure is low energy. [Robetta](http://robetta.bakerlab.org) is a server that creates fragment libraries. Once we have 3-mer and 9-mer fragments, we can use movers to apply the fragment conformation to the pose. 

```python
fragset = ConstantLengthFragSet(3)
fragset.read_fragment_file("1gqm.3mers")
mover_3mer = ClassicFragmentMover(fragset, movemap)
mover_3mer.apply(pose)
```

The slides showed a video of Ubiquitin folding. First, the process starts with larger structural changes and then refines with smaller changes. 

Score Functions and Folding. We generally start with the `centroid` representation and score function of the residues to save computation time. This allows us to find a structure at lower resolution which we can then add the `full-atom` resolution to which will help it settle into its final structure.

We begin with centroid folding. Introduce the side chains. Then pack the side chains, minimize the structure and repeat (this is the relax algorithm) until you reach a minimal energy.

There are two assumptions. Local interactions set local shapes. There are also long range interactions that are essential for solving the structure. [GREMLIN](http://gremlin.bakerlab.org) predicts residue-residue contacts from statistical analysis of sequence co-evolution. 

Comparative Modeling with RosettaCM. *ab initio* is rarely useful for proteins with >150 residues. Aligns target sequence with a known structure sequence. Threads the target sequence onto the target backbone to create multiple possible structures. Then a `HybridizeMover` is used to sample the structural combinations of multiple templates. It rebuilds the loops and other missing segments with fragment insertion, refines, and then clusters. 

###### Packing and Relax

Packing. A subroutine that does sidechain optimization. We will almost certainly run into the packing function at some point this summer. The packer is the name given to the Rosetta module responsible for sidechain optimization. Optimizes the sidechain rotamers of the backbone. Has a pose, a score function, and a packer-task which tells the packer what exactly should happen inside it. 

![image-20210609211251354](C:\Users\benfy\OneDrive - Johns Hopkins\Documents\Markdown Notes\.images\image-20210609211251354.png)

Packer Task. Is controlled by the `TaskFactory`. Design is essentially packing. Design is packing with rotamers of different AA. Allows you to turn off certain amino acids at a given position. The operations you give to the Packer Task are commutative. The modifications can occur in any order and the resulting task is the same (order independent). Once you turn off an AA at one location it cannot be turned back on. It is like sculpting you can only take away and can't put things back. A `TaskFactory` builds a `PackerTask` from instructions. 

```python
factory = TaskFactory()
factory.push_back(operation)
packer_task = factory.create_task_and_apply_taskoperations(pose)
```

there are many factories that exist in Rosetta. A `MoverFactory` creates movers from a string for RosettaScripts. The factory is aware of the pose at all times. A packer task can only be used once and should be created as soon as you need to use it. You should immediately discard it after use as it retains memory of previous runs. `TaskOperations` are objects that represent a behavior. In a software engineering sense, the the factory encodes a behavior to be performed in the future (the command design pattern similar to the Mover objects). The `TaskFactory` is a list of instructions that are initialized from the command line which allows the information to live in global memory (which is generally bad but we need to do it for this).  There are other ways to create task factories. 

Simulated Annealing.

![image-20210609213134386](C:\Users\benfy\OneDrive - Johns Hopkins\Documents\Markdown Notes\.images\image-20210609213134386.png)

The deltaE calculation. We need to calculate the change in energy for substituting one sidechain for another. We could do this by scoring the pose and then scoring the changed pose. However, this is inefficient because most of the protein will remain unchanged. We can instead calculate only the interaction energy of that sidechain. They do this by representing all the sidechains nearby as a nodes in a graph which each have a one-body energy (`InteractionGraph`) and each edge is a two-body interaction energy. Iterate through neighbors and sum two-body energies to find the total difference in energy. The nodes cache their previous energies to save time from recalculating. Caching makes this calculation extremely fast.

`InteractionGraph`. precomputes and stores the graph of thousands of possible rotamers, positions, and edges. Uses a lot of memory. There is also a method that takes calculates pair energies on the fly which uses less memory. There is a way to automatically choose which will be faster for us.  Every residue has an atom that we use to find neighbors (usually beta carbon) and we apply a bounding radius away from that atom to identify which atoms nearby could potentially have a non-bonded interaction. At distances beyond the cutoff we say there is no interaction. 

Rotamer Set. A class that holds a vector of all the possible rotamers which is an instance of a residue object in a particular configuration. We also want to get rid of useless rotamers by doing a "bump check" this discards rotamers that collide with the backbone since these will have a very high LJ potential and highly unlikely to occur. We use a backbone-dependent rotamer library that is named after the Dunbrack lab. 

Above has been a description of the `pack_rotamers` function. There are other functions which take other approaches (such as making a greedy decision of lowest energy rotamer `rotamer_trials` but it's a bit outdated and not used as often anymore). `rt_min` runs a gradient descent algorithm and then makes a greedy decision for which rotamer to pick. This finds much lower energies than `rotamer_trials` though is a bit slower and no longer used as frequently anymore. `min_pack` runs the gradient minimization and allows the Metropolis-Hastings accept/reject criterion this is more used than the previous two but is used less than `pack_rotamers.`

![image-20210609215623942](C:\Users\benfy\OneDrive - Johns Hopkins\Documents\Markdown Notes\.images\image-20210609215623942.png)

(fast) Relax. A protocol that uses the packer as one of the steps. It attempts to find nearby energy minima. It is more rigorous and aggressive in conformation sampling than minimization alone. The default runs 5 cycles of packing to minimization. Iterates between running the packer and running gradient based minimization on the backbone energies. 

![image-20210609215957786](C:\Users\benfy\OneDrive - Johns Hopkins\Documents\Markdown Notes\.images\image-20210609215957786.png)

forms a saw-toothed pattern of weights on the repulsive-component of the Lennard-Jones potential. Makes a breathing effect allowing inward followed by outward movement of the atoms. This helps to jiggle the atoms into their energy minimum. 

(classic) Relax applies the rotamer trials algorithm. 

Optimization. There are several minimizers we can use to find minimal energies. `AtomTreeMinimizer` minimizes the internal coordinates such as dihedrals. `CartesianMinimizer` minimizes the 3-dimensional Euclidean coordinates which is extremely expensive. Minimizer is an implementation of abstract minimization routines. 

###### Constraints

Additions to a score function that bias or evaluate certain structural properties of the pose. If you know for some reason that two residues should be bonded (like from experimental data), you can reward structures for putting those residues close together. Can ensure certain residues have a particular dihedral angle, or distances between residues are maintained. You can lock an enzyme at its transition state even if its less energetically favorable with this technique. 

A constraint is defined with three specifications. One of th emost common constraints is `atom_pair_constraint` which is defined for two atoms and adds a penalty if the distance between the two deviates from a certain distance. `angle_constraint`s can be used to constrain an angle between three atoms. You can add a buffer that allows some flexibility in the angle. `dihedral_constraint`s are used to constrain a dihedral angle (defined by a plane) between 4 atoms. 

There are many other constraint types. `NamedAtomPair`, `NamedAngle`, `CoordinateConstraint`, `AmbiguousNMRDistance`

There are different penalty functions that can be applied to the constraint:

![image-20210610094325275](C:\Users\benfy\OneDrive - Johns Hopkins\Documents\Markdown Notes\.images\image-20210610094325275.png)

![image-20210610094411232](C:\Users\benfy\OneDrive - Johns Hopkins\Documents\Markdown Notes\.images\image-20210610094411232.png)

![image-20210610094506852](C:\Users\benfy\OneDrive - Johns Hopkins\Documents\Markdown Notes\.images\image-20210610094506852.png)

the y-axis of the line plots represent the penalty we are applying to being in a particular region of the x-axis.

There are also linear penalties, bounded penalties (similar to flat harmonic), `GaussianFunc` and `SOGFunc`, and Specialized Angle Functions.

