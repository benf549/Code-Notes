# Problem Set 1

### Genomic Data Science - Spring 2021

*Benjamin Fry*

*JHED: bfry2*



##### Assembly Summary

My assembly resulted in `3` contigs with a total length of `5519570 bp`. The N50 of the scaffolds is `5337609` and the mean coverage is `23`. This result is promising as the reference genome we were provided has 1 chromosome with 2 plasmids. Since there are 3 contigs and 3 scaffolds, the contigs are not connected. The chromosome and plasmids are not continuous regions of DNA in the cell so we would not expect the alignment to connect the three contigs. One of the contigs was significantly longer (`5337609 bp`) than the others (`110374 bp` and `71587 bp`) as is the chromosome in the reference genome. Furthermore, the assembly info reports the contigs are circular which is also as we would expect from plasmids and bacterial chromosomes. Because of these similarities, we can be confident that the assembly was successful.



##### SNPs and Indels

The alignment produced `108` SNPs and `18` indels.



##### N50 Size of ONT Reads

I found that N50 size of the `trimmed_ONT_reads_genome01.fastq` file to be `17033 bp`.

