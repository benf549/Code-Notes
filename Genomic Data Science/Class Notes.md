# Syllabus Day

## 01/26/21

### Genomic Data Science

Learn about genomics. Focus on the analysis of very large sets of data. Structured around 3 projects. Each project given data our goal is to analyze that data and come up with findings. Lectures are to give the background on what the data is and the methods that created it. We will be running software not writing it. Small programs will be written to analyze the output of these programs. 

We will use the `bme-manatee.win.ad.jhu.edu` server which hosts the datasets. SSH into the server when logged into the Hopkins VPN. 

`ssh bfry2@bme-manatee.win.ad.jhu.edu` and log in with jhu password.

There are two directories that are important for this class:

`/opt/ccb/data` for data and `/opt/ccb/sw` for software.

> Tip:
>
> `zless` will show the content of a `.gz` file.

We need to copy the `global.bashrc` to out home directory's `.bashrc` to set our programs to the `$path`. Then we can call programs like blastn. 



### Genomics Background

##### DNA and Genomes

No molecular biology knowledge is required for this course so we will review it now. An important part of Data Science is understanding the data you are analyzing. 

DNA has 4 bases A, T, G, and C. Genome is all the DNA in every cell in your body. Every living thing (and some viruses) have a DNA genome. DNA double stranded with AT and GC pairs. The CG bond is stronger (3 hydrogen bonds) than the AT bond (2 hydrogen bonds).

###### **Genome Size**

Humans: 3Gb (gigabases) while the Redwood Tree: 26Gb. Typical Viruses: 1-100 Kb (kilobases). The Flu virus (RNA): ~13.5 Kb. The SARS-CoV2 virus: 29Kb. Bacteria: 1-10 Mb (megabases). Eukaryotes: 10-100 Mb.

Genome size does not give an idea of how complicated an organism is. Many conifers have larger genomes than humans. Genome size is also not necessarily correlated with number of genes.

##### **Sequencing**

Started with **Sanger Sequencing**. In 2004, next-generation sequencing was introduced. Now people are developing 3rd generation sequencing. 

DNA is read from 5' to 3'. The bonds between the strands can be be easily split with heat. DNA Polymerase starts at 5' end of one strand and copies the strand using free-floating bases in solution. 

Uses chain-terminator nucleotides (ddNTPs) mixed with normal nucleotides. When one of the ddNTPs bonds the strand, the strand cant be extended. You get a mix of strands of different rates. Since you can visualize the length of strands on a gel, if you ran the experiment separately with ddNTPs of each type (ATGC), you can visualize where that type of residue is. You can then add 4 different colored fluorescent ddNTPs for each and then you get a series of different colors corresponding to the sequence. 

The data output from Sanger sequencing is known as a chromatogram. 

Inherently limited by the rate at which DNA moves through the gel. As you get to longer segments of DNA, the 1000th and 1001st bp start to overlap. Could only read about 700bp at a time. Would need to break the genome up into many pieces and align them.





### Project 1

Assembling the genome of *Klebsiella pneumoniae* from DNA sequence data. Has about 2 million pairs of reads - so we will be assembling 5 million reads. 

###### Assignment 1

Use the linked documentation to figure out the homework.

The Illumina data sequences both ends of the same DNA fragment. Sequences 150 bases from the left and 150 bases from the right. 

Nanopore (ONT) reads are way longer (42,000). You can assemble the Illumina and Nanopore data at the same time. 



## 01/28/21

#### Sequencing Cont.

The first assembled human genome was done with Sanger sequencing at 800 bp/read and took a very long time. 

###### Next-Generation Sequencing

The advent of illumina sequencing technology has made sequencing faster and cheaper. 

Capillary sequencers use many lanes at one time. Each capillary can run a region of DNA for sequencing. Each sequence was kept seperate. The first could run 384 capillaries at a time. This would allow ~400 samples to be sequenced at a time.

In 1989 it cost $10 / base to sequence DNA. In 2001, they were able to do a whole read at around ~800bp for \$1. Today in 2021, the HiSeq 400 can process 400 billion bases/day with \$1 getting you 62 million bases.  From 2001, this process has gotten 77,000x faster. In 2001, it would cost \$30 million dollars to sequence a human genome. Now it costs about \$1000 to sequence a human genome. 

Because of this increase in availability, the amount of data that has come out of sequencing has resulted in more data than can possibly be analyzed! This course will teach us how to interpret and process this data.

###### Illumina Sequencing

First a library is prepared. A library is a collection of DNA you're preparing to sequence. The library will be many millions of identical copies of the sample replicated in a PCR. You break the DNA into small pieces about 500-1000bp long. You can physically break it in a blender, blasting it with ultrasound, etc... 

To get a particular size, you can run the DNA through a gel and slice out the desired range of lengths.

Once broken up, small adapter sequences get added to the end of the sequences. Ligases attach these adapters to the ends of the fragments. A different adapter gets added to 5' and 3' ends. The adapters are of known sequences. 

