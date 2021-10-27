###### PosterText.md

### A Novel Computational Pipeline for Glycoprotein Immunofocusing Utilizing Distributed PyRosetta

#### Abstract

A Novel Computational Pipeline for Glycoprotein Immunofocusing Utilizing Distributed PyRosetta

The human immune system is mediated by the specific binding of its components. Glycosylation is a common post-translational modification through which bulky sugar trees are affixed to specific structural motifs on the surface of proteins. When glycosylation is found on immunogen surfaces it modifies immune recognition and can potentially be used to focus responses to sites of interest. Rosetta's recently developed GlycanTreeModeler mover provides us with the tools for the de novo modeling and refinement of glycan structures. By selectively introducing N-linked glycosylation to an immunogen of interest, we can dissuade immune recognition from undesired sites and focus responses to the sites of interest. To do this, we have developed a novel autonomous protocol in PyRosetta dubbed Cloaking With Glycans (CWG) which coats a target protein with the maximum number of glycans that fit on its surface while leaving target regions exposed. Distributed PyRosetta and Python's Dask library are used to run many independent processes in parallel greatly speeding up the algorithm. The result is an efficient, easy to use, end to end computational protocol for glycoprotein immunofocusing.

