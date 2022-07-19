# Spring 2022 Lab Note

## Week 1 (2/06/2022)

Rewrote the combination selection component of the `./find_optimal_combinations` script. Using the findings from last semester's research on acceptable overlap for a pair of sugars, removed bounding sphere projection and combinatorial enumeration and replaced this with random sampling of the file names and pairwise checks of selected sugars with a sugar being evaluated for selection. If over $0.3$ of the sugar voxel cloud being evaluated is occupied, the sugar is not selected. I want to step through different confidence intervals to generate more potential combinations for evaluation, also perhaps create the constructs rather than just outputting a text file. I also moved the virtualization of native glycans to virtualize the `_0` samples which was not happening before. Extra structures we wish to avoid are pre-loaded into the collision grid matrix which should add additional collisions to selected. 

I may need to check that the initial sugar which we pop from the file_names array does not exceed the overlap threshold from the additional structures in the matrix which is unlikely but may be possible if someone loads in a lot of structures. 

## Week 2 (2/13/2022)

Currently running the script to test the moved virtualization code and initial results look promising. I think the next thing to do is to find some confidence intervals of interest which we want to output combinations for which could potentially be used to experimentally validate the algorithm!

Visual inspection of the combinations generated appears to be well distributed on the surface as desired!

Recalculated 99, 98, 97, 95, and 90 percent confidence intervals for pairwise glycan overlap to be allowed and reworked the output to generate a text file with combination structures for each as well as create an output directory with all of the sugars and sampled conformations. I want to create the constructs with at least the sequon mutations and potentially glycosylate them as part of the output. Perhaps I could leave it up to the user to run `./build_native_glycans` after the sequons are introduced. 

## Week 3 (2/20/2022)

Updated the find optimal selection code to output the constructs which can then be passed through build native glycans script. I realized that some of the sequons overlap so I think I want to only select a sugar if its sequon doesn't overlap with that of any other in the selections which should be easy to do. Once this is done, we should have a pretty solid algorithm!

Maybe find a way to allow coordinate input which builds "antibody" cloud at a desired site even if no antibody is known to bind there? maybe not and just tell user to dock w/ receptor or manually cull introduced PNGS.

Need to schedule meetings with Dr. Kulp/John and Dr. Gray to look at future directions. I want to see if its time to draft a manuscript for this work or if there are more benchmarks/experimental work that needs to be done.

## Week 4 (2/27/2022)

Debugged combination generation updates and set up and full-length protocol tests for both generating glycan conformations as well as reading them in from sampling files. 

Working on creating a powerpoint of research updates for John/Dr. Kulp to get them up to date with the work that I did last semester.

Ran full CWG protocol on scv2 receptor binding domain and Lassa Virus GPC trimer. RBD worked quickly, however the Lassa glycoprotein complex seemed to get stuck during the `./process_filter_and_mutate.py` script. This protein technically has 6 chains and I think it is maxing out the cluster's memory.

Met with John to go over CWG updates and finished draft powerpoint, need to identify protocol bottlenecks and find ways to address them.

## Week 5 (3/06/2022)

I rewrote the process filter and mutate script to handle making the mutations and glycosylation separately. It is clear that the bottle neck is in the GTM relax step because of the sheer number of glycosylations present on the lassa trimer. It may be interesting to look if results are changed significantly by virtualizing any glycans that are outside of a threshold range from the geometric center of the glycan being relaxed just to save potentially days from the computation time. 

Realized that the relax protocol can result in structures that are misaligned from the `./extra_structures` one may wish to avoid collisions with. The answer to this is just to align the relaxed structure to the original in pymol,  however from the test runs I ran earlier on sars rbd, I did not do this and realized the output products did not align well with the ace-2 receptor. I am rerunning the protocol with a relaxed and aligned input protein to generate figures for the presentation I mentioned earlier. 

## Week 6 (3/13/2022)

Building the glycosylated mutants is still in progress for LASV (going on 4 days now, there are about 50 processes yet to complete). Once this completes, I want to run combination selection on them. 

