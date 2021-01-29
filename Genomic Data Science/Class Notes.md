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

###### Genomes and Genome Assembley

Today, 10s of thousands of genomes have been sequenced. Once DNA has been sequenced, the reads need to be assembled. 

