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



## 02/04/21

### Genome Assembly, deBruijn graphs, and more

Why is genome assembly a hard problem? It is a very large scale computing task. The most computer-science-y thing out of all of genomics. Next generation sequencing data can produce > 5,000,000,000+ reads. With billions of reads, reads have gotten shorter. Even though we had more reads, the assembly problem actually got harder.  The basic operation in assembly is finding overlaps. When sequences match, a consensus is taken and weighted by quality to identify the identity of the base at that location. With 5 billion reads, this would be 12 quadrillion comparisons. 

##### De Bruijn Graphs

Think of every word of length k-1 as an edge on a graph. For every read, find every read of a given length and link that k-mer with an edge representing a k-1 word. 

![image-20210204151111493](C:\Users\benfy\OneDrive - Johns Hopkins\Documents\Markdown Notes\.images\image-20210204151111493.png)

Why use this technique?

The first sequencers as the ones we talked about (Tigr), represented each read as a graph with nodes connected by their overlaps. 

These graphs appear to have one node for every k-mer in the genome. There are 3 billion different kmers for a mammalian genome. When you have millions of reads, this is way more expensive. However, when you get into the billions of reads, you get to the point where this model has less nodes than reads. 

Now you have a read that is broken up into a bunch of nodes and need to walk along the path to reassemble the node. 

![image-20210204151629585](C:\Users\benfy\OneDrive - Johns Hopkins\Documents\Markdown Notes\.images\image-20210204151629585.png)

Breaking up the intro to a tale of two cities in above example. Has lots of repetitiveness. A unique Eulerian tour of the graph reconstructs the original text - this is a graph that hits every node in the graph exactly once. Unlike the Hamiltonian path problem like the other data structure, an Eulerian tour can be found in linear time. 

If there is no obvious tour, you can try to simplify the graph. 

Early assemblers that used this technique required 2TB of ram but they have gotten much more efficient. 

The next-gen data is short with high coverage, Illumina sequencers have trouble sequencing areas with low GC content. 

>Question for a genome project:
>
>How much sequencing coverage do I need?
>
>Which assembly software should I use?
>
>How accurate will the assembly be?
>
>
>
>To quantify the abilities of the various assemblers, they have looked at some genomes and compared the assemblers.  To test them, they used long reads and short reads. 
>
>When you look through reads and density of k-mers plotted as function of coverage,  most-kmers appear at about the coverage of the data. However, there is always a massive peak of kmers that appeared once or twice due to errors from the sequencer.
>
>You can use a cutoff to go through the k-mer and check if swapping each of the bases places it in the middle of the bell curve. 
>
>Comparing the assemblers, 4 of them are De Bruijn assemblers and the other 4 are not. 
>
>N50 size is a way to compare the quality of the genome. 
>
>Look at what half the genome length is. Sort data from biggest to smallest, added their lengths cumulative. Once the sum is greater than or equal to the XX% of the length, that value is the N50. Larger is good. 
>
>This is useful for the output of an assembler and also for the reads from sequencers like ONP which can also be sorted by length.

A dot plot is when you plot one genome assembly versus another or the truth. You pick a short sequence length, and see where that sequence on one contig occurs on another contig. You would expect the graph to look like $y=x$. However, different errors on the test contig look different. 

### Code Review

#### Unix, Commands, and Python Basics

You can use any language for the assignments but python is probably easier.

Python is probably not the best when you need to worry about memory management. 

Recall in unix:

`wc` counts words

`sort` sorts the input

`uniq` takes a sorted file and removes repeats

`cut` extract only a certain column

`grep` finds lines containing pattern match

`Top/Htop`: will tell you what's going on in the server's memory. Useful if you have a really slow program.

`TMUX` allows you to have multiple terminals open that are persistent if you get disconnected from the server. 

`shuf` shuffles data randomly

`|` allows command chaining ex: `grep ">" reads.fasta | wc -l` 

`cut -d'\t' -f1 annotation.gtf | sort | uniq -c` gives the number of scaffolds in the genome annotation file.



`awk`:

Print only transcript coordinates from annotations: `awk -F '\t' '$3=="transcript" {print $4,$5}' annotation.gtf`

