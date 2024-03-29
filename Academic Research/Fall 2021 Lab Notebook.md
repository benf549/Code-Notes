# Fall 2021

## Week 1 (9/26/2021)

Worked on getting Rosetta compiled on local machine to look into development of the protocol in C++. Trying to schedule a meeting with Dan to talk about the direction for the project.

## Week 2 (10/3/2021)

Want to create a script that samples all pairs or randomly samples a bunch of pairs of two "adjacent/overlapping" glycans on the native structure of the protein, say have atoms within fully extended glycan range (15A iirc). We can then run this script on benchmark proteins. The goal is to generate an 'average clash score' for nearby glycans on the surface of a glycoprotein. This will allow us to identify when a glycan is too close to an input structure. It may make sense to calculate this for each run through CWG based on the input protein but for now I think ill work on doing a benchmark.

May want to test the number of glycan conformations sampled to get a sphere and see number of cubes filled on each iteration. Could help find optimal number of cubes (point of diminishing returns). This is pretty easy just create some figures for different numbers of configurations. 

## Week 3 (10/10/2021)

Spoke with John about the work they wanted to see going forward. Decided to work on improving the speed of combination selection perhaps by following up with the clustering code or the port to C++. I need to talk to Sudhanshu or Morgan about the process of developing in C++ since I used distributed PyRosetta for everything over the summer. 

Contacted Matt to get access to the Gray lab cluster so I can actually run the code that I'm working on without torturing my laptop, but haven't gotten a response yet so my development speed is significantly hindered at the moment. 

RSVP'd to Keystone Conference in Colorado this winter. Planning to present the work I did over the summer and this semester on CWG. Dr Fleming mentioned to me that I have to present the work I did this year at some point to fulfill the biophysics research requirement so this might count but otherwise need to make sure I present at DREAMS (i think this is the name) in the spring. 

I think we also want to implement a way for the user to input a list of residue positions that we want to try to cover with a glycan. Even if the glycan wouldn't normally pass filtering, explain to them why in a warning message, but otherwise try glycans at that position. This can be used for blocking known off-target binding positions. 

Once I have the pairwise clash counts, visualize for different proteins using histograms and see if we can find an average. I think I will sample in the absence of the native glycans for now since it will be easy to remove the virtualization step if we decide it makes more sense to have the native glycans surrounding them. Sudhanshu suggests removing the native glycans for more generalizable (probability based) results. 

I think we may want to change the score function to use the default. I just realized what a 'beta' score function is haha.

By end of day Friday, completed a rudimentary script that counts the number of collisions for each pair. Need to parallelize since glycan sampling takes a while, benchmark what number of samples gives good coverage of a position (should find around 5). Also want to see the conformations so dump the PDB coordinates for visualization with the collision grid in pymol. For rbd, found 0 collisions between its two glycans.

## Week 4 (10/17/2021)

Still waiting for cluster access but should get it by the end of the day (Monday) hopefully. Continuing work on benchmark, implementing parallelism and pdb dumping to hopefully help visualize what's going on with the voxel visualization created over the summer. 

Finished implementing a basic parallelized version of the benchmark which should be sufficient to efficiently run the benchmark on heavily glycosylated proteins once I have cluster access. I did not get access today as promised but hopefully I will this week to begin running this benchmark.

I am planning to run the benchmark on HIV-env, Lassa, Flu HA and the other one for flu, SARS-CoV2, and maybe other members of the coronavirus/adenovirus families. It would be interesting to see if glycan density correlates with the evolutionary distance of the proteins.  

Got access to the cluster! 

## Week 5 (10/24/2021)

Struggled to get a working conda environment on Jazz and needed to write a bunch of essays for classes. Sent in a support ticket to the Gray lab IT but I didn't hear back. I am going to send a message to the general gray lab slack and hopefully, I will get some help from them. I never heard back from the support ticket :(