Lassa run finally completed and total runtime was **5 days, 6 hours, 50 minutes**. This is pretty abysmal, but we can use this as a baseline runtime to improve now. I want to try to implement a glycan area selector to simplify the combination relax step and need to update the relax protocol to discourage backbone movement. 

Wasn't able to do much work this week due to a heavy midterm/pre-spring break work load.

## Week 7 (3/20/2022)

Spring break.

## Week 8 (3/27/2022)

Since I was unable to do any work over spring break due to the grad program visits, I had a ton of work for my classes to do upon return from spring break and didn't get any research done. I will hopefully make this up in the coming weeks (reading period).

## Week 9 (4/03/2022)

Worked on updating my poster from Summer RosettaCON with current work for presentation at the Biophysics Undergraduate Research Fair (BURF). 

![image-20220415223607748](C:\Users\benfy\OneDrive - Johns Hopkins\Documents\Markdown Notes\.images\image-20220415223607748.png)

## Week 10 (4/10/2022)

Worked on creating presentation for lab meeting.

Ended up sleeping through the meeting and feeling horrible about that and then got sick for the next week so I guess that was an omen of what was to come.

Presented poster created in previous week at Biophysics Undergraduate Research Festival and had some fun interactions with professors and current students. Got some underclassmen interested in protein design and Dr. Gray's lab. 

On Friday worked on updating relax protocol to fixed backbone to hopefully provide some speedup as well as avoid the need to redock optional input structures. Ended up adding the `-relax:quick` and `-relax:sc_cst_maxdist 0.5` initialization flags as suggested by John.

I created the directory `test_relax_update` to compare the old and the new protocol to see if we have any time savings from this. I ran both with the `lassa_raw.pdb` glycoprotein as saved in `glycoproteins_for_benchmarking`. 

Condor concluded the relax protocols for each and the time savings were pretty small:

|         | Before Update | After Update  |
| ------- | ------------- | ------------- |
| Runtime | 5 hrs, 22 min | 5 hrs, 14 min |

Which isn't a great time save. The largest time save should come from the next part which I am currently thinking through how I want to approach. This is finding a way to reduce the time it takes to build and relax a glycan since we know this is where our bottle neck is.

## Week 11 (4/17/2022)

Working on creating a glycan 'layer selector' that selects the ring around the glycan being added in the 3rd CWG step. This should let us model the glycan conformations a little less accurately but get some large time savings especially for very large/heavily glycosylated constructs.

![Glycan Layers](C:\Users\benfy\OneDrive - Johns Hopkins\Documents\Markdown Notes\.images\Glycan Layers.png)

So in the image example above, the blue glycan will be the position on the mutant we wish to introduce the glycosylation at. The green and red glycosylations will be the native glycosylations that are built after the relax step. By selecting only the 'green' sugars which are those within direct interaction range of the new glycosylation site, we should be able to reduce the overhead for GTM. I think I want to consider a radius of 30 Angstroms from the predict geometric center of the new glycosylation as the position of the first 'layer' of trees from the mutation site. The conformations available to the glycan we want to introduce will be constricted by the conformations of this first layer. By virtualizing or holding fixed (not remodeling on each GTM call like we are currently) the native glycans that arent members of the first layer, we should see a significant speed increase. The current GTM models glycans on the opposite side of the protein from where we are modeling the mutation site which is not useful on large protein constructs. 

The 30 Angstrom cutoff we determined in the fall is approximately the length of a fully extended man9 glycan tree so, this should be the maximum distance in which a glycan can interact with another. A second glycan 'layer' could be constructed from all glycans within 30 Angstroms of the first layer. The number of layers is a parameter we may want to test. Furthermore, 30 Angstroms was an overestimate if I recall, so we may be able to decrease/increase this for additional time save if necessary.

There may be a way to convert the distance cutoff neighbor approximation to a graph problem, but I don't want to overcomplicate this at the moment.

Editing the `build_tree_at_mutation` method in the `process_filtered_and_select.py` script to implement this behavior. The full glycan relax step is what I believe is causing the bottle neck. I'm going to update just this for now and benchmark from there.

![layer2](C:\Users\benfy\OneDrive - Johns Hopkins\Documents\Markdown Notes\.images\layer2.png)