Sum a column: `swk '{sum+=$1} END {print sum}' file.txt`



Python Review

Probably want to write headers that describe a program. Put name, class, data, inputs/outputs and basic function

Annotate code blocks with comments. 



To take input from standard input

```python
import sys
for line in stys.stdin():
    line = line.strip() # best practice to strip every line to remove newlines that might mess stuff up
    [val1, val2] = line.split("\t") # splits columns
```



Main method

if executing the script from command line, executes the main function but wouldn't execute if you imported it from another function

```python
import sys, argparse

def main():
    pass

if __name__ == "__main__":
    main()
```



Command Line Input:

```python
#python my_prog.py < infile.txt > out.txt

sys.stdin and sys.stdout are used to read and write  to /from standard in and out
if Error:
    sys.stdout.write("Usage: python my_prog.py infile.txt ooutfile.txt\n")
```

Other options are sys.argv and sys.argparse



## 02/09/21

Assignment 2 Is Posted. We will be annotating the genome we assembled. Annotation is needed for a genome to be of any use for people studying the genome. We will use a program called glimmer to do this. Glimmer is a machine learning program that will be trained on the assembly itself.

We use gene to mean a protein encoding gene. To make things simpler, we will use the main >5Mbp chromosome. 

The glimmer output needs to be converted to a more standard format which we can use to spit out the protein sequences from the predicted genes. We have the Klebsiella known proteins and will use Mummer to align all of the protein sequences to all of the known sequences. 

### Assembly Wrap Up

#### Example of Recent Assembly Project

Their lab worked on the Sequoia tree's genome which is the largest tree on earth with an 8.2Gbp genome and they are working on the Red Wood which has even larger DNA. The trees can be hexaploid in that they have 6 copies of each chromosome per cell which makes sequencing very difficult. They sequenced the seeds (haploid) with both Illumina and ONT reads to do a hybrid assembly. The genome is so large that doing just small Illumina reads would not produce a good assembly. They got >100x Illumina coverage and 22x ONT coverage. The N50 was 9500bp.

The scaffolding algorithm they used is called Hi-C. Hi-C technique makes the DNA stick together when the DNA is in the cell as it does naturally. Then you get pieces of DNA that were physically adjacent usually within the same chromosome. The DNA is then broken up and the linked fragments are then identified as being from the same place. There are more links on parts of chromosomes that are nearby. The more links, correspond to a higher likelihood of contigs being close together. After assembly with MaSuRcA, they used the Hi-C reads to scaffold the assembly together. 

Every chromosome has a centromere which is a millions of bp long 100bp repeat in the center of the chromosome. Telomeres are very long repeats of 6-7bps. Errors in chromosome assembly can be identified when centromeres are at the beginning and end or when telomeres are in the center. 



Assembly of Ancient DNA:

DNA is remarkably stable when preserved. Freezing can preserve it for millennia. The mitochondrial genome can be preserved even longer because it is circular and has many copies per cell. 

### Bacterial Genome Annotation

We have a genome assembled now, what do we know about it?

Genes tend to be about 1000bp long

We observe a linear trend that correlates the genome size and the number of genes for bacteria. This does not work at all for eukaryotes. 

Humans have probably around 20,000 protein encoding genes. We are not end-to-end genes unlike viruses and bacteria. The coronavirus has around 29 genes. 

When DNA is read, the genetic code dictates what protein corresponds to each codon. 

Open Reading Frames. Read from one Stop to the next Stop. The ORF is defined by what base you start on and where you read from. You also have to look at the 3 reading frames on the complementary strand. For any part of the DNA, there are 6 reading frames in which you can go stop to stop. 

The stop codons are TAA, TAG, and TGA. Regions of DNA that have low GC content are more likely to have high AT content. In a low GC genome, when you're in the wrong reading frame, you have a lot of stop codons. Therefore, the longest ORF is most likely to be the true genes. 

However, high GC genomes have less stop codons and picking the longest ORF doesn't really work anymore. 

To identify where the genes are, we need to know where the Start codons are. The start codons must be within the stop codons. 

We use machine learning to identify the known genes. Feed a model data about distribution of nucleotides at the 3 codon positions. Look at hexamers. Look at amino acid composition. Look at ORF length.

