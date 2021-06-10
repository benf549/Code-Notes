# Problem Set 6

*Benjamin Fry - bfry2 - 04/30/21*

All the commands I used to generate my results are documented in `ps6_commands.txt` for your convenience. As mentioned in that file, the commands I used to generate all the data files following the procedure were first executed as contained in `RunStringTieProtocol.sh`

## Question 1

The script `CountAllTransFPKMS.sh` answers the question of how many transcripts are expressed with an FPKM `>= 0.1`. Here is the output:

```
Sample,		FPKM Count
ERR188044,	1911
ERR188104, 	1822
ERR188234, 	1853
ERR188245, 	1691
ERR188257, 	1749
ERR188273, 	1537
ERR188337, 	1884
ERR188383, 	1723
ERR188401, 	1884
ERR188428, 	1685
ERR188454, 	1768
ERR204916, 	1842
```

 

## Question 2

The number of transcripts with an FPKM `>=0.1` in at least one of the samples avoiding double counts is given by the script `./count_at_least_one.py` the output of which is here:

```
Number of Transcripts (FPKM > 0.1) in at least one:
2489
Number of Distinct Genes Represented:
734
Transcript With Highest FPKM (332957.28125) Across All Transcripts:
NM_021109
Value in each Sample
ERR188044, 293214.375
ERR188104, 295023.8125
ERR188234, 332957.28125
ERR188245, 239437.609375
ERR188257, 331374.34375
ERR188273, 322207.03125
ERR188337, 246929.078125
ERR188383, 266242.8125
ERR188401, 309042.09375
ERR188428, 279080.8125
ERR188454, 263732.75
ERR204916, 218461.6875
```

so according to this output there are `2489` such transcripts.

## Question 3

The script above also calculated the number of known/reference genes that are represented that are distinct (avoiding double counts), so according to the output above there were `734` such genes.

## Question 4

The transcript with the highest FPKM is also calculated in the previous script output. The highest FPKM that I measured was `332957.28125` which corresponded to the transcript `NM_021109` which had the reference gene name `TMSB4X`. The value of this transcript in each of the samples is also outputted above but here it is again:

```
Value in each Sample
ERR188044, 293214.375
ERR188104, 295023.8125
ERR188234, 332957.28125
ERR188245, 239437.609375
ERR188257, 331374.34375
ERR188273, 322207.03125
ERR188337, 246929.078125
ERR188383, 266242.8125
ERR188401, 309042.09375
ERR188428, 279080.8125
ERR188454, 263732.75
ERR204916, 218461.6875
```

## Question 5

Here are the two tables I generated following step 16 in the protocol:

```
     geneNames   geneIDs    feature   id          fc         pval         qval
1658         . MSTRG.528 transcript 1658 0.030734570 1.552551e-10 2.409145e-07
1657      XIST MSTRG.528 transcript 1657 0.003001388 2.189797e-10 2.409145e-07
1656         . MSTRG.528 transcript 1656 0.016007921 3.235199e-10 2.409145e-07
1659         . MSTRG.528 transcript 1659 0.028411794 6.867990e-08 3.835772e-05
1655      TSIX MSTRG.527 transcript 1655 0.078000276 1.846819e-06 8.251588e-04
1849         . MSTRG.613 transcript 1849 7.322833968 1.261251e-05 4.696060e-03
1853         . MSTRG.619 transcript 1853 9.166330666 4.887834e-05 1.559917e-02
422          . MSTRG.142 transcript  422 3.030351803 7.085958e-05 1.978754e-02
736      KDM6A MSTRG.258 transcript  736 0.054840545 1.212793e-04 3.010423e-02
187     PNPLA4  MSTRG.67 transcript  187 0.592080152 2.105663e-04 4.704052e-02
```

the above table compares to table 3 in the protocol which shows the differentially expressed transcripts between sexes with q values less than 0.05. This table differs from the table shown in the protocol in that my table does not report the transcript name as a column, and the order of the rows are slightly changed with different fold change, p-values, and q-values. The KDM6A gene is included in this table when it is not in the table reported in the protocol.

```
   feature        id          fc         pval         qval
1     gene MSTRG.528 0.002419734 2.236922e-11 2.272713e-08
2     gene MSTRG.527 0.083631438 7.301875e-06 2.943606e-03
3     gene MSTRG.613 7.348233552 1.072525e-05 2.943606e-03
4     gene MSTRG.142 3.077840308 1.158900e-05 2.943606e-03
5     gene MSTRG.619 8.996831733 4.956551e-05 1.007171e-02
6     gene MSTRG.515 0.634289525 6.426792e-05 1.088270e-02
7     gene MSTRG.376 0.611394059 1.132114e-04 1.643183e-02
8     gene  MSTRG.67 0.599882917 1.515588e-04 1.924797e-02
9     gene MSTRG.621 7.937320574 3.548628e-04 4.006007e-02
10    gene MSTRG.231 1.411480422 4.065836e-04 4.130890e-02
```

the above table compares to table 4 in the protocol which shows differentially expressed transcripts between sexes (q value <0.05). The difference between my table and protocol is not the structure of the table, but rather all of the elements (gene ids) of the table are different. The fc, pval, and qvals are all on comparable orders of magnitude and the order of columns is the same. 

## Question 6

The third named gene in my generated table is `KDM6A`.

I have chosen to compare sample `ERR188044` which came from a male and the sample `ERR188234` which came from a female.

![image-20210430211100223](C:\Users\benfy\OneDrive - Johns Hopkins\Documents\Markdown Notes\.images\image-20210430211100223.png)

![image-20210430211113914](C:\Users\benfy\OneDrive - Johns Hopkins\Documents\Markdown Notes\.images\image-20210430211113914.png)

The main difference I see between the male and female is that the 8th isoform (second from bottom) of `KDM6A` is more highly expressed (darker color) in the male figure than the female figure. The first 4 isoforms seem to be expressed pretty similarly between the genders and the 6th, 7th, and 9th isoforms appear to be expressed more in females than in males. 

