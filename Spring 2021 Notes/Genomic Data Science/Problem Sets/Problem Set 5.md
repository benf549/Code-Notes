# Problem Set 5

*Benjamin Fry - 04/15/21*

All the commands I used to generate my results are documented in `ps5_commands.txt` for your convenience.

## Part 1: Human Samples

I created a script called `Part1.sh` which runs HISAT on the 12 input files, counts the mapped and unmapped reads for each input file and writes the findings to `number_map_unmap.txt`, as well as counts the number of spliced alignments and writes the findings to `number_splice_aligns.txt`. 

The file to which the counts of mapped and unmapped reads were written is as follows:

```
file: mapped unmapped
ERR188044_chrX.sam: 2523279 119675
ERR188104_chrX.sam: 2481663 103023
ERR188234_chrX.sam: 2972648 162680
ERR188245_chrX.sam: 1646813 65153
ERR188257_chrX.sam: 1827283 93537
ERR188273_chrX.sam: 1110577 49507
ERR188337_chrX.sam: 2459086 96536
ERR188383_chrX.sam: 1870994 57940
ERR188401_chrX.sam: 2540148 94918
ERR188428_chrX.sam: 1623884 62520
ERR188454_chrX.sam: 2014469 67177
ERR204916_chrX.sam: 2110026 84970
```

where the first line is a header indicating what each column represents, the first column being the file that was used to generate the counts, the second column being the number of mapped reads, and the third being the number of unmapped reads. 

The code used to generate these outputs is the second block of `Part1.sh`.

The number of spliced alignments is contained in the file `number_splice_aligns.txt` and the contents of it are as follows:

```
file: number of spliced alignments
ERR188044_chrX.sam: 731658
ERR188104_chrX.sam: 666925
ERR188234_chrX.sam: 855555
ERR188245_chrX.sam: 449293
ERR188257_chrX.sam: 489416
ERR188273_chrX.sam: 305089
ERR188337_chrX.sam: 651933
ERR188383_chrX.sam: 488030
ERR188401_chrX.sam: 704130
ERR188428_chrX.sam: 448507
ERR188454_chrX.sam: 522094
ERR204916_chrX.sam: 578269
```

where the first column is the file that was used to generate the number of spliced alignments and the second column is the number of spliced alignments contained in the file. The code used to generate this is found in the third block of `Part1.sh`.

## Part 2: *S. pombe* Samples

Again, the commands I ran to generate these data are documented in `ps5_commands.txt`. 

My findings using the *S. pombe* data are summarized in the table below:

| HISAT Settings               | No. Mapped Reads | No. Unmapped Reads | No. Spliced Alignments |
| ---------------------------- | ---------------- | ------------------ | ---------------------- |
| Default                      | 4662226          | 330624             | 162990                 |
| Canonical Splice Penalty (5) | 4655178          | 337672             | 153873                 |



The parameter I changed for the HISAT alignment, was the Canonical Splice Penalty. I changed this from the default of 0 to 5. As a result of doing this, there was a slight bias introduced against creating spliced alignments and this manifested in the counts as a reduction of 9117 fewer reads being called as spliced alignments.  Since they didn't get spliced, around 7,000 of these reads, did not align to the index and became unmapped when they were mapped with the default parameters. Thus, around 2,000 reads were still mapped despite not being called as spliced alignments. This makes complete sense as we would expect penalizing calling canonical splices would result in fewer splices and fewer mapped reads as a result.