Once the adapters are attached, the sample is poured over a flow cell. The flow cell has billions of little primers embedded in it. The adapters are designed to be complementary to the DNA randomly created on the flow cell. Now you have single random strands of DNA attached to the flow cell by the primers on the end.

Once the DNA is attached to the flow cell, bridge amplification is performed similar to PCR and the anchored fragments get copied (about 1 million times) in place. To do this, primers are added that can bind the doubly-bound DNA strands and the strand is copied 5' to 3'. Heating the flow cell will release the second strand. You then get many complementary strands anchored to the flow cell nearby eachother. Have to ensure that not too much DNA is added so that the clusters are visually distinct.

Now the DNA is prepared and sequencing can begin. This sequencing requires another special type of base. One base is added per cycle of the machine. These modified bases are modified such that they stop addition once added. The four bases fluoresce in different covers. The termination reaction is then reversible and extension can be resumed after the cycle. 

Add base, read base, remove terminator and repeat! This is one cycle. The primer ensures the forward strand is read first and a seperate reaction is used to read the reverse strand. 

Because the DNA is replicated locally, you get clusters with many identical copies that fluoresce based on the base that was added. The machine keeps track of the change in color per cycle per cluster. This allows billions of clusters to be sequenced in parallel. 

At the beginning this could do 1 million at 25bp at a time. These were so small that they almost weren't useful. Now the readlengths are around 50bp with a max of around 300bp with millions run in parallel. 

You can actually run multiple samples at once by DNA barcoding the samples. Entend each strand with a barcode of 6 bases. This alows multiplexing 15-20 samples at the same time!

###### FASTQ Format

The output of these machines is often in FASTQ. 

![image-20210128154413221](C:\Users\benfy\AppData\Roaming\Typora\typora-user-images\image-20210128154413221.png)

The sequence ID has changed over the years to become more complicated. Understanding this metadata can be used to go back into old data and make new findings in other people's data.

![image-20210128154451058](C:\Users\benfy\AppData\Roaming\Typora\typora-user-images\image-20210128154451058.png)

The quality scores are ascii representations of a hexadecimal number. The numbers are based on something called the Phred scale. For each base, there is a program that guessed whether that base was a A/T/G/C. The computer encodes the liklihood of error at that base as the quality score. 
$$
Q = -10\ log_{10}(P_{err})
$$
![image-20210128154808694](C:\Users\benfy\AppData\Roaming\Typora\typora-user-images\image-20210128154808694.png)

Places the error probability on the logarithmic scale. Since the numbers are always integers, the corresponding ascii character is in the fastq file. 

###### PacBio Sequencing (3rd Generation Sequencing)

We are now on 3rd Generation Sequencing. This tech is more expensive but can generate much longer reads (around 20,000bp long). 

Works with flow cells which this time are super small pores that hold single strands of DNA. At the bottom of the well is a single DNA polymerase molecule. Once it starts feeding through the polymerase, there are fluorescently tagged A/T/C/Gs as before. The tags will fluoresce once when a light shining through the well hits the fluorophore. The fluorescence pattern is then recorded per base added. 

"Eavesdrops On the Activity of the Polymerase"

Has a much lower accuracy than Illumina. Error rate at around 15%. But, you have very long reads, so you should be able to compare. Illumina has <1% error rate on the other hand. 

###### Genomes and Genome Assembly

Today, 10s of thousands of genomes have been sequenced. Once DNA has been sequenced, the reads need to be assembled. 

## 02/02/21

### Genome Assembly Continued

When Assembling a genome, we have paired reads where we have both ends of the fragments are labelled. We then have reads that overlap. An assembler identifies the sequences that overlap.

Sequencing Gap - We know the order and orientation of the contigs and have at least one clone spanning the gap

Physical Gaps - We dont know anything about because we dont have any contigs or fragments to bridge the gap.

A contig is a region of the sequences that have many overlaps. A 

We assemble the fragments into contigs, then the contigs get assembled into contigs.

###### Lander-Waterman Statistics

Developed to figure out how many bases we need to sequence to put together useful contigs.

The coverage of a genome is the number of reads that overlap at a given point in the DNA sequence. The coverage is distributed randomly. 

A contig is an island with two or more reads. 

![image-20210202151226885](C:\Users\benfy\OneDrive - Johns Hopkins\Documents\Markdown Notes\.images\image-20210202151226885.png)

Where E(x) is expected value. 

T is the minimum amount of overlap to say that the reads actually came from the same place in the genome. 

c is number of reads, times length of reads, divided by the size of the genome. 

s is just a derived number that is useful. 

This assumes that the reads are perfectly uniformly distributed. This model was developed for random shotgun sequencing.

Up at about 1.7x coverage, the number of contigs decreases. Up around 10x coverage, we can get one contig that is essentially the chromosome that was sequenced. 

This analysis assumes there are no errors in the reads and that the alignment algorithm is infallibly for the sequences of length T.

Most projects get about 8x coverage historically in the late 90s and early 2000s. Now we can do way better than that! Basically can ensure we only have a few contigs that aren't connected!



