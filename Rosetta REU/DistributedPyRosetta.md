# Distributed PyRosetta

*Benjamin Fry* - 06/21/2021

### Documentation Notes

The `pyrosetta.distributed` namespace allows us to use `Pose` and `Score` objects from PyRosetta while doing parallel processing to save memory/time. This package integrates with `pandas`, `dask`, and `jupyter notebooks`. 

```python
import pyrosetta.distributed
```

The python primitives can be easily serialized. The `pyrosetta.distributed.packed_pose` namespace contains functions that serialize a `Pose` object. The `PackedPose` is a class that contains the serialized model and score information. The `packed_pose` namespace contains useful functions such as `packed_pose.to_pose()`, `packed_pose.to_packed()`, and `packed_pose.to_dict()` help convert the `packed_pose` object between states.

The `pickle` package is used to serialize and deserialize the python classes. The `pyrosetta.distributed.io` namespace implements functions that mirror the `pyrosetta.io` namespace, providing conversion between `PackedPose` and the PDB, MMCIF & Rosetta-specific formats.

The `PackedPose` object can be serialized to take minimal memory and can also be transmitted between processes for distributed computing. 

There should be equivalents to the important PyRosetta functions in the `import pyrosetta.distributed.tasks` package. The functions in this package work by deserializing the `PackedPose` into a temporary pose, running the function on the pose, and then reserializing the pose. These functions are pure as they do not mutate the object but rather return a copy/new object.

The `Dask.distributed` library interfaces with PyRosetta for cluster computing.
