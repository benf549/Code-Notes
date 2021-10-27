### Procedure For Running CWG On Lassa GPC

We began by loading the LASV spike complex into PyMOL with [5VK2](https://www.rcsb.org/structure/5VK2) from RCSB. We selected the GPC subunits and left out the native glycans and neutralizing antibodies and exported this to `lassa_mod.pdb`.

I then ran the first step of the CWG protocol:

```
python /home/ywu/wistar/software/tools/Glycan_Scanner/core/relax.py --pdb lassa_mod.pdb
```

which generated the file `lassa_mod_0001.pdb` which corresponds to the relaxed structure of the protein. 

I then ran the next step of the protocol:

```
python /home/ywu/wistar/software/tools/Glycan_Scanner/core/glycan_auto.py --pdb lassa_mod_0001.pdb
```

which generated `lassa_mod_0001_0001.pdb` and `man9.pdb` and `score.sc`

I then tried running the next steps of the protocol but encountered errors because of different names for my output files. To fix this, I copied `lassa_mod_0001.pdb` to `gs_relax.pdb` and `lassa_mod_0001_0001.pdb` to `gs_glycan.pdb` which corresponded with their appearances when I viewed them in PyMOL. 

Once I had done this I was then able to run the next step:

```
python /home/ywu/wistar/software/tools/Glycan_Scanner/core/model_pngs.py --pdb gs_relax.pdb --chain A --start 59 --end 416
```

 which generated two new folders `gly_pp` and `pp` containing our mutation and PNGSs

Next, I ran the next step:

```
python /home/ywu/wistar/software/tools/Glycan_Scanner/core/model_glycan.py --pdb gs_relax.pdb --chain A --start 59 --end 416
```

which was able to run once the `gs_relax.pdb` and `gs_glycan.pdb` were created as above. 

This ran for a week and the following Monday, I was able to run 

```
python /home/ywu/wistar/software/tools/Glycan_Scanner/core/st_select.py --pdb gs_relax.pdb --chain A --start 59 --end 416
```