Most codons are redundant and most organisms have a typical GC content. We can look by reading frame and identify percentage of each base at the position in the codon. For a low GC content organism, choose the codon position that minimizes GC percentage. If a high GC codon, choose the codon that maximizes the GC content. 



###### Markov Chains

Used by Glimmer. A chain of events that once an event is seen, can be used to predict what the next event will be. Dictated by Bayes' Law
$$
P(a|b) = \frac{P(b|a) P(a)}{b}
$$
Modeling Start Codons. If we have frequencies of the start codons in a gene. Say 4 probabilities corresponding to each codon. We use the probabilities of each codon to build a model based on the empirical data. If we have a codon and we want to identify which model it applies to. Want to know probability of M1 and M2 given a sequence X. So, we use Bayes' law to convert the probabilities to probability we want. 

Markov Chains work by assigning the probability of any character being independent of previous characters after a certain order. We can compute the probabilities of combinations of events just by multiplying. 

We make a prediction from the current state only. Can be written out as a chain of nodes representing states and edges representing probabilities of traveling between states. 

Training a Markov Model

Compute the probabilities from the data. Based on conditional probability. If you want probability of C given T in previous position, count all the Ts in the data and see how many have a C after them. Then you can calculate the probability. 



## 02/11/21

### Markov Chains Continued

A Markov Chain is just a way of modeling the likelihood of an event based on where you are in the procedure at the moment. Basically a bunch of computed conditional probabilities. 

Markov models are just sets of probabilities. They have order, the 0th order is the probability of being at the current position. The first order is the probability of a given base given the previous base. second order is the same given the second base and so on. 

0th order model score is just probabilities of each base multiplied together. 

1st order model score is the multiplication is first base from 0th order times the probability of the current base given the previous base and so on to the end of the sequence. 

Markov assumes the current position is independent of everything else except to a certain number of residues which can be multiplied. 

Markov Model make is very easy to score the chains.

An Nth-order Markov Model requires 4^n+1^ probabilities for DNA and 20^n+1^ probabilities for Amino Acids



#### Markov Chains

Each position in a DNA sequence is a state. The probabilities are the same in every state for a 0th order chain.

When using for bacteria and viruses, 5th order chains work very well. GeneMark uses these

Why 5th order? Because GeneMark is looking for protein coding DNA, there is useful information in keeping track of the codons. A codon is 3 bases. The model is predicting a sixth base based on the previous 5 codons. 

The problem with higher order chains is that each requires an exponential 4^n+1^ probabilities which is computationally expensive. The genome just isn't large enough to see all of the nth base combinations of bases. 

##### Scoring A Sequence with a 5th Order Markov Chain

#####  ![image-20210211151754584](C:\Users\benfy\OneDrive - Johns Hopkins\Documents\Markdown Notes\.images\image-20210211151754584.png)

The probabilities are super small so to avoid underflow, convert each probability to a logarithm and add them for the same effect to avoid zeroing out the sequence probability.

When scoring the sequence, 

##### Nonhomogeneous Markov Chains

More advanced programs like Glimmer can have different probabilities if they are aware of the codon positions that A, C, T, and G can occur in per codon. Therefore, you'd have 3 sets of probabilities per triplet in the ORF. 

Allow the program to vary the number of previous positions that the model looks at based on the codon being looked at. It may be that this happens to work better than always using a 5th order markov model.

##### Interpolated Markov Model

Uses a weight function to calculate the probabilities for models of different orders. 

This is interpolating the results of the different order models. 

Now glimmer uses Interpolated Context Models which don't necessarily use the bases right next to the target. It could theoretically pull from bases anywhere in the sequence that are most informative for the call.



#### Overlapping ORFs

When you have two ORFs that overlap, this isn't possible, therefore you need to make calls as to whether to accept one or reject it. We don't want to predict that genes overlap. The ORF scores each reading frame. The model looks at the overlapping region and scores that. It then picks the higher scoring reading frame. 

We don't want to throw away long reading frames though, gimmer used to just leave a flag that says that the overlap scored higher in the reading frame but didn't want to throw away the larger gene. It is possible for the model to just move the start codon over as well. 