## Week 6 (10/31/2021)

Trying to get help with setting up the conda environment from the GrayLab slack instead of from an IT ticket since I never got a response from that. I still need to get a condor setup file from morgan to be able to run the benchmark. 

I was able to activate the PyRosetta conda environment with the following code snippet found on stack overflow. This seems to be an issue specific to CentOS

```bash
source /home/bfry2/miniconda3/bin/activate PyRosetta.notebooks
```

`condor_q` is to check the job queue. You do not get a job run until a system becomes available. 

```bash
condor_submit default_condor_submit.conf
```

where `#!/home/bfry2/miniconda3/env/PyRosetta.notebooks/bin/python` is found as the first line of the file being submitted to the cluster. 

Is there a way for Dan to test distance from antibody binding site for likelihood to disrupt binding?

###### Now That I Have a Working Cluster Environment, I Am Unstoppable:

Ran CWG on SARS RBD from the pdbs folder on the git repo. Condor seems to be working with Dask and PyRosetta installed with conda. It looks like the files are fine to run with `#!/usr/bin/env python` in the header rather than the longer one but I am leaving it  above in case this becomes an issue in the future. I haven't found any issues with Condor running CWG, other than some bugs I found and fixed in the protocol implementation with path parsing.

To begin running the benchmark I wrote two weeks ago, I have submitted a job to condor that should relax and glycosylate the Flu hemagglutinin spike protein which is heavily glycosylated as we observed over the summer. Once we have a glycosylated pdb file, I should be able to benchmark the native glycan overlaps in the spatial hash grid using this protein and others. The SARS rbd was a small example for me to make sure that the the protocol is working on the new cluster environment. Flu HA will be the first test of the benchmark. I still need to see if I can turn the overlap information into some sort of probability distribution to guess the liklihood of an overlap being unstable. There may be more information I want to extract from the glycan pairs. Right now, I am only getting the number of overlaps in the collision grid data structure. Maybe something like average distance between geometric centers could be useful for setting clustering distance cutoffs and could be easily found with this code as it is right now. The job I submitted was using a bash script launched with `#!/usr/bin/env bash` it is possible that this script will not have the pyrosetta environment variables set, in which case, I will need to run the relax and glycosylation steps separately one after the other. This is fine, but I figured I'd try running it like this.

To run the benchmark, I will probably try running the code that I had originally written. However, it might be faster to try running many different condor processes with the list of known nearby glycan pairs and collecting the data afterwards. If there are memory issues, I will look into doing it this way.

The next thing I want to work on, is implementing the clustering into the combination selection algorithm as running CWG on SARS reminded me that combinatorial selection is not memory efficient or quick when there are more than around 15 glycans to work with. Specifically, I experienced Condor killing the combination selection process with error code 9. I suspect this is due to using several GB of memory. If we can cluster the glycans and sort them by lowest Rosetta energy (whether that be of the tree itself or of the protein as a whole once they are introduced), we can take the minimal energy glycan from each cluster and this should give a good coverage of the surface of the protein. We can cluster the glycans by projection onto the bounding sphere or by their geometric center calculated as the average X,Y,and Z coordinate across all sugars. This will also allow us to implement specific protein domain targeting. 

## Week 7 (11/07/2021)

Began running benchmarking on native glycoproteins. After some thinking, rather than using the clash score for the "special input pdb" and the glycan lain on top of that. I think it makes more sense to put the glycan into the data structure and then put any input pdbs onto that. Then, we have a number of clash cubes over number of cubes for a single glycan which we should be able to turn into a probability distribution? I need to talk some more to the grad students about this. I also want to run a benchmark that runs GTM and see how many cubes I can fill as a function of glycan samples. Once there is a diminishing return for number of samples vs additional cubes filled, we will know how many samples on average we need to run to get good coverage of the space around the protein. 

