# Problem Set 4

*Benjamin Fry - 03/26/21*

All the commands I used to generate my results are documented in `ps4_commands.txt` for your convenience.



#### Top Bacterial Species as Identified by Kraken

`kraken_report` output processed with `process_kraken.py` script. The top 20 bacterial species that were identified by Kraken are as follows:

>```
>Bradyrhizobium sp. BTAi1 4217
>Pseudomonas oryzihabitans 2814
>Planktomarina temperata 2394
>Pseudomonas psychrotolerans 1556
>Candidatus Pelagibacter ubique 1422
>Cutibacterium acnes 702
>Psychrobacter sp. PRwf-1 524
>Pseudomonas putida 482
>Halioglobus pacificus 481
>Pantoea vagans 405
>Cycloclasticus sp. PY97N 369
>Stenotrophomonas rhizophila 367
>Pantoea agglomerans 312
>Escherichia coli 309
>Ilumatobacter coccineus 245
>Enterococcus casseliflavus 243
>Marivivens sp. JLT3646 218
>Cycloclasticus zancles 211
>Pseudomonas tolaasii 199
>Algibacter alginicilyticus 198
>```



#### Top Non-Bacterial Species as Identified by Centrifuge

The 20 non-bacterial species identified by Centrifuge. Centrifuge output passed to `centrifuge-kreport` which I then processed with the script `process_centrifuge.py`

> ```
> Cyprinus carpio 27007
> Homo sapiens 11126
> Mus musculus 4701
> Ovis canadensis 4330
> Danio rerio 2734
> Apteryx australis 2585
> Diphyllobothrium latum 2188
> Solanum lycopersicum 1644
> melanogaster group 1577
> Solanum pennellii 1526
> Triticum aestivum 1501
> Trichobilharzia regenti 1419
> Oryzias latipes 1293
> Spirometra erinaceieuropaei 1265
> Oryza sativa 1254
> Vitis vinifera 1244
> Cucumis melo 1215
> Protopolystoma xenopodis 1203
> Vigna angularis 1119
> Echinostoma caproni 1040
> ```



#### Read Classification

###### Bacterial Read Classification of Kraken Reads

1.  Read `SRR1750106.1.346` has a length of 302 and was identified by Kraken as *Bradyrhizobium sp. BTAi1*. Upon BLASTing, found this read to have 100% identity to *Bradyrhizobium sp. BTAi1* with an E value of `6e-71`. Because of the 100% identity, low E value, and agreement with Kraken, I conclude that this read likely belongs to *Bradyrhizobium sp. BTAi1*
2.  Read `SRR1750106.1.948` has a length of 302 and was identified by Kraken as *Pseudomonas oryzihabitans*. Upon BLASTing, found this read has 99.34% identity with *Pseudomonas oryzihabitans* and matched with an E value of 8e-70. Again, the low E value, high identity, and agreement with Kraken brings me to the conclusion that this read likely belongs to *Pseudomonas oryzihabitans*.
3.  Read `SRR1750106.1.230` has a length of 302 and was identified by Kraken as *Planktomarina temperata RCA23*. Upon BLASTing, found this read to have 97.39% identity with *Planktomarina temperata RCA23* and matched it with an E value of 2e-65. Again, the low E value, high identity, and agreement with kraken indicates that this read is likely belongs to *Planktomarina temperata RCA23*

###### Non-Bacterial Read Classification of Centrifuge Reads

1. Read `SRR1750106.1.1816522` was identified by Centrifuge as belonging to *Homo sapiens*. Upon BLASTing, found that this read has 97.01% identity with `Homo sapiens`  and matched a gene for an inorganic phosphate receptor with E value of 2e-70.  As with the bacterial samples, this agreement between the BLAST results and Centrifuge, the high identity and low E value indicates that this read truly belongs to *Homo Sapiens* which belongs to the Chordata phylum
2.  Read `SRR1750106.1.554695` was identified by Centrifuge as belonging to *Beauveria bassiana*. Upon BLASTing, found this read aligned to two species within the genus *Thioclava* with percent identity of 88% and 87% and corresponding E values of 6e-36 and 3e-34 respectively. Many of the other reads I searched for *Beauvaria bassiana* did not align to it when BLASTed, so it is likely that centrifuge has misclassified the reads it assigned to it. Because two members of the *Thioclava* genus aligned with high identity and low E value, it is likely the true genus from which the read came from. The *Beauvaria* genus falls under the Ascomycota phylum.
3.  Read `SRR1750106.1.97172` was identified by Centrifuge as belonging to *Plasmodium vinckei*. Upon BLASTing, found this read aligned better to *Aquimarina sp. BL5* with a percent identity of 87.02% and an E value of 2e-31. Because `Plasmodium` didn't appear in the BLAST results at all, it is likely Centrifuge misclassified this read. The high percent identity and low E value indicates that this read aligns much better to *Aquimarina* and this I believe *Aquimarina sp. BL5* to be the origin of this read. The *Plasmodium* genus falls under the Apicomplexa phylum.



