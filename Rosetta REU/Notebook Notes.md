# PyRosetta Exercise Notebook Notes

*Benjamin Fry - 6/10/21*

### PyRosetta Setup

To run PyRosetta, we have been trained to use Google CoLab which runs Jupyter Notebooks. These allow you to access the file system of your google drive. The first cell of these notebooks is always the following:

```python
# Wheel install setup. This takes ~1.5 minutes each time you start a new notebook or do a "factory reset".
google_drive_mount_point = '/content/google_drive'

import os, sys, time

if 'google.colab' in sys.modules:
    from google.colab import drive
    drive.mount(google_drive_mount_point)
    
if not os.getenv("DEBUG"):
    google_drive = google_drive_mount_point + '/My Drive'
    pyrosetta_distr_path = google_drive + '/PyRosetta'  
    wheel_path = pyrosetta_distr_path + '/' + [ f for f in os.listdir(pyrosetta_distr_path) if f.endswith('.whl')][0]
    print(f'Using PyRosetta wheel package: {wheel_path}')
    !pip3 install '{wheel_path}'
```

 this assumes that you have created a directory in your google drive called `/PyRosetta/` within which you have uploaded a PyRosetta `*.whl`file downloaded from the Gray Lab website. 

Once you have run a cell containing this code, you will be asked to give access to your google drive and enter an authentication code. Once the authentication code has been entered, you should have access to the PyRosetta module:

```python
from pyrosetta import *
from pyrosetta.teaching import *
pyrosetta.init()
```

 can then be run.

### Poses

###### Creating a Pose

We can create a pose from a `*.pdb` file. Rosetta can read these in and output them as well. We can move directories in CoLab using `%cd /content/google_drive/My\ Drive/pyrbc_202106_notebooks/` where the `%` sign indicates you want to run a console command. We want to load in the the protein `PafA` (PDB ID: 5tj3). We were provided the file `inputs/5tj3.pdb` and can load a pose object from this file like so:

```python
pose = pose_from_pdb("inputs/5tj3.pdb")
```

alternatively, we can fetch this structure from the RCSB protein data bank using:

```python
pose = pose_from_rcsb("5TJ3")
```

```python
pose = pose_from_sequence("PHSRN")
```

```python
pose_clone = pose.clone()
```

the `.clone()` operation can be used to make a deep (rather than shallow) copy of a pose.

###### What is a Pose

The pose class contains information that describes a structure. The pose has access to energies, PDB_info, and the conformation of the atoms. We can access the protein sequence using the method:

```python
pose.sequence()
```

however, sometimes PDB files are not standardized and need to be cleaned before use with Rosetta. Including only the ATOM lines of the PDB file helps the structure properly import. Alternatively, we can use:

```python
from pyrosetta.toolbox import cleanATOM
cleanATOM("inputs/5tj3.pdb")
```

which will generate a new file called `inputs/5tj3.clean.pdb` which we can import using `pose_from_pdb` as before.

The `pose.annotated_sequence()` method will print a more verbose version of the sequence that describes non-standard residues present in the pose. `pose.total_residues()` is a method that will print the total number of residues in the protein sequence.

###### Residue Objects

You can access the individual residues using the `pose.residue(residue_number)` method. This returns a `Residue` object which holds information about its type. `Residue.name()` will return the 3-letter code of the residue. The residues (and most structures in Rosetta) are one-indexed. This means, the first residue in a pose is always 1 and the last is `pose.total_residues()`. Running `print(pose.residue(1))` will print detailed information about the residue's identity and 3D coordinates of its atoms. 

Because Poses are numbered starting from 1, this may conflict with the numbering from the PDB file. To use the PDB numbering, we can use `pose.pdb_info.chain(residue_number)` to return the identity of the chain that a residue belongs to and `pose.pdb_info.number(residue_number)` to get the pose residue numbering's corresponding number in the PDB sequence. The `pose.pdb_info.pdb2pose(chain_id, pdb_residue_number)` function will output the corresponding number in the pose. You can convert pose numbering to PDB numbering using the `pose.pdb_info().pose2pdb(residue_number)` method.

Residues also have useful methods like `pose.residue(residue_number).is_charged()` which returns the charge state of the residue. 

Residues are not always amino acids. PyRosetta also considers coordinate metal atoms and nucleic acids residues when they are part of the pose.

You can access individual atoms within each residue. Printing the residue will show you the identity of the atoms available. The atoms are numbered and the number of each atom can be found using the `residue.atom_index("CA")` which would give the numerical index of the alpha carbon atom (usually 2). Once you have an atom index, you can call functions like `residue.atom_is_backbone(residue.atom_index("CA"))` which will tell you if that atom is a member of the protein backbone. 

### Protein Geometry

Once you have a residue number, you can easily access information about its torsion angles and atom-atom distances:

```python
print("phi:", pose.phi(residue_number))
print("psi:", pose.psi(residue_number))
print("chi1:", pose.chi(1, residue_number))
```

There are several ways to find atom-atom bond lengths. We can use a `Conformation`object to do this which stores information about the protein geometry. `conformation = pose.conformation()` creates a new variable to store the conformation of our pose. The conformation object will require `AtomID` objects:

```python
residue = pose.residue(residue_number)

Nitrogen = AtomID(residue.atom_index("N"), residue)
C_alpha = AtomID(residue.atom_index("CA"), residue)
Carbon = AtomID(residue.atom_index("C"), residue)

print(conformation.bond_length(Nitrogen, C_alpha))
print(conformation.bond_length(C_alpha, Carbon))
 
print(conformation.bond_angle(Nitrogen, C_alpha, Carbon))
```

An alternative way to calculate pairwise-atomic distances would be using Rosetta's`Vector` class:

```python
N_xyz = residue.xyz("N")
CA_xyz = residue.xyz("CA")

NtoCAvector = CA_xyz - N_xyz

print(NtoCAvector.norm())
```

When you import the wheel file, information about the residues gets stored in the `/chemical/residue_type_sets/fa_standard/l-caa` which contains information about the canonical amino acids. The files located in this directory contain the ideal bond-lengths and torsion angles for a peptide created from a sequence of amino acids with no prior information. 

###### Manipulating Geometry

We can manually set the geometry of the protein backbone and $\chi$ dihedrals. The `set_phi(residue_number, angle_deg)` function, `set_psi()`, and `set_chi()` functions work similarly to manually change the angle the residue sits at in the backbone. 

###### Visualizing With PyMol Mover

To set this up, you have to download a script and set it to run on PyMol startup. Then in CoLab, run:

```python
import os
if os.getenv("DEBUG"): 
    sys.exit(0)
import pyrosetta.network

pyrosetta.network.start_udp_to_tcp_bridge_daemon(secret='my_code')
```

followed by

```python
pmm = PyMOLMover()
pmm.apply(pose)
```

where the `apply()` method sends the pose to PyMol. The `pmm.send_hbonds(pose)` method allows you to visualize all the hydrogen bonds in the protein. The `pmm.keep_history(True)` method allows you to load in structures with the same name as different states of the same object in PyMol which you can play as a video.