###### Where are we today?

Only 20 animal and plant genomes are finished today. The largest is at 40Mb fungus. We have been trying to finish the human genome since around 2001. When it was published it was 90% complete and in 100s of 1000s of pieces. We can see from the human genome assembly data that the assembly actually isn't complete. The reason that we still haven't finished the genome is because there are small repetitive sequences that can appear thousands or millions of times. It's hard to assemble DNA that has a ton of repeats because our assembler would identify many points in these sequences as identical even though they're from distant regions. 

The T2T consortium is an effort to finish the human genome. The Ts are the Telomeres which are repetitive short sequences used to pad the ends of the genome. This consortium wants to sequence from one telomere to the other. To do this they are employing very long reads. 

They are using hydatidiform mole cells which are unfertilized eggs cells that spontaneously began developing. They are haploid and have two identical copies of each chromosome rather than two chromosomes that are slightly different copies. 

Celera was a company that worked on completing the human genome project. This company was formed by Applied Biosystems to race the international effort to sequence the human genome after the creation of the capillary sequencer. Once Celera entered, the speed of the race was increased and resulted in an earlier than anticipated completion. They were proud to announce that they could produce 100Mb per day.

Today, the Oxford Nanopore which is a handheld device can do more than an entire factory floor could at the time. One run of a HiSeq 4000 can produce over 1000Gb in around 4 days. The maximum read length is around 150bp in paired reads. A single HiSeq 2500 in 2015 had over 1000 times the sequencing power of Celera's entire factory in 2001.

###### Shotgun Sequencing

Start with library, shear it into many pieces, select size desired, ligate and clone the DNA into a vector. Then sequence the vector. 

###### TIGR Assembler and phrap Assembler (1990s)

They are Greedy algorithms - apply things that are easy to compute and maximal and do that first. Build a rough map of fragment overlaps. Picks the largest scoring overlap. Merges the fragments and repeats until no more merges can be done. 

![image-20210202154047424](C:\Users\benfy\OneDrive - Johns Hopkins\Documents\Markdown Notes\.images\image-20210202154047424.png)

Because we look at data from two not necessarily identical chromosomes, we want to look at the percent identity that we will accept for the two to be called identical. 

We can look at the fragments as nodes and overlaps as edges between the nodes. We can then create a graph that uses the edges to represent the overlaps so we can apply algorithms from graph theory to compute overlaps more efficiently. 

Once we have a number of overlaps from high coverage, the consensus will use quality values and number of individual base reads to calculate the identity of the base at each position.

*Assembly is a graph problem*

A Hamiltonian circuit visits every node in the graph exactly once. Finding these paths is an NP complete problem so is computationally intensive. If we could find the path that connects the reads, we would have the assembled genome. 

*How many overlaps are there*

Look at all pairs of reads at least once ${n}\choose{2}$ there are theoretically this many overlaps. 

The number of pairs that actually overlap should just be $N\times coverage$

Build a table of sequences of length k (k-mers).

Generate pairs from the k-mer table by taking a single pass through it. Use the reads that likely overlap from the table to expose to the more computationally intensive computation. 

*Trimming*

Need to trim off adapter sequences. 

Overlap Based Trimming (OBT): Computes local alignments ("partial overlaps") between untrimmed reads. If two reads align and only mismatch at the very beginning and very end, the algorithm can trim them. 

*Error Correction*

Even at 0.5% error rate of Illumina sequencing, there are still errors in very large libraries. When correcting errors, after the alignment can look at all the bases at a given locus and can weight based on the number and quality of other bases at a given point.

Once error correction is performed, the reads are adjusted and the assembler realigns that read which can improve the assembly.

*Assembler Errors*

Collapsed Tandem:

When there are identical repeats in a DNA region, the assembler may tend to collapse the repeats to appear as only one copy of the repeat at one position in the DNA which is incorrect. 

![image-20210202155804611](C:\Users\benfy\OneDrive - Johns Hopkins\Documents\Markdown Notes\.images\image-20210202155804611.png)

Excision:

If you have 3 regions of DNA in sequence with a repetitive sequence surrounding region 2, the assembler may align the repeats and excise the middle region. This would be erroneous as well. Results in chopping out a piece and you don't know where it goes.

![image-20210202160013623](C:\Users\benfy\OneDrive - Johns Hopkins\Documents\Markdown Notes\.images\image-20210202160013623.png)

Rearrangement:

Again, if you have 4 segments separated by repeat sequences, the alignment might misplace the segments because they're identical. 



Overlap Graphs:

Represent the overlaps as graphs as well. Repetitive overlaps get trimmed to simplify.



###### Diploid Genomes

Our chromosomes are not identical. This is why we are using bacterial genomes. All of our assemblies represent a genome whether it comes from one genome of two.

When the assembler is processing data from a diploid genome, it may mistakenly form two contigs from the two chromosomes. If a contig is a heterozygous locus, we should merge it into the other contig. The heterozygous loci match but not super well so the assembler may mark the contig as not being the same even though it should be.