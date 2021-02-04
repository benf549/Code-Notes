# MaSuRCA

### Genome Assembly and Analysis Quick Start Notes

`/install_path` is the directory where `./install.sh` was run so I assume the folder on the server. No pre-processing should be done before feeding data to MaSuRCA

##### Configuration File

Need to create a config file with the location of the compiled assembler, the location of the data, and some parameters.

Make an assembly directory and copy the `sr_config_example.txt` into it. Many projects will only need to set the input data paths in this file without modifying anything else. 

###### DATA

This section, specify the types of data available for the assembly. Each line is a library and must start with PE, JUMP, or OTHER. There can be multiple lines that start with `PE` or `JUMP` with one line per library. the PE and JUMP data must be in fastq format. Give each library a unique two letter prefix.

For Illumina Paired-End data add

`PE = two_letter_prefix mean stdev /PATH/fwd_reads.fastq /PATH/rev_reads.fastq`

The assembler will recalculate the mean and stddev so you just have to ballpark them. We will set mean to 2xREAD_LENGTH and stddev to 15% of that. 

For Nanopore reads add

`NANOPORE=file.fa`



###### N Statistic

Given a collection of random DNA strings. the N statistic takes the form `NXX` where `XX` ranges from 01 to 99 to represent the positive integer $L$ such that the total number of nucleotides of all contigs have length $\ge L$ is at least `XX%` of the sum of the contig lengths. 



 