Shown above are two layers of flu hemagglutinin glycans surrounding a tree at (pdb) position 81 on chain A colored as in the drawing above with threshold distance of 30 Angstroms.

running speed benchmarks in `test_pfas_speed_update` with just filtering, pfas, and combination selection (no relax or native glycosylation).

### Week 11 (4/24/2022)

The updated script runs much faster as desired! With pre-relaxed lassa and pre-built native glycans on the relaxed protein, the entire protocol ran in **1 day 10 hours** (concluding on Tuesday the 26th). As of Wednesday, the old version of the program is still running and has just crossed 3 days... I will report the runtime when it does finally conclude. Both jobs were submitted with 8 cores requested on Jazz.  

I want to create a glycosylated Lassa construct I can send to Kulp Lab as a result of this, though I realized the fa_rep cutoff is too strict for this protein only selecting 2 glycosylations a the end of the protocol. I raised the REU cutoff from 5 to 15 and am rerunning to get better designs.

Also noticed that `./process_filtered_and_select.py` doesn't have a load samples from command line option. If you just want to re-run with a different `fa_rep` cutoff, you have to rerun sampling or move the constructs yourself which is annoying. Want to implement this functionality at some point. 

Amending the above paragraph, this isn't really necessary because a log of the fa_rep scores is saved in selections and you can just copy from `gly_gly` to `selections` using the logged info. I ended up doing this for the LASV GPC complex that was the original focus of my work in the Kulp lab over the summer and I'm copying the results below:

###### 90% Confidence Interval (least overlap permissive)

![90_with_abs](C:\Users\benfy\OneDrive - Johns Hopkins\Documents\Markdown Notes\.images\90_with_abs.png)

![90_no_abs](C:\Users\benfy\OneDrive - Johns Hopkins\Documents\Markdown Notes\.images\90_no_abs.png)

###### 99% Confidence Interval (most overlap permissive)

![99_with_abs](C:\Users\benfy\OneDrive - Johns Hopkins\Documents\Markdown Notes\.images\99_with_abs.png)

![99_no_abs](C:\Users\benfy\OneDrive - Johns Hopkins\Documents\Markdown Notes\.images\99_no_abs.png)

### Week 12 (5/1/2022)

Further amending the first paragraph from last week, the old version of the program is still running on Jazz. As of Sunday night it has been running for a full week... It concluded on Monday for a total runtime of **7 days 18 Hours 46 minutes**

Need to present the speed improvements we made this semester to John. This will hopefully greatly advance the general applicability of the protocol and make it actually usable for large protein complexes and Lassa in particular as that was the original project I was working on for Dr. Kulp.

Need to submit the research grading form to Dr. Gray and Dr. Fleming for the semester this week to ensure I graduate on time. 

I am currently working on doing some full CWG runs to maybe create a plot of protocol execution time as a function of amino acids/native glycans. This is hard to do with the previous revision because too many glycans can cause it to run out of memory or take so long that it's killed by the cluster manager. That being said, it is still useful to know to give Kulp lab/potential users an idea of how long the protocol will take. 

I'll continue talking to Kulp lab over the summer to get everything wrapped up before starting grad school in the fall.

I went to compare the fast protocol to the old protocol and noticed that the fa_rep component of the glycan trees (which we use to filter out malformed trees) was calculated incorrectly for both resulting in undefined behavior. I think I have corrected this, and I am re-running the selection script again which should be quick for both. The point of doing this was to see if the speed increase has impacted the results from the previous implementation. From what I see so far, it hasn't but it's hard to say since the `fa_rep` calculation script was indexing the pose residues incorrectly (truncating the pdb_number).

From re-running found that for this Lassa GPC input, the new protocol selects basically the same positions for a total of 124 with the new protocol compared to 128 in the old protocol. For this specific protein, the energies were on average 3.65 REU higher than they were when relaxing with all sugars on the protein, but this is likely just due to random chance.  Seems like any positions with very high fa_rep are due to GTM running with too few rounds. This is something we could increase if we notice it is a problem, but I'd need to do a lot of benchmarking to optimize this I think. Maybe I could reach out to Jared to see what he would recommend as settings for this task since we now save a lot of time using the layer selection. 
