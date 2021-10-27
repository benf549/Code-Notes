### PyRosetta Bug Report - Glycan Tree Modeler Quench Mode

*Benjamin Fry* - 07/06/2021

###### Environment

I've encountered this bug running the `PyRosetta.notebooks` environment as installed via the instructions in [Jupyter Notebook 16.00](https://github.com/RosettaCommons/PyRosetta.notebooks/blob/master/notebooks/16.00-Running-PyRosetta-in-Parallel.ipynb) via Anaconda on our cluster server. After installing, I updated PyRosetta and the version that I am running is `2021.25+release.a320e4c` according to `conda list`.

###### Reproducibility

This bug occurs consistently every time this protocol is run in PyRosetta. The bug does not occur when running the same protocol in Rosetta Scripts. I have reproduced the problem using the XML interface to PyRosetta as well as using PyRosetta objects. The problem seems to be with Quench Mode. We do not get any errors using the default of `Quench Mode = False`. However, the protocol we want to use starts with `Quench Mode = True` to build the individual trees and then follows with GTM run with its defaults to relax the trees.

The code that is causing the bug:

```python
### Runs for a while and eventually crashes with a Segmentation Fault ###
model_glycans = GlycanTreeModeler()

model_glycans.set_quench_mode(True) #Probably causing error
model_glycans.set_glycan_sampler_rounds(1)
model_glycans.set_window_size(2) # Not setting window = segmentation fault immediately
# model_glycans.set_rounds(5) # Setting rounds creates endless console spam
# model_glycans.set_layer_size(5) # Setting layer size = segmentation fault immediately

model_glycans.apply(pose)
```

When running tests, it was helpful to add `-mute core.conformation` and `-mute protocols.simple_moves` to the initialization flags to see what was actually going on as warning messages from these modules spam the console when running GTM with these settings. Running with the wrong combination of settings, when Quench Mode is set the program eventually will terminate with:

```
Segmentation fault (core dumped)
```

I thought I had found a solution by running the Quench Mode step first and dumping pose to PDB (as the code block above does not create an error until the pose is passed to a default `GlycanTreeModeler()` object for the relax step). However, when dumping the PDB, only one glycosylation is saved and when inspecting the file, most lines have all energies set to zero except the one glycosylation that can be viewed in PyMol. Reloading the dumped pose logs errors of the form:

`Link between   79 A and  417 A is ill-formed - one/both residues don't exist!`

and attempting to pass into the default GlycanTreeModeler will run but ignores the trees that weren't saved properly in the PDB.

###### Steps to Reproduce

Running `./build_native_glycosylations.py` with `gs_relax.pdb` in the same directory should recreate the problem. 

To speed up encountering the error, I have restricted the PNGS scanner to run only on chain A, all the same errors occur with the reduced number of glycosylations. 

###### Result

I have attached the log file for a previous run of this script. It ends with a segmentation fault.

Please email me at bfry@wistar.org if you have any questions about this issue.
