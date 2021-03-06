# Lab 1, Report 2: Annotation of *Klebsiella pneumoniae*

## Benjamin Fry - JHED: bfry2

*02/23/21*



### Part 1:

I documented all of my terminal commands in the file shellcommands.txt for your convenience. I followed the directions given up through running glimmer and then set to converting the glimmer output to the desired `gtf` format. I wrote my glimmer output to `gtf` converter in python and named it `problem1ci.py` This program takes a prediction file generated by glimmer though standard input and writes the conversion to standard out. To use this program you run `./problem1ci.py < filename.predict > filename.gtf` where the `.predict` file is produced by glimmer. The output of this program is the `gtf` conversion for each line of the prediction file with the seqname set to whatever the most recent `>` prefixed line was, the format and feature type hard coded as `glimmer` and `cds` The start, end, score, and strand direction are then pulled from the prediction file and the frame is hardcoded to `.` to account for bacterial genome.

To convert the output of Mummer to GTF format, I wrote the converter in python as well. It takes in 3 command line arguments and is run as follows `./problem1dii.py reference_proteins.faa output.mummer output.gtf` where `output.mummer` is the output from the mummer run and `output.gtf` is the `gtf` file that was generated from running the `problem1ci.py` program as described above. The program outputs the processed annotation in `gtf` format where the seqname, start, end, and direction are obtained from the previous `gtf` file, the source is set to the ORF name like in the example, and the line ends with the ORF's match to the reference genome with its description or `match=none` if there was no match. When running this to complete the homework assignment, I stored the output in `annotation.gtf`