##### Overlapping Genes

It is possible for genes to actually overlap in bacteria. Something around 15% of all genes in prokaryotes overlap. They found that around 29% of the genes in bacteria overlapped on at least one end.

It is possible for genes to lose their stop codon to mutation. Polymerase would then keep reading until a stop codon is eventually reached. 



#### Translation

Genes start with AUG and have a Ribosome binding site just before the start codon which you can also look for in the Markov Model. Glimmer will run through the data and look for the genes it called and look right before them to find a ribosome binding site. Then it bootstraps by running again, looking for the pattern it found that is likely the ribosome binding site. 



### Glimmer Homework

We will run the Long-Orfs program that finds the orfs longer than min0length that do not overlap other such orfs. It finds this min-length automatically. 

This works well for low to medium GC content genomes but does not work very well for high GC genomes. Glimmer3 can do better now. 

![image-20210211154753095](C:\Users\benfy\OneDrive - Johns Hopkins\Documents\Markdown Notes\.images\image-20210211154753095.png)





## 02/16/21

`MUMMER` is an aligner that contains a lot of different useful packages. What is whole genome alignment. For two genomes A and B, find a mapping from each position in A to its corresponding position in B. When he was sequencing the tuberculosis genome they needed a way to compare two sequences. 

Genomes can change over time. SNPs and mutations vary by individual. 

Plots can visualize alignments with an identity plot which shows identity (percent similarity) as a function of position along the genome. If we want to look at changes, we can use dot plots. We have the genomes in a matrix NxM where rows are the position in genome A and j are the position in genome B. We plot the matrix by filling in a dot at (i,j) if A and B are identical. If A and B are identical, you just get a straight line from zero to N, N.

Here are the patterns for the various types of changes between chromosomes. 

![image-20210216151144577](C:\Users\benfy\OneDrive - Johns Hopkins\Documents\Markdown Notes\.images\image-20210216151144577.png)

Here the pink part and the blue part were swapped in B. 



### Alignment

Once we have assembled genomes, we compare them to reference genomes with alignment. We want to do a whole genome ideally, but we can't really do this because there are so many changes between large genomes.

To compensate, we have to use small pieces at a time. 

When we use Whole Genome Alignment, we do synteny analysis which looks at evolutionary conservation of large chunks of DNA, polymorphism detection, and sequence mapping.

Multiple Genome Alignment identifies conserved sequences between species. 

Multiple Alignment allows us to figure out the evolutionary history of all species. 

Local Alignment allows us to identify similarities in small sequences between species like protein alignments. 

Mummer stands for Maximal Unique Matcher. 

* A match is an exact match of some minimal length
* Maximal gives the longest sequence that is bounded by mismatches
* Unique occurs only once in both sequence 
  * A MUM is exact match with no repeats while a MEM (Maximal Exact Match) allows repeats. MUMMER can find both. 

The exact match criteria makes it difficult because the sequences have to be exact. Uses a Seed and Extend strategy - finds an exact MUM, then extends the matches and tries to connect them. Finds all MUMs and clusters consistent MUMs. Extends the alignments between the mums and fills in between them. This is done by the `nucmer` program that we will run that is in the Mummer package

Uses a data structure called a suffix tree for sequence alignment. Makes a tree of all ends to the string. Includes the string itself, its last character, and then all of the other endings starting from different positions within the sequence. 

To build a suffix tree first put the whole string in, then look from second index, and add to tree. Since it starts with another letter, add a new edge. Then put third index in and split the side of the tree if the first few characters are shared between existing nodes and the new nodes.  

#### Clustering

Sums cluster length and can calculate the indel factor that separates clusters. Score the alignment based on difference. The alignment can be done with the Smith-Waterman algorithm. Nucmer uses Banded alignment to align the sequences. 

The seed and extend algorithm may not work when sequences are highly divergent, yet are homologous. Many conservative substitutions may result in the same protein sequence with highly different DNA sequence. DNA may not align well, but proteins do. It is more useful then to sequence the proteins and align those. `promer` translates the DNA in all 6 reading frames and aligns the proteins and maps the alignments back to the protein sequence. 

