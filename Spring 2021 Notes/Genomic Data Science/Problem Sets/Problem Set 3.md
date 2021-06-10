# Problem Set 3

*Benjamin Fry - 03/12/21*

All the commands I used to generate my results are documented in `ps3_commands.txt` for your convenience.

### Q1: Kraken-Report

The output of kraken-report is in `kraken_report.out`



### Q2: Genera and Species in Sample

The output of the program `process_kraken.py` generates the two sorted lists requested. The genera in the sample are under the `Genus:` and  `Species:` sections of what that program prints to standard out. I have redirected this output to genera.txt for your convenience.

```
genera.txt
___________________________________________
Genus:
Ebolavirus 14650
Bradyrhizobium 284
Ralstonia 84
Pseudomonas 65
Cutibacterium 41
Rhodococcus 26
Caulobacter 10
Delftia 9
Stenotrophomonas 8
Mycobacterium 8
Staphylococcus 7
Rhodopseudomonas 6
Kocuria 6
Sphingomonas 5
Afipia 4
Burkholderia 4
Corynebacterium 4
Rhizobium 3
Moraxella 3
Microbacterium 3
Agrobacterium 2
Xanthobacter 2
Methylobacterium 2
Cupriavidus 2
Paraburkholderia 2
Paucibacter 2
Brevibacterium 2
Streptococcus 2
Finegoldia 2

Species:
Zaire ebolavirus 14650
Bradyrhizobium sp. BTAi1 215
Ralstonia pickettii 76
Cutibacterium acnes 38
Pseudomonas fluorescens 7
Rhodopseudomonas palustris 6
Bradyrhizobium oligotrophicum 5
Bradyrhizobium lablabi 5
Caulobacter vibrioides 5
Kocuria palustris 5
Bradyrhizobium sp. S23321 4
Afipia sp. GAS231 4
Caulobacter segnis 4
Delftia acidovorans 4
Stenotrophomonas maltophilia 4
Bradyrhizobium icense 3
Bradyrhizobium diazoefficiens 3
Bradyrhizobium erythrophlei 3
Sphingomonas melonis 3
Pseudomonas yamanorum 3
Moraxella osloensis 3
Mycobacterium sp. QIA-37 3
Staphylococcus epidermidis 3
Bradyrhizobium sp. ORS 278 2
Bradyrhizobium sp. CCGE-LA001 2
Xanthobacter autotrophicus 2
Burkholderia multivorans 2
Cupriavidus metallidurans 2
Paucibacter sp. KCTC 42545 2
Pseudomonas alcaliphila 2
Pseudomonas sihuiensis 2
Rhodococcus sp. 008 2
Microbacterium sp. TPU 3598 2
Finegoldia magna 2
```



### Q3: Single Reads

###### Species 1:  *Celeribacter indicus* 

This species was predicted with NCBI Taxonomy ID: `1208324` for the following read and had only one read assigned to it which from the fasta file had the identifier: `SRR1613382.12007.1`

When its the corresponding sequence is BLASTed, this sequence aligned to `Bradyrhizobium sp.` with a BLAST e-value of `9e-71`



###### Species 2: *Veilllonella parvula* 

This species was predicted with NCBI Taxonomy ID: `29466` for the following read and had only one read assigned to it which from the fasta file had the identifier: `SRR1613382.6005.1`

When its the corresponding sequence is BLASTed, this sequence aligned to `Veillonella parvula` with a BLAST e-value of `2e-67` which interestingly is the same as what Kraken predicted. 