I am also building the native glycosylations for some more proteins so my benchmarks aren't only run on one protein even though they are all run on the same glycan. I'm making a folder of relaxed and glycosylated PDB files and I want to keep track of what their corresponding PDB code is. Before running them through CWG, I first remove any antibodies bound to their structure, then I delete any existing glycosylations. I export the protein and then allow it to be relaxed by the first step of GTM. 

Here is a table to keep track of which RSCB PDB IDs correspond to which files:

| RCSB Code | Relaxed File Name      | Glycosylated File Name | Raw File Name      |
| --------- | ---------------------- | ---------------------- | ------------------ |
| 5VK2      | lassa_relaxed.pdb      | lassa_glycan.pdb       | lassa_raw.pdb      |
| 6BKP      | flu_relaxed.pdb        | flu_glycan.pdb         | flu_raw.pdb        |
| 4NCO      | hiv_relaxed.pdb        | hiv_glycan.pdb         | hiv_raw.pdb        |
| 6VXX      | scv2_spike_relaxed.pdb | scv2_spike_glycan.pdb  | scv2_spike_raw.pdb |
| 5W1K      | junv_relaxed.pdb       |                        |                    |
| 6M0J      | scv2_rbd_relaxed.pdb   |                        |                    |

Okay so while doing that, I realized that last week I accidentally created the glycoprotein for Lassa Virus spike protein rather than for flu hemagglutinin which is fine because I was going to do it now anyways, but I need to remember that things I called Flu before are actually lassa. I am running flu, hiv, and scv2 spike now. I need to remember that the folder called ACTUAL flu is indeed actually flu whereas the other folder is actually Lassa virus. I can tell just by looking at the PDBs but this isn't easy since its on the server. in summary `Flu_Benchmark_CWG_Copy` is actually a cwg run for Lassa virus but I can't rename it today since I'm running the benchmarking script on the Lassa glycosylations. Once condor job `13596364.0` completes It should be good to delete.

Once the other 3 spike proteins finish building their glycosylations, I will run the same benchmark on their glycosylated structures. I will probably need to create a data analysis pipeline for the result from this. I also want to benchmark the number of conformation samples. I think the sars RBD would be a good candidate for this since it already only has one sugar anyway.

Looking at the data from the conformation sampling. It seems like new cubes are populated even after 20 conformations are sampled. The thing is, the farther they are from the geometric center, the less likely they are to exist at that point. Is it possible to create a probability distribution from the geometric center of the glycan from this data which we could use to estimate the probability of a structure overlapping with the glycan? It seems like Sudhanshu has experience with this so I will try to ask on Friday. In the mean time, I am going to re-run the same with 50 conformations. to see where the diminishing returns point is. I think I am going to want to track the individual atom coordinates, right now, I am just tracking the voxels populated. This seems to run pretty quickly since it's just one sugar to sample so it shouldn't be too much of an issue to re-run. Promisingly though, none of the conformations got built into the protein backbone, so it seems like Jared's advice for setting the glycan sampler rounds higher was good!

To do this, I might want to create a sugar tree in the absence of a protein backbone to let it explore more conformations? Or maybe on a flat surface to assume it is generally oriented in a particular direction?

Looking at the initial results of the benchmark, there appears to be a bimodal distribution. I looked at the first conformation that claimed to have 251 overlaps, but it doesn't look to me like there are any overlaps at all... I need to look into the benchmark code to make sure that the code isn't counting overlap with themselves between sampling because that doesn't tell us anything.... Also, now that I have conformations samples, i could probably save time rerunning the benchmark by just loading the files. We'll see how frustrating that is.

Running the benchmark on Flu to get some more data and see if the same distribution of overlaps is observed.

###### Gray's Grad School Lab Recommendations (get him a list and see if he has any more recommendations)

- Eva-Marie Strauch at UGA
- UCSF
- Colin Smith
- Eric Fischer
- Frank DiMaio

I wrote a script that reanalyzes the benchmark data which should hopefully give better results.