![image-20210216155223939](C:\Users\benfy\OneDrive - Johns Hopkins\Documents\Markdown Notes\.images\image-20210216155223939.png)

![image-20210216155241432](C:\Users\benfy\OneDrive - Johns Hopkins\Documents\Markdown Notes\.images\image-20210216155241432.png)

NUCMER is hundreds of times faster than BLAST.

MUMMER/NUCMER helps identify differenced between alignments.



For the homework, we will align proteins. To figure out protein names, we align to reference genome. 

## 02/18/21

### Genome Organization in Bacteria

#### Operons

In bacteria, there are genes that can be co-transcribed meaning some genes can be transcribed more than one at a time. Genes can generally be transcribed in units called operons. The genes are transcribed onto a single piece of RNA. This generally doesn't happen in humans, but generally does in bacteria. The amount of the gene that the cell produces of that gene is pretty much the as all of the other genes on that RNA strand. 

When the genes are connected by transcription, they are generally biologically related as well. 

Polymerase will stop transcribing when it reaches a termination sequence. Operon genes must face the same direction. The polymerase binds at the promotor.

We can find these operons computationally by looking for a promotor and terminator sequences between genes in the same direction. There are also intrinsic terminators which are not consistent sequences. These work by forming hairpin loops which are the DNA binds back onto itself even if the bases aren't perfect matches. This forms a loop of a few bases that are followed by a sequence of T residues. We can look for sequences that fit this description. When polymerase reaches the line of many T residues, it can recognize that it has passed a loop and will fall off ceasing transcription. 

To find intrinsic terminators, we score regions for having a sufficient number of T residues and score the energy of the residues predicted to bind eachother and forming the loop. 

They created a program that can find operons called TransTerm. 

### Phylogenetic Trees

Molecular evolution studies the changes in genes, proteins and genomes to understand how things have evolved over time. Phylogeny is the inference of evolutionary relationships. This is all done with molecular sequence data basically. 

Sequence alignments of globin genes between animals were aligned and scored based on distance between the animals. This was done first by Margaret Dayhoff. This would be a tree of orthologs. You could also make a tree of paralogs that compare similar proteins across and within species. Paralogs are those that are related within the same organism. 

Protein sequences evolve at a constant rate based on the freedom they have to evolve in their structure.

Positive selection is when traits that enhance survival are selected for, negative selection traits that harm you are selected against. 

**I fell asleep....**



## 02/23/21

More on phylogenetics and virues

### Phylogeny Continued

How are trees built: 

There are a many different algorithms for computing phylogenetic trees. For tree building methods like UPGMA, use a distance metric such as nucleotide differences between MSAs. Calculates the pairwise alignments for each sequences. The lowest distances are grouped. Can use clustering algorithms to identify closest groups and distances from groups to other groups. UPGMA trees are always rooted. It makes the assumption that molecular clocks are constant in sequences for the tree which isn't always true necessarily. 

Neighbor joining connects neighbors creating an unrooted tree.

Maximum parsimony looks at differences between columns in an MSA - character-based methods. Consider all possible ways to make a tree and then minimize the cost/number of features. 

You can also use maximum likelihood estimation with a model of mutation likelihoods. 

### Viruses

Viruses mutate fast enough that we can observe evolution and build phylogenies for them and know when we are correct.

The flu genome is an RNA virus that had 8 segments with particles around 1 to 2 microns. The virus was not discovered until the 1930s because they only knew about bacteria back then. Needed a more powerful microscope to see it. 

Has Hemaglutinin and Neuraminidase on its capsid which adhere to cells. Injects its 8 RNA particles into the cell, RNA Polymerase converts the RNA to DNA. The virus RNA is negative strand so the positive strand needs to be created to be translated to proteins. 

We can use Reverse Transcriptase to copy the RNA to DNA and PCR that sample to sequence it. 

## 03/02/21

Project 2 is due March 12th. Data is from Illumina MySeq. All can be run locally, but its installed on the server. 

### Metagenomics

DNA is extracted directly from all microbes extracted from the environment. 

The Human Microbiome Project is an effort to study the microscopic things that live on and inside the human body. 



### Week 8 - Tues

 