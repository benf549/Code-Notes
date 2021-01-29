# TA Office Hours

### Programming Review

###### Unix

On piazza, there is a unix review powerpoint we can check. 

`pwd` prints working directory

`cd` moves between folders. `cd /` moves to root directory. `cd ~` moves home. 

`ln -s file_path .` creates a symbolic link to the original file without copying it as files like these can be very large. 

`samtools faidx file_name.fna` creates `.fni` file which describes the index (what is in the .fna file.

`cut -f2 file_name.fai` will cut the second field of the file. 

`awk '{sum+=$2;} END{print sum;}' file_name.fai` prints the sum of the second column. 

`sort -nk2 file_name.fai` sorts lines viewing the second column as a number.

**TMUX** is already installed on the server. 

`tmux` command can be used to create persistent terminal sessions that persist even if you get disconnected from the server. 