## Week 8 (11/14/2021)

Working on reanalyzing the data from the benchmarks in the jupyter notebook `Collisions\ Analysis.ipynb`. Finished building GTM glycoproteins for HIV, SARS COV2 spike, Lassa, and Flu.

Here is a plot of the data (the geometric center of the voxels in 3D) from running a bunch of conformation sampling and appending the filled voxel coordinates for each additional conformation sampled:

![image-20211115190849255](C:\Users\benfy\OneDrive - Johns Hopkins\Documents\Markdown Notes\.images\image-20211115190849255.png)

and the same plot represented as distance from the final position after 100 samples

![image-20211115184031248](C:\Users\benfy\OneDrive - Johns Hopkins\Documents\Markdown Notes\.images\image-20211115184031248.png)

which it looks like it takes around 15 conformations sampled to get the geometric center of the voxel cloud within 1 angstrom of where it will be asymptotically which we can see takes around 100 samples here. I'm not sure if 1 or 3 angstroms should be the target as we are dealing with a 3 angstrom discretization of space. The next one shows the number of cubes filled vs number of conformations sampled. :

![image-20211115184144554](C:\Users\benfy\OneDrive - Johns Hopkins\Documents\Markdown Notes\.images\image-20211115184144554.png)

I am re-running the conformation sampling out to 500 different conformations to get a better picture of the hyperbola.

Now that we know the behavior of running different numbers of conformation sampling, we look at if there are going to be overlaps between voxels, how many cubes are they on average for native sugar trees? If we can get a cutoff for the number of cubes allowed to overlap for native trees, we can get a cutoff for other things overlapping with the tree:

![image-20211115190000594](C:\Users\benfy\OneDrive - Johns Hopkins\Documents\Markdown Notes\.images\image-20211115190000594.png)

I want to fit this to a probability distribution to estimate the likelihood of a given number of voxel overlaps being allowed by nature. I am struggling with this, I have tried fitting to exponential, and normal distributions but these don't seem to apply. I want to talk to the grad students about this on Wednesday because I am stuck.

![image-20211115203408444](C:\Users\benfy\OneDrive - Johns Hopkins\Documents\Markdown Notes\.images\image-20211115203408444.png)

above is the spread of the data with +/- one standard deviation from the mean shown. Not sure how to handle when the probability of <= 0 is 0 since this wouldn't fit to a normal distribution. 

Maybe I should scale the number of overlaps by the number of voxels taken up by the glycan to get a fraction? This makes more sense now that I think about it because the fraction should be independent of the size of the sample conformation voxel cloud. I am trying this with the Lassa data and I'll see if the distribution changes.

Recalculating the fractional overlaps which I think can be thought of the probability of existence given a fraction of overlaps, allowed me to fit the data with a Beta Distribution which is a probability distribution that itself represents probabilities bounded by 0 and 1. I got the following data from this:

![image-20211116150353577](C:\Users\benfy\OneDrive - Johns Hopkins\Documents\Markdown Notes\.images\image-20211116150353577.png)

I interpret this as meaning if there are no overlaps, you can definitely exist as the probability tends to infinity. Greater than around 40% overlap is extremely unlikely and the probability of the overlap being greater than 0.33 is 0.01

The 99% confidence interval was calculated numerically because the CDF function in `scipy` seems to be giving me lower values for probability than I think should work. This is probably because it's handling the asymptote at zero weirdly.

I started rewriting the combinatorial selection algorithm to use clustering like we had discussed over the summer. I wrote a backbone but havent added much substance yet. Looking at using the agglomerative clustering with decreasing pairwise distance until you get clashes with the collision grid that exceed the newly benchmarked cutoff. We also want to implement a way to target a particular region with sugars. I think we could do this by finding the shortest distance of a given position to a sugar from the ./pp and present the user with an option for amount of destabilization that we allow for that sugar. 

